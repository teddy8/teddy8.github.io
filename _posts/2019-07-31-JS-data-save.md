---
layout: post   
title:  " JavaScript 데이터 저장 방법"
categories: JavaScript
comments: true
tags: JavaScript js 로컬스토리지 Local Storage 세션스토리지 Session Storage 쿠키 Cookie
author: teddy8  
---
* content
{:toc}


## 현재 페이지의 url 가져오기
```
1. 로컬스토리지(Local Storage), 
2. 세션스토리지(Session Storage), 
3. 쿠키(Cookie)

다음은 웹브라우저에서 데이터를 기억하고 싶을 때 쓰는 방법이다.
이 방법들의 대한 차이를 간단히 정리한다.
```

## 로컬스토리지 (Local Storage)
```
웹 브라우저의 탭을 닫았다 켜도 유지된다.
자동로그인 여부나 설문조사 선택한 것 유지할 때 사용한다.
저장소의 구분은 (프로토콜 + 호스트 + 포트)로 한다. (ex: http://127.0.0.1:8080)
```
공식문서 [https://teddy8.github.io/2019/07/15/ide-vscode-plugin/](https://developer.mozilla.org/en-US/docs/Web/API/Storage)

## 세션스토리지 (Session Storage)
```
웹 브라우저의 탭을 닫으면 제거 된다.
그렇기 때문에 잠깐 보관해야할 때 사용한다.
```

## 쿠키 (Cookie)
```
최대 4kb를 담을 수 있지만 서버와 지속적으로 통신해야하기 때문에
불필요한 데이터를 담으면 트래픽이 낭비될 수 있다.
그렇기 때문에 중요하지 않은 데이터는 최대한 로컬, 세션스토리지로 보관하면 좋다.
```