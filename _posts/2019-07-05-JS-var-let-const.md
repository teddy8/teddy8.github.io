---
layout: post   
title:  " JavaScript var vs let vs const 특징 및 차이점 "
categories: JavaScript
comments: true
tags: JavaScript js var let const 특징 차이점
author: teddy8  
---
* content
{:toc}

## var vs let vs const <br>

자바스크립트에서 var만 사용해야 했지만 <br>
es6부터 let과 const를 사용할 수 있게 되었습니다<br>
각 특징을 나열하면 다음과 같습니다.

```
var
  재선언 가능
  재할당 가능

let
  재선언 불가능
  재할당 가능

const
  재선언 불가능
  재할당 불가능
```

`var vs let`
---
example.js

``` js
if (true) {
  var str1 = '1';
  let str2 = '2';
}
console.log(str1); 
console.log(str2);
```
출력
```
1
error
```

```
var은 함수 단위의 유효 범위로 if문 안에서 정의해도 밖에서도 사용 가능합니다.
let은 블록 단위의 유효 범위로 밖에선 사용 불가능합니다.

따라서 1은 출력되지만 2는 오류로 인해 출력할 수 없습니다.
```
example.js

``` js
let str = "1";

if (true) {
  let str = "2";
  console.log(str);
}

console.log(str);
```
출력
```
2
1
```
```
let은 var와 다르게 전역변수와 지역변수처럼
유효범위를 구분되게 사용할 수 있습니다.
```
example.js

``` js
let str = "1";
  if (true) {
    console.log(value);
    let str = "2";
  }
```
출력
```
error
```
```
단, let변수를 함수 단위에서 선언해서 전역변수처럼 사용하려는 경우  
블록 단위에서 같은이름으로 재선언하면 호이스팅이 일어나기 때문에
변수선언의 위치에 따라 에러가 발생할 수 있습니다.
```

`let vs const`
---
```
const도 let처럼 블록단위로 스코프를 정의할 수 있습니다.
let과의 차이점은 선언과 동시에 값을 할당해야합니다. 
그 후, 재할당은 할 수 없습니다.
단, 객체를 할당한 경우 새로운 객체는 할당할 수 없지만 
객체 내부의 상태는 추가 및 변경 가능합니다.
```