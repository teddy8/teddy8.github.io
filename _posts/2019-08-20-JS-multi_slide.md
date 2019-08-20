---
layout: post   
title:  " JavaScript 멀티 슬라이드(Multi Slide)"
categories: JavaScript
comments: true
tags: JavaScript js 
author: teddy8  
---
* content
{:toc}

```
js에서 멀티 슬라이드(Multi Slide)에 대한 내용을 예제를 통해 정리한다.
```

## 실행결과
```
왼쪽 화살표와 오른쪽 화살표 버튼을 통해 아이템을 넘길 수가 있다.
넘어갈 때는 아이템 1개의 너비만큼 스크롤이 이동된다. 
```
![](/assets\img\javascript\multi_slide.png)

## 예제 소스코드
example.html
``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>멀티 슬라이드쇼 만들기</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>국내 여행</h1>
  <div class="slider">
    <div class="slider-btn-wrapper slider-btn-wrapper-left"> <!-- 왼쪽 화살표 -->
      <button id="left-btn" class="slider-btn">&larr;</button>
    </div>
    <div class="item-wrapper">
      <div class="item">
        <img src="./images/seoul.jpg"/>
        <div class="title">
          <h2>서울</h2>
          <p>3000원</p>
        </div>
      </div>
      <div class="item">
        <img src="./images/jeju.jpg"/>
        <div class="title">
          <h2>제주도</h2>
          <p>4000원</p>
        </div>
      </div>
      <div class="item">
        <img src="images/suwon.jpg"/>
        <div class="title">
          <h2>수원</h2>
          <p>3000원</p>
        </div>
      </div>
      <div class="item">
        <img src="./images/muju.jpg"/>
        <div class="title">
          <h2>무주</h2>
          <p>5000원</p>
        </div>
      </div>
    </div>
    <div class="slider-btn-wrapper slider-btn-wrapper-right"> <!-- 오른쪽 화살표 -->
      <button id="right-btn" class="slider-btn">&rarr;</button>
    </div>
  </div>
  <script>
  (function() { // 즉각 호출 패턴을 통해 정의와 동시에 실행
    const itemWrapperEl = document.querySelector('.item-wrapper'),  // 아이템들을 감싸는 부모 요소
          leftBtnEl = document.getElementById('left-btn'),  // 왼쪽 버튼
          rightBtnEl = document.getElementById('right-btn');  // 오른쪽 버튼

    function moveSlides(direction) {
      const item = itemWrapperEl.querySelector('.item'),  // 아이템을 선택하고
            itemMargin = parseFloat(getComputedStyle(item).marginRight); // 아이템의 오른쪽 마진값을 구한다. getComputedStyle()메소드는 해당 인자의 스타일 반환. margin은 px을 포함한 문자열로 반환되기 때문에 소수점으로 변환
            itemWidth = itemMargin + item.offsetWidth + 2; // 아이템의 너비값 계산

      let itemCount = Math.round(itemWrapperEl.scrollLeft / itemWidth); // scrollLeft값을 통해 왼쪽으로 스크롤바가 얼만큼 움직였는지 알 수 있다. 이걸 아이템너비로 나누면 몇개의 아이템을 넘겼는지 알 수 있다?

      if (direction === 'left') {
        itemCount = itemCount - 1;
      } else {
        itemCount = itemCount + 1;
      }
      itemWrapperEl.scrollLeft = itemWidth * itemCount; // 위에서 구한 값으로 이동할 스크롤의 위치값 지정
    }

    leftBtnEl.addEventListener("click", e => moveSlides("left"));
    rightBtnEl.addEventListener("click", e => moveSlides("right"));
  })();
  </script>
</body>
</html>
```

(style.css 생략)

## 설명

```
위에 주석친 부분을 문단단위로 정리한다. 

[A] 

[B] 

[C] 
```