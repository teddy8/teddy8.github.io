---
layout: post   
title:  " JavaScript 투두리스트(Todo List) (5/5)"
categories: JavaScript
comments: true
tags: JavaScript js 
author: teddy8  
---
* content
{:toc}

```
저번 포스팅에 이어서 투두리스트에 변경된 내용이다.
1. 로컬스토리지 적용 (새로고침해도 데이터 그대로 남아있도록)
2. 모듈시스템 적용 (import해서 쓸 수 있도록)
```

## 실행화면
```
아이템을 추가했을 때와 삭제했을 때,
새로고침시, 데이터가 남아있는 것을 확인할 수 있다.
```
![](/assets\img\javascript\todo_list(4).gif)

## 소스코드
index.js
``` html
(생략)
```

index.html
``` html
(생략)
```

app.js
```
(생략)
```

models.js
```
(생략)
```

TodoManagerWithStorage.js
``` js
import {TodoManager} from './models.js';

class TodoManagerWithStorage extends TodoManager {
  static get STORAGE_KEY() { // [A]
    return "TODO-APP";
  }

  constructor() { // [B]
    const todoJSON = localStorage.getItem(TodoManagerWithStorage.STORAGE_KEY);  
    const todos = (todoJSON) ? JSON.parse(todoJSON) : [];
    super(todos)
  }

  addTodo(contents, done = false) { // [C]
    const newTodo = super.addTodo(contents, done);  
    const original = newTodo.toggle; 
    newTodo.toggle = () => { 
      original.apply(newTodo); 
      this.saveToLocalStorage();
    }
    this.saveToLocalStorage();
    return newTodo;
  }

  delTodo(index) { // [D]
    super.delTodo(index);
    this.saveToLocalStorage();
  }

  saveToLocalStorage() { // [E]
    const todoJSON = JSON.stringify(this._todos); 
    localStorage.setItem(TodoManagerWithStorage.STORAGE_KEY, todoJSON); 
  }
}

export {TodoManagerWithStorage};
```

```
[A] 저장소 키를 get타입의 정적메소드로 정의한다. 
(로컬스토리지에 이 키를 사용해 데이터를 set하고 get하기 위함)

[B] 생성자를 정의한다. (TodoManagerWithStorage클래스)
로컬스토리지의 getItem()메소드를 통해 해당 저장소 키에 대한 데이터를 가져온다.
가져온 데이터는 JSON문자열로 파싱한다. (데이터가 없을 경우 빈리스트 할당)
JSON문자열을 super클래스의 생성자에 전달한다. 
(이 때, TodoManager의 생성자는 데이터들을 하나하나 push하여 리스트를 생성한다)

[C] TodoManager의 addTodo 메소드를 오버라이딩 한다. (메소드 재정의)
먼저, 기존의 addTodo 메소드를 호출하고, toggle 메소드를 변수에 할당한다.
할당한 toggle 메소드를 재정의한다. 
변수에 할당한 tooggle 메소드를 apply()메소드를 통해 newTodo를 this객체로 호출한다.
saveToLocalStorage()메소드를 호출한다. 
(완료 여부(done)가 변경될 때 마다 로컬스토리지에 동기화한다)

[D] 기존의 delTodo 메소드를 호출하고, saveToLocalStorage()메소드를 
호출하여 삭제된 것을 로컬스토리지에 동기화한다.

[E] 할 일 리스트를 json문자열로 바꿔서 로컬스토리지의 setItem을 통해 데이터를 저장한다.
```