---
layout: default
title: Data Abstraction?
parent: C++
grand_parent: 코딩공부
nav_order: 1

---

# Data Abstraction  
= encapsulation, information hiding  
- 인터페이스와 implementation(코드)를 분리하는 것  

- 사용 이유
1. protection  
- 데이터에 대한 접근을 제한하기 위해 사용한다.  
- 오직 인터페이스를 통해 접근 가능  

2. readability  

3. implementation independence  
인터페이스를 변경하지 않고 코드만 개선시킬 수 있다는 장점이 있다.  

## class의 구성  
1. behavior ( method )  
- actions that an instance can perform in response to a request  
- implemented by methods  

2. state (Variable)  
- behavior 를 잘 실행하기위해 object(객체)가 반드시 유지해야할 데이터를 의미함  
- stored in instance variables (= data members, data fields)  

## methods  
1. name  

2. signature = argument type
- return type, argument type 모두를 의미함  
- method 이름이 같으면 다른 signature로 분류될 수 있다!    

3. body  
- 말 그대로 execute 될 코드 부분이다  

세가지로 구성된다!  


## message passing  

`aGame.displayCard (aCard, 42, 27); `  

displayCard 멤버를 호출한다, 이것이 곧 message(Request)  
aGame 은 message receiver 이다.    

## public에 data member 넣는 것들 피하라!  
왜?  
- 데이터 멤버 접근 통제가 더 정확해진다.    
    - 특정 멤버에 직접 접근이 안되고 그와 관련된 public 메소드만 호출하도록 한다.  
- functional abstraction  
    - 로직을 효과적으로 너흥ㄹ 수 있다. 예를 들어 readonly를 리턴하면서 *2 를 하고 싶으면 그냥 하면 된다.  


![image](https://user-images.githubusercontent.com/37579661/97939017-4ac3ad00-1dc6-11eb-9478-a623979a0b8c.png)

이 이미지에서 
public 이 interface, private 이 implementation이다.  
이 때 public 의 getReadOnly() 를 통해 private member인 readOnly에 접근을 하고 있다.  

## getter & setter  
- getter = accessor  
    - simply return internal data value
    - data를 read-only로 만들어줌
    - data field 가 접근가능하다는 것을 잘 알림  
    - 이후에 access behavior 를 바꾸는데 용이함을 제공함  
 
- setter = mutator   
    - 객체의 변수를 바꾸는데 쓰임  
    - mutator 는 위의 getter 보다는 덜 쓰인다. 

## assert function  
-  `assert(e)`  
    - 항상 참이어야한다. 그렇지 않다면 프로그램은 멈추고 에러메세지를 보낸다.  
    - 상황에 따라 변수별로 조건이 필요할 수 있다. (0보다 커야한다던지, 등) 이런 경우에 assert문을 활용한다.  


## 예시  

![image](https://user-images.githubusercontent.com/37579661/97945542-333af300-1dcb-11eb-8b20-11d297c8df2f.png)

위에서의 public, private은 **visibility modifier** 이다.  
만약 visilibity modifier 가 없으면, 디폴트는 **private**이다.  
private members of a class can be accessed only within that class's member function.  



## constructor  
- 멤버 변수 초기화에 쓰인다.  
`PlayingCard()`  
`PlayingCard(Suit is, int ir)`   
 
- return 은 없다!  

- 이름이 클래스랑 같다!  

![image](https://user-images.githubusercontent.com/37579661/97945959-6467f300-1dcc-11eb-9b36-9341a635e164.png)


## destructor 가 필요한 때  
- deallocation이 필요한 때  

## default constructor  
- 클래스에 어떤 constructor 도 만들지 않았다면, 컴파일러는 디폴트 constructor 를 생성하게 된다.  
eg. `TintStack::TIntStak() { }`  

## Copy Constructor  
- 기존에 존재하는 객체로부터 새로운 객체가 똑같은 타입으로 만들어질 때 호출되는 constructor 이다.  

- typical constructor  
`Person q("Mickey")`  
Mickey argument를 가지는 새로운 객체 q class type Person 이다.  

- Copy Constructor 3 경우  
1. `Person r(p)`  
- p객체를 새로운 객체 r에 카피한다.  

2. `Person p = q`  
- 위와 같다.  

3. `f(p)` 
- f는 function, p는 객체이다. 
- call-by-value  
```c++
void f(Person x){
    
} 
```
-> x 가 새로 만들어진 것이고, p 의 value가 x로 카피된다.   


## Copy Constructor 만들기  
`Person(const Person& p {      } `  

1. shallow copy/ deep copy 모두 같은 경우   
```c++
class Person{
    int x
    float y
}
```

2. deep / shallow copy 가 다른 경우    
deep : variable values are indirectly copied!   
shallow : directly copy!  

actual value pointer points to 
```c++
class Person{
    char * s;
}
```


![image](https://user-images.githubusercontent.com/37579661/97948485-10610c80-1dd4-11eb-92be-caadcc1d87dd.png)

shallow copy는 카피의 의미 + sharing 이다. 왜냐하면 카피한 원본이 값이 바뀌면 copy한 값도 바뀌기 때문!  
deep copy는 원본이 바뀌더라도 사본에 영향을 주지 않는다.  

## deafult copy constructor  
- shallow 카피만 해준다.  
- 컴파일러가 그냥 자동으로 디폴트 카피 생성자를 만들기 때문에 shallow 로 족하면 굳이 copy constructor 를 만들어줄 필요가 없다.  
- 뭔가 포인터가 가르키고 있는 곳은 copy 하려고 할 때에는 deep copy 가 필요하다. 

 ## 객체 생성  
 ```c++
 //1. static 하게 객체 만들기
 PlayingCard* aCard(diamond, 3);

//2. dynamic 하게 객체 만들기
 PlyaingCard* aCardPtr = new PlayingCard(diamond, 3);
 PlayingCard* CardsPtr = new PlayingCard[100];
 //dynamic memory allocation 

 delete aCardPtr;
 delete [] CardsPtr;

 ```

 - Memory Leak  
    - the condition where you cannot deallocate the dynamically allocated memory. 
    - eg. you allocate memory in a function and the funciton is returned without decllocating it. 

- Garbage Collection  
    - 정보가 더이상 쓰이지 않으면 프로그램 내에서 collect 되어지는 것.  
    - 그리고 아라서 deallocate 됨  


## static  
- all isntance share the same value!  
- One per class  
```c++
class Person{
    static int x;
    int y;
    int z; 

}

Person 01, 02, 03; 
```
이렇게 있으면, 
class 1,2,3 마다 int y, z 는 다 각각 다르게 있을 수 있는데, 
**x는 공통으로 존재한다** 

- 객체 상관없이 static은 쓰일 수 있다.  

![image](https://user-images.githubusercontent.com/37579661/97950388-0a6e2a00-1dda-11eb-8341-2bec155ab95b.png)


`static int open_files;`  
로 클래스 내부에서 선언한 후에, 이를 쓸 때에는 **class 외부**에서 `int File::open_files =0;` 이렇게 새로 선언을 한 후에 사용하여야 한다. 


## const mumber function  
```c++

int PlayingCard::rank () const
{ return rankValue; }

```

- 호출하는 data member를 수정하지 않는다.  
- read-only function 느낌!  
- 왜 사용할까?  
    - 값이 변경되지 않을 거라는 것을 보장해준다! ==safety, readability  


```c++

int PlayingCard::rank () //const를 쓰지 않더라도 영향은 없다. 그냥 safety를 느끼게 해줌!
{ return rankValue; }

```


## inline member function  
- compiler generates function body code into the place of each function call.  
- 원래는 f() 이런 function이 호출되면, void f() 까지 가서 그것을 돌리고 다시 돌아오는식인데, 아예 f() 이 있는 body code에 f() 내용을 바로 거기서 사용하는 것이다.  
- speed 가 좋아진다.  

- 언제 사용해야할까?  
    - 호출하는 function의 내용이 굉장히 짧을 때 (1,2 줄 정도)  
    - 엄청 많은 iteration이 있는 루프에서 호출될 때  

- 단점은 프로그램의 사이즈가 커진다는 것이다.  


- 사용법  
01. 
```c++
inline void f() {
}
````

02. 

```c++
class Person {
    ....

    void f() {
        ...
    }
    ....
}
```
이렇게 쓰이면 자동으로 `inline` 처리가 된다~  


## order of methods  
- 맨 첫번째로 나오는 메소드가 **중요한 메소드**이다.  

- constructor는 보통 가장 중요하기 때문에, 가장 먼저 list 해두는게 맞다.  

- public 이 먼저, 그 다음이 private.  


## separation of definition and implementation  

보통 쓰는 식?  
1. 헤더파일  
```c++
class PlayingCard {
    public: ... 
            Colors color ();
    
    ...

    int f(){

        ...
    }

    ...
}
```

2. PlayingCard.cpp  
```c++

//      return type / class name / member function name 
PlayingCard::Colors PlayingCard::color() {

    // return the face color of a playing card

    if((suit == Diamond) || (suit == Heart)){
        return Red;
    }

    return Black;
}
```

## friend  
 = private 개념을 나눌 수 있는 대상 을 의미함.  

 - friend 인 function 는 class의 private 멤버들을 접근할 수 있음  

 - friend class 는 그 클래스의 멤버 function들에게 private 멤버 접권권한을 주는 것이다.  

   
## & , *  

reference(참조) 는 물체에 대한 별명이(alias)다. 

예를 들어, A물체의 이름은 hong, kim 두개가 있다고 보자.  
이것이 바로 reference 이다.  


- call-by-reference, pass-by-reference 에서 쓰인다.  

- function에 argument 를 넘길 때 사용된다.  

eg. 
```c++
int y=7;
int& x = y;
x=4; //y=7이 된다. 
````


eg. 
```c++
double square(double &x) { 
    return x *= x;
}

int bar(void) {
    double foo = 10.0;
    square(foo); //x와 foo가 같은 object 를 가르키게 됨, foo = foo*foo
    cout << foo; //prints 100.0
}

```

- `double &x` 이런식으로 선언되어 쓰이는 & 는 참조자로 선언하겠다는 것이고,  

- 아래에서 처럼 c에서 중간에 `&foo`이렇게 쓰이면 'address-of'의 의미이다.  
- *x 에서의 `*` 는 value at 이다.  


--> rewritten in C  
```c
 double square(double *x){
     return *x *= *x;
 }

 int bar(void){
     double foo = 10.0;
     square(&foo);
     printf(%f, foo) 
 }

```


정리하자면...  
1) declaration  
    - *: pointer type
    eg. int* x; 

    - & : reference type
    eg. int& y=x;

2) non-declaration  
    - unary
        - * : value at the address of 
        - & : address- of 




## 쓰임에 따른 argument passing modes!  

```c++
//1. pass by value
void X::f(T arg)

//2. pass by value
void X::f(const T arg)

//3. pass by reference 
void X::f(T& arg)

//4. pass by reference 
void X::f(const T& arg)

//5. pass by pointer
void X::f(T* argp)

//6. pass by pointer
void X::f(const T* argp)

//7. pointer is constant
void X::f(T* const argp)

//8.
void X::f(const T* const argp)

```

만약 arg 가 큰 object 라면, call by value 보다는 call by reference (3,5)가 적절하다.  
단, call by reference 가 쓰이면, create parameter variable, copy 두개나 실행되어서 cost 가 크다. 


4,6 은 비슷하다. function 안에 있는 arg를 변경할 수는 없다.  
큰 object를 변경 없이 pass 하고 싶다~ 라는 정도의 의미이다.  


## 상속성  
1. private  
- 해당 클래스 에서만 접근가능하다.  
- parent class에 있는 private class는 그 child 에서는 접근불가하다.  

2. public  
- 어디서나 접근 가능  

3. protected  
- 해당 클래스 내부 + 그 클래스를 상속받은 child class에서는 접근 가능하다.  
- 즉, less encapsulation!  
- 정말 필요할 때만 쓰기! less encapsulation 자체가 좋은건 아니다!  

## constructor, destructor 의 순서 

![image](https://user-images.githubusercontent.com/37579661/97963352-4d3ffa00-1dfa-11eb-828e-0cdd34e92bd5.png)

1. Person() constructor  
- student 가 person 을 상속받기 때문에 먼저 호출된다.  

2. Address() constructor  
- constructor 는 initialize 를 해주는데, 따라서 Student constructor 전에 그 안에 있는 변수들을 모두 채워준 다음에 initialize 해야한다.  

3. Student() constructor  

**이 다음부터는 destructor 인데, 그 순서는 반대이다**  

4. ~Student()  
5. ~Address()  
6. ~Person()  


## dynamic binding  
- dynamic : runtime/execution time에서 일어나는 것을 의미함  
- binding : name(function)  과 actual code가 바인딩이 된다!  
    - 예를 들어, 
    ```c++
    main() {
        ...
        f();
    }
    
    ...

    f() {
        ...
    }
    ````
    이러한 코드가 있다면, 

