---
layout: post   
title:  " JavaScript 투두리스트(Todo List) (4)"
categories: JavaScript
comments: true
tags: JavaScript js 
author: teddy8  
---
* content
{:toc}

```
저번 포스팅에 이어서 투두리스트에 삭제기능을 추가한 것을 정리한다.
```

## 실행화면
```
각 아이템의 오른쪽에 있는 'X'버튼을 통해 메모를 제거할 수 있다.
```
![](/assets\img\javascript\todo_list(3).png)

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
    this.renderTodos(); 
    this.bindEvents(); 
  }

  renderTodos() {  // 할 일 데이터를 화면에 그림
    const todoCount = document.getElementsByClassName('todo').length;
    this.todoManager.getList().slice(todoCount).forEach((todo, i) => {  
      const addIndex = todoCount + i;
      const todoEl = this.createTodoEl(todo, addIndex); 
      this.todoContainerEl.appendChild(todoEl); 
      this.todoManager.getList()[addIndex].id = addIndex; // 고유키 할당
    });
    this.renderTitle(); 
  }

  createTodoEl(todo, id) {  // '+'버튼을 눌렀을 때 생성 될 div 영역.    
    const todoEl = document.createElement("div");
    todoEl.dataset.todoId = id;
    todoEl.classList.add("todo");
    todoEl.innerHTML = 
      `<input type="checkbox" ${todo.done ? "checked" : ""}> 
        <label>${todo.contents}</label>
        <span class="close">&times;</span>`;
    todoEl.addEventListener('click', evt => {
      if(evt.target.type == 'checkbox') {
        const index = todoEl.dataset.todoId;
        this.todoManager.getList()[index].toggle();
        this.renderTitle();
      }
      if(evt.target.className == 'close') { // [A]
        const index = todoEl.dataset.todoId;
        todoEl.remove();
        this.todoManager.delTodo(index);
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

  bindEvents() { // 이벤트에 반응하는 리스너 함수를 등록하는 메소드
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

models.js
``` js
class Todo {
  constructor(contents, done) {
    this.contents = contents;
    this.done = done;
  }
  toggle() {
    this.done = !this.done;
  }
}

class TodoManager {
  constructor(todos = []) {
    this._todos = [];
    todos.forEach(todo => {
      this.addTodo(todo.contents, todo.done);
    });
  }

  addTodo(contents, done = false) {
    const newTodo = new Todo(contents, done);
    this._todos.push(newTodo);
    return newTodo;
  }

  delTodo(index) { // [A]
    this._todos = this._todos.filter(function(obj) {
      return obj.id != index;
    });
  }

  getList() {
    return this._todos;
  }

  get leftTodoCount() {
    return this._todos.reduce((p, c) => {
      if (c.done === false) {
        return ++p;
      } else {
        return p;
      }
    }, 0);
  }
}

export {Todo, TodoManager};
```

```
삭제 기능의 핵심부분은 index.js와 models.js에 [A]로 주석친 곳이다.
먼저, remove()를 사용해 화면에 보이는 아이템을 제거해준다. 
그 후, 모델클래스로 생성한 인스턴스에 동기화시켜주기 위해
dataset의 todoId값을 가져와 삭제할 아이템의 고유키값을 delTodo()메소드로 전달한다. 
해당 키값을 갖지 않는 아이템을 filter해준다. 
즉, 해당 키값을 갖는 아이템은 제거된다.
```