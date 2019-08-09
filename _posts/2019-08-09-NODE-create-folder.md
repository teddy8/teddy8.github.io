---
layout: post   
title:  " Node.js 폴더 생성(Create Folder) "
categories: Node.js
comments: true
tags: Node.js 폴더 생성 Create Folder
author: teddy8  
---
* content
{:toc}

```
Node.js에서 fs 모듈을 활용하여 폴더를 생성하는 방법을 예제를 통해 정리한다.
```

## 비
example.js

``` js
"use strict";

const fs = require('fs'); // 내장 모듈인 파일 시스템 모듈을 가져온다

const checkDir = (path, callback) => {  // 해당 경로가 파일생성 가능한 지
  fs.stat(path, (err, stats) => {       // 해당 path의 파일 존재 여부 확인 가능
    if (err && err.code === 'ENOENT')   // 에러인데 어떤 파일도 존재하지 않는 경우. 파일을 생성할 수 있기 때문에 true전달
      return callback(null, true);
    if (err) // 기타 에러시 에러정보 전달
      return callback(err);

    return callback(null, !stats.isDirectory());  // 디렉토리에 이미 동일한 폴더가 있으면 isDirectory는 true므로, false전달, 그렇지 않으면 false므로 true를 전달하게 됨
  });
};

const currentPath = __dirname;  // 현재 경로를 가져온다
let path = `${currentPath}/js200`;  // 현재 경로에 특정 파일명을 붙여준다

checkDir(path, (err, isTrue) => {
  if (err) // 그 외 다른 에러가 발생한 경우
    return console.log(err);

  if (!isTrue) {  // 이미 동일한 폴더가 존재하는 경우
    console.log('이미 동일한 디렉토리가 있습니다. 디렉토리명을 변경합니다.');
    path = `${currentPath}/js200-new`;
  }

  fs.mkdir(path, (err) => { // 해당 경로에 새로운 폴더 생성
    if (err) // 에러가 발생한 경우
      console.log(err);

    console.log(`${path} 경로로 디렉토리를 생성했습니다.`);
  });
});
```



```
fs.stat 모듈을 사용 폴더를 생성했다.
하지만 fs.open(), fs.readFile(), fs.writeFile()와 같이 파일을 직접 접근할 때는 
파일을 직접 읽고 쓰기 시에는 반드시 접근 권한을 확인해야 하므로 fs.stat대신 fs.access 모듈이 권장된다.  
 

이 경우에는 
활용 방법에 대해서는 다음에 살펴본다 
fs.stat 모듈과 fs.Stat 클래스에 대해 더 자세한 내용은 공식홈페이지 www 에서 확인할 수 있다
```