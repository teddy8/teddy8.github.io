---
layout: post
title: ' JavaScript의 함수는 1급 객체(Frist Clss Object)이다.'
categories: JavaScript
comments: true
tags: JavaScript js
author: teddy8
---

- content
  {:toc}

# JavaScript의 함수는 1급 객체(first class object)다.

## 먼저 1급 시민(first class citizen)의 정의에 대해 알아보자.

### 일반적으로 1급 시민의 조건을 다음과 같이 정의한다.

- 변수(variable)에 담을 수 있다.

- 인자(parameter)로 전달할 수 있다.

- 반환값(return value)으로 전달할 수 있다.

### 예를들어, 대부분의 프로그래밍 언어에서 "숫자"는 1급 시민의 조건을 충족한다.

- 변수에 저장 가능

- 인자나 반환값으로 전달 가능

## 1급 객체(first class object)

### 1급 객체(first class object)라는 것은 특정 언어에서 객체(object)를 1급 시민으로써 취급한다는 뜻이다.

#### 위의 조건을 모두 충족한다.

## 1급 함수(first class function)

### 1급 객체 뿐만 아니라 1급 함수도 존재한다.

### 함수를 1급 시민으로 취급하는 것이다.

#### 몇몇의 학자들은 1급 시민의 조건과 함께 다음과 같은 추가적인 조건을 요구한다.

- 런타임(runtime) 생성 가능

- 익명(anonymous)으로 생성 가능

#### 이런 추가조건으로 봤을 때 C의 함수는 1급 함수로 볼 수 없다.

## JavaScript의 함수는 1급 함수? 1급 객체?

### JavaScript에서는 객체를 1급 시민으로 취급한다.

### JavaScript의 함수는 객체로써 관리되므로 1급 객체라고 볼 수 있다.

### JavaScript의 함수는 1급 함수의 추가조건도 만족한다.

#### 이렇게 1급 객체인 동시에 1급 함수이지만, 보통 1급 객체로 기술하는 편인듯하다. 아마 함수가 객체이기 때문이지 않을까 싶다.

## JavaScript에서 함수가 1급 객체인 것이 중요한 이유

### 함수가 1급 객체라는 사실은 겉으로 봤을 땐 그리 특별하지 않다. 함수를 그냥 주고받을 수 있다는 것 뿐이지만 이것이 아주 큰 차이점을 만든다.

### 가장 중요한 장점은 바로 <b>고차 함수</b>(high order function)가 가능하다는 점이다. JavaScript의 each, filter, map, sort 등의 함수들이 얼마나 편리한지는 잘 알고 있을 것이다. 인자로 목적에 맞는 함수를 하나 넘겨주면 아주 쉽게 처리가 된다. 반면, Java 7의 Collections.sort함수같은 경우도 비교를 위해 인자를 하나 넘겨주게 되는데, 이것은 함수가 아니라 Comparator interface 타입의 인스턴스(instance)이다. 함수 하나를 넘겨주기 위해서 새로운 클래스를 만들고 그것의 인스턴스까지 생성해야 하는 것이다 – ES6와 Java 8에서는 람다(lambda)가 지원되면서 훨신 간편해졌다.

### 1급 객체가 JavaScript의 <b>클로져(closure)</b>와 만나면 또 하나의 장점이 생긴다. JavaScript의 함수는 생성될 당시의 Lexical Environment를 기억하게 되는데, 함수를 주고받게 되면 이 Lexical Environment도 함께 전달된다. 이것을 이용해서 <b>커링(currying)</b>과 <b>메모이제이션(memoization)</b>이 가능해진다. 이 주제는 기회가 될 때 따로 다룰 예정이다.

## 참고

https://bestalign.github.io/2015/10/18/first-class-object/
