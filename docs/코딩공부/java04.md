---
layout: default
title: 모듈 
parent: Java 공부
nav_order: 4
has_children: true

---

## 모듈이란?!  
- java 9에서 도입된 개념  
- 클래스들이 포함되어 있는 패키지 들과, 이미지등 리소스를 담은 **컨테이너**  
  
## JRE  
=Java Runtime Environment  
=자바 실행 환경  
  
- 자바 모듈(컴파일된 자바 API 클래스들, 예를 들어 scanner 같은 것!), 자바 가상 기계 등으로 구성되어 있다.  
- Java 9 이후부터는 **rt.jar** 을 설치할 필요가 없고, 필요한 모듈 및 클래스를 따로 import 하여 JRE 를 개선함  
- 예전에는 rt.jar에 모든 자바 api 를 담아두었는데, 이제는 99개의 모듈로 나누어졌다! ~~자바 모듈화 라고 불린다~~  
  
## Java API에 대한 정보를 알고싶다면..  
https://docs.oracle.com/javase/10/docs/api/overview-summary.html  

## Object 클래스  
-모든 클래스의 수퍼 클래스  
-모든 객체가 공통으로 가지는 객체의 속성을 나타내는 메소드를 보유한다.  

-object 클래스의 주요 메소드  
<img src = "./objectclass.png">


