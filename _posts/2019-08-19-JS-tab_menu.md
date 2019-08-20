---
layout: post   
title:  " JavaScript 탭 메뉴(Tab Menu)"
categories: JavaScript
comments: true
tags: JavaScript js 
author: teddy8  
---
* content
{:toc}

```
js에서 탭 메뉴(Tab Menu)에 대한 내용을 예제를 통해 정리한다.
```

## 실행결과
```
'체코'탭을 누르면 url뒤에 #czech가
'독일'탭을 누르면 url뒤에 #germany가 붙는다.
이처럼 탭이 바뀔 때마다 브라우저의 url이 변경되는
해쉬 URL값을 통한 탭 메뉴 예제이다.
```
![](/assets\img\javascript\tab_menu.png)

## 예제 소스코드
example.html
``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>탭메뉴 만들기 예제</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>여행지 설명</h1>
  <div class="tabs"> <!-- A -->
    <ul>
      <li><a href="#czech">체코</a></li>
      <li><a href="#germany">독일</a></li>
      <li><a href="#british">영국</a></li>     
    </ul>
    <div class="tab_content">
      <div id="czech">
        <h3>체코</h3>
        <p>체코는 아름다운 동유럽의 나라입니다.</p>
      </div>
      <div id="germany">
        <h3>독일</h3>
        <p>독일은 맥주가 유명한 유럽의 나라입니다.</p>
      </div>
      <div id="british">
        <h3>영국</h3>
        <p>영국은 유럽의 서북쪽에 위치한 섬나라입니다.</p>
      </div>
    </div>
  </div>
<script>
function createTabs(selector) { // B   
  const el = document.querySelector(selector);  
  const liEls = el.querySelectorAll('ul li'); 
  const tabContentEl = el.querySelector('.tab_content'); 
  const firstTabEl = liEls.item(0).firstElementChild  

  function activate(target) { // C   
    const hash = target.hash;
    const anchors = target.closest('ul')
    .querySelectorAll('li a');  
    
    Array.from(anchors).forEach(v => v.className = '');  
    Array.from(tabContentEl.children).forEach(v => v.style.display = 'none'); 
    tabContentEl.querySelector(hash).style.display = '';  
    target.className = 'active';
  } // 끝

  const handleHash = () => { // D    
    if (location.hash) {  
      const selector = `a[href="${location.hash}"]`;  
      activate(document.querySelector(selector)); 
    } else {
      activate(firstTabEl); 
    }
  }

  window.addEventListener('hashchange', handleHash);  // E
  handleHash(); 
}

createTabs('.tabs');  // F
</script>
</body>
</html>
```

(style.css 생략)

## 설명

```
위에 주석친 부분을 문단단위로 정리한다. 

[A] a태그에 해시값(#)이 붙는 특징이 있다.

[B] 탭을 만드는 메소드를 정의한다. 탭을 만들어야 할 요소를 인자로 받는다.
전달받은 요소를 selector로 찾아서 변수 선언한다.
ul밑에 있는 모든 li를 liEls로 변수 선언한다.
class가 tab_content인 요소를 selector로 찾아서 변수 선언한다.
모든 li중 첫번째 li의 child요소를 첫번째탭 요소로 지정하기 위한 변수 선언한다.

[C] 특정탭을 활성화하기 위한 activate()메소드를 정의한다. 특정탭의 <a>요소를 인자로 받는다.
전달받은 <a>요소의 hash 속성값을 상수로 정의한다.
(hasg 속성값은 예를들면 #czech #germany #british ... 이다)
closest()메소드를 통해 부모 요소들 중 가장 가까운 <ul> 요소를 선택하고 
해당 ul요소의 li요소에 있는 모든 a요소를 변수에 할당한다.

기존에 활성화된 탭을 제거하기 위해 모든 a요소들의 클래스 명을 제거한다.
전체 탭의 상세 내용을 담고 있는 모든 요소(class가 tab_content인)들을 화면에서 보이지 않게 처리한다.
hash를 selector로 찾은 후, display를 초기화해서 화면에 보여지게 한다.

[D] 해쉬가 변경될 때 처리하는 콜백 메소드를 정의한다.
현재 해쉬값이 있으면 해당 해쉬값을 href 속성으로 가지는 탭버튼을 선택하고, activate()메소드를 통해 해당 탭버튼 활성화한다.
현재 해쉬값이 없으면 첫번째 탭을 활성화 시킨다.

[E] 'hashchange'이벤트 리스너를 등록한다. (브라우저의 URL 해쉬값이 변경될 때마다 'hashchange'이벤트가 발생한다.)
handleHash()콜백 메소드를 통해 createTabs()메소드를 호출할 당시의 브라우저의 URL 해쉬값에 대해 처리한다.

[F] createTabs()메소드의 호출을 통해 탭메뉴를 생성한다.(class가 tabs인 요소를 createTabs()메소드에 전달)
```