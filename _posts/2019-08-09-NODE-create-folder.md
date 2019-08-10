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

## 소스코드
example.js

``` js
"use strict"; // A
const fs = require('fs'); 

const checkDir = (path, callback) => {  
  fs.stat(path, (err, stats) => {       
    if (err && err.code === 'ENOENT')   
      return callback(null, true);
    if (err) 
      return callback(err);

    return callback(null, !stats.isDirectory()); 
  });
};

const currentPath = __dirname;  // B
let path = `${currentPath}/js200`;  

checkDir(path, (err, isTrue) => {  // C
  if (err) 
    return console.log(err);

  if (!isTrue) {  
    console.log('이미 동일한 디렉토리가 있습니다. 디렉토리명을 변경합니다.');
    path = `${currentPath}/js200-new`;
  }

  fs.mkdir(path, (err) => { 
    if (err) 
      console.log(err);

    console.log(`${path} 경로로 디렉토리를 생성했습니다.`);
  });
});
```

## 설명
```
위에 주석친 부분을 문단단위로 정리한다.

[A] "use strict"로 엄격한 모드로 실행하고
내장 모듈인 fs(파일 시스템)모듈을 가져온다.
파일생성 가능한 경로인지 해당경로를 체크하는 checkDir 콜백함수를 정의한다. 
checkDir에서 fs의 stat()메소드를 통해 해당 path의 파일 존재 여부를 확인한다. 
만약 에러가 날 경우 어떤 파일도 존재하지 않는 경우 파일을 생성할 수 있기 때문에 
이 경우는 true를 전달하고, 기타 에러 발생시 에러정보만 전달한다. 
에러가 아닌 경우 isDirectory()메소드를 통해 논리부정 연산자를 붙여 전달해준다. 
isDirectory()메소드는 디렉토리에 이미 동일한 폴더가 있는지 알려준다. 
isDirectory()메소드에 논리 부정 연산자를 붙여주는 이유는
isDirectory()가 true면 정상적으로 폴더를 생성할 수 없기 때문에 false를 전달하고 
false면 비어있다는 뜻이므로 정상적으로 파일을 생성할 수 있기 때문에 true를 전달하기 때문이다.

[B] __dirname으로 현재 경로를 가져와서 특정 파일명을 붙여준다.

[C] 위에서 정의한 checkDir() 콜백함수를 실행한다. 
에러가 발생되면 에러정보를 반환한다.
checkDir은 결국 정상적으로 폴더를 생성할 수 있으면
true를 반환하고 그렇지 않으면 false를 반환한다.
false를 반환했다면 디렉토리를 변경해서 폴더를 생성한다. 
true를 반환했다면 해당경로에 정상적으로 폴더를 생성한다.
```

## 마치며
```
fs.stat 모듈을 사용 폴더를 생성했다.
하지만 fs.open(), fs.readFile(), fs.writeFile()와 같이 
파일을 직접 접근하여 읽고 쓸 때는 반드시 접근 권한을 확인해야 하므로 
fs.stat보단 fs.access 모듈이 권장된다.   
fs.access 모듈 활용 방법은 다음에 포스팅 예정이다
fs.stat 모듈과 클래스에 대해 더 자세한 내용은 다음링크에서 확인할 수 있다
```
[https://nodejs.org/docs/latest/api/fs.html#fs_fs_stat_path_callback](https://nodejs.org/docs/latest/api/fs.html#fs_fs_stat_path_callback)