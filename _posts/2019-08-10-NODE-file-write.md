---
layout: post   
title:  " Node.js 파일 입력(File Write) "
categories: Node.js
comments: true
tags: Node.js 파일 입력 File Write
author: teddy8  
---
* content
{:toc}

```
Node.js에서 fs, path 모듈을 사용하여 파일에 입력하는 방법을 예제를 통해 정리한다.
```

## 소스코드
example.js

``` js
"use strict";

const fs = require('fs');
const path = require('path');

const makeFile = (path, callback) => { // A
    fs.writeFile(path, 'New file, New content', 'utf8', (err) => {  
        if (err) return callback(err);

        console.log('파일이 생성됐습니다.');
        callback(null);
    });
};

const appendFile = (path, callback) => { // B 
    fs.appendFile(path, '\nUpdate file', (err) => { 
        if (err) return callback(err);

        console.log('파일 내용을 추가합니다.');
        callback(null);
    })
};

const printErrIfExist = (err) => { // C
    if (err) console.log(err);
};



const folderName = 'test' // D
const fileName = 'hello.txt'
const filePath = path.join(__dirname, folderName, fileName);    

fs.open(filePath, 'wx', (err, fd) => { // E
    if (err && err.code === 'EEXIST') 
        return appendFile(filePath, (err) => printErrIfExist(err));
    if (err) { 
      return callback(err);
    }
   
    return makeFile(filePath, (err) => printErrIfExist(err));
});
```

## 설명
```
위에 주석친 부분을 문단단위로 정리한다.

[A] makeFile
새로운 파일에 내용을 추가하는 하는 함수. 
fs모듈의 writeFile()메소드에 경로, 파일내용, 인코딩, 에러콜백함수를 전달해 파일을 새로 생성한다. 

[B] appendFile
기존파일에 내용을 추가하는 함수
fs의 appendFile()메소드를 이용해 경로, 추가할 문자열, 에러콜백함수를 전달해 기존파일에 내용을 추가한다.

[C] printErrIfExist
에러가 존재할 시 에러를 출력하는 함수

[D] path의 join모듈로 경로를 만들어준다.
// path.join(현재 경로, 폴더명, 파일명)

[E] fs.open()
해당경로의 파일 또는 폴더의 존재 여부 확인 함수 
fs.open(경로, wx(쓰기 접근 권한), 에러정보)
동일한 파일이 있을 경우. appendFile함수로 내용만 추가한다.
그렇지 않을 경우. makeFile함수로 새로운 파일에 내용을 추가한다.
그 외 기타 오류가 발생한 경우 에러를 반환한다.
```

## 마치며
```
파일을 생성할 때 해당 경로에 폴더가 존재하지 않으면
fs.open을 실행할 때 에러가 발생한다.
그래서 미리 만들어놔야 한다.
아니면 폴더가 없는 경우 새로 생성해주는 방법도 있을 것 같은데
폴더가 하나만 없다면 생성해주면 되지만 여러 개가 없을 경우도 존재할 것이다. 
이 부분은 구현하려다 코드만 괜히 더러워질 것 같아서 말았다.
```