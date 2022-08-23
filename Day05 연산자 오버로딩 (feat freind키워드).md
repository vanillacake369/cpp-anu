# Day05 연산자 오버로딩 (feat. freind키워드, ostream)

# Contents

---

# ****입출력 클래스 istream, ostream****

- `istream` : **입력**을 수행하는 클래스
- `ostream` : **출력**을 수행하는 클래스
- `iostream`
    - #include <iostream>으로 우리에게 익숙한 그 클래스
    - `istream`과 `ostream`의 자식이다. 두 클래스를 상속 받음(다중 상속)
    - **입출력**과 관련된 모든 데이터와 기능을 담고 있다.
    - 맨 아래 예제를 보면 알 수 있다 싶이 `<<`삽입연산자 오버로딩을 하는 경우
    freind ostream을

---

# friend 클래스 & friend 함수

friend 클래스와 마찬가지로 private 및 protected 멤버에 접근할 수 있는 권한을 부여할 수 있습니다.

friend 기능을 클래스단위가 아닌 **멤버 함수 단위로 지정**해 주는것입니다.

아래 코드를 확인해보시죠.

```cpp
#include <iostream>
#include <string>
using namespace std;
 
class Friend1 {
private :
    string name;
    friend void set_name(Friend1&, string);
};
 
 
void set_name(Friend1& f, string s) {
    f.name = s;
    cout << f.name << "\n";
}
 
int main(void) {
    Friend1 f1;
 
    set_name(f1, "열코");
 
    return 0;
}

출처: https://yeolco.tistory.com/116 [열코의 프로그래밍 일기]
```

friend 키워드를 사용하여 set_name이라는 함수가 내 친구라는것을 컴파일러에게 알려주는 것입니다.

그래서 set_name 함수에서는 Friend1 클래스의 private 멤버인 name 변수에 접근이 가능한 것이죠.

생각보다 간단하고 쉬운 개념이죠?

- **주의사항**
- 친구의 친구는 friend 키워드로 명시하지 않은 경우 친구 관계가 형성되지 않습니다.
- 친구의 자식도 마찬가지로 friend 키워드로 명시하지 않은 경우 친구 관계가 형성되지 않습니다.

---

# delete 키워드 :: 포인터 삭제

delete 키워드는 아래 두 가지로 쓰이는데 여기서 우리는 첫 번째 목적으로 쓴다.

- 객체 생성(new) 이후 삭제(delete)
- 컴파일러 기본 생성해주는 것을 삭제(delete)
→ 이건 [여기를](https://woo-dev.tistory.com/100#:~:text=delete%20%ED%82%A4%EC%9B%8C%EB%93%9C%EB%8A%94%20%EC%BB%B4%ED%8C%8C%EC%9D%BC%EB%9F%AC%EA%B0%80,%ED%8A%B8%EB%A6%AD%EC%9D%84%20%EC%82%AC%EC%9A%A9%ED%95%A0%20%EC%88%98%20%EC%9E%88%EB%8B%A4.) 참고해보자

객체이든 변수이든 할당받았던 메모리 공간을 해제하기 위해서는 **delete**키워드를 사용한다.

아래 예제를 참조해보자.

```cpp
int *ptr_i; 
ptr_i = new int; 
delete ptr_i;
```

---

# 연산자 오버로딩

연산자를 오버로딩 하는 방법에는 두 가지 방법이 있다.

- 멤버함수
- 일반함수 (= 프렌드함수)

## 멤버함수로 연산자 오버로딩

```cpp
Complex{
	private :
		int real;
		int image;
	public :
		Complex operator+(Complex rightHand);
		Complex operator-(const Complex &rightHand) const; //const function <- (param : const) 
};

Complex Complex::operator+(Complex rightHand){
	Complex res;
	res.real = this->real+rightHand.real;
	return res;
}
Complex Complex::operator-(const Complex &rightHand) const{
	Complex res;
	res.real = this->real - rightHand.real;
	return res;
}
```

## 일반함수(freind함수)로 연산자 오버로딩

```cpp
Complex{
	private :
		int real;
		int image;
	public :
		friend Complex operator+ (Complex& c1, Complex& c2);
};
 
Complex operator+ (Complex& c1, Complex& c2) {
    return Complex(c1.x + c2.x, c1.y + c2.y);
}
```

# 출력을 담당하는 연산자 오버로딩

이를 하기 위해서는 출력연산자`<<`에 대해 알아보아야한다. 

ostream 클래스를 살펴보면 출력을 위한 다양한 멤버함수와 연산자 함수가 정의되어 있다. 아래 출력을 담당하는 연산자`<<`를 살펴보면 기본 자료형인 char,int,long 등에 대한 출력을 할 수 있도록 오버로딩 되어있는 것을 알 수 있다.

```cpp
arithmetic types (1)	
ostream& operator<< (bool val);
ostream& operator<< (short val);
ostream& operator<< (unsigned short val);
ostream& operator<< (int val);
ostream& operator<< (unsigned int val);
ostream& operator<< (long val);
ostream& operator<< (unsigned long val);
ostream& operator<< (float val);
ostream& operator<< (double val);
ostream& operator<< (long double val);
ostream& operator<< (void* val);
stream buffers (2)	
ostream& operator<< (streambuf* sb );
manipulators (3)	
ostream& operator<< (ostream& (*pf)(ostream&));
ostream& operator<< (ios& (*pf)(ios&));
ostream& operator<< (ios_base& (*pf)(ios_base&));
```

비트시프트 연산자를 C++에서 출력연산자로 오버로딩해놓은 것이다.

## 멤버함수로 구현할 경우

cout이 연산자 함수를 호출해주는 객체이므로 이 객체를 생성하는 클래스 ostream에 <<연산자를 오버로딩해야한다. 

기존 `cout << x`를 `cout.operator<<(x)`의 형태로 구현해야한다는 것이다

이는 C++에서 제공하는 ostream을 개발자가 함부로 바꾸는 것이므로 바람직하지 않다.

***그렇다면 x에 오버로딩하면 안 되는 것인가?***

***그렇게 하게 되는 경우 Syntax가 어긋나게 된다.***

`x.operator(cout)` 혹은 `x<<cout;`는 코딩을 모르는 사람이 봐도 연산순서와 호출순서가 다르지 않은가. 

따라서 ostream의 cout를 통한 <<연산자를 오버로딩하기 위해서는 일반함수(freind함수)를 통해 오버로딩해줄 수 밖에 없다.

## 일반함수(freind함수)로 구현할 경우

일반 함수로 operator<<() 연산자 함수를 오버로딩하려면 <<연산자 자체가 이항연산자이기 때문ㅇ네 피연산자가 두 개 있어야 한다.

기존 cout<<x를 `operator<<(cout,x);`로 구현해야한다는 것이다.

이에 따라 다음과 같이 구현된다.

```cpp
class Complex{
...
public :
	freind ostream& operator<<(ostream &os,const Complex &comObj);
};
```

- `freind`
    
    : 외부 `ostream`의 `<<`연산자함수를 오버로딩하는 것이므로 `freind`키워드를 통해 `Complex`멤버에 대한 접근제한을 푼다.
    
- `ostream&` (반환값) :
    
    : `cout` 객체에 `<<`연산자를 연속적으로 기술하여 여러 개의 자료를 출력할 수 있도록 하기 위함
    
- `operator<<` (함수명)
    
    : `<<`연산을 오버로딩함을 지시함
    
- `ostream &os` (첫번째 param)
    
    : 클래스 ostream은 프로그래머가 임의로 객체생성을 할 수 없기 때문에 반드시 ostream &os와 같이 레퍼런스 변수 형태로 선언해야한다. 레퍼런스 변수인 os는 따로 메모리를 할당하는 것이 아니라 이미 존재하는 cout 객체를 참조만 하므로 프로그래머에 의해서 객체 생성하지 못 하는 ostream 객체 cout을 매개변수로 전달받을 수 있다.
    
- `const Complex&`
    
    : Complex 객체의 주소를 받는다. (C나 C++이나 call by value를 기본적 원칙으로 함으로, 주소를 매개변수로 받아 call by reference 효과를 내게한다)
    [** const에 대해 기록해둔 것이 있으니 헷갈린다면 여기를 참조해보자](Why%20use%20%E2%80%9Cconst(%20)&%20rather%20than%20%E2%80%9C(%20)&%E2%80%9D%207dde46ba5d8f4b648fcd71c1976b122f.md).
    

---

# 위 개념 총 집합 Example Code

```cpp
#include <iostream>
#include <string>
using namespace std;
class CPnt
{
    int x, y;

public:
    CPnt(int a, int b) : x(a), y(b) {}
    friend ostream& operator<<(ostream &me, CPnt p)
    {
        me << p.x << " " << p.y;
    }
};

int main()
{
    CPnt *p = new CPnt(2, 3);
    // CPnt k(2, 3);
    cout << *p;
    delete p;
    return 0;
}
```

## 코드 분석

```cpp
friend ostream& operator<<(ostream &me, CPnt p)
{
    me << p.x << " " << p.y;
}
```

ostream의 멤버삼수인 operator<<(

---

# Reference

- **쉽게 배우는 C++프로그래밍 Ch10 연산자 오버로딩**
- ****chapter 9. 연산자 오버로딩 : 입출력 연산자 오버로딩****

[https://ansohxxn.github.io/cpp/chapter9-3/](https://ansohxxn.github.io/cpp/chapter9-3/)

- **C++ friend 클래스와 함수**

[https://yeolco.tistory.com/116](https://yeolco.tistory.com/116)

- **C++ 동적 메모리 할당 (new, delete 키워드)**

[https://swstar.tistory.com/222#gref](https://swstar.tistory.com/222#gref)

- **std::ostream::operator<<**

[https://www.cplusplus.com/reference/ostream/ostream/operator<</](https://www.cplusplus.com/reference/ostream/ostream/operator%3C%3C/)