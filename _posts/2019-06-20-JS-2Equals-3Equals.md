---
layout: post   
title:  " JavaScript 비교연산자 == vs === 차이 "
categories: JavaScript
comments: true
tags: JavaScript Equals Operator
author: teddy8  
---
* content
{:toc}

## 비교 연산자
두 개의 값을 비교하여 true 또는 false 결과값을 반환합니다.<br> 
그 중 "=="와 "==="의 차이를 알아봅니다.

---

## 코드 실행 결과
``` js
var a = "5";
var b = 5;

console.log(a == b);
console.log(a === b);
```

---

![](/assets/img/javascript\Double_Equals_vs_Triple_Equals.png)
---

## 결론<br>
"=="는 데이터 타입이 다를 경우 강제로 형변환을 하여 
비교하기<br> 때문에 `내용만 같으면` 됩니다.<br><br>
"==="는 `내용뿐만 아니라, 데이터 타입도 같아야` 합니다.