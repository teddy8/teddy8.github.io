---
layout: post   
title:  " JavaScript iframe 통신"
categories: JavaScript
comments: true
tags: JavaScript js iframe 통신 communication 메시지 전달
author: teddy8  
---
* content
{:toc}

```
js에서 iframe에서 main-frame으로 메시지를 전달하는 방법을 예제를 통해 정리한다.
```

## 예제 소스코드
example.html
``` html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>iframe 메시지 교환하기</title>
  </head>
  <body>
    <div>
      <label>결제금액 :</label> <b>20000원</b>
      <br />
      <button id="checkout-btn">카드입력</button>
    </div>
    <iframe
      id="card-payment"
      width="500px"
      height="200px"
      frameborder="0"
    ></iframe>
    <script>
      const iWindow = document.getElementById("card-payment").contentWindow;

      document.getElementById("checkout-btn").addEventListener("click", e => { // A
        iWindow.location = "payment.html";
      });

      window.addEventListener("message", e => { // B
        if(!e.data.hasOwnProperty('cardNumber'))
          return;
        console.log(e);
      });
    </script>
  </body>
</html>

```

payment.html
``` html
<script>
  function submitForm() { // C
    const form = document.getElementById("card-form");
    const formData = new FormData(form);
    const formObj = {
      cardNumber: formData.get("cardNumber"),
      holderName: formData.get("holderName")
    };
    window.parent.postMessage(formObj, "*");
  }
</script>

<form id="card-form" onsubmit="submitForm()">
  <div>
    <label>카드번호</label>
    <input type="text" name="cardNumber" />
  </div>
  <div>
    <label>이름</label>
    <input type="text" name="holderName" />
  </div>
  <button type="submit">결제하기</button>
</form>
```

![](/assets\img\javascript\iframe_communication.png)

```
전체적인 흐름을 설명하고 위에 주석친 부분을 문단단위로 정리한다.

main-frame인 example.html에 iframe이 내장되 있고 "카드입력" 버튼을 클릭하면 
iframe의 내부페이지가 payment.html로 변경된다. 그 후, 카드번호와 이름을 입력해서 
결제하기로 submit하면 해당 폼 데이터를 payment.html에서 객체로 생성해서 
postMessage로 main-frame에 전달한다.

그런데 payment.html에서 submit버튼을 눌러야 
158.html의 message 이벤트리스너가 호출되는 것이 정상인데

Live Server로 실행해보면 아무것도 건들지 않았는데도 뭔가 예약된 메시지가 있는 것인지
message 이벤트 리스너가 기본적으로 2번 호출되고 시작한다. 전달받은 데이터는 
콘솔내용을 확인해보니 data의 id가 "js"인 것과 "patterns"이다. 
이게 왜 오는 것인지 확인중이며, 이 때 카드번호와 이름이 넘어오진 않기 때문에 
iframe과는 연관이 없어보인다. 그래서 일단 카드번호를 전달하는 프로퍼티인 
"cardNumber"가 존재하는지 hasOwnProperty()메소드로 확인하여 처리하였다.


[A] 카드입력 버튼을 누르면 내부페이지를 payment.html로 location을 통해 변경한다.


[B] iframe에서 postMessage로 전달하면 message 이벤트가 발생한다. 전달받은 메시지도 event 파라미터로 접근가능하다.


[C] submit 버튼이 눌렸을 때 postMessage()를 통해 main-frame으로 데이터를 전달한다.
```

## postMessage

```
postMessage는 안전하게 cross-origin통신을 할 수 있게 한다. 
페이지와 생성된 팝업 간의 통신이나, 페이지와 페이지 안의 iframe 간의 통신할 때 사용할 수 있다.
함수원형은 다음과 같다. 
postMessage(message, targetOrigin, [transfer])
쉽게 말하면 postMessage(데이터, 타겟)이다.
타겟은 주의할 점이 있는데 비밀번호가 전송된다면, 악의적인 제 3자가 가로챌 수 있기 때문에 데이터가 
유출될 수 있다. 따라서 다른 window의 document의 위치를 알고 있다면 "*"와 같이 
별도로 지정하지 않는 것 보다 특정한 대상을 지정해주는 것이 좋다.
```
참고 [https://developer.mozilla.org/ko/docs/Web/API/Window/postMessage](https://developer.mozilla.org/ko/docs/Web/API/Window/postMessage)