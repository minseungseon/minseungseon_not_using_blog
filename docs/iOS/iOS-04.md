---
layout: default
title: Closure 
parent: iOS
nav_order: 4
has_children: true
---

```swift
func helloGenerator(message: String) -> (String, String) -> String {
  func hello(firstName: String, lastName: String) -> String {
    return lastName + firstName + message
  }
  return hello
}

let hello = helloGenerator(message: "님 안녕하세요!")
hello("수열", "전")

``` 

이랬던 것을!

hello function 부분을 { } 중괄호 처리하여 간단하게 할 수 있다.  
이렇게 {} 중괄호로 감싸진 **실행 가능한 코드블럭**을 클로져라고 한다.  

```swift
func helloGenerator(message: String) -> (String, String) -> String {
  return { (firstName: String, lastName: String) -> String in
    return lastName + firstName + message
  }
}
```

 키워드를 사용해서 파라미터, 반환 타입 영역과 실제 클로저의 코드를 분리한다! 즉, 정의부와 실행부가 분리된다~    

들어오는 파라미터의 순서를 활용하여 더 간단히 할 수 있다. 파라미터 첫번재는 $0, 두번째는 $1 로 처리해서 다음과 같이 간단히 할 수 있다.  

```swift 
func helloGenerator(message: String) -> (String, String) -> String {
  return {
    return $1 + $0 + message
  }
}

```

기본형태는 다음과 같다고 볼 수 있다. 

```swift
{ (매개 변수들) -> 반환 타입 in
   실행 코드
}

```

## closure 와 Function  

```swift
let closure = { print("Test") }
func function() -> (){ print("Test") }

closure()
function()

```

## pod install 을 통한 SwiftLint 설정하기  


![image](https://user-images.githubusercontent.com/37579661/90916783-ad8ae680-e41c-11ea-961d-2617d584ac3d.png)


- 맞닥뜨린 에러:  
`" Pod_chatty " Framework not found  `

이 문제는 그냥 프로젝트 폴더 내에 있는 `Frameworks` 폴더 내에 있는 .framework 파일들을 그냥 지워서 해결했다!
![image](https://user-images.githubusercontent.com/37579661/90918083-09566f00-e41f-11ea-8e91-e51c84fe108e.png)
thanks to [StackOverFlow](https://stackoverflow.com/questions/29865899/ld-framework-not-found-pods)


...  
그리고..  
![image](https://user-images.githubusercontent.com/37579661/90918067-02c7f780-e41f-11ea-9219-fe897e6054c6.png)
이것만 해결하니 바로 우다다다 나오는 SwiftLint에 걸린 에러들...!  

내가 원했던 것은 그냥 너가 아라서 안되는 것을 고쳐주는 거였오..  

이것을 하려면?!?!  

![image](https://user-images.githubusercontent.com/37579661/90918825-50912f80-e420-11ea-8e98-21a46a9e8d90.png)

이렇게 `autocorrect` 를 뒤에 추가해주면된당~  

제 앱의 경우에는 바로 모든 에러가 자동으로 고쳐지고 build succeed 했습니다 ㅎㅎ  




