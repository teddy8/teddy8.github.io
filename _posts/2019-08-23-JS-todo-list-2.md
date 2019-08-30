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
js에서 투두리스트(Todo List)를 예제를 통해 정리한다.
```
## 실행결과
```
'할 일 추가'란에 텍스트를 입력 후, '+'버튼을 누르면 할 일을 추가할 수 있다. 각각의 할 일은 완료 여부를 지정할 수 있다.
```

![](/assets\img\javascript\todo_list(2).png)

## 예제 소스코드
example.html
``` html

```

models.js
``` js

```

## 설명

```
위에 주석친 부분을 문단단위로 정리한다. 
// 할 일 데이터를 화면에 그림
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