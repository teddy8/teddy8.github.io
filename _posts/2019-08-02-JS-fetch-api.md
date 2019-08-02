---
layout: post   
title:  " JavaScript Fetch API"
categories: JavaScript
comments: true
tags: JavaScript js Fetch API
author: teddy8  
---
* content
{:toc}

```
지난 포스팅에 XMLHttpRequest로 HTTP 통신을 정리했었다.
```
[https://teddy8.github.io/2019/08/01/JS-xmlhttprequest/](https://teddy8.github.io/2019/08/01/JS-xmlhttprequest/)
```
이번 포스팅은 Fetch-api라는 Promise기반의 비동기로 처리하는 방법을 정리한다.
```
공식문서 [https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

## 예제 소스코드
``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Fetch API 예제</title>
</head>
<body>
<div id="user"></div>
<script>
const userEl = document.getElementById('user');
const reqPromise = fetch('https://naver.com', { 
    headers: { Accept: 'application/json' },
    method: 'GET'
  });
reqPromise
  .then(res => {
    if (res.status >= 200 && res.status < 300) {
      return res.json();
    } else {
      return Promise.reject(new Error(`error ${res.status}`));
    }
  })
  .then(data => { userEl.innerHTML = data })
  .catch(error => alert(error));
</script>
</body>
</html>
```

```
XMLHttpRequest처럼 CORS가(지난번 포스팅) 발생할 수 있으며,
XMLHttpRequest처럼 와 비교했을 때, 가독성이 조금 더 증가 된 느낌이다.
```