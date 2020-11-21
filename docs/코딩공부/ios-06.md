---
layout: default
title: String!
parent: iOS
grand_parent: 코딩공부
nav_order: 6

---

## 정말 오랜만에 유다시티...ios...  
아무래도... ㅋㅋㅋㅋㅋㅋㅋ 12월 말까지 다 들을 수 있을란지 모르겠다...ㅎ  
다다음주에 제주도에 가서 정말 유다시티만 파볼 예정이긴하지만...ㅎㅎ  
일단은 해보겠다...!!  


## `.count()`  
swift에서는 `.count()`를 통해 문자열의 크기를 셀 수 있다.  
예시는 다음과 같다!!  

1. As part of the spam filter for a message board app, there's a function called checkLength(). The goal of this function is to prevent posts that are too short (less than 10 characters) and prevent posts that are too long (more than 10,000 characters). Finish implementing the function to return true if a message is within the length restrictions and false if it is too long or too short.  

나의 답:  

```swift
import Foundation

func checkLength(message: String) -> Bool {
    if(message.count>=10 && message.count<=10000){
        return true
    }else{
        return false
    }
}
```

## sensitive, insensitive  
그 흔한 대소문자 없애기...? 관련 문제였다.  
이는 `.lowercased()`, `.uppercased()` 를 통해 풀 수 있다.  

2. Finish implementing search(). If the second string (s2) occurs anywhere in the first string (s1), return true. Otherwise, return false. The search should be case insensitive. For example, search(s1: "Udacity", s2: "CITY") returns true.  

나의 답:  
```swift
import Foundation

func search(s1: String, s2: String) -> Bool {
    let str1 = s1.lowercased()
    let str2 = s2.lowercased()
    
    if(str1.contains(str2)==true){
        return true
    }else{
        return false
    }
}
```

## `.reversed()`  

문자열 거꾸로 만들기이다!  
정말 간편한 기능인 것 같다. 하지만 코테 준비에서만 자주 볼 것 같은 아이...  

3. Finish implementing isPalindrome() to return true if the input string is the same forwards and backwards, and false if not. The search should be case sensitive, for example, isPalindrome(input: "taCoCat") would return true whereas isPalindrome(input: "TaCoCAt") would return false.

나의 답 :  
```swift
import Foundation

func isPalindrome(input: String) -> Bool {
    let inputReversed = String(input.reversed())
    if(inputReversed == input){
        return true
    }else{
        return false
    }
}
```

## `.append` 

말그대로 문자열 두개를 합칠 수 있다!  

```swift
var hello = "hello"
let world = "world" 

//append 사용
hello.append(world)

//수식 사용  
hello = hello + world
hello += world
```

다양한 방법으로 이루어질 수 있다~  

## character 고치기  
String 내용을 고칠!! 수도 있는 기능이 있다.  

예를 들어... "          so many blanks           "  
라는 string 값에서 모든 빈칸을 없앨 수도 있다.  

```swift 
var message = "       so many blanks        "
while message.last == " " {
    message.removeLast()
}
while message.first == " " {
    message.removeFirst()
}

```

## replace substring  
말그대로! string 내부에 있는 몇가지 문자열을 '대체'하는 코드를 쓸 수 있다!  

```swift
let verbose = "Why don't you replace THIS word?"  
let better = verbose.replacingOccurrences(of: "THIS", with: " ")

```

하지만!  
이 `replacingOccurrences` 를 사용하려면, `Foundation`을 설치하여야 한다~  

## Foundation 이란?  
- 하나의 **framework** 로서, 자주쓰이는 코드가 제공되는 것이다. string 관련된 것들이 한 예시이다. 


