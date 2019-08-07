---
layout: post   
title:  " JavaScript 웹 워커(Web Worker)"
categories: JavaScript
comments: true
tags: JavaScript js 웹 워커 Web Worker
author: teddy8  
---
* content
{:toc}

```
js에서 별도의 스레드에서 실행할 수 있는 웹 워커(Web Worker)의 사용방법을 예제를 통해 정리한다.
```

## 예제 소스코드
example.html
``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>웹워커 예제</title>
</head>
<body>
  <div>
    <input type="number" id="number">
    <button id="start-btn">피보나치수열 계산시작</button>      
  </div>
  <div id="result"></div>
  <script>
    const result = document.getElementById('result');
    let isCalculation = false;
    if (window.Worker) {
      const fibonacciWorker = new Worker('fibonacci.js'); // A
      document.getElementById('start-btn').addEventListener('click', e => {
          if (isCalculation) { 
            return;
          }
          const value = document.getElementById('number').value;
          fibonacciWorker.postMessage({ num: value });  
          result.innerHTML = '계산중...';
          isCalculation = true;
        });
      fibonacciWorker.onmessage = function(e) { // B
        result.innerHTML= e.data;
        isCalculation = false;
      };
      fibonacciWorker.onerror = function(error) { // C
        console.error('에러 발생', error.message);
        result.innerHTML= error.message;
        isCalculation = false;
      };
    }
  </script>
</body>
</html>
```

fibonacci.js
``` js
function fibonacci(num) { 
  if (num <= 1) {
    return 1;
  }
  return fibonacci(num - 1) + fibonacci(num - 2);
}

onmessage = function(e) { // D
  const num = e.data.num;
  console.log('메인 스크립트에서 전달 받은 메시지', e.data);
  if (num == null || num === "")  {
    throw new Error('숫자를 전달하지 않았습니다.');
  }
  const result = fibonacci(num);
  postMessage(result);  
}
```

실행 결과
![](/assets\img\javascript\web-worker.png)

```
전체적인 흐름을 설명하고 위에 주석친 부분을 문단단위로 정리한다.

계산시작 버튼을 누르면 입력한 숫자값을 fibonacci.js의 onmessage 콜백함수에 전달한다. 
fibonacci.js는 전달받은 숫자값으로 계산을 수행한 뒤, 다시 example.html의 onmessage로 
postMessage() 메소드를 통해 결과값을 전달한다. 단, 전달받은 숫자가 null이거나 공백일 경우 
에러를 반환하여 example.html에 onerror 콜백함수가 호출된다.


[A] 계산시작 버튼을 누르면 입력한 숫자값을 fibonacci.js의 onmessage 콜백함수에 전달한다. 


[B] fibonacci.js에서 postMessage()로 데이터 전달 시 호출되는 콜백함수를 정의한다. 전달받은 결과값은 화면에 표시한다.


[C] fibonacci.js에서 에러반환시 호출되는 콜백함수를 정의한다.


[D] example.html에서 postMessage()로 데이터 전달 시 호출되는 콜백함수를 정의한다. 전달받은 데이터가 null이거나 공백이면 에러를 반환하고 그렇지 않으면 계산을 수행해서 결과값을 반환한다.
```