---
layout: post   
title:  " JavaScript XMLHttpRequest"
categories: JavaScript
comments: true
tags: JavaScript js XMLHttpRequest
author: teddy8  
---
* content
{:toc}

```
XMLHttpRequest로 데이터를 전송하여 Request하고 결과값을 Response 받을 수 있다.
XMLHttpRequest 객체를 통해 비동기로 처리하는 방법을 정리한다.
비동기의 장점은 지난번 포스팅에서 설명했듯이
Response 받는 동안 다른작업을 바로 진행할 수 있다.
```

예제 소스코드
``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>XMLHttpRequest 예제</title>
</head>
<body>
<div id="user"></div>
<script>
function httpGet(url, successCallback, errorCallback) {
  const req = new XMLHttpRequest();
  req.onload = () => {
    if (req.status >= 200 && req.status < 300) {
      successCallback(req.responseText);
    } else { 
      errorCallback(new Error(req.statusText));
    }
  }
  req.onerror = errorCallback;
  req.open('GET', url);
  req.setRequestHeader('Accept', 'application/json');
  req.send();
}

const userEl = document.getElementById('user');

httpGet('https://www.naver.com/', data => {
    userEl.innerHTML = data
  }, error => alert(error));
</script>  
</body>
</html>
```

```
위와 같이 사용할 수 있다.
하지만 해당소스는
CORS(Cross-Origin Resource Sharing) 에러가 발생한다.
```

## CORS란?
```
최근 여러 도메인에 걸쳐서 구성되는 대규모 웹 프로젝트 및 REST API 등을 이용한
외부 호출이 많아지면서 해당 정책에 문제가 발생 하여 만들어진 정책이다.
웹 브라우저에서 자바스크립트의 XMLHttpRequest로 다른 웹페이지에 접근할 때는 
동일한 출처(same origin)의 페이지만 접근 할 수 있다. (혹은 그쪽에서 허락해야 한다.)
출처 : 프로토콜 + 호스트명 + 포트

CORS 에러 발생 시, GET 방식으로 전달하더라도 OPTIONS로 전달하게 된다.
그 이유는 preflight request 라고 커스텀 헤더가 추가된 요청의 경우, 
먼저 allow 헤더를 체크하기 위한 요청으로 options 메소드로 보내기 때문이다.

Access-Control-Allow-Headers 라는 응답 헤더에 서버에서 허용할 헤더값을 넣어서 주게 된다. 거기에 없는 헤더값을 클라이언트에서 요청하게 되면 CORS 정책에 의해 브라우저에서 요청을 날리지 않고 막아버리는 것이다.

즉, CORS 는 브라우저에서 요청을 날리지 않고 막는 것이다.
다만, 브라우저가 아닌 클라이언트에서 요청을 보내는 경우 응답을 받을 수 있다.

참고로 CORS에러를 우회하는 방법도 있지만 바람직한 방법은 아니므로 생략한다.
```

## References
1. [http://blog.naver.com/PostView.nhn?blogId=janghohyoung&logNo=221416034948&categoryNo=0&parentCategoryNo=41&viewDate=&currentPage=1&postListTopCurrentPage=1&from=postView](http://blog.naver.com/PostView.nhn?blogId=janghohyoung&logNo=221416034948&categoryNo=0&parentCategoryNo=41&viewDate=&currentPage=1&postListTopCurrentPage=1&from=postView)