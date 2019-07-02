---
layout: post   
title:  " JavaScript 모듈시스템 "
categories: JavaScript
comments: true
tags: JavaScript js module system
author: teddy8  
---
* content
{:toc}

## 모듈 시스템 <br>
ES6에 추가된 모듈시스템에 대해서 살펴보겠습니다.<br>자바스크립트 파일을 export 키워드를 통해 내보낸 후,<br>import 키워드를 통해 쉽게 가져올 수 있습니다.<br>아래의 간단한 예제로 살펴보겠습니다.

---
index.html
---
``` html
<!DOCTYPE html>
<html lang="ko">
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
---
``` js
import { sum } from './test.js';
sum(2, 3);
```
test.js
---
``` js
export function sum(a, b) {
  console.log(`${a} + ${b} = ${a+b}`);
}
```
---

## 출력값<br>
```
2 + 3 = 5
```