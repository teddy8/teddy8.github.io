---
layout: post   
title:  " JavaScript 로컬 파일 읽기"
categories: JavaScript
comments: true
tags: JavaScript js local file read 
author: teddy8  
---
* content
{:toc}

```
로컬이미지 파일을 드래그 앤 드랍하면 
브라우저에 이미지가 표시되는 예제의 내용을 정리한다.
```

## 예제 소스코드
``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8"> 
  <title>로컬 파일을 브라우저에서 읽기 예제</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div id="file-box" class="dot-box">
    이미지 파일을 선택한 후 이곳에 끌어서 놓아주세요.
  </div>
  <output id="result"></output>
  <script>
    var dropZone = document.getElementById('file-box');
    dropZone.addEventListener('dragover', e => {
      e.stopPropagation();  // 상위 전파 막기
      e.preventDefault();   // 기본 동작 막기. 브라우저가 이미지화면으로 전환하는 것을 막기 위함
    });
    dropZone.addEventListener('drop', e => {
      e.stopPropagation();
      e.preventDefault();
      const files = e.dataTransfer.files;      
      Array.from(files) // files를 배열화
        .filter(file => file.type.match('image.*')) // file type이 image인것만 필터링
        .forEach(file => {  // 여러개의 이미지 처리하기 위해
          const reader = new FileReader();
          reader.onload = (e) => {
            const imgEl = document.createElement('img');
            imgEl.src = e.target.result;
            imgEl.title = file.name;
            document.getElementById('result').appendChild(imgEl);
          };
          reader.readAsDataURL(file);
        });
    });
  </script>
</body>
</html>
```

```
소스코드를 간략히 설명하자면 "dragover"와 "drag"시 이벤트가 전파되는 것을 방지한다.
브라우저에 이미지를 끌어다 놓으면 이미지화면으로 전환되기 때문에 기본 동작을 방지한다.
드랍 시킨 file들을 Array.from()으로 배열화 시킨다.
file중 image파일인 것만 필터링한다.
파일을 하나씩 처리하는데 FileReader()를 통해 onload 이벤트리스너를 콜백함수(비동기)로 등록한다.
(onload는 리소스를 다 읽었을 때 이벤트가 발생된다)
파일을 다 읽을 때마다 'img'라는 엘리먼트를 생성해서 'result'란에 이미지를 표시한다.

다음과 같이 로컬이미지파일을 드래그 앤 드랍하여 업로드하면 화면에 표시된다.
```

![](/assets\img\javascript\local_image_upload.png)
