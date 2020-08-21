---
layout: default
title: Ellie the Chatbot
parent: Portfolio Log
nav_order: 1
has_children: true
---

<h2 align="center">Ellie the Chatbot</h2>

<p align="center"> <img src ="https://user-images.githubusercontent.com/37579661/89458116-77553200-d7a1-11ea-8ced-905038871d70.gif">
 </p>
 
 

 ## Design Pattern  
 : MVC (Model-View-Controller)  
 *애플의 MVC패턴은 기존 MVC패턴과 다르다, View와 Controller가 강하게 연결되어 있어 View Controller가 거의 모든 일을 한다.*

 1. Model:  

 2. View:  
ChatView.swift
ContentView.swift

MainView.swift
MissionChallengeMenu.swift
SpeakingGamesMenuView.swift

LoginView.swift
SignupView.swift

KeyboardObserving.swift


 3. Controller:
    3-1. ChatController.swift
      - imported : ObservableObject protocol, Observer 
      - 내부 코드 : 
      ```swift
         private var typeObj : Type = Type() //chat type 의 핵심이 되는 부분 
         private var messages: Message = Message()
         
         // didChange will let the SwiftUI know that some changes have happened in this object
         // and we need to rebuild all the views related to that object
         var didChange = PassthroughSubject<Void, Never>()
         
         // defulat type is type1
         var type: String = "type1"
         var strUrl : String = "https://chatbot.smartteaching.or.kr/"
         
         let defaultSession = URLSession(configuration: .default)
         var dataTask: URLSessionDataTask?
      
      ```
      
    3-2. UserController.swift
      - imported : ObservableObject protocol

chatbot 관련된 것: 
Message.swift : message를 observer에 등록
Type.swift : type를 observer에 등록 
Observer.swift
```swift
protocol Observer {
    // For type passing
    func update(_ notifyValue: String)
    
    // For messages
    func update(_ notifyValue: [ChatMessage])
}
``` 




 observer Pattern
 there is obersavable protocol - 

 communication patterns
 1. delegates and protocols 
one to one communication (one view 와 one view)
boss and an intern! 느낌이다. 
인턴은 보스의 명령만을 기다린다! 

 
 2. observer and notifications 
one to many communication 
 

ObservableObject protocol can use SwiftUI’s @Published property wrapper to automatically announce changes to properties, so that any views using the object get their body property reinvoked and stay in sync with their data. That works really well a lot of the time, but sometimes you want a little more control and SwiftUI’s solution is called objectWillChange.

Every class that conforms to ObservableObject automatically gains a property called objectWillChange. This is a publisher, which means it does the same job as the @Published property wrapper: it notifies any views that are observing that object that something important has changed. As its name implies, this publisher should be triggered immediately before we make our change, which allows SwiftUI to examine the state of our UI and prepare for animation changes.

