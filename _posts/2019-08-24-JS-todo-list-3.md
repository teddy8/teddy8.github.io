---
layout: post   
title:  " JavaScript 투두리스트(Todo List) (3/5)"
categories: JavaScript
comments: true
tags: JavaScript js 
author: teddy8  
---
* content
{:toc}

```
js에서 투두리스트(Todo List)를 예제를 통해 포스팅한다.
지난번 포스팅에서 피드백 받은 내용에 대해 개선작업을 완료 했는데 
해당 코드에 대해 다시 피드백 받은 내용은 다음과 같다.

1. todoCount는 this.num으로 교체해도 되지 않는지? (할 일을 제거할 땐 어떻게 할 건지)

2. id 낭비하지말고 data 속성을 쓰면 좋다. (data-id 또는 data-todo-id 이런식으로)

3. className = "todo"; 같은 경우는 classList를 써라. (classList.add('todo') 이런식으로)

4. 체크박스에 거는 이벤트는 엘리먼트 만들 때 바로바로 걸어라 그럼 좀 더 간결해진다.

5. innerHtml같은경우는 살짝 위험하다 나중에 디비 넣을 때 아무처리없이 다이렉트로 넣기는 좀 그렇다.

6. getList().slice().foreach 이부분이 나중에 로직 꼬일 위험감이 느껴진다.

다음 소스코드는 피드백을 반영하여 개선작업한 주요 소스코드이다.
```


## 소스코드
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
</body>
</html>
```

index.js
``` js
import './style.css';
import {Todo, TodoManager} from './models.js';

class TodoApp {
  constructor(todos) {
    this.todoManager = new TodoManager(todos);
    this.todoContainerEl = document.querySelector(".todo-container");
    this.titleEl = document.querySelector(".title h2");
    this.plusBtnEl = document.querySelector(".add-todo button");
    this.renderTodos(); // 할 일 데이터를 화면에 그림
    this.bindEvents(); // 이벤트에 반응하는 리스너 함수를 등록하는 메소드 (메소드와 사용자입력에 따른)
  }

  renderTodos() {  // 할 일 데이터를 화면에 그림
    const todoCount = document.getElementsByClassName('todo').length;
    this.todoManager.getList().slice(todoCount).forEach((todo, i) => {  
      const todoEl = this.createTodoEl(todo, todoCount + i); 
      this.todoContainerEl.appendChild(todoEl); 
      console.log(todoCount + i);
    });
    this.renderTitle(); 
  }

  createTodoEl(todo, id) {  // '+'버튼을 눌렀을 때 생성 될 div 영역.    
    const todoEl = document.createElement("div");
    todoEl.dataset.todoId = id;
    todoEl.classList.add("todo");
    todoEl.innerHTML = 
      `<input type="checkbox" ${todo.done ? "checked" : ""}> 
        <label>${todo.contents}</label>`;
    todoEl.addEventListener('click', evt => {
      if(evt.target.type == 'checkbox') {
        const index = todoEl.dataset.todoId;
        this.todoManager.getList()[index].toggle();
        this.renderTitle();
      }
    })
    return todoEl;
  }

  renderTitle() { // 현재날짜와 남은 할 일 갱신 
    const now = new Date(); 
    const month = now.getMonth() + 1; 
    const date = now.getDate();
    if (this.titleEl) {
      this.titleEl.innerHTML = 
        `${month}월 ${date}일 <span class="left-count"> 
          (${this.todoManager.leftTodoCount}개)</span>`;  
    }
  }

  bindEvents() {
    this.plusBtnEl.addEventListener('click', evt => { 
      const textEl = document.querySelector('.add-todo input[type="text"]'); 
      this.todoManager.addTodo(textEl.value); 
      textEl.value = ''; 
      this.renderTodos();  
    });
  }
}

const todoApp = new TodoApp([
  { contents: "공부하기", done: false },
  { contents: "놀기", done: true },
  { contents: "밥먹기", done: false }
]);
```

## 후기
```
다음 포스팅에는 투두리스트에 삭제기능을 추가해볼 것이다.
```