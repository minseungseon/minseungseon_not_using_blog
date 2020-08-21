---
layout: default
title: 기타등등
parent: iOS
nav_order: 2
has_children: true
---


트러블 슈팅

## 1. 다크모드 예외처리 문제

문제점: 
![IMG_1742](https://user-images.githubusercontent.com/37579661/90278661-b7ec3400-dea2-11ea-9972-932169cc4b30.PNG)

이렇게 다크모드가 되면 자동으로 글씨가 하얗게 되면서 placeholder와 안에 써지는 글씨가 보이지 않게 된다!  

이를 해결하기 위해서는 
text field에서 Place holder와 textfield를 '분리'시켜야한다.  
[이 글](https://stackoverflow.com/questions/57688242/swiftui-how-to-change-the-placeholder-color-of-the-textfield) 을 참고하여 해결해보았다.  

해결 코드:
![image](https://user-images.githubusercontent.com/37579661/90278490-7c516a00-dea2-11ea-8830-dc79310155dc.png)

해결 후:  
![IMG_1743](https://user-images.githubusercontent.com/37579661/90279326-fb936d80-dea3-11ea-92b2-17199edfec9f.PNG)
![IMG_1744](https://user-images.githubusercontent.com/37579661/90279327-fcc49a80-dea3-11ea-9111-f3a9062effe8.PNG)


또는..  

그냥 
.background(Color(.systemBackground))
를 추가할 수도 있는 문제였다 ㅠㅠ  


## better iOS developer가 되는 방법 
## 1. 주석활용: //MARK 

![image](https://user-images.githubusercontent.com/37579661/90313251-f686fa80-df45-11ea-91a6-53d656fa1d4e.png)

이렇게 `// MARK: Alerts` 주석을 달아놓으면 사진에서 처럼 쉽게 navigate를 할 수 있게 된다! 

## 2. 코드 정리하기  
코드를 정리하는 방식은 다양하다!
뭔가 좋은 코드를 많이 보고 직접 연습해보는 과정이 많아져야지 이런 좋은 코드를 술술 잘 쓸 수 있게 되는 것 같다.  

![image](https://user-images.githubusercontent.com/37579661/90313845-a3637680-df4a-11ea-903b-2153c3c79a1d.png)

일단 복붙 해놓고 연습해보고자 한다.. 



# playSound function 헤쳐보기  
## optional parameters  
`func playSound(rate: Float? = nil, pitch: Float? = nil, echo: Bool = false, reverb: Bool = false) {`  
이러한 것을 **optional parameters**라고 부른다.  

 위는 AVAudio 에서 저장된 음성을 재생해주는 function이다. 
 이 때 playSound()를 호출하면서 `rate` 에 해당하는 parameter값을 호출 할 때에 지정해주지 않으면, 위에 명시된 `rate = nil `값으로 디폴트 설정 그대로 설정된다.  


위에서 설정한 optional 값(rate, pitch)이 들어왔는지 확인해주는 부분이 필요하다. 
```swift
if let pitch = pitch {
            changeRatePitchNode.pitch = pitch
        }
```
이 때 pitch = pitch 는 'pitch 값이 nill이 아니라면, 이 코드를 실행하라 라는 의미이다.  

그 다음에 echo, reverb의 경우에는

```swift
if echo == true && reverb == true {
            connectAudioNodes(audioPlayerNode, changeRatePitchNode, echoNode, reverbNode, audioEngine.outputNode)
        } else if echo == true {
            connectAudioNodes(audioPlayerNode, changeRatePitchNode, echoNode, audioEngine.outputNode)
        } else if reverb == true {
            connectAudioNodes(audioPlayerNode, changeRatePitchNode, reverbNode, audioEngine.outputNode)
        } else {
            connectAudioNodes(audioPlayerNode, changeRatePitchNode, audioEngine.outputNode)
        }
```
위에서 false로 되어있었던 디폴트값이 호출되면서 true 가 된다면, 그리고 둘다 true인 경우, 하나씩만 true 인 경우 등으로 나누어 실행시킨다.  


```swift
// schedule to play and start the engine!
        audioPlayerNode.stop()
        audioPlayerNode.scheduleFile(audioFile, at: nil) {
            
            var delayInSeconds: Double = 0
            
            if let lastRenderTime = self.audioPlayerNode.lastRenderTime, let playerTime = self.audioPlayerNode.playerTime(forNodeTime: lastRenderTime) {
                
                if let rate = rate {
                    delayInSeconds = Double(self.audioFile.length - playerTime.sampleTime) / Double(self.audioFile.processingFormat.sampleRate) / Double(rate)
                } else {
                    delayInSeconds = Double(self.audioFile.length - playerTime.sampleTime) / Double(self.audioFile.processingFormat.sampleRate)
                }
            }
            
            // schedule a stop timer for when audio finishes playing
            self.stopTimer = Timer(timeInterval: delayInSeconds, target: self, selector: #selector(PlaySoundsViewController.stopAudio), userInfo: nil, repeats: false)
            RunLoop.main.add(self.stopTimer!, forMode: RunLoop.Mode.default)
        }

```
메모리에 audioFile이 존재하는지를 확실하게 해주고, play 될 준비가 되있는지를 확실하게 해주는 부분이다.  
그리고 
`audioPlayerNode.scheduleFile(audioFile, at: nil) {` 뒤에 이어지는 거대한 코드 덩어리는 **trailing closure** 이다.  
이를 이해하기 위해서는 **closure**이 무엇인지에 대해서 이해해야한다!  
They are essentially functions or chunks of code that can be passed around just like regular variables 
, 그리고 sceduleFile은 재생될 준비가 되었을 때 동작하는 closure 를 가지고 있다고 해석 할 수 있다. 
다 재생되면 멈추고, notplaying state로 바꾸어주는 내용을 지니고 있다. 


## design pattern
NBC
MVC 

## action, outlet
action is a method, outlet is a property
marking a variable as an IBOutlet makes it visible in Storyboard
A view in Storyboard needs an outlet if it needs to be modified programmatically

A view in Storyboard needs an action if it is expected to respond to user input.


## Xcode meanings in various Sent Event

오랜만에 storyboard를 하다가 궁금하게된 이 어마무시한 리스트..

![image](https://user-images.githubusercontent.com/37579661/90339574-a33ba780-e02c-11ea-9075-1c2a3cd8820f.png)

궁금해서 찾아보게되었다!
일단 가장 많이 사용하는 것은 touch up inside 인데..
놀랍게도 그 의미는 "Press and release the button within the scope", 즉 특정 범위에서 버튼을 누르고 떼는 동작을 의미한다.  
![image](https://user-images.githubusercontent.com/37579661/90339246-8900ca00-e02a-11ea-927b-3e7571ea84fc.png)

더 하다 보면 이런 것들이 다 어떤 역할을 하는지 몸에 베이겠지...? ㅎㅎ 
[여기](https://www.logcg.com/en/archives/1833.html)에서 위의 소스는 가져와본 것이었다. 2016년 게시물이라서.. 바뀌었을지 모르지만~!~!~  

## UIButton
To handle an interaction with a switch, our actions use the valueChanged event.
![image](https://user-images.githubusercontent.com/37579661/90339788-1d206080-e02e-11ea-8a4f-fe31a9df8831.png)
[다큐멘테이션](https://developer.apple.com/documentation/uikit/uiswitch)에 의하면 위와 같다고 한다..!  
즉, 스위치와의 상호작용을 다루기 위해서는 우리의 action은 valueChanged event를 사용한다는 것!  
그리고 switch 가 on/off 되었다는 상태를 알리기 위해 사용하는 property는 `isOn` 이다!  

## ImagePicker  
아이폰에서 자신의 사진을 올리기 위해 앨범을 사용할 때 올라오는 모달을 구현하는 메소드이다!  

아주 쉽게 구현해볼 수 있다~

참고 : 
![image](https://user-images.githubusercontent.com/37579661/90364228-0534f500-e09f-11ea-9711-eec82c3573a7.png)


```swift
import UIKit

class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.
    }
    @IBAction func experiment(send: UIButton) {
        let nextController = UIImagePickerController()
        present(nextController,animated: true, completion: nil)
    }


}

```

위의 코드를 viewcontroller.swift에 추가하고, IBAction을 스토리보드상의 버튼과 연결 시켜주면 끝!  
![image](https://user-images.githubusercontent.com/37579661/90364274-18e05b80-e09f-11ea-91c8-847c45b449e1.png)

![image](https://user-images.githubusercontent.com/37579661/90364612-593fd980-e09f-11ea-9476-585fdccdbd1e.png)
![image](https://user-images.githubusercontent.com/37579661/90364657-678df580-e09f-11ea-8453-6fbcb40d7586.png)

그리고 info.plist 파일에서 위와 같이 row 를 추가해준다.  

위의 image picker controller는 다른 controller들과 다르다. 

Of the view controllers that we have presented so far, which ones required the presenting controller to provide information to the new controller.

For the Activity View, we supplied an image to be shared. For the Alert View, we supplied the title, message, and OK button. And for the Dice View Controller, we supplied the two dice values.

We did not give the Image Picker any information, although we could have modified it to use the camera instead of the photo library.

## prepare for segue

![image](https://user-images.githubusercontent.com/37579661/90374038-d1ad9700-e0ad-11ea-97db-010e8959193d.png)


## delegate  
- an object that executes a group of methods on behalf of another object
- view reuse, cutomize를 도와준다!  

- 질문과 관련을 지으면 쉽게 이해할 수 있다. delegate한테 view는 질문을 던진다!  
ex. 이 새로운 characters로 내가 뭘 해야하니? return button이 눌러지면 내가 어떻게 반응해야하니?  
- view의 delegate은 보통 control object가 된다.  그리고 그 control object가 위의 질문들에 대답한다. 그리고 그 과정에서 protocol에 기록을 한다. 그 protocol을 만족하면 delegate이 된다!  

-If the only difference between the three text fields is their delegates, can we swap the delegates and see the behaviors swap?
--> 가능하다. custom behavior는 delegate에 의해 제공되어진다!  

예를 들어, 
RandomColorTextFieldDelegate.swift 를 구성할 때, 처음으로 넣은 것은
![image](https://user-images.githubusercontent.com/37579661/90543752-1aa24000-e1c1-11ea-9b40-db766eb005b5.png)
이것인데,  

NSObject는 ![image](https://user-images.githubusercontent.com/37579661/90543871-386fa500-e1c1-11ea-833e-806fa0890cc3.png)
Objective-C class 상속에서의 루트 클래스인것으로 다큐멘트에서 소개되어진다.  
아마 가장 루트를 건들기 위해서 이렇게 Delegate 을 사용하면서 같이 implement 하는 것으로 보인다.  


![image](https://user-images.githubusercontent.com/37579661/90544768-93ee6280-e1c2-11ea-9e7a-4952ea2ea509.png)

![image](https://user-images.githubusercontent.com/37579661/90544794-9e106100-e1c2-11ea-84f6-6afbc103f606.png)





