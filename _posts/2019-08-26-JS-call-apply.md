---
layout: post   
title:  " JavaScript call apply bind"
categories: JavaScript
comments: true
tags: JavaScript js 
author: teddy8  
---
* content
{:toc}

```
JS에서 call(), apply(), bind() 메소드를 예제를 통해 정리한다.
```

## 소스 코드

``` js
const test1 = {
  num: 4,
  sum(a, b) {
    return this.num + a + b;
  }
}

const test2 = {
  num: 2
}

num = 3;
```

```
위와 같은 소스코드가 미리 작성되어 있을 때, 각 메소드에 따른 사용방법을 살펴본다.
```

## call

``` js
console.log(test1.sum.call(test2, 2, 3)); // 7
console.log(test1.sum.call(test1, 2, 3)); // 9
```

```
call()메소드는 첫 번째 인자에 this를 전달한다.
두 번째 인자부터는 call()을 수행하는 메소드에 해당하는 인자값을 넣어준다.
변수 test의 sum(a, b)메소드는 전달받은 2개의 숫자와 this의 num값과 더한 값을 반환한다.

첫 번째 출력결과는
test2의 this를 전달했기 때문에 해당 this의 num값인 2와 2, 3을 더 한 값인 7이 출력된다.

두 번째 출력결과는
test1의 this를 전달했기 때문에 해당 this의 num값인 4와 2, 3을 더 한 값인 9가 출력된다.
```

## apply

``` js
console.log(test1.sum.apply(test2, [2, 3])); // 7
console.log(test1.sum.apply(test1, [2, 3])); // 9
```

```
call()메소드와의 차이는 apply()메소드는 인자를 묶어서 전달한다는 점이다.
```

## bind

``` js
const a = test1.sum;
console.log(a(2, 3)); // 8

const newA = a.bind(test1);
console.log(newA(2, 3));  // 9
```

```
첫 번째 출력결과는
test1의 sum()메소드를 다른 변수에 저장하고 그 변수를 통해 메소드를 호출하면 this는 전역객체를 가리킨다.
따라서, 전역객체의 num값인 3과 2, 3을 더 한 8이 출력된다.

두 번째 출력결과는
test1의 sum()메소드를 bind()메소드를 통해 test1을 기준으로 this를 지정했다. 
따라서, 해당 this의 num값인 4와 2, 3을 더 한 값인 9가 출력된다.
```

## 공통점
```
call(), apply(), bind()메소드는 원하는 환경의 this를 지정하여 사용할 수 있다는 점이 동일하다.
```