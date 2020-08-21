---
layout: default
title: Xcode Previews
parent: iOS
nav_order: 3
has_children: true
---


iOS 개발자와 디자이너의 소통 과정은 다음과 같다.  

- configuring (디자이너의 요구조건 반영하기)  
- building (변경하고 앱 빌드하기)
- running (실제 디바이스 올리기)
- navigating (실제 화면 찾아가기)
- getting to the state (그 state 만들기)
 
 너무 복잡하고 긴 과정이야~~  

 이러한 것을 **preview**로 해결할 수 있다!!  


XIB의 문제점 

 - XIB(Xcdoe Interface Builder)는 그냥 XML인데, 읽거나 수정할 수 없는 XML이다..  
 
 storyboard 문제점
 - 파일이 정말 커지고, 소스 컨트롤을 바꿀 때 마다 다시 작업해야하는 상황이 발생하기도 함  

 IB는 swift 코드를 서로 잘 모른다.
  그래서 IBOutlet, IBAction을 통해 Interface Builder와 실제 swift코드를 연결해준다..
근데 만약 그 view를 지워버리면 IB가 남아있게 된다. (물론 속이 비어있는 동그라미로 남아있긴 하지만 이런것까지 github에서는 확인불가..)
cell in tableview 에서 identifier로 가져와야하는데, 이 때 또 typecast도 해야한다..

programmatically UI를 짜는 것의 단점은?  
visualization이 거의 안되고, views, constraints 상속 및 그 속 구조 파악이 한눈에 어렵다  ㅠㅠ  
지나치게 layout설정, background 설정 코드들이 많이 들어가야하고, 그래서 코드가 복잡해진다.

위의 문제를 해결하기 위해~  
**IBKit**을 김형남 씨는 소개해준다!  
- programmatically UI를 짜는 것의 단점인, 
    1. visualization 은 **Xcode Previes**로 해결하고,  
    2. 직관적인 코드 이해는 **Declarative 스타일**을 활용하여 해결하자는 것이다.  

- declarative style ?  
    - @_functionBuilder feature를 사용하여 최대한 decalarative 하게 사용하고자했다.   
    ![image](https://user-images.githubusercontent.com/37579661/90806519-18beb500-e358-11ea-9699-a17ff9c8ff13.png)

