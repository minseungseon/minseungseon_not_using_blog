Command Line으로 작동하는 Http Client  

## Httpie 설치  
```python 
pip install --upgrade httpie  

#맥 터미널에서는..
brew install httpie 

#홈페이지를 보니 거의 모든 tool로 install 이 가능하다!
#https://httpie.org/doc#installation

``` 

## Httpie 명령어  
http 키워드로 시작함!!!  
  
`http [flags_옵션] [METHOD_예를들어 POST] URL [ITEM[ITEM]] `  
  
* [ITEM[ITEM]] : **옵션** 을 입력하는 곳  
* POST,PUT 방식 요청 : ** = **으로 표현  
* GET 방식 요청 : ** == **으로 표현  
  
* `Json`형식의 요청:  
`http --json POST 대상주소 GET인자 == 값 POST인자 =값`  
  
* `HTML form` 형식의 요청:  
`http --form POST 대상주소 GET인자==값 POST인자=값`  
  
  * Get인자가 있으면 쓰고, 없으면 안써도됨!  
  * Put인자도 마찬가지.  
  
  
~~잘 이해가 되지 않으니 직접 해보도록 하자~~ 
  
## 직접 해보기  
맥이라면, `$ brew install httpie` 를 하여 설치를 하면 된다!  
설치후에 `$ http` 를 터미널에 치면, 아래와 같이 나온다.  

[터미널]<img src=./http.png>
  
`$ http get 아무페이지의주소`  
를 치게 되면 그 페이지에 대한 다양한 정보를 얻을 수 있다.  
~~정말 신기방기~~  
<img src=./http02.png>  
  
  
* **port 번호로 http 명령어를 사용하고 싶으면  **  
```$ http :8000```  
이런식으로 터미널에 작성하여햐 한다.  
