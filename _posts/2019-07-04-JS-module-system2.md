---
layout: post   
title:  " JavaScript 모듈시스템2 "
categories: JavaScript
comments: true
tags: JavaScript js module system
author: teddy8  
---
* content
{:toc}

## 모듈 시스템 <br>
지난번 예제에서 function을 export로 내보내고 import로 가져와서 사용해봤습니다.
이번 예제에서는 class를 다룬 간단한 예제를 살펴보겠습니다.

---
index.html
``` html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Module Sample</title>
  <script type="module" src="app.js"></script>
</head>
<body>
</body>
</html>
```
---
app.js
``` js
import Person from './person.js';

const chulsu = new Person(20);
chulsu.speedUp(5);
```
person.js
``` js
export default class Person {
  constructor(speed) {
    this.speed = speed;
  }
  speedUp(n=0) {
    console.log(`before speed = ${this.speed}`);
    this.speed += n;
    console.log(`after speed = ${this.speed}`);
  }
}
```
---

## 출력값<br>
```
before speed = 20
after speed = 25
```