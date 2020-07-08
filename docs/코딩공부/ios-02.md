---
layout: default
title: operators
parent: iOS
grand_parent: 코딩공부
nav_order: 2

---

## Core Terms  
>> operator 와 관련하여 알아두면 좋은 핵심 영어 용어들을 정리해보았다!  

| **영어 단어** | 뜻 | 예시 |  
| :---------:|:---:| :----:|
| **Operator** | 연산자 | |
| **Operand** | 연산자(operator)의 영향을 받는 하나의 target, 혹은 value(값)을 의미한다. | 8-5 라는 expression 에서, operator(연산자)는 '-' 이고, operand는 8과 5이다. 즉, 8-5의 expression 에서는 8과 5 의 operand 에 '-'가 적용이 되었다고 이해한다. |  
| **Precedence** | 우선시 되는 것 | 어떤 연산자가 먼저 계산되는지에 대한 우선권을 의미한다. 더하기보다는 곱하기 연산자를 먼저 계산하는 것이 precedence rule 에 의한 순서 이다. |
| **Associativity** | 연관성 | **left-assosicative** 는 더하기 연산자에 해당한다. 왼쪽부터 차례대로 계산한다.   **right associatvie**는 제곱 연산자'^'에 해당하는 것이다. 오른쪽부터 제곱해나간다.  |


## 문자열에 연산자 쓰기  
기존의 java 언어 처럼 문자열을 숫자처럼 연산할 수 있다!  
```swift 
var stringConcat = "my"
var withOperator = "name"
let myName = stringConcat + " " + withOperator  
```

출력: `my name`  

```swift 
withOperator += "!"
```
이렇게 추가하는 것도 가능하다.




