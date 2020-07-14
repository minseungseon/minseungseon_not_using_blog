---
layout: default
title: server에 대한 기본 이해
parent: Backend Basics
grand_parent: Web Backend
nav_order: 6

---

## 서버..
은행은 자기 서버를 구축하기도함...

서버는 이제 가상의 개념..
로컬호스트 장고에서 8000 같은것도 자기 컴퓨터가 서버가 되는 것이다.
8000 서버를 띄웠을 때, 

## 서버란 
request가 들어오면 response 를 보내주는게 서버이다  
서빙하는 웨이터와 같은 역할을 해서 서버이다...  

## 서버의 종류  
Database  
WAS(Weg Application Server) - django  
Nginx(파일을 저장하는데, 무거운 데이터들이 있을 때 쉽게빠르게 가져오기 위해 '캐싱'을 한다. 캐싱: 직접 파일 접근이 아니라, 파일의 위치로 접근하는것이다, 계층을 둬서 다 읽을 필요없음, static file 에 대한 로딩을 해줌. 특정 IP에서 공격이 들어오는데 이런것도 무시하도록 해주기도 함(white list), 과부하가 걸리지 않도록 데이터베이스를 여러개 두었을 때 나누도록 해주는 기능을 함(reverse proxy) 정말 실무용 서버! / Apache HTTP 

## database  
- 간단하게 각종 데이터를 더 잘 관리하기 위해 만든 시스템 
- 예전에는 텍스트 파일로 데이터를 관리함. 복구도 어렵고 이런 문제들을 해결하기 위해서 만들어진 것이 database  
- 표 형태로 만든것 ( RDMBS )  
- NoSQL : 빠르게 확장할 수 있는 DB (좋아요 같은 것과 같이 빠르게 저장하고 빠르게 데이터를 가져오는 것)  
- Reqest를 주면 저장된 데이터 기반으로 Response 원하는 데이터를 준다.  

## protocol (프로토콜)  
- 사람들이 통신하기 위해 만든 규약  
- 우리가 편지쓰는 것과 같이 ' 양식 ' 을 만드는 것.  
- request, response 의 양식이 바로 프로토콜인 것이다.  
- HTTP 가 일종의 프로토콜임. (Cors, Csrf) :웹에서의 대표적인 프로토콜 
  - GET, PUT, DELETE, POST 가 있음.  
  - 

## 인프라  
- AWS, GCP이런것들이 예전에 없었음. 그래서 물리적인 서버가 필요했다. 서버의 습도..등도 확인해야했다 ㅎ... 원래는 이런것이 인프라의 개념  
- 하지만 지금은 물리적인 서버가 거의 없음. 현재의 EC
- CICD : 예전에는 개발을 하고 나서 배포를 하려고 할 때 복잡했다. database가 잘 연결됐는지, 등을 확인하는것. 서버 버전도 관리해주고. product manager 가 하는 일이 되었음.  

## 소프트웨어 공학... 분야.. 
-확장성, 재사용성 등을 위해 아키텍트(구조)를 설계해야함  


## 엘리 챗봇 
- ec2 instance 위에 두가지 (챗봇 서버, 어드민 서버)  
- maria db 를 사용함 (mysql와 비슷하지만, 라이선스 돈을 안내서)  
- dialogflow api 을 통해 챗봇 서버를   
- iOS app 은 챗봇 서버와만 연락을 한다.  
- 챗봇 뷰도 서버에서 보여주는 것이다(ssr server side rendering)  
- react는 client side rendering 이다.  

- admin server : db와만 통신을 함  
- 쿼리 : request 
- 쿼리를 어떻게 짜느냐에 그 데이터 속도가 다라짐  
- 쿼리를 튜닝하기도 함 ( 더 성능좋게 인덱스를 넣기도 하고... )
- 쿼리셋 : 하나의 api임.  


처음으로 데이터베이스를 만드는거는 rds 
local에 mysql 만들어서 거기에 데이터베이스를 만들어도 됨 
