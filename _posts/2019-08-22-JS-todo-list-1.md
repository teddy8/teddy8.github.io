---
layout: post   
title:  " JavaScript 투두리스트(Todo List) (1/1)"
categories: JavaScript
comments: true
tags: JavaScript js 
author: teddy8  
---
* content
{:toc}

```
js에서 투두리스트(Todo List)를 예제를 통해 포스팅한다.
투두리스트라는 것은 간단하게 오늘의 계획을 작성하고,
계획을 완료하면 체크를 해나가면서 관리하는
즉, 스케쥴을 작성하고 관리하는 일종의 체크리스트 같은 것이다.
이번 포스팅에서는 화면작업을 들어가기전 할 일 들을 입출력하는 작업이다.

이를 위한 models.js의 주요 내용은 다음과 같다.

[Todo class] 할 일에 다음과 같은 내용을 저장한다. (계획의 내용, 완료여부)
완료여부를 토글 할 수 있다. (호출 시 true -> false 또는 false -> true)

[TodoManager class] 할 일을 지속해서 추가할 수 있고
모든 할 일들을 가져올 수 있으며, 
완료 되지 않은 할일의 개수를 가져올 수 있다. 

```

## 예제 소스코드
example.html
``` html
<!DOCTYPE html>
<html>
<head>
  <title>할일 앱 만들기 예제</title>
</head>
<body>
  <script src="./src/models.js"></script>
  <script>
    const todos = new TodoManager(); // A
    todos.addTodo('공부하기');
    todos.addTodo('운동하기');
    console.log(todos.getList());
    console.log(todos.leftTodoCount);
    setTimeout(() => {
      todos.getList()[0].toggle()
      console.log(todos.leftTodoCount);
      console.log(todos.getList());
    }, 3000);
  </script>
</body>
</html>
```

models.js
``` js
class Todo { // B
  constructor(contents, done) { 
    this.contents = contents;
    this.done = done;
  }
  toggle() {  
    this.done = !this.done;
  }
}

class TodoManager { // C
  constructor(todos = []) { 
    this._todos = [];
    todos.forEach(todo => {
      this.addTodo(todo.contents, todo.done);
    });
  }

  addTodo(contents, done = false) { // D
    const newTodo = new Todo(contents, done);
    this._todos.push(newTodo);
    return newTodo;
  }

  getList() { // E
    return this._todos;
  }

  get leftTodoCount() { // F  
    return this._todos.reduce((p, c) => {
      if (c.done === false) { 
        return ++p;
      } else {
        return p;
      }
    }, 0);
  }
}
```

## 설명

```
위에 주석친 부분을 문단단위로 정리한다. 

[A] TodoManager()클래스를 통해 인스턴스를 생성한다.
addTodo()메소드를 통해 2개의 할 일을 추가한다.
추가했던 할 일의 목록을 getList()메소드를 사용해 출력한다.
leftTodoCount메소드를 사용해 남아있는 할 일의 개수를 출력한다.
setTimeout()메소드를 통해 3초 후 아래의 명령을 수행한다.
getList()메소드를 통해 첫번째에 등록되 있는 할 일을 토글한다.
(완료여부가 true면 false, false면 true로 변경 됨)
leftTodoCount메소드를 사용해 남아있는 할 일의 개수를 출력한다.
할 일의 목록을 getList()메소드를 사용해 출력한다.

[B] Todo클래스를 정의한다. 
생성자(constructor)는 할 일과 완료 여부를 설정할 수 있다.
toggle()메소드를 정의한다. 
완료 된 상태에서 호출하면 완료되지 않은 상태가 된다.
반대로 완료되지 않은 상태에서 호출하면 완료 된 상태가 된다.

[C] TodoManager클래스를 정의한다.
생성자(constructor)는 할 일의 리스트를 전달받았을 경우
addTodo()메소드를 통해 각각의 할 일을 추가한다.
(멤버변수 _todos라는 리스트에 추가 된다)

[D] addTodo()메소드를 정의한다. 
할 일과 완료 여부를 인자로 받는다.
Todo()클래스를 통해 할 일과 완료 여부를 설정한 인스턴스를 생성한다.
멤버변수인 _todos 리스트에 push()메소드를 통해 원소를 추가한다.
Todo()클래스를 통해 생성한 인스턴스를 반환한다.

[E] getList()메소드를 정의한다.
멤버변수인 _todos 리스트를 반환한다.

[F] leftTodoCount()메소드를 정의한다.
이 메소드는 남은 할일의 개수를 반환한다.
읽기만 가능한 메소드이기 때문에 앞에 get이 붙는다.  
멤버변수인 _todos 리스트에 reduce()메소드를 통해 
완료 여부가 false인 경우만 count를 진행한다.
즉, 미완료 작업의 개수만 더해서 반환한다.

```

## 실행결과
```
처음에 2개의 할 일을 추가했으므로 2개의 할 일이 기록된 리스트가 출력된다.
그리고 남은 할 일의 개수를 출력했을 때 2가 출력된다.
그 후, 3초뒤 첫번째 할 일에 toggle()을 수행하고 
남은 할 일의 개수를 출력하면 1이 출력된다.
그 이유는 남은 할 일의 개수는 미완료 작업의 개수를 반환하는데 
첫번째 할 일에 toggle()을 수행함으로 써 완료 여부가
false에서 true로 변경되었기 때문에
남은 미완료 작업의 개수는 1개가 되기 때문이다.
한번 더 할 일 리스트를 출력해보면 첫번째 할 일이 true로 변경되어있다.
```
![](/assets\img\javascript\todo_list.png)