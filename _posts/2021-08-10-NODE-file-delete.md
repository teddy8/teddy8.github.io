---
layout: post   
title:  " Node.js 파일 삭제(File Delete) "
categories: Node.js
comments: true
tags: Node.js 파일 폴더 삭제 File Folder Delete
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
파
```