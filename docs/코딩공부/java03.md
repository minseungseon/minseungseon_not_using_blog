---
layout: default
title: 인터페이스
parent: java
grand_parent: 코딩공부
nav_order: 3

---

## 인터페이스의 구성 요소  
* **상수**  
public만 허용하고, public static final 은 생략한다!  

* **추상 메소드**  
public abstract 생략 가능  
  
* **default 메소드**  
인터페이스에 **코드가 작성된** 메소드이다.  
인터페이스를 구현하는 클래스에 자동 상속된다.  

* **private 메소드** 
인터페이스 **내**에 메소드 코드가 작성되어야 한다.  
인터페이스 **내**에 있는 다른 메소드에 의해서만 호출이 가능하다.  
  
* **static 메소드**  
public, private 모두 지정 가능 -> 생략하면 public  

## 인터페이스를 구현하자!  

1. 선언  
``` java
interface PhoneInterface { //인터페이스 선언

}
```

