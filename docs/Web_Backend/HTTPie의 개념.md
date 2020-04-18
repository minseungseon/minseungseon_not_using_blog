Command Line으로 작동하는 Http Client  

## Httpie 설치  
```python 
pip install --upgrade httpie
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
