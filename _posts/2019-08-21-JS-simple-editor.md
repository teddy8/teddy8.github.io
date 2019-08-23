---
layout: post   
title:  " JavaScript 간단한 에디터(Simple Editor)"
categories: JavaScript
comments: true
tags: JavaScript js 
author: teddy8  
---
* content
{:toc}

```
js에서 간단한 에디터를 만드는 방법을 예제를 통해 정리한다.
```

## 실행결과
```

```
![](/assets\img\javascript\simple_editor.png)

## 예제 소스코드
example.html
``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.5.0/css/all.css"> <!-- 폰트 어썸 css 적용. html에서 'fa fa-bold'처럼 css클래스 이름을 주면 적용가능 -->
  <link rel="stylesheet" href="style.css">
  <title>간단한 텍스트 에디터 만들기 예제</title>
</head>
<body>
  <div class="toolbar"> <!-- 39라인까지 상단 툴바 작성. data-command='h1' 이런식으로 텍스트에 전달할 명렁 작성가능-->
    <a href="" data-command='h1'>H1</a> 
    <a href="" data-command='h2'>H2</a>
    <a href="" data-command='h3'>H3</a>
    <a href="" data-command='p' style="margin-right: 8px;">P</a>

    <a href="" data-command='bold'>
      <i class='fa fa-bold'></i>
    </a>
    <a href="" data-command='italic'>
      <i class='fa fa-italic'></i>
    </a>
    <a href="" data-command='underline'>
      <i class='fa fa-underline'></i>
    </a>
    <a href="" data-command='strikeThrough'style="margin-right: 8px;">
      <i class='fa fa-strikethrough'></i>
    </a>

    <a href="" data-command='justifyLeft'>
      <i class='fa fa-align-left'></i>
    </a>
    <a href="" data-command='justifyCenter'>
      <i class='fa fa-align-center'></i>
    </a>
    <a href="" data-command='justifyRight'>
      <i class='fa fa-align-right'></i>
    </a>
    <a href="" data-command='justifyFull' style="margin-right: 8px;">
      <i class='fa fa-align-justify'></i>
    </a>
  </div>
  <div class='editor' contenteditable="true"> <!-- contenteditable이 true면 편집가능 -->
    <h1>심플 에디터</h1>
    <p>간단한 에디터</p>
  </div>
  <script>
    document.querySelectorAll('.toolbar a') // 툴바 영역의 모든 버튼 선택
      .forEach(aEl => aEl.addEventListener('click', function (e) {  
        e.preventDefault(); // 기본 행위 방지
        const command = aEl.dataset.command;  // data-command 속성값을 dataset 객체의 command 속성을 통해 가져온다.
        if (command == 'h1' || command == 'h2' || command == 'h3' || command == 'p') { 
          document.execCommand('formatBlock', false, command); // execCommand(명령이름, 기본 사용자 UI를 보여주는 여부, 특정 명령에 필요한 값)
        } else {
          document.execCommand(command); }
        }));    
  </script>
</body>
</html>

<!-- 
formatBlock 같은 명령의 자세한 확인  
https://developer.mozilla.org/en-US/docs/Web/API/Document/execCommand#Commands)
-->
```

(style.css 생략)

## 설명

```
위에 주석친 부분을 문단단위로 정리한다. 

[A] 즉

[B] mo

[C] 왼쪽
```