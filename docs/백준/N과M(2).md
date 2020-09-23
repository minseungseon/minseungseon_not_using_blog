---
layout: default
title: 백트래킹-N과M(2)-15650
parent: 백준
nav_order: 12

---

## 문제:   
**문제 이름: N과M(2)**  
**내피셜 난이도: :star: :star:**  

**문제 본문**:  

## 입력:   

## 출력:   

## 개념설명:   
N, M이 주어졌을 때, 

## 접근방법:   
```c++
#include <iostream>
#include <cstring>
#include <queue> //bfs 위한 것 
#define MAX 8 

using namespace std;

int N,M,cnt,idx;
int arr[MAX];
bool visited[MAX];

void Print() {
    for (int i=0; i<N; i++){
        if(visited[i]){
            cout << arr[i] << " ";
        }
    }
    cout << "\n";

}
void DFS(int cnt, int idx){ //첫번째 턴: cnt=0 idx=0 , 두번째 턴: cnt=1 idx=1
    if(cnt == M) {//M=2 
        Print();
        return;
    }
    
    for (int i=idx; i<N; i++){ //idx 는 수열의 첫번째 숫자가 된다!
        if(visited[i]){
            continue;
        }
        visited[i]=true;
        DFS(cnt+1, idx+1);
        visited[i]=false; // 1,2 출력 후 arr[1]=2 는 false 처리됨. 
    }
}


int main(void){
    cin >> N >> M;
    for(int i=0; i<N; i++){
        arr[i]=i+1; //수열에 나올 수 있는 숫자들 넣어주기! N=4 이면 1,2,3,4 를 arr 배열에 넣어준다 
        visited[i]=false; //모두 false 처리
    }
    DFS(0,0);

}

//며칠이 되면 다 익게되는지? 
//첫번재 토마토를 DFS함수에 넣고, 방문표시/주변을 확인/, 
//지도를 벗어나지 않고 토마토가 안익었으면서(0) 방문하지 않았다면 -> 방문
// 방문하면서 [x][y]=익은토마토(1)+1 
//방문 시작 포인트는 [M][N] x좌표에 -1, y 좌표에 -1
```
## 첫번째 시도:   
```java

``` 
## 두번째 시도:   
```java

``` 
