---
layout: post   
title:  " Node.js 예외처리 "
categories: Node.js
comments: true
tags: Node.js 예외처리
author: teddy8  
---
* content
{:toc}

```
Node.js에서 다음과 같은 예외처리 방법 2가지를 예제를 통해 정리한다.
1. 비동기(Async) 모듈, 콜백함수
2. try-catch, throw

참고로 
동기(Sync) 패턴에선 try-catch를 사용할 수 있지만
비동기(Async) 패턴에선 try-catch를 사용할 수 없다.
```

## 비동기(Async) 모듈
example.js

``` js
"use strict";

const cbFunc = (err, result) => {   
    if (err && err instanceof Error) 
        return console.error(err.message); 
    if (err) 
        return console.error(err); 

    console.log('에러가 발생하지 않음');
};

const asyncFunction = (isTrue, callback) => {
    if (isTrue)
        return callback(null, isTrue);
    else 
        return callback(new Error('This is error!!'));
};

asyncFunction(true, cbFunc);
asyncFunction(false, cbFunc);
```

```
asyncFunction의 첫번째 인자에 어떤 연산의 결과값이 들어간다고 가정하고,
두번째 인자에 예외를 처리하는 비동기 콜백함수인 cbFunc를 넣어준다고 하자

연산의 결과값이 true(이상이 없는)인 경우 예외가 발생할 필요가 없으므로, 
cbFunc의 예외변수에는 null을 전달하고 결과값은 true를 전달한다.

연산의 결과값이 false(이상이 있는)인 경우 예외를 발생시켜야 하므로, 
cbFunc의 예외변수에 에러객체를 전달한다.

이 때, cbFunc는 에러가 빈 값이면 "에러가 발생하지 않음"을 출력하고,
에러정보가 있다면 에러메시지를 출력하는데
에러객체로 넘어온경우 객체에 담긴 메시지를 출력하고 그렇지 않은경우 그 메시지 자체를 출력한다.
```

실행결과
```
에러가 발생하지 않음
This is error!!
```


## try-catch, throw
example.js
``` js
"use strict";

const fs = require('fs');

try {
    const fileList = fs.readdirSync('/undefined/');
    console.log('hello');
    fileList.forEach(f => console.log(f));
} catch (err) {
    if (err) console.error(err);
}

```

실행결과
```
{ Error: ENOENT: no such file or directory, scandir 'c:\undefined'
    at Object.fs.readdirSync (fs.js:928:18)
    at Object.<anonymous> (c:\Program Files\Git\usr\practicejs\JSExerciseFiles\part4\166.js:27:25)
    at Module._compile (module.js:649:30)
    at Object.Module._extensions..js (module.js:660:10)
    at Module.load (module.js:561:32)
    at tryModuleLoad (module.js:501:12)
    at Function.Module._load (module.js:493:3)
    at Function.Module.runMain (module.js:690:10)
    at startup (bootstrap_node.js:194:16)
    at bootstrap_node.js:666:3
  errno: -4058,
  code: 'ENOENT',
  syscall: 'scandir',
  path: 'c:\\undefined' }
```
```
내장 모듈인 fs(파일시스템) 모듈을 가져와서
특정경로에 있는 파일을 출력하는 상황이다.
"/undefined/" 경로의 파일리스트를 가져오는 순간(아무것도 없어서) 
예외가 발생하여 바로 catch문으로 가게 된다.
따라서 try문 안에 있는 "hello"는 출력되지 않는다.
```