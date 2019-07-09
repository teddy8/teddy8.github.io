---
layout: post   
title:  " Git reset vs revert 차이 "
categories: Git
comments: true
tags: git reset revert difference 차이 
author: teddy8  
---
* content
{:toc}

## Goal
Git에서 reset과 revert에 차이에 대해 이해합니다.
---

reset과 revert는 작업을 하다가 작업내용을 다시 되돌려야 하는 경우 사용하는 방법입니다.<br> 

두 방법에 대한 차이를 간단히 정리하겠습니다.<br>
<br>

reset
```
원격저장소에 push하기전 로컬저장소에서 되돌릴 경우
(push 이전엔 말그대로 서버엔 아무 영향이 없는 상태라 로컬데이터만 reset이나 rebase 하면 된다)
```

revert
```
원격저장소에 push한 후 되돌릴 경우
(push 한 이후엔 서버의 데이터가 바뀌어 있기 때문에 reset 이나 rebase 는 좋지 않다)
```
