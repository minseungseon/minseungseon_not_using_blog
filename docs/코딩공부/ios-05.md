---
layout: default
title: struct and enums 
parent: iOS
grand_parent: 코딩공부
nav_order: 5

---

## iOS 3.5일차..!  
매 강의를 기록하면서 들으려고 하다보니 기초 부분에서 시간이 굉장히 많이 할애되는 것 같다..  
그래도 결국 기록을 안해놓으면 똥이 되니까..  
기록의 버릇을 들이기 위해 열심히 기록해보겠다 ㅠㅠ  
지금 github.io 메인 페이지에도 심지어 아무것도 안써져 있는데 ㅋㅋㅋㅋㅋㅋㅋ  
내용만 채워가는 나자신...ㅎㅎ....  


## list of lessons for today  

| **index** | **topic** |  
| :----------: | :-----------------------: |
| 1 | [](#) |
| 2 | [](#) |
| 3 | [](#)|
| 4 | [](#)|
| 5 | [](#) |  
| 6 | [](#) |
| 7 | [](#)|
| 8 | [](#)|
| 9 | [](#) |  
| 10 | [](#)|

## swift에서의 구조체  
가장 기본적인 형태는 다음과 같다.  

```swift
struct student {
  let name: String //프로그램 상에서 학생의 이름이 바뀌는 것을 원하지 않기 때문에 let 을 통해 상수로 선언한다  
  var age: Int 
  var school: String
}
```

## property 란  
알아두면 좋은 **swift 용어**이다.  
struct(구조체)에서 위에서 보았듯이 '학생'이라는 구조체 내에서 '이름, 나이, 학교'와 같은 것을 `member` 혹은 `property`라고 일컫는다. 
이것은 애플에서 사용하는 용어이기 때문에 알아두면 좋다!  

## 언제 initialize(값 초기화)를 해야할까?  
이 부분이 항상 헷갈리는 것 같다.  
java 언어를 배울 때에도 초기화를 언제 해줘야하는건지, mandatory(필수)인 것인지에 대해 굉장히 궁금했다.  

**해답**은 , `변수의 값 초기화는 필수는 아니다` 라는 것이다.  
하지만, 잘 생각해보면 값이 정해져 있지 않으면 그냥 '0'으로 디폴트 값을 주고 계산을 잘 넘겨야하는 경우가 있다.  
기본 값이 0으로도 안정해져있으면 `null`값이 넘어가기 때문에 프로그램 자체가 돌아가지 않을 수 있기 때문이다.  
그래서 이러한 경우에는 다음과 같이 디폴트 값을 초기화 해준다.  

```swift 
struct GeoLocation {
    var latitude: Double = 0.0
    var longitude: Double = 0.0
}
```
  
  

## 구조체 별 인스턴스 선언하기  
구조체만을 만들어서는 아무것도 안된다..! 구조체 별로 인스턴스를 선언하여 구조체를 백분 활용해보자!  

```swift 
struct Movie {
    let title: String
    let year: Int
}

var firstMovie = Movie(title: "첫번째 영화 제목", year: 1999)
var secondMovie = Movie(title: "두번째 영화 제목", year: 2000)

print(firstMovie)
print(secondMovie)
``` 
  
출력: `Movie(title: "첫번째 영화 제목", year: 1999) 
Movie(title: "두번째 영화 제목", year: 2000)`
  
## 구조체의 인스턴스에 접근하기  
인스턴스의 접근은 굉장히 쉽다!   
java 에서 처럼 `구조체.proprety이름` 으로 접근하면된다!  
예를 들어서, 위의 movie 예시에서 firstMovie의 title 에 접근해서 출력하고 싶으면,  

```swift
print(firstMovie.title)
``` 
   
이렇게 접근하면 된다!  


