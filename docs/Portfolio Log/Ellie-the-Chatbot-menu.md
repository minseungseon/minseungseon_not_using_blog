---
layout: default
title: Ellie the Chatbot
parent: Portfolio Log
nav_order: 1
has_children: true
---

<h2 align="center">Ellie the Chatbot</h2>
<br/>
<p align="center"> <img src ="https://user-images.githubusercontent.com/37579661/89458116-77553200-d7a1-11ea-8ced-905038871d70.gif">
 </p>
 
<br/>

## :sparkles: About Ellie the Chatbot  
중앙대학교 영어교육학과 김혜영 교수님 지도 하에 만들어진 앱입니다.   
  

## :open_hands: How to use?  
본 앱은 학교코드를 부여받은 유저가 사용할 수 있습니다.  
학교코드를 부여받기 위해서 먼저 seonminseung@naver.com 으로 연락주시기 바랍니다:)  

## :pray: Contact  
만약 앱에 관련하여 연락하고 싶으시다면 개발자인 저에게 연락주시면 됩니다!  
contact email: seonminseung@naver.com  
감사합니다 :)

<br> 

## 화면 설명  

<br>

## Login View - 로그인 화면

<img src="https://user-images.githubusercontent.com/37579661/116289436-73ed5500-a7cd-11eb-8017-04277a51cccb.png" width = 100%>

Ellie The Chatbot 로그인 화면입니다. 

아이디, 비밀번호를 입력하면https://chatbot.smartteaching.or.kr/login 서버를 통해 통신하여 로그인이 진행됩니다. 

아이디, 비밀번호를 입력하지 않고 로그인 버튼을 누르면 로그인이 실행되지 않습니다.

<br>

## 회원가입 화면

<img src="https://user-images.githubusercontent.com/37579661/116289693-ac8d2e80-a7cd-11eb-883e-a21d97cb5eb6.png" width = 100%>

회원가입 화면에서는 자신의 정보를 입력하고, 만약 선생님의 지도 하에 Ellie The Chatbot을 사용하는 경우에는 학교코드를 입력할 수 있습니다. 선생님의 지도하에 앱을 다운로드 받은 경우가 아니라면, 외부인 코드를 입력하여 회원가입을 진행합니다.

정보없이 회원가입을 진행하려고 한다면 에러 문구가 나타납니다.

<br>

## Main View - 홈 화면
<img src="https://user-images.githubusercontent.com/37579661/116289829-cdee1a80-a7cd-11eb-9d14-2679b18f2e24.png" width = 40%>

메인 홈 화면 입니다. 

유저는 본인이 원하는 모드로 선택하여 들어가서 Ellie와 대화할 수 있습니다. 

1) Free Talking - 자유롭게 Ellie 와 대화를 할 수 있습니다. 

2) Mission Challenge - 다양한 미션을 수행하며 Ellie 와 대화합니다.

3) Speaking Games - Ellie와 게임을 진행하며 대화를 이어나갑니다.

<br>

## 1) Free Talking

<img src="https://user-images.githubusercontent.com/37579661/116290055-068df400-a7ce-11eb-9e8f-2f599e29ea27.png" width = 40%>

유저는 Free Talking에서 엘리와 자유 대화를 이어나갑니다. 

<br>

## 2) Mission Challenge

<img src="https://user-images.githubusercontent.com/37579661/116290163-23c2c280-a7ce-11eb-8718-b9d4e328c946.png" width = 100%>


유저는 원하는 미션을 탭하여 들어가 Ellie와 대화를 하며 미션을 수행합니다.

<br>

## 3) Speaking Games

<img src="https://user-images.githubusercontent.com/37579661/116290232-3c32dd00-a7ce-11eb-8c9a-dfecd6794e13.png" width = 100%>

Speaking Games 에서 유저는 다양한 영어회화 관련 게임을 Ellie와의 대화를 통해 이어나갑니다.

<br>

## Framework  

| **server** | **front end** |  
| :----------: | :-----------------------: |
| Node.js | iOS |

was in charge of iOS.  


<br/>

## Progress  
pre-launched through TestFlight, preparing to be launched in AppStore. 
<br/>


## Design Pattern   
: Ellie the Chatbot uses **MVC pattern**.   
  
## Details  
 1. Model:  
   
 2. View:  
   
| **view 이름** | 역할 | 내용 |  
|:------------:|:---:|:---:|  
|ChatView.swift|     | struct - ChatMessage(Hashable, Identifiable)
ContentView.swift  |
  
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
  - type, message그리고 ChatView.swift의 `ChatView` struct를 가져오기 위해 선언한다.
      ```swift
      let type: Type
      let messages: Message
      var chatView: ChatView
      ```
  - 선언 후에 init을 해준다. 그 이유는 ChatView를 상속받으면서 현재 struct의 타입과 메시지 파라미터를 넘겨준다.   
      ```swift
       init(_ typeObj: Type) { 
        self.type = typeObj
        self.messages = Message() 
        chatView = ChatView(self.type, messages: self.messages)
        }
       ```
        
  - 메인 `body`에서는 `GeometryReader`를 통해 `self.chatView`를 띄운다!  
      ```swift
      var body: some View {
        return
            GeometryReader { geometry in
                    ZStack(alignment: .leading) {
                        self.chatView
                            .padding(.bottom, 20)
                            .padding(.top, 20)
                            .frame(width: geometry.size.width, height: geometry.size.height)
                    }
        }
    } 
      ```
  
- 그 외 종속성 
    1. `@ObservedObject var closedCap: ClosedCaptioning`은 `class ClosedCaptioning: ObservableObject`에서 이렇게 import 되어지는 `ObservableObject`와 소통한다!  
    2. `ClosedCaptioning.swift`은 `ChatController.swift`와 소통한다. 




       




 1. View Controller:  
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
  
chatbot 관련된 부분 소개:  
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
  



 

