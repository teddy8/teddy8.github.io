---
layout: post   
title:  " JavaScript 투두리스트(Todo List) (2)"
categories: JavaScript
comments: true
tags: JavaScript js 
author: teddy8  
---
* content
{:toc}

```
js에서 투두리스트(Todo List)를 예제를 통해 포스팅한다.
지난번 포스팅에 이어서 화면부분에 대한 작업이다.
```
## 실행결과
```
'할 일 추가'란에 텍스트를 입력 후, '+'버튼을 누르면 할 일을 추가할 수 있다. 
각각의 할 일은 체크박스처럼 완료 여부를 지정할 수 있다.
현재 체크되 있는 완료 여부의 개수는 변경될 때 마다 갱신 된다.
아래는 '공부하기', '놀기', '밥먹기'라는 3개의 할 일이 추가된 상태에서 
'산책하기'를 입력한 후, '+'버튼을 클릭해서 할 일을 추가한 모습이다.
```

![](/assets\img\javascript\todo_list(2).png)

## 예제 소스코드
example.html
``` html
<!DOCTYPE html>
<html>
<head>
  <title>할 일 앱 만들기 예제</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="title">
    <h1>나의 하루</h1>
    <h2>10월 28일</h2>
  </div>
  <div class="todo-container">
  </div>
  <div class="add-todo">
    <button>+</button>
    <input type="text" placeholder="할 일 추가">
  </div>
  <script src="./models.js"></script>
  <script src="./app.js"></script>
  <script>
    const todoApp = new TodoApp([ // A 
      { contents: "공부하기", done: false },
      { contents: "놀기", done: true },
      { contents: "밥먹기", done: false }
    ]);
  </script>
</body>
</html>
```

app.js
``` js
class TodoApp {
  constructor(todos) { // B
    this.todoManager = new TodoManager(todos);
    this.todoContainerEl = document.querySelector(".todo-container");
    this.titleEl = document.querySelector(".title h2");
    this.plusBtnEl = document.querySelector(".add-todo button");
    this.bindEvents();
  }

  renderTodos() {  // C   
    this.todoContainerEl.innerHTML = '';  
    this.todoManager.getList().forEach((todo, i) => {   
      const todoEl = this.createTodoEl(todo, i); 
      this.todoContainerEl.appendChild(todoEl); 
    });
    this.renderTitle(); 
  }

  createTodoEl(todo, id) {  // D     
    const todoEl = document.createElement("div");
    todoEl.id = "todo-" + id;
    todoEl.className = "todo";
    todoEl.innerHTML = 
      `<input type="checkbox" ${todo.done ? "checked" : ""}> 
        <label>${todo.contents}</label>`;
    return todoEl;
  }

  renderTitle() { // E     
    const now = new Date(); 
    const month = now.getMonth(); 
    console.log('month = ', month);
    const date = now.getDate();
    if (this.titleEl) {
      this.titleEl.innerHTML = 
        `${month}월 ${date}일 <span class="left-count"> 
          (${this.todoManager.leftTodoCount}개)</span>`;  
    }
  }

  bindEvents() { // F     
    this.plusBtnEl.addEventListener('click', evt => { 
      const textEl = document.querySelector('.add-todo input[type="text"]'); 
      this.todoManager.addTodo(textEl.value); 
      textEl.value = '';  
      this.renderTodos(); 
    });
    this.todoContainerEl.addEventListener('click', evt => {
      if (evt.target.nodeName === 'INPUT' && evt.target.parentElement.className === 'todo') { 
        const clickedEl = evt.target.parentElement;
        const index = clickedEl.id.replace('todo-', '');  
        this.todoManager.getList()[index].toggle(); 
        this.renderTitle(); 
      }
    });
  }
}
```

## 설명

```
위에 주석친 부분을 문단단위로 정리한다. 

// 할 일 데이터를 화면에 그림
[A] TodoApp()클래스를 통해 3개의 할 일과 완료여부를 생성자를 통해 인스턴스를 생성한다.

[B] models.js의 TodoManager()클래스를 사용해 생성자로 전달받은 할 일들과 완료여부를 리스트에 모두 push시킨다.
할 일들의 내용이 표시되는 영역을 찾아 변수 선언한다.
타이틀 영역을 찾아 변수 선언한다. (현재날짜와 완료여부 개수가 표시되는 곳)
'+'버튼을 찾아 변수 선언한다.
bindEvents()를 호출한다. (처리해야 할 이벤트를 모아놓은 메소드)

[C] renderTodos()를 정의한다. (할 일 데이터를 화면에 그려주는 메소드)
모든 데이터를 지우고 todoManager의 getList()를 통해 할 일과 완료여부가 담긴 리스트를 가져온다.
각각의 할일과 완료여부는 createTodoEl()에 전달한다. (해당 데이터로 div영역을 생성하는 메소드)
생성된 div영역은 todoContainer의 자식으로 달아준다.
renderTitle()메소드를 통해 현재날짜와 남은 할 일을 갱신한다.

[D] createTodoEl()메소드를 정의한다. 
('+'버튼을 눌렀을 때 할 일 데이터를 통해 화면에 그려질 div영역을 생성한다)      

[E] renderTitle()메소드를 정의한다.
(현재날짜와 남은 할 일을 갱신한다) 
Date()객체를 사용해 현재 날짜를 가져온다. 
todoManager의 leftTodoCount()메소드를 통해 남은 할 일의 개수를 표시해준다.
이 메소드는 할 일이 추가되거나 완료여부가 변경될 때 마다 호출 되어야 한다.

[F] bindEvents()메소드를 정의한다. (등록해야하는 이벤트리스너를 모아놓은 메소드) 

plusBtnEl에 등록한 이벤트리스너는 할 일을 입력하고 '+'버튼을 클릭하면 발생된다.
입력한 내용은 todoManager를 통해 할 일의 내용과 완료여부를 추가한다.
input창에 입력한 내용은 공백으로 비워준다.
renderTodos()메소드를 통해 할 일들을 화면에 다시 그려준다.

todoContainerEl에 등록한 이벤트리스너는 완료 여부를 클릭했을 경우 발생된다.
(클릭한 타겟의 nodeName이 'input'이면서 부모요소의 class가 'todo'일 경우)
몇번째에 있는 할 일의 완료 여부를 클릭했는지 파악하기 위해 id값에 있는 todo- 뒤에 숫자를 추출한다.
추출한 숫자로 todoManager의 getList를 통해 인덱스로 접근 후 toggle()메소드를 수행한다. (t->f OR f->t)
renderTitle()메소드를 통해 현재날짜와 남은 할 일을 갱신한다.
```

## 피드백
```
이 방식은 3개의 할 일이 등록되어 있을 때, 4번째 할 일을 추가할 경우
현재 화면에 보이는 모든 할 일을 제거한 후 할 일들을 다시 하나하나 표시한다.
이러한 경우 화면깜박임이 발생될 수 있으며, 퍼포먼스적으로도 효율적이지 않다고 한다.
따라서, 할 일을 추가할 경우 기존에 있는 할 일들은 그대로 둔 상태에서 
새로운 할 일만 추가되도록 변경해야 한다.
```

## 개선 작업 완료
```
원래 포스팅했던 내용은 할 일을 추가할 때마다 다 지우고 처음부터 그리는 방식이다.
이 방식은 위에도 언급했지만 비효율적이다. 그렇기 때문에
할 일을 추가하면 기존 할 일은 그대로 두고 추가되는 것만 그리는 방식으로 수정했다.
아래와 같이 [B]부분과 [C]부분을 수정하면 된다.
원래는 할 일의 리스트를 getList()로 모두 받아온 뒤, forEach문을 처음부터 돌면서 그렸지만
getList()로 받아온 것을 slice()메소드를 통해 현재 할일의 개수를 start인덱스를 주어서
마지막 할 일의 다음부터 그리도록 변경하였다.
```
``` js
  constructor(todos) { // B
    this.num = 0;
    this.todoManager = new TodoManager(todos);
    this.todoContainerEl = document.querySelector(".todo-container");
    this.titleEl = document.querySelector(".title h2");
    this.plusBtnEl = document.querySelector(".add-todo button");
    this.renderTodos(); 
    this.bindEvents(); 
  }

  renderTodos() {  // C
    const todoCount = document.getElementsByClassName('todo').length;
    this.todoManager.getList().slice(todoCount).forEach(todo => {  
      const todoEl = this.createTodoEl(todo, this.num); 
      this.todoContainerEl.appendChild(todoEl); 
      console.log(this.num++);
    });
    this.renderTitle(); 
  }
```