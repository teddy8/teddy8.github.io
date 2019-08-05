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
157.html
``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>iframe 예제</title>
</head>
<body>
  <h1>iframe 바깥문서</h1>
  <iframe id="iframe1" src="./157-1.html" frameborder="0" 
          width="100%" height="500px"></iframe>
  <script>
    const iframe1 = document.getElementById('iframe1');
    iframe1.addEventListener('load', e => {               // 로드 되면
      console.log("test");
      const iframeDocument = iframe1.contentDocument; // contentDocument (동일출처가 아니면 에러)
      iframeDocument.body.style.backgroundColor = "blue"; // 파랑색으로 바꾸고

      const newEl = document.createElement('div');
      newEl.innerHTML = '<h1>iframe 안쪽 문서';             // "안쪽 문서"라 적은 흰색 div영역 생성
      newEl.style.color = 'white';
      iframeDocument.body.appendChild(newEl);      

      setTimeout(() => {
        const iframeWindow = iframe1.contentWindow; // contentWindow
        iframeWindow.location = 'https://google-analytics.com';
      }, 3000);
    });
  </script>
</body>
</html>
```

157-1.html
``` html
<!DOCTYPE html>
<html>
<head>
  <title>iframe inner document</title>
</head>
<body>
</body>
</html>
```

```
iframe태그에 src속성에 내장할 페이지를 지정한다.
내장하는 iframe은 'load' 이벤트리스너를 등록한다.
등록할 때와 로드되고 난 후, 두 번 
```