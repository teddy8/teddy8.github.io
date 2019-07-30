---
layout: post   
title:  " JavaScript 현재 문서정보 확인하기"
categories: JavaScript
comments: true
tags: JavaScript js window location
author: teddy8  
---
* content
{:toc}


## 현재 페이지의 url 가져오기

example.html

``` html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>예제</title>
  </head>
  <body>
    <script>
      alert(location.href);
    </script>
  </body>
</html>

```

실행결과

```
http://127.0.0.1:5500/example.html
```

## 현재 도메인 이름 가져오기

example.html

``` html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>예제</title>
  </head>
  <body>
    <script>
      alert(location.hostname);
    </script>
  </body>
</html>

```

실행결과

```
127.0.0.1
```

## 현재 경로 및 파일이름 가져오기

example.html

``` html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>예제</title>
  </head>
  <body>
    <script>
      alert(location.pathname);
    </script>
  </body>
</html>

```

실행결과

```
/example.html
```

## 현재 웹 프로토콜 가져오기

example.html

``` html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>예제</title>
  </head>
  <body>
    <script>
      alert(location.protocol);
    </script>
  </body>
</html>

```

실행결과

```
http:
(or https:)
```

## 다른 페이지로 이동하기

example.html

``` html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>예제</title>
  </head>
  <body>
    <script>
      location.href("https://naver.com");
    </script>
  </body>
</html>

```

```
location.assign으로도 가능하다
```

## 부록
```
location.search는 
?a=12&b=34 와 같이
GET방식으로 넘긴 데이터값을 가져올 수 있다.
```