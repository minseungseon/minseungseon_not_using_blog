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


![image](https://user-images.githubusercontent.com/37579661/ 97948485-10610c80-1dd4-11eb-92be-caadcc1d87dd.png)

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

    void f() {
        ...
    }
    ````
    이러한 코드가 있다면, 우리는 main 에서의 f()가 아래의 f() 코드임을 안다. 이게 바로 binding!  




## virtual function   
virtual function은 상속받는 'child class'안에서 정의되어지게 된다! 그리고 그 child class 는 부모와 같은 signature(argument type) 를 가진 것이어야 한다.  

1. without virtual  
virtual 이 없는 경우에는, 포인터의 클래스 타입에 의존하여 멤버를 호출한다.  

2. with virtual  
virtual 로 하는 경우에는, 실제 객체에 의존하게 된다.  

```c++
#include <iostream>

//parent class Animal! 
class Animal {
    public:
    virtual void eat() //eat() 이라는 function이 child class 에서 다시 정의될 것이라는 것을 알려줌. 
    {
        std::cout << "I eat like a generic Animal.\n";
    }
};

//inheritance -> public Animal 이렇게 써준다. 
class Wolf : public Animal {
    public:
    void eat() { std::cout << "I eat like a wolf!\n"; }
};

class Fish : public Animal {
    public:
    void eat() { std::cout << "I eat like a fish!\n"; }
};

class OtherAnimal : public Animal {
};

int main()
{
    Animal *anAnimal[4];
    //각각은 Animal 포인터 타입으로 배열에 4개가 존재한다.


    // dynamic binding
    // 아래는 모두 Animal 포인터 타입이기 때문에, 보통 Animal 객체를 가르키게 되어있다. 하지만 actual obejct는 여기에서 child type 이다! 
    anAnimal[0] = new Animal();
    anAnimal[1] = new Wolf();
    anAnimal[2] = new Fish();
    anAnimal[3] = new OtherAnimal();

    for(int i = 0; i < 4; i++) anAnimal[i]->eat();
    //virtual은 이 function이 child class 에서 다시 정의될 것임을 알려주는 것이다.  
    //이렇게 eat이 불리더라도 actual obejct의 eat()이 불리게 됨. 
    // i=0: Animal eat
    // i=1: Wolf eat --> dynamic binding 
    // i=2: Fish eat --> dynamic binding 
    // i=3: Animal eat 

    return 0;
} 
```

이러한 코드에 

```c++
cin >> i;
anAnimal[i]->eat();
```
이렇게 i의 값을 런타임에서 결정되도록 하면,  
어떻게 될까?  

이 상태로는 알 수가 없다.  
컴파일 타임에서는 알 수가 없고, execution에서만 알 수 있다.  
따라서 i의 implementation은 runtime에서만 결정된다.  
그래서 이를 'dynamic binding' 이라고 말한다!  

## abstract class  
- 최소 하나의 **pure virtual function** 을 지니는 클래스를 추상 클래스라고 부른다!  
- implementation이 따로 없는, 오직 **interface**로서 제공한다.  
- pure virtual function은 **=0** 으로 선언된다! 그리고 항상 derived class에서 정의된다..!! 즉, 그 자체만으로는 사용되지 않고 inherited 되어서 사용되기 위해 존재한다~~  

- 예:  

```c++ 
class A {
    public: virtual void f() = 0; // = pure virtual function 
}
```

- 이러한 abstract class 는 그 자체로 사용이 안되기 때문에  

```c++

A x; 

```

이렇게는 쓰일 수 없다!  

```c++

A* x; //가능  

```

![image](https://user-images.githubusercontent.com/37579661/98824110-3e022180-2476-11eb-8bed-aa0784985748.png)


## polymorphism 의 네가지 요소!  

1. overloading  
이름은 같고, parameter타입은 다른 것!  

2. overriding  
이름도 같고, parameter도 같은 것  

```c++
#include <iostream.h> using namespace std;
void Func( int one, int two=2, int three=3);
// 이런식으로 디폴트 값까지 설정할 수 있다!  
// one, two 만 주어지면 three 의 값은 3 으로 자동으로 넣어진다. 

void Func( float fv );
main () {
    Func(10, 20, 30);
    Func(10, 20); // Let the last parm default Func(10); // Just provide the required parm. Func(1.5f);
}
void Func( int one, int two, int three)
{
    cout << "One = " << one << endl;
    cout << "Two = " << two << endl;
    cout << "Three = " << three << endl << endl;
}
void Func ( float fv)
{
    cout << fv << endl;
}

```

## Generics  
- 몇개의 key type이 정해져있지 않게 두는 것이다.  
- Template 과 같은 개념이다!  

## Template  

1. function template  
```c++
template<typename T>
T max(const T& a, const T& b)
{
    return (a > b) ? a : b;

}


cout << max(4, 5.5) //불가
cout << max<double> (4.5, 5) //타입을 명시해주었으니 가능하다.

```

2. 한개 이상의 argument 를 가진 템플릿  

```c++
template<typename T1, typename T2>
void print_max(const T1& a, const T2& b)
{
    cout<< ((a > b) ? a : b) << endl;
}
void f()
{
    print_max(4, 5.5);// Prints 5.5
    print_max(5.5, 4);// Prints 5.5
} 

```

3. class templates  
```c++
template<typename T> //T를 사용하기 위해 이렇게 써준다. 
class thing {
    public:
        thing(T data);
        ~thing() { delete x; }
        T get_data() { return *x; }
        T set_data(T data);
    private:
        T* x;
};

template<typename T>
thing<T>:: thing(T data)
{
    x = new T; *x = data;
}
template<typename T>
T thing<T>::set_data(T data)
{
    *x = data;
} 


#include <iostream>
#include <string>
using namespace std;
main()
{
    thing<int> i_thing(5); // int type 
    thing<string> s_thing(“COMP151”); //string type

    cout<< i_thing.get_data()<< endl;
    cout<< s_thing.get_data()<< endl;
    i_thing.set_data(10);
    s_thing.set_data(''CPEG'');
    cout<< i_thing.get_data()<< endl;
    cout<< s_thing.get_data()<< endl;
} 


```


- 템플릿은 class 에도 잘 쓰인다.  
- 특히나 container classes 를 정의하는데 굉장히 유용하다.  
ex. stack, queue, list...  


## class template 예시 : List_Node!  

1. 한 노드에 해당하는 코드!  
한 노드는 보통 세가지 정보가 필요하다.  
1. data itself  
2. pointer to next node  
3. pointer to previous node  


```c++
template<typename T> //T 사용하기 위해 써주기 
class List_Node{
public:
    List_Node(const T& data);
    List_Node<T>* next();
     
// Other member functions
private:
    List_Node<T>* next_m;
    List_Node<T>* prev_m;
    T data_m;

    friend class List<T>; 
    //List is a friend of List Node! 
    //즉, List 는 List_Node의 private member를 접근할 수 있다는 명시이다. 
};

template<typename T>
List_Node<T>::List_Node(const T& data)
: data_m(data), next_m(0), prev_m(0) { } 
//데이터는 data 로 initialize 해주고, 그 이후 포인터와 그 전 포인터는 null 로 만들어준다. 


template<typename T>
List_Node<T>* List_Node<T>::next()
{ return next_m; } 

```

2. 전체 리스트에 해당하는 코드!  
- head와, tail 이 필요하다.  
- information of head, tail 이 필요한 것이다~  

```c++
template<typename T>
class List {
public:
    List();
    void append(const T& item);
// Other member functions
private:
    List_Node<T>* head_m;
    List_Node<T>* tail_m;
};
template<typename T>
List<T>::List():head_m(0),tail_m(0)
{}

template<typename T>
void List<T>::append(const T& item)
{
List_Node<T>* new_node
= new List_Node<T>(item);
if (! tail_m) {
head_m= tail_m= new_node;
} else {
// ...
}
}



```

```c++
template<typename T>
Stack<T>::Stack(int n)
{
    stackPtr = new T[n];
    size = n;
    top =0;

}

template<typename T>
Stack<T>::~Stack()
{
    if(stackPtr) delete[] StackPtr;

}

template<typename T>
bool Stack<T>::push(const T& x)
{
    if(isFull()) return false;
    stackPtr[top++] = x;
    return true
}

template<typename T>
bool Stack<T>::pop(T& x)
{
    if(isEmpty()) return false;
    x = stackPtr[--top];
    return true;
}

template<typename T>
bool Stack<T>::isEmpty()
{
    if(top == 0) return true;
    return false;
}

template<typename T>
bool Stack<T>::isFull()
{
    if(top == size) return true;
    return false;
}


```
## STL  
: Standard Template Library  

3개 카테고리가 있다.  
1. container class  
: a holder object that stores a collection of other objects with any (user defined or built-in) data types.  

2. iterator  
container 의 요소를 하나하나 접근 할 때 쓰인다.  
pointer! 개념이 들어간다.  


3. algorithm  


## 01 container classes  
1. sequences  
- vector, list, deque(double ended queue) 가 sequences 이다.  
2. associative container:  
- set  
- map : balanced BST 에 저장된다.  
- hash_map : hash 에 저장된다. 
    -> 트리, 그냥 map 는 서치에 시간이 조금 걸린다. 하지만 hash는 데이터에 직접적으로 접근이 가능해서 더 빠르다.  
    -> 순서가 없다. map은 순서가 있다.  

3. container adapters  
- implemented on top of another container  
- stack, queue, priority queue 

### sequence containers  
Element access for all:  
`front()`  
`back()` 
  
Element access for vector and deque:  
`[ ]`: Subscript operator, index not checked  


Add/remove elements for all  
`push_back()`: Append element.  
`pop_back()`: Remove last element  

Add/remove elements for list and deque:  
`push_front()`: Insert element at the front.  
`pop_front()`: Remove first element.  

Miscellaneous operations for all:  
`size()`: Returns the number of elements.  
`empty()`: Returns true if the sequence is empty.  
`resize(int i)`: Change size of the sequence.   

- 선언 
`vector<data type> variable_name;`  
Ex) `vector<int> vec_int;`  

- 활용

```c++
// four ints (size=4) with value 100
// second 는 100, 100, 100, 100 을 가지게 된다. 
vector<int> second (4,100); 

//second 의 처음~끝을 copy 한다.
vector<int> third (second.begin(),second.end());


//third를 그대로 카피한다. 
vector<int> fourth (third);

//myint 리스트 배열을 fith에 카피한다. 
int myints[] = {16,2,77,29};
vector<int> fifth (myints, myints + sizeof(myints) / sizeof(int) ); //sizeof(myints) / sizeof(int) = 4

```

## 02 iterators  
- 각각의 요소를 "traverse", 즉 하나하나를 방문하게 해준다.  
- 포인터처럼 쓰인다.  

```c++
// vector::begin
#include <iostream>
#include <vector>
using namespace std;
int main ()
{
    vector<int> myvector;
    for (int i=1; i<=5; i++) myvector.push_back(i);
    vector<int>::iterator it;

    cout << "myvector contains:";
    for ( it=myvector.begin() ; it < myvector.end(); it++ )
    cout << " " << *it; //순차적으로 vector 에 있는 원소들을 프린트한다. 
    cout << endl;
    return 0;
}
```

- `begin()` , `end()`  
`begin()` 은 맨 앞 요소를 가르키지만, `end()` 는 맨 마지막 요소 다음 null 을 가르킨다.  


## vector example  
```c++
// erasing from vector
#include <iostream>
#include <vector>
using namespace std;
int main ()
{
    unsigned int i;
    vector<unsigned int> myvector;
    // set some values (from 1 to 10)
    for (i=1; i<=10; i++) myvector.push_back(i);

    // erase the 6th element
    // begin을 기준으로 5를 더한 차례의 요소를 지운다. = 6번째 요소
    myvector.erase (myvector.begin()+5);

    // erase the first 3 elements:
    myvector.erase (myvector.begin(),myvector.begin()+3);
    cout << "myvector contains:";
    for (i=0; i<myvector.size(); i++)
    cout << " " << myvector[i];
    cout << endl;
    return 0;
}
```

## stack example  
stack 도 쓸 수 있다~  
```c++
// stack::push/pop
#include <iostream>
#include <stack>
using namespace std;
int main ()
{
    stack<int> mystack;

    //0~5 를 push 한다!
    for (int i=0; i<5; ++i) mystack.push(i);

    cout << "Popping out elements...";
    while (!mystack.empty())
    {
    // top 출력하고
    cout << " " << mystack.top();
    // 팝 하고 
    mystack.pop();
    }
    cout << endl;
    return 0;
}
```

## vector 파라미터로 넘기기  
그냥 vector 자체를 넘기게 되면 그 속의 '모든 값' 이 call by value 가 되어서 효율이 나빠질 수 있다.  
이럴 때에는 `&` 를 활용하여 call by reference 로, 값 자체를 넘기는 것이 아니라 그 값에 접근할 수 있는 'reference'를 넘기는 것이 바람직 하다!  

```c++
// vector/vector-average.cpp - Averages numbers in vector
// Fred Swartz - 2003-11-20

#include <vector>
#include <iostream>
using namespace std;

float sum(const vector<float>& x); // prototype

//====================================================== main
int main() {
    vector<float> a;   // Declare a vector.

    float temp;
    while (cin >> temp) {
        a.push_back(temp);
    }
    
    cout << "Average = " << sum(a)/a.size() << endl;
    
    return 0;
}


//======================================================= sum
// sum adds the values of the vector it is passed.

//파라미터로 넘기면서 & 를 사용한다!
float sum(const vector<float>& x) {
    float total = 0.0;  // the sum is accumulated here
    for (int i=0; i<x.size(); i++) {
        total = total + x[i];  
    }
    return total;
}


```