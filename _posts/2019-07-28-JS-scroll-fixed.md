---
layout: post   
title:  " JavaScript 스크롤(Scroll) 처리"
categories: JavaScript
comments: true
tags: JavaScript js 스크롤 Scroll 고정 처리 Sticky
author: teddy8  
---
* content
{:toc}

# 스크롤 고정

```
스크롤을 내려도 네비게이션이 항상 보이게 처리하는 방법 2가지를 소개한다
1. Javascript
2. CSS
```

## In Javascript

example.html

``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>DOM 네비게이션 예제</title>
  <link rel="stylesheet" href="./scroll.css">
</head>
<body>
  <section class="hero">
    <h1>스크롤을 아래로 내려보세요.</h1>
  </section>
  <nav>
    <a>자바스크립트 200제</a>
  </nav>
  <section class="articles">
  </section>
  <script>
    const nav = document.querySelector('nav');
    const navTopOffset = nav.offsetTop;
    window.addEventListener('scroll', e => {
      // nav를 상단에 고정. (브라우저 상단의 차이가 nav와 브라우저 상단의 차이보다 클 경우)
      if (window.pageYOffset >= navTopOffset) { 
        nav.style.position = 'fixed';
        nav.style.top = 0;
        nav.style.left = 0;
        nav.style.right = 0;
      } else {
        nav.style.position = '';
        nav.style.top = '';
      }
    });
  </script>
</body>
</html>
```

scroll.css

``` css
* { margin: 0; }
.hero {
  height: 100px;
  padding: 20px;
  text-align: center;
  background-color: #ccc;
}
nav {
  background-color: black;
  padding: 10px;
}
a {
  text-decoration: none;
  color: white;
}
.articles { height: 2000px; }
```

실행결과

![](/assets\img\javascript\Scroll_Fixed.png)

```
스크롤을 내리면 원래 검정색 nav부분이 사라져야 하지만
브라우저 상단의 차이가 nav와 브라우저 상단의 차이보다 클 경우
nav요소를 상단에 위치하게 fixed 처리하여 고정된 모습을 볼 수 있다.
```

## In CSS

example.html

``` html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>네비게이션 예제</title>
    <link rel="stylesheet" href="./scroll.css" />
  </head>
  <body>
    <div id="header">Header</div>
    <nav id="nav">Navigation</nav>
    <div id="content">Content</div>
  </body>
</html>
```

scroll.css

``` css
#header,
#nav,
#content {
  color: white;
  text-decoration: none;
}

#header {
  background: red;
  height: 100px;
}

#nav {
  background: cornflowerblue;
  text-align: center;
  padding: 40px 0px;
  position: sticky;
  top: 0;
}

#content {
  background-color: green;
  height: 1000vh;
}
```

실행결과

![](/assets\img\javascript\Scroll_Fixed(2).png)

```
position을 sticky로 설정하고 top을 0으로 설정하면
마찬가지로 스크롤 고정을 구현할 수 있다.
(단 IE는 지원하지 않는다.)
```