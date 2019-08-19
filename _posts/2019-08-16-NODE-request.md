---
layout: post   
title:  " Node.js request "
categories: Node.js
comments: true
tags: Node.js request
author: teddy8  
---
* content
{:toc}

## request
[https://teddy8.github.io/2019/08/13/NODE-api-get/](https://teddy8.github.io/2019/08/13/NODE-api-get/)
```
지난 포스팅에서 간단하게 GET요청을 할 때 http의 get()메소드를 사용했다. 
이번에는 더 직관적으로 사용할 수 있는 request로 요청하는 방법을 예제를 통해 정리한다.
```

![](/assets\img\node\request.png)

```
테스트할 url을 간단히 설명하면
'uinames.com/api' 라는 api url에서 테스트를 진행한다.
region에 'korea'를 넣으면 그 지역에 해당하는 데이터만,
amount에 적은 숫자로 반환 될 데이터의 양을 설정할 수 있다.
```

## 소스코드

``` js
const request = require('request');

const options = {
  url : 'http://uinames.com/api',
  json : true,
  qs : { 
    region: 'korea', 
    amount: 3 
  }
};

request.get(options, (err, res, result) => {
  if (err) return console.log('err', err);
  if (res && res.statusCode >= 400) return console.log(res.statusCode);

  result.forEach(person2 => {
    console.log(`${person2.name}${person2.surname} 님의 성별은 ${person2.gender}입니다.`);
  });
});
```

## 설명

```
request 모듈을 npm으로 설치한 뒤, requeire로 가져온다.
url은 'uinames.com/api'이며,
json을 'true'로 설정해 json형태로 읽어들인다.
qs에 region: 'korea', amount: 3을 넣음으로 써
url뒤에 'uinames.com/api?region=korea&amount' 이런식으로 붙여서 요청하게 된다.

request.get()메소드를 통해 설정한 객체값을 넣어주고
상태코드가 400이상이거나(비정상), 에러 유무를 확인한다.
그 후, result변수로 response받은 내용을 하나씩 꺼내어 출력한다.
```

출력결과
```
탁예원님의 성별은 female입니다.
곽영철님의 성별은 male입니다.
모민지님의 성별은 female입니다.
```

```
추가로 헤더값을 설정할 수 있으며,
POST요청, 이미지전송, 비동기처리도 가능하다.
더 자세한 사항은 공식문서에서 확인할 수 있다.
```
공식문서<br>
[https://github.com/request/request#readme](https://github.com/request/request#readme)<br>
[https://github.com/request/request-promise-native](https://github.com/request/request-promise-native)