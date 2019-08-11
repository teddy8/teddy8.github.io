---
layout: post   
title:  " Node.js 파일 검색(File Search) "
categories: Node.js
comments: true
tags: Node.js 파일 검색 File Search
author: teddy8  
---
* content
{:toc}

```
Node.js에서 fs, path 모듈을 사용하여 파일을 검색하는 방법을 예제를 통해 정리한다.
```

## 소스코드

example.js

``` js
"use strict";

const fs = require('fs');
const path = require('path');

const fileName = 'hello.txt';   // A
const filePath = path.join(__dirname, 'js200', fileName);
console.log(path.parse(filePath));

const isFileInPath = (path, fileName, callback) => {  // B 
  fs.readdir(path, (err, files) => { 
    if (err) return callback(err);

    let isHere = false; 
    files.forEach(f => {
      if (f === fileName) isHere = true;  
    });

    return callback(null, isHere);
  });
};

isFileInPath(path.join(__dirname, 'js200'), fileName, (err, isTrue) => {  // C
  if (err || !isTrue) return console.log('파일을 읽을 수 없습니다');

  fs.stat(filePath, (err, fileInfo) => {  
    if (err) return console.log(err);

    return console.log(fileInfo);
  });
});
```

## 설명

```
위에 주석친 부분을 문단단위로 정리한다.

[A] 파일 경로를 생성한다.

[A] isFileInPath 메소드
isFileInPath(경로, 파일명, 콜백함수)
해당경로에 파일이 존재하는지 파악하는 하는 함수. 
fs의 readdir함수를 통해 특정 경로 안에 있는 모든 파일명을 콜백 함수의 매개변수로 전달하고
모든 파일을 forEach로 하나씩 꺼내서 동일한 파일명이 존재할 경우 true를 반환한다.

[B] 위에서 정의한 isFileInPath 메소드를 실행한다.
false를 반환했을 경우(동일한 파일명이 존재하지 않음)나
기타에러가 발생한 경우 '파일을 읽을 수 없습니다' 출력 후 종료한다.
그렇지 않은 경우 fs.stat함수를 통해 파일의 상세정보(fileInfo)를 출력한다.
```

## 실행 결과
![](/assets\img\javascript\file_search.png)