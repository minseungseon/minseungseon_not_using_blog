---
layout: default
title: DRF에서의 Http Method
parent: 웹백앤드 기초
nav_order: 2
has_children: true
---

## DRF에서의 Http Method  
~~다 하나하나 외우기까지 할 필요는 없다고 한다..~~  

| Method | Meaning |  
| :----------: | :-------------: |
| Get | 요청받은 URL의 정보를 검색하여 응답함 |
|Post|요청된 자원을 생성함|
|Put|요청된 자원을 수정함|
|Delete|요청된 자원을 삭제함|
|Patch|요청된 자원의 일부를 교체(수정)함|
|Option|웹서버에서 지원되는 메소드의 종류를 확인함|

## 쉬운 예시  
<div class="code-example" markdown="1">
### Get
글의 **목록을 가져달라**는 명령어!  
### Post
minseung.github.io/post  
새 글을 **작성** 하게 해주는 명령어!  
</div>

<div class="code-example" markdown="1">
### 예를 들어..
minseung.hithub.io/post/1  
에 대해서 
  
1. **GET** 요청이 들어왔다면  
-> 1번 글을 가져오라는 요청이 됨  
  
2. **DELETE** 요청이 들어오면  
-> 1번 글을 지워달라는 요청이 됨  
  
3. **PUT(PATCH)** 요청이 들어오면  
1번 글에 이런 내용을 수정해달라는 요청이 됨  
  
4. **POST**는 필요가 없음  
작성이 이미 된 글에 대해서는 새로운 글을 작성하는 요청을 주는 POST 는 의미가 없음.  
</div>


