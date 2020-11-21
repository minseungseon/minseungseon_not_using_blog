---
layout: default
title: Array 활용
parent: iOS
grand_parent: 코딩공부
nav_order: 7

---

## array 활용해보기  
사실 array의 기본적인 모든것을 적기에는 (귀찮아서) ㅎ...  
그냥 활용 부분을 작성해놓고자 한다!  
for my future sake...!!  


## array 와 for loop  

```swift
for item in Array {

}
```
를 활용하여 array 안에 있는 값들에 접근을 하여 어쩌고저쩌고를 할 수 있다!  


### 배열에 있는 숫자들의 합 구하기  

```swift
let intArray = [2,3,4,5,5] 
var sum = 0 
for value in intArray{
    sum += value
}
```

이렇게 할 수 있다!!  


### 배열 안에 있는 값 출력하기 

func printElements(array: [Int]) {
    for value in array{
        print("\(value)")
    }
}

### 입력한 수만큼 배열에서 숫자 제거하기 

![image](https://user-images.githubusercontent.com/37579661/98463194-e86f1000-21fc-11eb-9b96-be0b8155f51d.png)


```swift
func removeElements(array: [Int], n: Int) -> [Int] {
    // You may need to modify newArray
     var returnArray = array

    for _ in 0..<n{
        returnArray.removeFirst()
        
    }
 return returnArray
}

var newArray = [3,4,5,6,4,6]

for value in removeElements(array:newArray, n:3){
    print("\(value)")
}

```

