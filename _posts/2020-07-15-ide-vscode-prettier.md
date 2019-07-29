---
layout: post   
title:  " vscode prettier 설치 및 사용법 "
categories: ide
comments: true
tags: ide vscode vsc plugin extention prettier
author: teddy8  
---
* content
{:toc}

## Goal
[https://teddy8.github.io/2019/07/15/ide-vscode-plugin/](https://teddy8.github.io/2019/07/15/ide-vscode-plugin/)<br>
위 포스팅에서 Prettier라는 vscode extension을 소개했었다.<br>
알아두면 편리한 Prettier의 설치 및 사용법을 간단하게 알아본다.

---


## Details


![](/assets\img\javascript\vsc_prettier(2).png)
```
왼쪽의 Extensions를 클릭하고
"Prettier" 검색 후 선택해서
install을 눌러 설치한다.
```

![](/assets\img\javascript\vsc_prettier(3).png)

```
조금 더 편하게 사용하고 싶다면 간단한 설정이 필요하다.
(기본 단축키 Shift+Alt+F 에서 Ctrl+S로 사용할 수 있다)

왼쪽하단에 톱니바퀴를 누르고 Settings 클릭한다.
"prettier" 검색 후 Edit in settings.json을 누른다
```

![](/assets\img\javascript\vsc_prettier(4).png)

```
settings.json 파일에 
"editor.formatOnsave": true
위 코드를 추가한 후 저장해준다.
```

![](/assets\img\javascript\vsc_prettier(1).png)
```
이제 코드 타이핑 후 Ctrl+S 를 누르면 자동으로 코드가 정렬되는 것을 확인할 수 있다
```