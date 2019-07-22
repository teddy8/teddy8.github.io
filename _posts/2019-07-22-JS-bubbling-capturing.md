---
layout: post   
title:  " JavaScript 버블링(Bubbling) vs 캡처링(Capturing)"
categories: JavaScript
comments: true
tags: JavaScript js 이벤트 버블링 Bubbling 캡처링 Capturing
author: teddy8  
---
* content
{:toc}

## 개념

```
DOM에서 이벤트가 발생하면 이벤트가 부모에서 자식으로 가는지
자식에서 부모로 가는지에 따라 버블링과 캡처링으로 구분된다.
특징을 정리하자면 다음과 같다.
버블링 : Top-down
캡처링 : Bottom-up
```

## 예제
``` html
<div id="A" class="box">
  <div id="B" class="box2"></div>
</div>
<div id="C" class="box">
  <div id="D" class="box2"></div>
</div>
<script>
  element1.addEventListener('click', e => console.log('1'));
  element2.addEventListener('click', e => console.log('2'));
  element3.addEventListener('click', e => console.log('3'), true);
  element4.addEventListener('click', e => console.log('4'));
</script>
```

```
위처럼 A, B, C, D의 id를 부여한 4개의 div영역을 생성한다.
또한, 클릭 시 1, 2, 3, 4가 출력되게 이벤트리스너를 등록한다.
```

![](/assets\img\javascript\Bubbling_vs_Capturing.png)

```
A 클릭 시 1
C 클릭 시 3
이 출력됩니다. 하지만

B 클릭 시 2 1
D 클릭 시 3 4 가 출력 됩니다.

그 이유는
A, B는 버블링(Top-down) 단계에서 호출 되지만
C, D는 C의 리스너에 TRUE로 설정해줌으로써 캡처링(Bottom-up) 단계에서 호출되기 때문이다.
```