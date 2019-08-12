---
layout: post   
title:  " Node.js 모든 파일 삭제(File Delete All) "
categories: Node.js
comments: true
tags: Node.js 모든 파일 삭제 File Delete All
author: teddy8  
---
* content
{:toc}

```
Node.js에서 fs, path 모듈을 사용하여 파일 및 폴더를 삭제하는 방법을 예제를 통해 정리한다.
```

## 소스코드

example.js

``` js
'use strict';

const fs = require('fs');
const path = require('path');

const removePath = (p, callback) => { // A 
  fs.stat(p, (err, stats) => { 
    if (err) return callback(err);

    if (!stats.isDirectory()) { // B 
      console.log('이 경로는 파일');
      return fs.unlink(p, err => err ? callback(err) : callback(null, p));
    }

    console.log('이 경로는 폴더');  // C 
    fs.rmdir(p, (err) => {  
      if (err) return callback(err);

      return callback(null, p);
    });
  });
};

const printResult = (err, result) => {
  if (err) return console.log(err);

  console.log(`${result} 를 정상적으로 삭제했습니다`);
};

const p = path.join(__dirname, 'js200');

try { // D
  const files = fs.readdirSync(p);  
  if (files.length) 
    files.forEach(f => removePath(path.join(p, f), printResult)); 
} catch (err) {
  if (err) return console.log(err);
}

removePath(p, printResult); 
```

## 설명

```
특정 경로의 폴더안에 있는 파일들을 모두 삭제한 후, 마지막에 폴더까지 삭제한다.
위에 주석친 부분을 문단단위로 정리한다.

[A] removePath
특정 경로의 파일 또는 폴더를 삭제하는 함수이다.
fs.stat()메소드를 통해 해당 경로가 파일인지 폴더인지 확인한다.
(에러발생 시 에러정보를 출력한다)

[B] stats.isDirectory()메소드가 false일 경우. 
즉, 파일인 경우(폴더가 아닌 경우)
fs.unlink()메소드를 통해 해당 경로의 파일을 삭제한다.

[C] 폴더인 경우(파일이 아닌 경우)
fs.rmdir()메소드를 통해 해당 경로의 폴더를 삭제한다.

[D] 동기패턴인 readdirSync()메소드를 통해 해당경로(p)의 폴더의 파일들을 가져온다.
가져온 파일의 개수(length)가 0이 아니면(0이면 빈 폴더라는 것) 
forEach로 하나하나 돌면서 removePath()메소드를 통해 삭제한다.
(해당경로(p)의 파일명 값(f)을 접근해서 삭제한다)
폴더 안 파일들을 모두 삭제했으면 해당경로(p)의 폴더 자체를 삭제해준다.
```