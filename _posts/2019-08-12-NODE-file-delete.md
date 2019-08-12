---
layout: post   
title:  " Node.js 파일 삭제(File Delete) "
categories: Node.js
comments: true
tags: Node.js 파일 삭제 File Delete
author: teddy8  
---
* content
{:toc}

```
Node.js에서 fs, path 모듈을 사용하여 파일을 삭제하는 방법을 예제를 통해 정리한다.
```

## 소스코드

example.js

``` js
'use strict';

const fs = require('fs');
const path = require('path');

const filePath = path.join(__dirname, 'js200', 'hello.txt');

fs.access(filePath, fs.constants.F_OK, (err) => { // A
  if (err) return console.log('삭제할 수 없는 파일입니다');

  fs.unlink(filePath, (err) => err ?  
    console.log(err) : console.log(`${filePath} 를 정상적으로 삭제했습니다`));
});
```

## 설명

```
위에 주석친 부분을 문단단위로 정리한다.

[A] fs의 access()메소드로 해당경로에 대한 접근가능여부 확인한다.
(에러발생 시 에러문구를 출력한다.)
[fs.access(경로, mode정보, 콜백함수)]
(fs.constants.F_OK = 접근과 관련된 mode 정보)
(constants = 파일 시스템과 관련된 상수들을 그룹으로 모아놓은 상수.)
(그 중 상수 F_OK = 파일 존재 여부 확인)

fs.constants.F_OK를 전달하고 에러를 반환하지 않은 경우
MODE 상수값 조건을 충족(삭제할 수 있는)한다는 뜻이므로
fs.unlink() 메소드를 이용해 삭제한다.
```

## 마치며

```
F_OK말고도 다양한 상수가 있다.

O_RDONLY            : read-only 접근을 위해 파일을 여는 권한
X_OK                : 파일이 다른 프로세스 호출에 의해 실행 가능한지 접근 권한을 확인
S_IWUSR, S_IXGRP    : 파일 쓰기에서 소유권 또는 그룹소유권 확인

더 자세한 내용은 아래 링크에서 확인할 수 있다.
```
[https://nodejs.org/docs/latest/api/fs.html#fs_fs_constants_1](https://nodejs.org/docs/latest/api/fs.html#fs_fs_constants_1)