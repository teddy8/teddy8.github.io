---
layout: post   
title:  " JavaScript "
categories: JavaScript
comments: true
tags: JavaScript js 
author: teddy8  
---
* content
{:toc}

```
js에서 커스텀 이벤트에 대한 내용을 예제를 통해 정리한다.
```

## 실행결과
```
주문하기 버튼 클릭 시, 로그인을 해달라는 문구가 표시 된 영역이 생성된다.
이 영역의 닫기버튼을 눌렀을 때 커스텀이벤트가 발생되는 간단한 예제이다.
```
![](/assets\img\javascript\custom_event.png)

## 예제 소스코드
example.html
``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>사용자 이벤트 생성하기 예제</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>   
<div class="order-area">
  <div>상품정보: 노트북 1대</div>
  <button id="order-btn">주문하기</button>
</div>
<script>
  function buildAlert(title, message) { // A   
    const alert = document.createElement('div');  
    const id = Math.ceil(Math.random() * 1000);   
    alert.id = id;
    alert.className = 'alert';  
    alert.innerHTML = `<span class="close">&times;</span> 
                       <h3>${title}</h3>
                       <p>${message}</p>`;
    
    alert.querySelector('span.close').addEventListener('click', e => {  // B
        const closeEvt = new CustomEvent('close', { bubbles: true,
                                                    detail: {id, message} });
        alert.dispatchEvent(closeEvt);
        alert.remove(); 
      });

    document.body.append(alert); // C
    return alert;
  }

  document.getElementById("order-btn").addEventListener('click', e => { 
    const alertE1 = buildAlert('에러', '로그인을 해주세요.');
    alertE1.addEventListener('close', e => {  
      console.log(e.detail);
      console.log('error 창을 닫았습니다.');
    })
  });
</script>
</body>
</html>
```

## 설명

```
위에 주석친 부분을 문단단위로 정리한다. 

[A] 알림창을 생성하는 메소드를 정의한다. 
createElement() 메소드를 통해 div를 생성한다.
이 알림창의 고유키를 부여하기 위해 랜덤번호를 부여한다.
&times;(특수문자 'x')를 통해 div내부에 닫기버튼을 표시한다.

[B] 닫기버튼에 클릭 이벤트 리스너를 등록한다.
new키워드를 통해 CustomEvent()메소드로 커스텀이벤트 인스턴스를 생성한다. 
생성할 때, 이벤트명과(close) 옵션객체(고유번호 및 오류문구)를 매개변수로 전달한다. 
dispatchEvent()메소드를 통해 이벤트 발생 시, 커스텀이벤트가 발생되게 한다.
커스텀이벤트가 발생되면 remove()메소드를 통해 해당 알림창이 삭제된다.

[C] 알림창을 body의 가장 아래에 추가한다.
위에 추가해도 되고 아래에 추가해도 되는데 append()를 통해 아래에 추가하였다.
이것과 유사한 메소드의 특징은 다음과 같다.
append()  - 콘텐츠를 선택한 요소 내부의 끝 부분에서 삽입
prepend() - 콘텐츠를 선택한 요소 내부의 시작 부분에서 삽입
after()   - 선택한 요소 뒤에 컨텐츠 삽입
before()  - 선택된 요소 앞에 컨텐츠 삽입
```