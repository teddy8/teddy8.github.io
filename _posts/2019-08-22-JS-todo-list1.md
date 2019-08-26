---
layout: post   
title:  " JavaScript 투두리스트(Todo List)"
categories: JavaScript
comments: true
tags: JavaScript js 
author: teddy8  
---
* content
{:toc}

```
js에서 투두리스트(Todo List)를 예제를 통해 정리한다.
```

## 실행결과
```
다.
```
![](/assets\img\javascript\simple_editr.png)

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
    const todos = new TodoManager();
    todos.addTodo('공부하기');
    todos.addTodo('운동하기');
    console.log(todos.getList());
    console.log(todos.leftTodoCount);
    todos.getList()[0].toggle()
    console.log(todos.leftTodoCount);
    console.log(todos.getList());
  </script>
</body>
</html>
```

models.js
``` js
class Todo {
  constructor(contents, done) { // 할일내용, 완료여부
    this.contents = contents;
    this.done = done;
  }
  toggle() {  // 완료된 상태에서 호출하면 완료되지 않은 상태가 되게끔
    this.done = !this.done;
  }
}

class TodoManager {
  constructor(todos = []) {
    this._todos = [];
    // todos.forEach(todo => {
    //   this.addTodo(todo.contents, todo.done);
    // });
  }

  addTodo(contents, done = false) {
    const newTodo = new Todo(contents, done);
    this._todos.push(newTodo);
    // return newTodo;
  }

  getList() {
    return this._todos;
  }

  get leftTodoCount() { // get(읽기만 가능), 남은 할일 개수 반환
    return this._todos.reduce((p, c) => {
      if (c.done === false) { // 미완료작업의 개수만 더해서 반환함
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

[A] 폰

[B] 상

[C] 툴