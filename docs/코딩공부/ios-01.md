---
layout: default
title: udacity 1일차
parent: iOS
grand_parent: 코딩공부
nav_order: 1

---


## 첫 iOS udacity!  
드디어! 첫번째 iOS 강의를 듣게 되었다.  
오늘 들은 강의 리스트는 다음과 같다.  

## list of lessons for today  
1. Variables and Types  
    -udacity 에서는 'sandbox'라는 용어로 코드 실습 시간을 지칭한다.  
2. 코드 실습  

## variable 작성 연습  

```swift
var question = "Ready to write your first lines of Swift code?"
print(question)
var response = "Yes, I am ready!"
print(response)
```

위의 두 문장이 출력되게 된다!  

예를 들어, Hello, world! 를 출력하기 위해서는 다음과 같이 작성한다.  
```swift
var welcome = "Hello, world"
print(welcome)
```

## 주석 달기  
주석은 java와 똑같이 달면 된다!!  

1. 라인 주석  
```swift
// 코멘트입니다 
```

2. multi line 주석  
```swift
/* 여러 
라인을 
위한 
주석입니다*/
```

## text 외에 숫자도 variable 은 담을 수 있다!  

```swift
var amountToUseToday = 4
```

## swift 안에 있는 data type  
swift 에는 다른 언어들과 비슷하게 **int, float, double, bool, character, string**의 데이터타입이 있다.  
1. int : whole number values (0,2,-2)  
2. float: 32 bit의 floating-point(decimal)numbers that require no more than 6 decimal digits(3.14,5.675,-12.34)  
3. double: 64 bit의 floating-point(decimal) numberst that require more precision(예시는 float과 같음)  
4. bool : a boolean truth value (truth, false 와 같은 것)  
5. character : 글자 한글자 한글자 ("a", "+", )  
6. String : 문자열 ("swift", 등)  

이 때, **float 과 더블의 차이**는 무엇일까?  
    - float 과 double 의 차이는 **'정확성의 차이'**에 있다.  
    - 컴퓨터는 floating-point number를 다루는데에 항상 어려움을 겪는다!  
    - 그리고 보통은 더 정확한 값을 다루기 위해 double 을 사용하는 것이 대부분의 경우이다.  
    - 하지만, 그렇다고 해서 항상 double 이 가장 좋은 것만은 아니다. **속도**가 더 중요할 때에는, float를 선택하는 것이 더 나은 선택이 될 수 있다!  
    
