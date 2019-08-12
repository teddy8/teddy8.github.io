---
layout: post   
title:  " Node.js 파일 읽기(File Read) "
categories: Node.js
comments: true
tags: Node.js 파일 읽기 File Read
author: teddy8  
---
* content
{:toc}

```
Node.js에서 fs, path 모듈을 사용하여 파일의 내용을 읽는 방법을 예제를 통해 정리한다.
```

## 소스코드

example.js

``` js
"use strict";

const fs = require('fs');
const path = require('path');

const filePath = path.join(__dirname, 'js200', 'hello.txt');

fs.open(filePath, 'r', (err, fd) => { // A
  if (err && err.code === 'ENOENT') return console.log('읽을 수 없는 파일입니다');
  if (err) return console.log(err);

  fs.readFile(filePath, 'utf-8', (err, data) => { // B
    if (err) return console.log(err);

    console.log(data);
  });

  try { // C
    const data = fs.readFileSync(filePath, 'utf-8');
    console.log(data);
  } catch (err) {
    console.log(err);
  }
});
```

## 설명

```
위에 주석친 부분을 문단단위로 정리한다.

[A] fs.open()메소드를 통해 해당 경로의 파일을 'r'모드로 open한다.
(읽을 수 없거나 기타 에러시 에러정보를 출력한다)

[B] fs의 readFile()메소드를 통해 파일을 읽어온다.
[fs.readFile(파일경로, 인코딩, 콜백함수)]
그 후, 파일정보를 출력한다.
이 방식은 비동기 패턴이다.

[C] fs의 readFileSync()메소드를 통해 반환된 파일정보를 출력한다.
[fs.readFileSync()메소드  파일경로, 인코딩]
Sync가 붙은 이유는 동기패턴이기 때문이다. 
동기 패턴은 에러에 대한 값이 반환되는 것은 아니기 때문에 
try-catch문을 통해 에러를 catch해야 한다.
그렇지 않고 동기 패턴에서 에러가 발생하면 idle상태에 빠져서 작동하지 않게 된다.
```