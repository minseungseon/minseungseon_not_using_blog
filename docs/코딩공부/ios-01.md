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
    

## 변수의 데이터 타입 정확하게 지정해주기  
```swift
var myMiddleInitial: Character = "A"  //이렇게 :datatype 을 써줌으로서 변수의 데이터타입을 지정해준다!  
```

이렇게 변수타입을 지정해주지 않더라도, swift는 언어의 특성상 '변수 타입에 대한 추론'기능이 좋은 편이다. 예를 들어서  
```swift
var isThisString = "Minseung"
```
의 변수에 대해서 자동으로 String data type 으로 인식한다.  
하지만 앞의 예서에서의 "A" 와 같은 변수에 대해서는 character 로 바로 인식하지는 못한다.  

double, bool, string에 대해서는 그 변수의 데이터 타입은 따로 지정해주지 않아도 swift가 잘 인식하는 반면에, **character** 타입은 String 으로 인식하기 때문에, character 의 경우에는 따로 위에서 언급했듯이 변수지정을 sepecify 해줘야 한다.  


## 상수 (constant)  
variable(변수)는 다시 그 값이 할당 될 수 있으나, constant(상수)는 값이 변할 수 없다.  
변수는 `var` 로, 상수는 `let`으로 선언한다.  

## 변수 이름 짓기  
**정말 신기하게도!!!** swift 에서는 이모티콘을 변수이름으로 쓸 수 있게 한다. (물론 드물다고 한다 ㅎ)  
안되는 경우의 수는 다음과 같다.  
        1. 숫자로 시작하는 이름  
        2. 특별문자로 시작하는 경우  

swift에서는 **'lowerCamelCase'**로 변수 이름을 짓도록 규정하고 있다는 것을 기억하자!  


## 'literal' 이란?  
swift 에서는 리터럴을 'a literal is the source code representation of a value of a type, such as a number or string' 이라고 정의한다.  
즉, **숫자, 문자열 과 같은 하나의 타입의 값**을 literal 이라고 정의하게 된다.  
변수 자체는 literal 이 될 수도 있고, 아닐 수도 있는 것이다.  
그 변수 속에 담겨있는 숫자와 문자열 값이 바로 literal 을 의미한다.  

```swift
var myNumber = 5 
var welcome = "hello"
var getting = welcome 
```
위의 코드에서, 5와 hello 는 literal 이지만, welcome 은 literal 이 아니다.  

## Escpate Characters  
String 의 값을 넣을 때에, **띄어쓰기, 탭, "", '', 또는 backslash**의 경우에는 `escape character`를 통해 표현해줘야한다.  

| **character** | **usage** |  
| :----------: | :-------------: |
| \n | newline 새로운 줄로 넘어갈 때 엔터치는 것을 의미함 |
|\t| horizontal tab 탭을 의미함 |
|\"| 쌍따옴표 double quotation mark|
|\'|single quotation mark|
|\| backslash|  

## String Interpolation 문자열 삽입  
```swift
\(variableName) 
```
을 통해 문자열을 특정 문자열에 삽입할 수 있다!!  
  
```swift
var insertThis = "Minseung"
var insertHere = "My name is, \(insertThis)"

print(insertHere)
```
출력: My name is, Minseung

