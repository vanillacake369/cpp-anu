# Day02 Overloading, Template

# Contents

---

# Template Function

```cpp
#include <iostream>
using namespace std;

template <class T>
T sum (T a,T b)
{
	return a+b;
}

int main()
{
	cout << sum(3,6) << endl;
	cout << sum(3.1515, 43.3) << endl;
	return 0;
}
```

```cpp
template <typename T>
T func(T num)
{
	...
}
```

<aside>
💡 ***Template이란??***
: “함수나 클래스를 개별적으로 다시 작성하지 않아도, 여러 자료 형으로 사용할 수 있도록 하게 만들어 놓은 틀”

</aside>

자바에서의 템플릿과 동일하다...ㅎ

- 클래스 내부에 함수 선언 시 기본 접근 제한자는 private
    
    위와 같이 함수를 독립적으로 선언 및 정의 시에는 해당 함수를 main에서 접근할 수 있다. 
    
    그러나 아래처럼 클래스 내부에서 선언하게 되면 다음 규칙에 의해 접근할 수가 없다.
    
    > A whole lot of C code exists, including libraries that were desired to work with C++ as well, that use structs. Classes were introduced in C++, and to conform with the OO philosophy of encapsulation, **their members are private by default.
    -** [https://stackoverflow.com/questions/1247745/default-visibility-of-c-class-struct-members](https://stackoverflow.com/questions/1247745/default-visibility-of-c-class-struct-members)
    > 
    
    ```cpp
    #include <iostream>
    using namespace std;
    
    class Clas{
    	template<class T>
    	T sum(T a,T b){
    		return a+b;
    	}
    };
    
    int main(){
    	Clas c;
    	cout <<c.sum(3,6) << endl;
    }
    // [Error] 'T Clas::sum(T, T) [with T = int]' is private
    ```
    
    이와 같은 경우를 위해 C++에서는 private으로 막아놓은 변수들을 다른 클래스가 접근할 수 있게끔 하는 freind 키워드를 제공한다.
    
    ( freind키워드에 대해서는 [여기를 참고](https://yeolco.tistory.com/116)해보자 )
    
- `template<typename T>` vs `template<class T> ??`
    
    `typename` and `class` are interchangeable in the basic case of specifying a template:
    
    ```cpp
    template<class T>
    class Foo
    {
    };
    
    ```
    
    and
    
    ```cpp
    template<typename T>
    class Foo
    {
    };
    
    ```
    
    are equivalent. (이렇게만 알아두자..ㅎ)
    
    - ***BUT! there’s something more.***
        
        Having said that, there are specific cases where there is a difference between `typename` and `class`.
        
        The first one is in the case of dependent types. `typename` is used to declare when you are referencing a nested type that depends on another template parameter, such as the `typedef` in this example:
        
        ```
        template<typename param_t>
        class Foo
        {
            typedef typename param_t::baz sub_t;
        };
        
        ```
        
        The second one you actually show in your question, though you might not realize it:
        
        ```
        template < template < typename, typename > class Container, typename Type >
        
        ```
        
        When specifying a **template template**, the `class` keyword MUST be used as above -- it is **not** interchangeable with `typename` in this case *(note: since C++17 both keywords are allowed in this case)*.
        
        You also must use `class` when explicitly instantiating a template:
        
        ```
        template class Foo<int>;
        
        ```
        
        I'm sure that there are other cases that I've missed, but the bottom line is: these two keywords are not equivalent, and these are some common cases where you need to use one or the other.
        

## Example Code : sum

```cpp
#include <iostream>
using namespace std;

template <class T>
T sum(T a, T b)
{
    T result;
    result = a + b;
    return result;
}

int main()
{
    int i = 5, j = 6, k;
    double f = 2.0, g = 0.5, h;

    k = sum<int>(i, j);
    h = sum<double>(f, g);

    cout << k << '\n';
    cout << h << '\n';

    return 0;
}
```

---

# Overloading

```cpp
#include <iostream>
#include <string>
using namespace std;

void op()
{
    cout << "hello"
         << "\n";
}
int op(int a, int b)
{
    return a + b;
}
double op(double x, double y)
{
    return x - y;
}
int op(int a)
{
    return a * a;
}
int main()
{
    op();
    cout << op(4, 2) << endl;
    cout << op(4.4, 2.2) << endl;
    cout << op(2);
}
```

## Operator Overloading

```cpp
#include <iostream>
#include <string>

using namespace std;

class CPnt
{
    int x;
    int y;

public:
    CPnt(){};
    CPnt(int a, int b) : x(a), y(b){};
    CPnt operator+(CPnt point)
    {
        /*CPnt t;
        t.x = x + point.x;
        t.y = y + point.y;
        return t;*/
        return (CPnt(x + point.x, y + point.y));
    }
    void pr()
    {
        cout << "point x : " << x << endl;
        cout << "point y : " << y << endl;
    }
};

int main()
{
    CPnt a(1, 2);
    CPnt b(3, 4);
    CPnt c;
    c = a + b;
    c.pr();

    return 0;
}
```

## Example Code : 두 점의 좌표 계산하기

```cpp
#include <iostream>
#include <string>

using namespace std;

class CPnt
{
    int x;
    int y;

public:
    CPnt(){};
		CPnt(int a,int b){x=a;y=b;}
    CPnt operator+(CPnt point)
    {
        CPnt t;
        t.x = x + point.x;
        t.y = y + point.y;
        return t;
    }
    void pr()
    {
        cout << "point x : " << x << endl;
        cout << "point y : " << y << endl;
    }
};

int main()
{
    CPnt a(1, 2);
    CPnt b(3, 4);
    CPnt c;
    c = a + b;
    c.pr();

    return 0;
}
```

---

# Reference

- [C++] template(템플릿) 에 관하여 1 (템플릿이란, 함수 템플릿)
    
    [https://blockdmask.tistory.com/43](https://blockdmask.tistory.com/43)