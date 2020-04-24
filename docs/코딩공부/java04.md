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

## Wrapper 클래스  
-클래스 이름이 wrapper가 아님!  
-byte, short, int, long, char, float, double, boolean 을 앞글자 대문자로 하여 가지는 것을 Wrapper 클래스 라고 함!  
# Wrapper 클래스 객체 생성  
-기본 타임의 값으로 객체 생성  
```java
integer i = Integer.valueOf(10);
Character c = Character.valueOf('c');
Boolean b = Boolean.valueOf(true);
```
-문자열로 Wrapper 객체 생성  
```java
integer i = Integer.valueOf("10");
Double d = Double.valueOf("3.14");
Boolean b = Boolean.valueOf("false");
```
-Float 객체는 double 타입의 값으로부터 생성 가능  
```java
Float f = Float.valueOf((float) 3.14);
```

## String 객체  
-스트링 생성 방법 (리터럴로 생성)  
```java 
String a = "hello";
String b = "Java";
String c = "hello"; //a 와 c는 동일한 문자열을 참조함  
String d = new String("hello");
String e = new String("hello"); //d 와 e는 별로 메모리로 만들어짐  
```
-스트링 객체는 **수정 불가능**  
한 번 만들어지면, ~.concat 을 통해 두 문자열을 합치더라도 두개의 다른 메모리로 만들어진다.  

## 문자열 비교  
`int compareTo(String anotherString)`

## 공백제거  
`String trim()`  

## StringBuffer 클래스  
-가변크기의 문자열 저장 클래스  
-String 클래스와 달리 문자열 변경 가능  
-StringBuffer 객체의 크기는 스트링 길이에 따라 가변적  

## Calendar 객체  
-Calendar 객체 생성  
`Calendar now = Calendar.getInstance(); `  
