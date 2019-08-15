---
layout: post   
title:  " Node.js API 작성(POST) "
categories: Node.js
comments: true
tags: Node.js api 작성 http post
author: teddy8  
---
* content
{:toc}

```
Node.js에서 api를 작성하는 방법을 예제를 통해 정리한다.
api는 기본적으로 요청/응답한다.
이번에는 POST 메소드를 통한 요청/응답하는 api이다.
```

## 소스코드

example.js

``` js
"use strict";

const http = require('http');
const qs = require('querystring');  

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  switch (req.method) {
    case 'POST':  
      let body = '';

      req.on('data', (chunk) => { // A
        body += chunk;  
      });
      req.on('end', () => { // B
        const obj = qs.parse(body); 
        res.writeHead(200); 
        res.end(JSON.stringify(obj)); 
      });
      req.on('error', (err) => {
        console.error(err.stack);
      });
      break;
    default:
      res.end();
  }
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

## 설명

```
GET 요청과 다르게 POST 요청시엔 이벤트리스너를 통해 바디데이터를 주고 받는다.

위에 주석친 부분을 문단단위로 정리한다.

[A] on()메소드를 통해 'data'로 이벤트 등록하고
chunk(덩어리)로 전달받은 문자형 데이터를 덧셈 연산으로 받아준다.

[B] on()메소드를 통해 'end'로 이벤트 등록한다. (요청 전송이 완료되는 시점의 이벤트)
'data' 이벤트로 수집했던 문자열들은 querystring의 parse()메소드를 통해 객체 형식으로 파싱한다.
정상적으로 전달이 완료 된 경우 응답 상태 코드 200 반환하며, 
res.end() 메소드를 통해 응답 전송을 완료한다.
```

## Postman
```
GET 요청은 웹 브라우저에 url을 입력해서 호출하였다.
POST 요청은 'Postman'이라는 Tool을 사용하면 유용하다.
```
다운로드 링크 : [https://www.getpostman.com/downloads/](https://www.getpostman.com/downloads/)

![](/assets\img\javascript\node_api_post.png)

```
Untitled Request밑에 요청형태를 "POST"로 바꾸고
url을 입력한다.(http://localhost:3000)
Body의 "x-www-form-urlencoded"를 선택하고
KEY와 VALUE에 값을 입력한 후
(a1과 1, a2와 2를 입력했다)
"Send"버튼을 누르면 보내진다.
그럼 아래의 영역에서 전달받은 내용이 표시된다.
({"a1":1,"a2":2})
```