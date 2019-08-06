---
layout: post   
title:  " JavaScript iframe 제어"
categories: JavaScript
comments: true
tags: JavaScript js iframe 제어 control 
author: teddy8  
---
* content
{:toc}

```
js에서 iframe을 제어하는 방법을 예제를 통해 정리한다.
```

## 예제 소스코드
example.html
``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>iframe 예제</title>
</head>
<body>
  <h1>main-frame (바깥 문서)</h1>
  <iframe id="iframe1" src="./1.html" frameborder="0" 
          width="100%" height="500px"></iframe>
  <script>
    const iframe1 = document.getElementById('iframe1'); // A
    iframe1.addEventListener('load', e => {               
      const iframeDocument = iframe1.contentDocument;
      iframeDocument.body.style.backgroundColor = "blue";

      const newEl = document.createElement('div'); // B
      newEl.innerHTML = '<h1>iframe (안쪽 문서)</h1>';           
      newEl.style.color = 'white';
      iframeDocument.body.appendChild(newEl);      

      setTimeout(() => { // C
        const iframeWindow = iframe1.contentWindow; 
        iframeWindow.location = 'https://google-analytics.com';
      }, 3000);
    });
  </script>
</body>
</html>
```

1.html
``` html
<!DOCTYPE html>
<html>
<head>
  <title>iframe</title>
</head>
<body>
</body>
</html>
```

```
html에서 iframe태그에 src속성에 내장할 페이지를 지정할 수 있으며,
위에 주석친 부분을 문단단위로 정리한다.

[A] contentDocument를 통해 iframe의 독립적인 document를 접근해서 body의 배경색을 지정할 수 있다.

[B] iframe에 div요소를 추가할 때는 document.createElment로 div를 생성해서 
iframe의 독립적인 document인 contentDocument.body에 appendChild하면 된다.

[C] contentWindow를 통해 iframe의 독립적인 window를 접근해서 location을 변경할 수 있다.
다만, 동일 출처 정책이라 해서 서버에서 응답하는 HTTP 헤더는 X-Frame-Options가 'sameorigin'으로 설정되어 있기 때문에 
iframe통해 다른페이지를 내장할 순 있지만 동일 출처 정책에 부합하지 않으면 iframe의 window객체나 document객체에 접근하여 element를 수정하는 행위는 할 수 없다. 즉, iframe에 다른 페이지를 연결해서 element를 수정하는 행위는 
프로토콜(http/https), 포트(ex:8080), 도메인(com/co.kr/net/org)이 모두 같을 때 가능하다.      
```