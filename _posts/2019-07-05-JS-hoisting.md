---
layout: post   
title:  " JavaScript 호이스팅(Hoisting) "
categories: JavaScript
comments: true
tags: JavaScript js hoisting 호이스팅
author: teddy8  
---
* content
{:toc}

## 함수 호이스팅 <br>
```
함수 호이스팅이란?
간략히 말하면 함수를 선언하기 전에 호출이 가능한 것입니다.
아래의 예제로 살펴보겠습니다.
```

---
소스코드
---
example.js
``` js
test();
function test() {
	console.log("hello");
}
```
```
가능
```
example.js
``` js
test();
var test = function () {
	console.log("hello");
}
```
```
오류 (함수를 선언문이 아닌 구현식으로 사용하는 것은 불가합니다)
```
example.js
``` js
var test = function () {
	console.log("hello");
}
test();
```
```
가능 (이처럼 구현식은 호이스팅이 안되므로 미리 선언해서 사용해야 합니다)
```
