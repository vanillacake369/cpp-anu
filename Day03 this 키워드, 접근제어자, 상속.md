# Day03 this 키워드, 접근제어자, 상속

# Contents

# Const

## const vs static

A `const` is a promise that you will not try to modify the value once set.

A `static` variable means that the object's lifetime is the entire execution of the program and it's value is initialized only once before the program startup. All statics are initialized if you do not explicitly set a value to them.

- `const &` ??
    
    Even though the `const` is keeping you from changing the value of your parameter, it's better to send a reference to it, rather than send it by value, because, in large objects, sending it by value would require copying it first, which is not necessary when calling by reference
    
    큰 객체를 넘기는 경우에는 call by value 로 인해 모든 값을 복사해야하기 때문에 ( +a로 shallow copy 이슈로 인해 ) 
    &로 참조값을 받고 const를 통해 값의 수정없음을 확정하여 전달 받거나 하도록 하는 것이다.
    

# Example Code :: 연산자 오버로딩

### 클래스 중심

외부로부터 객체 하나를 받아 

자기자신의 멤버변수와 외부객체의 멤버변수를 더하여

새로운 객체를 생성한 뒤 반환

```cpp
#include <iostream>
using namespace std;

class CVec {
    int x, y;

public:
    CVec () {};
    CVec (int a, int b) : x(a), y(b) {}
    CVec operator + (const CVec&);
    void pr(const CVec& v){
       cout << v.x << ',' << v.y << '\n';
    }
};

CVec CVec::operator+ (const CVec& p) {
    CVec t;
    t.x = x + p.x;
    t.y = y + p.y;
    return t;
}

int main () {
  CVec v1 (1,1);
  CVec v2 (2,2);
  CVec v3;
  v3 = v1 + v2;
  v3.pr(v3);
  return 0;
}
```

### 함수 기반

외부로부터 객체 두개를 받아 

객체1의 멤버변수와 객체2의 멤버변수를 더하여

새로운 객체를 생성한 뒤 반환

```cpp
#include <iostream>
using namespace std;

class CVec {
  public:
    int x,y;
  public:
    CVec () {};
    CVec (int a,int b) : x(a), y(b) {}
    void pr(const CVec& v){
     cout << v.x << ',' << v.y << '\n';
		}
};

CVec operator+ (const CVec& l, const CVec& r ) {
  CVec t;
  t.x = l.x + r.x;
  t.y = l.y + r.y;
  return(t);
}

int main () {
  CVec v1 (1,1);
  CVec v2 (2,2);
  CVec v3;
  v3 = v1 + v2;
  v3.pr(v3);
  return 0;
}
```

---

# this pointer

<aside>
📖 자바에서의 this와 완전 다를 게 없는 것 같다.
this를 통해 현 scope에서의 클래스, 즉 자기 자신을 참조하는 것 같다!!

</aside>

## 정의

In C++ programming, **this** is a keyword that refers to the current instance of the class. There can be 3 main usage of this keyword in C++.

- It can be used **to pass current object as a parameter to another method.**
- It can be used **to refer current class instance variable.**
- It can be used **to declare indexers.**

## Example Code

```cpp
#include <iostream>  
using namespace std;  
class Employee {  
   public:  
       int id; //data member (also instance variable)      
       string name; //data member(also instance variable)  
       float salary;  
       Employee(int id, string name, float salary)    
        {    
            this->id = id;    
            this->name = name;    
            this->salary = salary;   
        }    
       void display()    
        {    
            cout<<id<<"  "<<name<<"  "<<salary<<endl;    
        }    
};  
int main(void) {  
    Employee e1 =Employee(101, "Sonoo", 890000); //creating an object of Employee   
    Employee e2=Employee(102, "Nakul", 59000); //creating an object of Employee  
    e1.display();    
    e2.display();    
    return 0;  
}
```

---

# Access Modifier 접근제어자

C++에서는 명시해주지 않으면 default 접근권한은 private이다.

따라서 생성자이든 메서드이든 외부에서 호출하려면 public인 메서드 혹은 생성자를 호출해야만 한다.

---

# Reference

- **[Why put const (...)& in C++](https://stackoverflow.com/questions/44795308/why-put-const-in-c)**

[https://stackoverflow.com/questions/44795308/why-put-const-in-c](https://stackoverflow.com/questions/44795308/why-put-const-in-c)

- **[What is the difference between a static and const variable?](https://stackoverflow.com/questions/2216239/what-is-the-difference-between-a-static-and-const-variable)**

[https://stackoverflow.com/questions/2216239/what-is-the-difference-between-a-static-and-const-variable#:~:text=A const is a promise,set a value to them](https://stackoverflow.com/questions/2216239/what-is-the-difference-between-a-static-and-const-variable#:~:text=A%20const%20is%20a%20promise,set%20a%20value%20to%20them).

- **C++ this Pointer**

[https://www.javatpoint.com/cpp-this-pointer#:~:text=In C%2B%2B programming%2C this is,refer current class instance variable](https://www.javatpoint.com/cpp-this-pointer#:~:text=In%20C%2B%2B%20programming%2C%20this%20is,refer%20current%20class%20instance%20variable).