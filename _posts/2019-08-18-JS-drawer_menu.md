---
layout: post   
title:  " JavaScript 숨김 메뉴(drawer menu)"
categories: JavaScript
comments: true
tags: JavaScript js 
author: teddy8  
---
* content
{:toc}

```
js에서 버튼을 클릭하면 메뉴가 표시되고 다시 누르면 
메뉴가 사라지는 것에 대한 내용을 예제를 통해 정리한다.
```

## 실행결과
```
버튼 클릭 시, 오른쪽에 숨겨져있던 메뉴가 표시된다. 
다시 클릭하면 메뉴가 들어가는 간단한 예제이다.
```
![](/assets\img\javascript\drawer_menu.png)

## 예제 소스코드
example.html
``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">    
  <title>숨김 메뉴(drawer menu) 만들기 예제</title>  
</head>
<body>
  <button id="drawer-opener">OPEN MENU</button>
  <div class="drawer">
    <h2>숨김 메뉴</h2>
    <ul>
      <li>항목 1</li>
      <li>항목 2</li>
    </ul>
  </div>  
  <script>
    function Drawer(el, open = false) { // A 
      this.el = el;
      this.isOpen = open;
      Object.assign(this.el.style, {
        display: 'block', 
        position: 'fixed',
        top: 0,
        bottom: 0,
        right: 0,
        width: '200px',
        padding: '10px',
        backgroundColor: 'white',
        boxShadow: '0 0 36px 0 rgba(0,0,0,0.1)',
        transition: 'all 0.4s ease-out' 
      });
      (this.isOpen) ? this.open() : this.close();
    }
    Drawer.prototype.open = function() {  // B 
      this.isOpen = true;
      this.el.style.transform = 'translate(0px)'; 
    }
    Drawer.prototype.close = function() { 
      this.isOpen = false;
      this.el.style.transform = 'translate(220px)'; 
    }

    const sideMenu = new Drawer(document.querySelector('.drawer')); // C
    document.getElementById('drawer-opener')
    .addEventListener('click', e => {  
        (!sideMenu.isOpen) ? sideMenu.open() : sideMenu.close();
      });
  </script>
</body>
</html>
```

## 설명

```
위에 주석친 부분을 문단단위로 정리한다. 

[A] Drawer()메소드를 정의한다. 숨김메뉴가 적용될 요소와 메뉴의 초기 열림상태를 전달받는다.
Object.assign()메소드를 통해 메뉴가 숨겨진 상태의 스타일 값을 지정한다.
메뉴의 초기 열림상태에 따라 prototype으로 정의한 메소드를 실행한다. (true면 open, false면 close)
메뉴의 초기 열림상태의 Default값은 false이다.

[B] Drawer()메소드를 prototype으로 정의한 open()메소드는 transform값을 이용해서 x축으로 0픽셀 이동하여 화면에 표시한다.
Drawer()메소드를 prototype으로 정의한 close()메소드는 transform값을 이용해서 x축으로 220픽셀 이동하여 화면에 표시한다.

[C] 숨김메뉴를 적용하기 위해 'drawer'를 클래스로 갖는 요소를 Drawer() 메소드로 전달하여 인스턴스를 생성한다.
'drawer-opener'를 id로 갖는 요소에 클릭 이벤트 리스너를 등록한다.
해당 요소를 클릭했을 경우 Drawer()를 통해 생성한 인스턴스의 변수 isOpen값이
false면(즉, 메뉴가 닫혀 있으면 open 하고) isOpen값이 true면(즉, 메뉴가 열려 있으면 close 한다.)
```