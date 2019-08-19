---
layout: post   
title:  " Node.js cheerio로 크롤링 "
categories: Node.js
comments: true
tags: Node.js cheerio 크롤링 스크랩핑
author: teddy8  
---
* content
{:toc}

## cheerio
```
node.js에서 request와 cheerio를 이용하여 크롤링하는 방법을 예제를 통해 정리한다.
테스트에 사용할 사이트는 위키백과의 HTML 페이지 이다.
```

![](/assets\img\node\cheerio.png)

```
목차를 보면 1. 역사, 1.1 개발 1.2 최종 규격 등등이 적힌 것을 확인할 수 있다.
여기서 역사, 개발, 최종 규격같이 숫자를 제외한 한글만 수집한다.
크롬의 F12 개발자 도구를 통해 확인해보면 한글 부분은 모두 
span이라는 태그에 class명이 'toctext'라는 공통점이 있다는 것을 확인할 수 있다.
```

## 소스코드

``` js
const cheerio = require('cheerio');
const request = require('request');

request('https://ko.wikipedia.org/wiki/HTML', (err, res, html) => {
  if (err) return console.log(err);
  if (res && res.statusCode >= 400) return console.log(res.statusCode);

  const $ = cheerio.load(html);
  console.log($('span[class=toctext]').text());
});
```

## 설명

```
npm으로 설치한 cheerio와 request 외부 모듈을 
reuqest()메소드를 통해 특정 url을 설정하여 실행한 후,
비정상 상태코드(res.statusCode 400 이상) 및 에러반환을 하지 않았다면,
필요한 정보만 골라내기 위해 cheerio모듈의 load()메소드를 통해 
response 받은 내용이 담긴 html변수를 넣어주면 반환값을 통해
셀렉터(Selector)형식으로 원하는 내용을 쉽게 접근할 수 있다. 
'span[class=toctext]'의 text()메소드를 통해 출력한 결과는 같다.
```

출력결과
```
역사개발최초 규격표준 버전의 역사HTML 버전 스케줄HTML 초안 버전 스케줄XHTML 버전마크업HTML 요소HTML 요소의 일반적인 형태HTML 요소의 가장 보편적인 형태태그의 기본적인 형태단락 구획주석 사용HTML에서 사용되는 마크업 요소의 형태주요 HTML 요소들속성데이터 형식문서 형식 선언시맨틱 웹전송HTTPHTML 전자 우편명명 규칙HTML 애플리케이션위지위그 편집기같이 보기각주외부 링크
```

```
참고로 크롤링의 난이도는 사이트의 구조에 따라서 천차만별이다.
만약 전달받은 값이 인코딩으로 인해 깨진 다면 iconv 모듈을 통해 인코딩의 타입을 변환하여 해결해야한다.
예를들어 해당 페이지의 인코딩 방식이 'CP949' 경우 아래와 같이 'UTF8'로 변환할 수 있다.
const Iconv = require('iconv').Iconv;
const iconv = new Iconv('CP949', 'utf-8//translit//ignore');
const html = iconv.convert(result).toString();
```