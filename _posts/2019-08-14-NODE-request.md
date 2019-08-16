---
layout: post   
title:  " Node.js request "
categories: Node.js
comments: true
tags: Node.js request
author: teddy8  
---
* content
{:toc}

## n
```
N
```

## 명령어

```
npm install npm@6.4.1 -g

특정 버전 설치
```

```
npm update -g npm

최신 버전 설치
```

```
npm -v

현재 버전 확인
```

```
npm init

패키지에 필요한 기본 파일들을 자동 생성한다.
패키지이름,버전,설명 등의 설정을 지정할 수 있는데 
기본 값으로 하고 싶다면 그냥 enter만 계속 누르면 된다.
완료되면 package.json파일과 node_modules폴더가 생성된다.
```

```
npm install <패키지명>

원하는 패키지를 다운 받을 수 있다.
npm install <패키지명> --save를 하면 package.json파일의 
dependencies속성에 자동으로 버전 정보가 기록된다.
```

```
npm install

어떤 프로젝트에 이미 package.json 파일이 작성되있다면 
npm install 명령어만 실행하면 된다.
그럼 package.json파일의 dependencies속성 정보를 읽어서 
지정된 패키지들을 자동으로 설치한다
```

```
더 자세한 사항은 공식문서에서 확인할 수 있다.
```
공식문서 : [https://www.npmjs.com](https://www.npmjs.com)