# Day01 C++ Intro

# Contents

---

# IDE

- Dev C++
- VS Code

VS Code 설정은 구글링 2,30분만 열심히 하면 되니까..화이팅..

( C++컴파일러 설치 → VSCode 연결 → VSCode Compile Path 연결설정 등등... )

# iostream, std

iostream(C++) → stdio.h(C)

- What is std
    
    "std" a namespace. The "::" operator is the "scope" operator. It tells the compiler which class/namespace to look in for an identifier.
    
    So `std::cout` tells the compiler that you want the *"cout" identifier, and that it is in the "std" namespace.* 
    
    If you just said `cout` then it will only look in the global namespace. 
    
    Since cout isn't defined in the global namespace, it won't be able to find it, and it will give you an error.
    
    `usingnamespace std;` tell the compiler "take everything that's in the std namespace and dump it in the global namespace". This allows you to use `cout` without the std:: prefix, but it increases the probability for name conflicts, since a bunch of extra names that you didn't expect also got added to the global namespace, and that might butt heads with some of your own names.
    

---

# Class 구조

## Constructor

생성자

- 클래스의 객체 생성 시에 private 멤버를 자동으로 초기화한다.
- 생성자의 이름은 클래스의 이름과 같아야 한다.
- 반환( return)형이 선언되어 있지 않고 실제로도 반환하지 않는다.
- 객체 생성시에 딱 한번 호출된다.
- 생성자도 일종의 함수이므로 오버로딩이 가능하다. (즉, 객체 생성을 다양하게 할 수 있다.)
- 생성자도 디폴트값을 설정할 수 있다.

```cpp
class SimpleClass
{
private:
    int num1;
    int num2;
public:
    SimpleClass()  // 생성자 1
    {
        num1 = 0;
        num2 = 0;
    }
    SimpleClass(int n)  // 생성자 2
    {
        num1 = n;
        num2 = 0;
    }
    SimpleClass(int n1, int n2)  // 생성자 3
    {
        num1 = n1;
        num2 = n2;
    }

    void Show() const
    {
        cout << num1 << ' ' << num2 << endl;
    }

};
```

### 클래스 내부에서 정의

```cpp
#include<iostream>
using namespace std;

class CRect{ // class
	int wid, hig;

public:
	CRect();
	CRect(){ wid = 4; hig = 5;}
};
int main(){
	CRect r1; // object
	cout << r1.Area();
}
```

### 클래스 외부에서 정의

```cpp
#include<iostream>
using namespace std;

class CRect{ // class
	int wid, hig;

public:
	CRect();
};
CRect::CRect(){ wid = 4; hig = 5;}
int main(){
	CRect r1; // object
	cout << r1.Area();
}
```

### Member Initializer

매개변수가 있는 생성자와 기본 생성자를 동시지원하기 위해 오버로딩을 사용한다.

```cpp
#include<iostream>using namespace std;
class CRect{ // class
  int wid, hig;
  public:
  CRect();
  CRect(int x, int y){
  	wid = x; hig = y;
  }
  int Area(); // prototype
};
CRect::CRect(){ wid = 4; hig = 5;}
int CRect::Area(){ return wid * hig;}

int main(){
  CRect r1; // object
  CRect r2(2,3);
  cout << r2.Area();
}
```

하지만 위 코드는 생성자를 주렁주렁 달게 되어 가독성이 떨어진다. (코드의 가독성은 리팩토링 및 디버깅에 굉장히 영향이 크므로 중요하다. 괜히 언어설계자가 추가로 다음과 같은 기능을 만드는 것이 아니다.)

이러한 난잡한 생성자코드들을 피하고자 멤버 이니셜라이저라는 기능을 추가했다.

```cpp
//member initializer
CRect(int x, int y):wid(x),hig(y){}
```

`CRect(int x,iny y)`를 통해 생성자의 시그니쳐를 만들어 준 뒤, `wid(x),hig(y){}`를 통해 **`CRect`클래스의 멤버 `wid,hig`를 x,y매개변수로 초기화한다.**

### Example Code

```cpp
#include<iostream>using namespace std;
class CRect{ // class
	int wid, hig;
	public:
		CRect();
		CRect(int x, int y):wid(x),hig(y){}
		int Area(); // prototype
};

CRect::CRect(){ wid = 4; hig = 5;}
int CRect::Area(){ return wid * hig;}

int main(){
	CRect r1; // object
	CRect r2(2,3);
	int a, b;
	cout << "Enter (a b):";
	cin >> a >> b;
	CRect r3(a,b);
	cout << r3.Area();
}
```

---

## 메소드

### Method냐 Function이냐

***Methods are functions that belongs to the class***.

There are two ways to define functions that belongs to a class: 

- Inside class definition.
- Outside class definition.

### 클래스 내부에서 정의

```cpp
#include<iostream>
using namespace std;

class CRect{ // class
	int wid, hig;

public:
	int Area(){ return wid * hig;}
};
int main(){
	CRect r1; // object
	cout << r1.Area();
}
```

### 클래스 외부에서 정의

```cpp
#include<iostream>
using namespace std;

class CRect{ // class
	int wid, hig;

public:
	int Area(); // prototype
};
int CRect::Area(){ return wid * hig;}
int main(){
	CRect r1; // object
	cout << r1.Area();
}
```

### Example Code :: 삼각형,사각형,원 면적 구하기

```cpp
class CRect{
  int w, h;
  public:
		CRect(int x,int y):w(x),h(y){}
    int Area() { return w*h; } // inline function 클래스속에서 구현한 함수, 속도가 빠름
};

class CCir {
  double r;
  public:
    CCir(double x):r(x){}
    double area() {return r*r*3.14;}
};

int main () {
	CRect r(4,5);
  cout << "(4,5) Area is: " << r.Area();

  CCir a (1.0); // functional form, 함수 형태
  cout << "Area: " << a.area() << '\n';
  return 0;
}
```

---

# Reference

- 생성자와 소멸자 그리고 멤버 이니셜라이저
[https://musket-ade.tistory.com/28](https://musket-ade.tistory.com/28)
- Class Methods
    
    [https://www.w3schools.com/cpp/cpp_class_methods.asp#:~:text=Methods are functions that belongs,Outside class definition](https://www.w3schools.com/cpp/cpp_class_methods.asp#:~:text=Methods%20are%20functions%20that%20belongs,Outside%20class%20definition)
    
- 생성자와 소멸자
[https://wikidocs.net/17145](https://wikidocs.net/17145)