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
  - isMe 변수는 유저가 메세지를 보내면 true 가 된다.  

- public struct **ListSeparatorStyleNoneModifier**  
  - imported ViewModifier protocol, viewModifier와 그 viewModifier struct 를 호출하는 extension View 를 활용하여 UITableView 내의 '줄(lineSeparator)'을 생략하는 뷰 스타일을 적용함 
  - lisenSeparator 생략하는 줄 : `UITableView.appearance().separatorStyle = .none`

- struct **CircleImage**: View
  - 변수 name 을 파라미터로 받는 구조체이다.  
  - 변수 name은 *struct ChatRow*에서 지정해준다. (앨리인지, user인지에 따라 name 부여. 앨리면 name = "a5" 부여, 유저라면 "a4"부여)  
  - 이 구조체 안에서는 name에 따라 들어온 Image를 `.resizable()`: 리사이즈 하고, `.clipShape(Circle())`: 원 모양으로 처리하고, `.aspectRatio(contentMode: .fit)`을 통해서는 프레임 스케일에 딱 맞게 비율이 조정되도록 한다. `.overlay(Circle().stroke(color4, lineWidth: 2))` overlay는 기존 뷰 위에 두번째 뷰를 layering 하는 것이다.  

- struct **ChatRow** : View  
  - 앨리는 왼쪽부터 프로필 이미지가 뜨기 때문에 'Ellie'라는 이름을 왼쪽에 띄워야하기 때문에 `VStack(alignment: .leading) ` , 유저(핸드폰을 들고 말하는 입장)는 오른쪽에 프로필 이미지가 떠고 이름도 왼쪽에 붙어야하기 때문에 `VStack(alignment: .trailing)`을 한다.  
  ![image](https://user-images.githubusercontent.com/37579661/90950525-540ed000-e48d-11ea-9a42-3285db93fecf.png)  

- struct **ChatView** : View  
  - `var type: Type` type 을 파라미터 변수로 받아온다.  
  - 
  ```swift
  @ObservedObject var messages: Message
    @ObservedObject var closedCap: ClosedCaptioning  
  ``` 
    : observer에 등록되어있는 `messages` 와 `closedCaptioning`을 가져온다.  
  
  - 
  ```swift
    init(_ typeObj: Type, messages: Message) {
        self.type = typeObj
        self.messages = messages
        self.closedCap = ClosedCaptioning(typeObj, messages: messages)
    }
    ```
    initialization을 `typeObj`에 `Type`객체를 담고, `messages`에 위에서 ObservedObject로 선언된 `Messages`를 담는다.  

- var **body**: some View  
  - 
  ```swift 
  var body: some View {

        return VStack {
                List {
                    ForEach(self.messages.getMessage(), id: \.id) { msg in
                        ChatRow(chatMessage: msg)
                    }
                }.listSeparatorStyleNone()

                VStack(alignment: .center) {
                    HStack {
                        Button(action: {
                            self.closedCap.micButtonTapped()
                        }) {
                            Image(systemName: !self.closedCap.micEnabled ? "mic.slash" : (self.closedCap.isPlaying ? "mic.circle.fill" : "mic.circle"))
                                .resizable()
                                .scaledToFit()
                                .aspectRatio(contentMode: .fit)
                                .frame(height: 80)
                                .padding()

                        }
                    }
                }
        }.onAppear {
            self.closedCap.getPermission()
        }
    }
  ```
    - 첫번째 VStack, 두번째 Vstack으로 이루어져 있다.  
    - 첫번째 VStack은 `messages`의 `getMessage()`메소드를 통해 수집되는 메세지의 내용을 각각에 고유 `id`를 넘겨주며 `ChatRow`구조체의 `msg` 파라미터(chatMessage)로 넘겨준다.  
    - 두번째 VStack 은 마이크 이미지를 가진 버튼이 보여지는 HStack을 포함하고 있다. (HStack: A view that arranges its children in a horizontal line.)  
    - 버튼의 action은 `closedCap.micButtonTapped()` 메소드를 불러오는 것으로 지정되어서, 
    ![image](https://user-images.githubusercontent.com/37579661/90952719-e66c9f00-e4a0-11ea-9627-5b43a899300a.png)
    녹움 중(if audioEngine.isRunning)이면 `.endAudio()`(Marks the end of audio input for the recognition request.) 메소드를 부르고, 아니라면 녹음을 시작( `try startRecording()isPlaying = true`) 하게 된다.  

    - 처음으로 이 메인 body가 나타날 때에, 마이크를 사용하는 것에 대한 permission을 받는데, 이 또한 observedobject인 closedcap의 .getPermission() 메소드를 통해 이루어진다. `.onAppear {self.closedCap.getPermission()}`  

2. ContentView.swift  
: 엘리와의 채팅 창을 보여주는 view. `ChatView.swift` 를 그대로 상속받아 보여주는 view 파일이다.  
    - struct **ContentView**: View  
      - 
       
  ```swift 
    let type: Type
    let messages: Message
     var chatView: ChatView
       ```
       chatView를 ContentView에서 




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
  



 

