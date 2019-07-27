---
layout: post   
title:  " JavaScript POST GET Request"
categories: JavaScript
comments: true
tags: JavaScript js POST GET REQUEST 전송 방식
author: teddy8  
---
* content
{:toc}

# In html

``` html
<form method="post" action="/login.php">
  <div>
    <label for="id">ID </label>
    <input type="text" name="id"/>
  </div>
  <div>
    <label for="pw">PW </label>
    <input type="text" name="pw"/>
  </div>

  <div class="button">
    <button type="submit"> login </button>
  </div>
</form>
```

```
html의 form 요소에서 method에 전달방식(post/get)과 action에 url을 입력한 후,

submit버튼을 클릭하면 입력값에 대한 데이터 값들을 해당 url에 request하게 된다.

js에서 이러한 기본로직을 막고 싶다면 preventDefault() 메소드를 호출하면 된다.

추가로, method와 url도 js에서 설정할 수 있다.

예제소스는 다음과 같다.
```


## In Javascript
``` html 
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">    
  <title>HTML 폼 활용하기 예제</title>
</head>
<body>
  <form name="order">
    <fieldset name="productInfo">
      <legend>상품 정보</legend>      
      상품명: <input name="productName" type="text">
      색상: 
      <select name="color">
        <option value="black">검은색</option>
        <option value="yellow">노란색</option>
      </select>
    </fieldset>
    <button type="submit">submit 제출</button>
  </form>
  <script>    
    const orderForm = document.forms.order,
          productField = orderForm.elements.productInfo;

    orderForm.addEventListener('submit', e => {
      e.preventDefault();         // html에서 form의 기본 로직 방지
      const { productName, color } = productField.elements;
      console.log(`${productName.value} 상품 ${color.value}색을 주문합니다.`);

      orderForm.method = 'GET';   // 전달방식 설정
      //orderForm.action = 'url'  // url 설정 (생략 시 해당파일에 보냄)
      orderForm.submit();         // request
    });
  </script>
</body>
</html>
```

```
XMLHttpRequest 객체를 사용하는 방법도 있다.
그건 추후에 포스팅 예정이다.
```