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
 : Ellie the Chatbot uses **MVC pattern**.   
  
## Details  
 1. Model:  
   
 2. View:  
   
| **view 이름** | 역할 | 내용 |  
|:------------:|:---:|:---:|  
|ChatView.swift|     | struct - ChatMessage(Hashable, Identifiable)
ContentView.swift  
  
MainView.swift  
MissionChallengeMenu.swift  
SpeakingGamesMenuView.swift  
  
LoginView.swift  
SignupView.swift  
  
KeyboardObserving.swift  

1. ChatView.swift  
- struct **ChatMessage**  
  - imported Identifiable protocol with UUID(Universally Unique Identifer), 구조체 안에 있는 **message, avatar, color, isMe**를 각각 유니크한 값으로 자동으로 인식하도록 처리해주었음  

- public struct **ListSeparatorStyleNoneModifier**  
  - imported ViewModifier protocol, viewModifier와 그 viewModifier struct 를 호출하는 extension View 를 활용하여 UITableView 내의 '줄(lineSeparator)'을 생략하는 뷰 스타일을 적용함 
  - lisenSeparator 생략하는 줄 : `UITableView.appearance().separatorStyle = .none`

 3. View Controller:  
    3-1. ChatController.swift  
      - imported : ObservableObject protocol, Observer  
      - 내부 코드 :  
      ```swift

         private var typeObj : Type = Type()  
         private var messages: Message = Message()
         
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
  



 

