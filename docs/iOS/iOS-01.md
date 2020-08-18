---
layout: default
title: 패턴
parent: iOS
nav_order: 1
has_children: true
---

1. MVC  
Model, View, Controller  
View와 Model을 최대한 관계가 없이 코드를 짜는 것이 clean code이다.  

MVC also allows re-use of the code, as there is only one model class used by the two view controllers.

MVC is also used for Mac apps, so we can look at examples there too.

맥에서의 mail app을 예시로 들자면, 
the mail message model is used by at least two view controllers. Remember that each view controller always has at least one view.

The view controller showing a list of messages only needs part of the mail message model class data, not all of it.

By abstracting away the data we need to a model class, the view controllers can just worry about the views and user interactions, leaving the inner details of how to store the mail message up to the model. 

ellie the chatbot의 경우에도 MVC 패턴을 이용한 앱이다.  

controller -> View Controller
View -> UIView UILable UIbutton 


## autolayout constraints
- intrinsic size: 처음부터 자동으로 주어지는 사이즈  
- you need a minimum of two constraints on each axis to properly lay out a UI element 
이 두 constraints on each axis 는 intrinsic size와 상대적인 constraints 를 포함한다. 

- 실습  
정말 오랜만에 스토리보드를 만진다...  

![image](https://user-images.githubusercontent.com/37579661/90018265-a0b51700-dce7-11ea-8f4e-51eb0f0b0047.png)

이렇게 기본적인 것도 헷갈리는중..  

1. swiftUI를 체크하고 Single View App을 만들면, 
![image](https://user-images.githubusercontent.com/37579661/90019930-0e624280-dcea-11ea-8904-a2386e9735be.png)

2. storyboard를 체크하고 만들면
![image](https://user-images.githubusercontent.com/37579661/90019948-16ba7d80-dcea-11ea-90b2-906267be4f44.png)

이렇게 된다..!  

udacity 에서는 main.storyboard 가 있길래... 뭐지..했는데 2018년도에 배웠던 이런 기본개념을 헷갈려서..! 이렇게 다시 서칭해서 깨달았다...ㅎ...  


## IBAction 과 IBOutlet의 차이  
- IBAction : UI element에서 code로 접근한다! (버튼과 같은 것)
- IBOutlet : code에서 UI element로 접근하다! (버튼을 누르면 라벨의 값이 바뀌는 것)  

## UIKit?
UILabel, UIButton, UIView, UIViewController 

## application lifecycle  
1. not running: 앱이 아예 안켜졌을 때
2. inactive : 앱이 켜졌는데 화면이 아직 나오지 않았을 때
3. active : 앱의 모든  부분 구동 됨 
4. background: 전화와 같은 다른 기능이 켜졌을 때, 잠시 기존에 쓰고있던 앱은 background로 감
5. suspended : 오랜시간 background에 있게 되면 app은 메모리에 존재하기는 하지만 어떤 코드도 실행하지 못하는 상태로 있는다. 그러다가 iOS 가 메모리가 부족하여 앱을 메모리에서 제거하고 not running 상태로 앱을 보낼 수 있다. 

viewWillAppear(_:) vs viewDidLoad()  
viewWillAppear(_:)는 화면에 뷰가 나타나는 것을 준비시켜준다. 
func viewDidLoad()
Called after the controller's view is loaded into memory.
viewDidLoad는 컨트롤러의 뷰가 메모리에 load된 이후에 불러와진다.
즉, 라이프사이클 상 viweDidLoad가 viewWillAppear보다 더 먼저 call 되어짐을 알 수 있다.  
viewDidLoad는 스크린에 뷰컨트롤러가 뜨기도 전에 메모리 자체에 들어올 때 쓰이는 메소드이기 때문이다.  

쉽게 말하자면, will function은 did function 보다 항상 먼저이다!  

## multiple views  
multiple view controller를 다루는 class로 대표적인 두가지가 있다!  
1. UINavigationController  
- view controller를 스택들로 다루는 컨트롤러이다  
- 팬케이크가 올라가는 접시라고 생각하면 된다!  
2. UITabBarController  

You can add as many UIViewControllers to a UINavigationController as you need, and can add and remove view controllers from the stack at any time.

This is in contrast to the UITabBarViewController, which you'll learn about later in the course, and which manages a fixed number of view controllers.

## Segue?  
![image](https://user-images.githubusercontent.com/37579661/90103029-c9d3b700-dd7c-11ea-832c-ab73fae6f05d.png)

root view controller 에 Navigation Controller를 설정하고, 새로운 view controller(초록색)에 그 전 view controller에있는 stop buttton을 연결하면 자동으로 생기는 두 뷰 사이의 '화살표'가 'segue'이다.  


## delegation

![image](https://user-images.githubusercontent.com/37579661/90106691-c0e5e400-dd82-11ea-8223-6851eb290709.png)

All of these are delegate relationships!

In a delegate relationship, one entity gets another to do some work for them, and the second entity can notify the first when the work is done.

Remember that protocols act as a kind of contract. AVAudioRecorder does not know what classes you have in your app. However, if you say that your class conforms to the AVAudioRecorderDelegate protocol, then it knows it can call a specific function in your class.

The specific function has been defined in the protocol (in this case, the AVAudioRecorderDelegate protocol). This way your class and the AVAudioRecorder are loosely coupled, and they can work together without having to know much about each other.

Loose coupling of classes is really useful in building interchangeable pieces of code, and used quite a lot in iOS.

![image](https://user-images.githubusercontent.com/37579661/90107271-8892d580-dd83-11ea-88bb-4e2def5f24e9.png)

프로토콜에 대해서 이해하기 위해서는 오른쪽 우클릭을 하여 jump to definition 을 통해 더 확인해볼 수 있다.  

![image](https://user-images.githubusercontent.com/37579661/90107393-b5df8380-dd83-11ea-8b62-00714345c0c9.png)

이렇게 주석과 함께 잘 설명이 되어있는 것을 볼 수 있다!  

```swift
func audioRecorderDidFinishRecording(_ recorder: AVAudioRecorder, successfully flag: Bool) {
        print("AV stopped recording")
``` 
AVAudioRecorder를  다 save한 후에 위의 `successfully flag`를 활용하여 잘 레코딩이 끝났는지 안끝났는지에 따라 다르게 코드를 짜볼 수도 있다.  

```swift
func audioRecorderDidFinishRecording(_ recorder: AVAudioRecorder, successfully flag: Bool) {
        if flag{
            performSegue(withIdentifier: "stopRecording", sender: audioRecorder.url)
            print("AVAudioRecorder worked SUCCESSFULLY!")

        }else{
            print("AVAudioRecorder did not work properly")
    }
 }
```

### stack view  
iOS 9에서 소개되었던 UI element이다!  
UI stack view 안에서는 UI View Subclass 가 들어간다! (뭐든지 가능)  
Horizontal, Vertical 모두 가능  
vertical 안에 horizontal을 쌓을 수 있기도 하다!  

Remember that many of the UI Elements you have come to know, such as UIButton and UILabel, are subclasses of UIView. In fact, all UI Elements that you are going to be using in iOS come from UIView, as they have to know how to draw or render themselves.

stack을 꽉차게 auto layout 처리하기: 
![image](https://user-images.githubusercontent.com/37579661/90169126-21a00b80-ddd9-11ea-9a03-3f5edd84ccb2.png)

이렇게 4개 Contraints를 먹인 다음에 

![image](https://user-images.githubusercontent.com/37579661/90168617-4e9fee80-ddd8-11ea-8752-3fae2a41be57.png)
4개 모두의 constant를 0처리를 해주면 된다!


Asking good questions
To ensure the most productive search possible, be specific about the kinds of results you’re looking for. Image squishing can happen to web developers and Android developers too, so we’ll want to specify that we are looking for iOS and Swift answers. Specifically we are working with image buttons contained in a stack view, so it will help to include UIButton, image, or UIStackView in our search. We also might need to try a few variations for describing the problem. Distorted, stretched, squished, squashed, and smooshed are all words to try in our search queries. Some queries will lead to better results than others.

Evaluating answers
When searching for iOS button stretched, the top result we got was a post called How to not stretch an image in UIButton on Stack Overflow. Stack Overflow is a site where developers can ask questions, and other developers answer them. Next to each answer, you can see how many people “upvoted” that same answer, meaning they agreed or found it helpful. The above post describes a similar problem to ours: a button with a stretched image. Below the original post are some promising suggestions about setting the image’s content mode to Aspect Fit. This sounds like something to look into!

## enums 
The initialization of an enum type is straightforward: a specific member of the enum is assigned to a variable or constant. Alternatively, enums can also be initialized with raw values. Here we initialize a constant of type, AmericanLeagueWest, using a raw value:
`let myFavoriteTeam = AmericanLeagueWest(rawValue: "Oakland")`

## optional
It’s important that a method like Int() can return something that represents “no value” or “none.” Declaring y as a type Int is not enough. We need a type that has two “options”: either an int value, or no value. We can’t pretend that nil values don’t exist.

The struct has two properties: name (a String) and evilScheme (a optional String). This means that all instances of Villain must have a name. However, the evilScheme can be determined at a later time. This choice between either having a value or nil is why we make evilScheme optional.
```swift
struct Villain {
    let name : String
    var evilScheme: String?
}

let villain = Villain(name:"Billy", evilScheme: nil)
```

[코코아팟 이해하기](https://guides.cocoapods.org/using/getting-started.html)

react native 

Step 1: Start Metro
First, you will need to start Metro, the JavaScript bundler that ships with React Native. Metro "takes in an entry file and various options, and returns a single JavaScript file that includes all your code and its dependencies."—Metro Docs



ios 폴더를 xcode에서 열어서 build를 하려고 할 때 빌드 에러가 발생하는데, 
![image](https://user-images.githubusercontent.com/37579661/89860093-90b11080-dbdd-11ea-9c25-868c6d05e0cd.png)

