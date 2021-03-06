---
layout: post   
title:  " JavaScript 프로미스(Promise) "
categories: JavaScript
comments: true
tags: JavaScript js 프로미스 Promise 동기 비동기
author: teddy8  
---
* content
{:toc}

## 프로미스란?

```
ES6에 추가 된 비동기 처리 객체입니다.
프로미스가 나오기 이전에는 콜백 함수로 처리했습니다.
하지만 비동기 처리가 완료된 후 결과값에서 
또 다른 비동기 처리를 수행해야하는 경우가 많은데
이렇게 비동기 처리가 중첩되다 보면 코드가 점점 안쪽으로 파고 들어가는
피라미드 형태의 코드( 콜백지옥이라고도 불림 )가 만들어집니다.
프로미스는 이런 가독성이 안좋은 코드에 대한 니즈에 의해 소개된 것입니다.
```

## 동기 vs 비동기
```
동기와 비동기를 쉽게 비유하여 설명하자면
동기(sync)는 무전기, 비동기(async)는 전화기로 예를 들 수 있습니다.
무전기는 상대가 응답해야 다음 대화를 진행할 수 있지만,
전화기는 상대가 듣던 말던 내가 하고 싶은 말을 내뱉으면서 
요리를 할 수도 있고 다른일을 동시에 진행할 수 있습니다.
```

## 프로미스의 상태 및 메소드
```
프로미스는 다음과 같은 3가지 상태를 갖습니다.

1. 대기중(Pending)	- 아직 결과가 없는 상태
2. 이행됨(Fulfilled)	- 비동기 처리가 성공적으로 완료되어 약속을 이행한 상태
3. 거부됨(Rejected)	- 비동기 처리가 실패한 상태

프로미스는 다음과 같은 2가지 메소드를 갖습니다.

1. then(onFulfilled, onReject)	- 약속이 완료됐을 때 호출될 함수
2. catch(onReject)		- 약속이 거부됐을 때 호출될 함수
```

## 예제

```
server라는 객체를 만들고 server의 여유 트래픽이 100이라고 가정하겠습니다.
하나의 작업을 비동기처리로 완료할 때마다 30의 트래픽이 깎인다고 했을 때,
트래픽이 30이하면 감당할 수 있는 트래픽이 초과되니 
promise에서 거부를 하도록 하겠습니다.
```

example.js

``` js
function doWork(name, server) {
  return new Promise((resolve, reject) => {  
    setTimeout(() => {
      // 여유트래픽이 30보다 많이 남았으면 이행
      if(server.traffic > 30) {   
        resolve({
          result: `${name} exec`,
          num: 30
        });
      } 
      // 30이하면 거부
      else {   
        reject(new Error(`${name} failed`));
      }
    }, 1000);
  });
};

const server = { traffic: 100 }; // 여유 트래픽 100

doWork('work1', server)  // 'work1'라는 이름의 promise 생성
  .then(v => {
    console.log(v.result);
    server.traffic -= v.num;
    return doWork('work2', server); // traffic 70
  })
  .then(v => {
    console.log(v.result);
    server.traffic -= v.num;
    return doWork('work1', server); // traffic 40 
  })
  .then(v => {
    console.log(v.result);
    server.traffic -= v.num;
    return doWork('work2', server); // traffic 10 (30보다 낮아서 거부)
  })
  .catch(e => console.error(e));
```

출력 결과

```
work1 exec
work2 exec
work1 exec
Error: work2 failed

트래픽이 100에서 70, 40이 됬다가 10이 됬을 때, 거부당하는 것을 확인할 수 있습니다.
```