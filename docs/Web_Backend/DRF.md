## Json 
-자바스크립트로 만들어짐  
-데이터의 송수신을 자바스크립트의 객체로서 수해할 수 있게끔 해주는 가벼운 문자열 데이터 표현식  
-대세이다..!  

## XML
-일종의 데이터 표현식  
-데이터 크기가 좀 커서 요즘은 Json 을 더 많이 씀!  

## Json 의 문법 형식  
```javascript
json_example = 
{
"string_name": "something",
"number_name": 3,
"null_name": null,
"bool_name": true
}
```
## Json 표현하기   
```javascript
{
"id":3,
"title": "민승.github.io",
"body": "블로그의 내용입니다"
}
```

## Json 을 Universal 한 언어로 바꾸기  
**모두가 아는 자료형** 인, **문자열** 로 변환하여 전송해야함  
**="직렬화_seriazlizing"** 이라고 함.  

따라서, 웹사이트에서도 DRF server 로 '문자열을 객체로 바꾸어 보내고', DRF에서는 '객체를 문자열로 바꾸어 보낸'다.  
=직렬화, 역직렬화  

## 참고하면 좋은 사이트  
www.json.org  

## 파이썬에서 json 사용 방법  
#### json import 시키기  

```python  
impot json  #매우간단...
```
이 때 파이썬 파일 이름을 `json.py` 로 설정하면 **안된다..**  
이렇게 하면 json module 을 읽어오지 못하더라구요..


#### 직렬화, 역직렬화 표현하기 
```python 
import json #json 임포트

practice_blog = {
    "id": 1,
    "title": "연습 블로그 글 제목",
    "body": "글에 따른 내용물",
}

print(practice_blog)        #위에 작성한 내용이 프린트됨 {'id': 1, 'title': '연습 블로그 글 제목', 'body': '글에 따른 내용물'}
print(type(practice_blog))  #<class 'dict'> 
                            #위에 작성된 것의 '타입'인, 딕셔너리가 프린트 됨 

#직렬화
practice_blog_srz = json.dumps(practice_blog) #dumps 를 쓰게 되면, distionary 타입을 ---> json 문자열로 바꾸어줌 

print (type(practice_blog_srz)) #<class 'str'>
                                #dumps 처리한 것은 이제 '딕셔너리'가 아닌, '문자열'로 프린트됨. 

#역직렬화
practice_blog_reverse = json.loads(practice_blog_srz) #문자열로 바뀐 것을 다시 딕셔너리로 바꾸어줌 
print(type(practice_blog_reverse)) #<class 'dict'>
```





