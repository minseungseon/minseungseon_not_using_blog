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

 *애플의 MVC패턴은 기존 MVC패턴과 다르다, View와 Controller가 강하게 연결되어 있어 View Controller가 거의 모든 일을 한다.*

 ```swift 
 struct ChatMessage: Hashable, Identifiable {
    var id = UUID() //Universally Unique Identifier
    var message: String
    var avatar: String
    var color: Color
    // isMe will be true if We sent the message
    var isMe: Bool = false
}
 ```

 ```swift 
 public struct ListSeparatorStyleNoneModifier: ViewModifier {
    public func body(content: Content) -> some View {
        content.onAppear {
            UITableView.appearance().separatorStyle = .none
        }.onDisappear {
            UITableView.appearance().separatorStyle = .singleLine
        }
    }
}

extension View {
    public func listSeparatorStyleNone() -> some View {
        modifier(ListSeparatorStyleNoneModifier())
    }
}
```


## AVAudio  
Summary

` static var duckOthers: AVAudioSession.CategoryOptions { get } `
: An option that reduces the volume of other audio session while audio from this session plays.



