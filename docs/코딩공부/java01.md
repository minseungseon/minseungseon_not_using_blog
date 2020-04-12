---
layout: page
title: do-while문
parent:Java공부
grand_parent: 코딩공부
nav_order: 1

---

# do-while문
특징: i의 값이 적어도 한번은 출력이 된다는 것이 특징  
  
형번환은 무조건 해주어야한다.  
c = (char)(c+1);  
c는 character 이고 c+1 은 integer 이기 때문에  (character + 정수형 은 integer)
c 값에 (char)(c+1) 을 넣어주려면 **형변환** 을 해주어야함 

loop 중첩은 3번정도가 제일 바람직함. 너무 복잡해짐!  

continue문이 있으면 조건식으로 다시 가게됨  

brake문은 완전히 반복문 하나를 빠져 나가게 함  

scanner.nextline() -> 엔터키를 칠때까지 = 한문장을 가져온다.  

# trouble-shooting  
println() 과 print() 를 헷갈렸다..  
println() 은 줄 바꿈을 하지만, print()는 줄을 바꾸지 않고 그냥 출력해주는 명령어이다.  
