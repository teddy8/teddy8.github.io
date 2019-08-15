---
layout: post   
title:  " Node.js API 작성(GET) "
categories: Node.js
comments: true
tags: Node.js api 작성 http get
author: teddy8  
---
* content
{:toc}

```
Node.js에서 api를 작성하는 방법을 예제를 통해 정리한다.
api는 기본적으로 요청/응답한다.
다음은 GET 메소드를 통한 요청/응답하는 api 이며,
2가지 경로로 요청한 경우를 처리하는 예제이다.
예를들면 다음과 같은 경우이다.
1. http://127.0.0.1:3000/
2. http://127.0.0.1:3000/data?qs1=2&qs2=3
```

## 소스코드

example.js

``` js
"use strict";

const http = require('http');
const url = require('url'); // url문자열 or 객체값을 쉽게 가져올 수 있음

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {  
  switch (req.method) {  
    case 'GET':
      if (req.url === '/') {
        res.setHeader('Content-Type', 'text/plain');
        res.writeHead(200);
        res.end('Hello! Node.js HTTP Server');
      } else if (req.url.substring(0, 5) === '/data') { 
        const queryParams = url.parse(req.url, true).query;

        res.setHeader('Content-Type', 'text/html');
        res.writeHead(200);
        res.write('<html><head><title>JavaScript 200제</title></head>');

        for (let key in queryParams) {  
          res.write(`<h1>${key}</h1>`); 
          res.write(`<h2>${queryParams[key]}</h2>`); 
        }

        res.end('</body></html>');
      }
      break;
    default:  // case에 없는 경우 바로 완료 처리
      res.end();
  }

});

server.listen(port, hostname, () => { 
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

## 설명

```
http의 createServer()메소드를 통해 서버를 생성한다.
req의 method를 통해 4가지중 어떤 동작을 하는지 파악할 수 있다.(GET, POST, PUT, DELETE) 
case 'GET'을 작성해 GET으로 요청한 경우를 처리해준다.
req의 url을 통해 요청한 경로가 '/'를 포함하는 요청인 경우
(http://127.0.0.1:3000/ 이런식인 경우)
기본적인 헤더값과 상태요청코드(200), res의 end()메소드를 통해 'Hello! Node.js HTTP Server'문구를 전달하고 끝낸다.
req의 url을 통해 요청한 경로가 '/data'를 포함하는 요청인 경우
(http://127.0.0.1:3000/data?qs1=2&qs2=3 이런식인 경우)
url의 parse()메소드를 통해 url의 문자열값을 객체값으로 파싱한다.
(파싱한 객체값은 이런식으로 들어가 있다. queryParams: {qs1: '1', qs2: '2'})
기본적인 헤더값과 상태요청코드(200), res의 write()메소드를 통해 html코드를 전달한다.
파싱한 객체값은 for-each문으로 key와 value를 접근하면서 res의 write()메소드로 html코드를 연달아 보내준다.
다 보냈으면 res의 end()메소드로 열어놓았던 html태그를 모두 닫아준 뒤 마무리한다.
(즉, write로 헤더정보 및 html코드 연달아 보내다가 end로 마무리한 것)
```

## 실행결과
![](/assets\img\javascript\node_api.png)

## http.get
```
GET요청을 웹 브라우저의 url입력을 통해 호출하였지만 http.get()메소드를 통해서도 가능하다.
보통 http의 request()메소드를 사용하지만, body 데이터의 전송 없이 간단하게 요청할 때는 
http.get()를 사용한다.
```

example.js

``` js
http.get('http://localhost:3000', (res) => {  
  let data = '';
  res.on('data', function(chunk) {
    data += chunk;
    console.log('data of res.on =====> ', data);
  });
  res.on('end', function() {
    try {
      console.log('end of res.on =====> ', data);
      return data;
    } catch (err) {
      if (err) console.log(err);
    }
  });
});
```