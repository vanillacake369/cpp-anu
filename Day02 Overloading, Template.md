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
๐ก ***Template์ด๋??***
: โํจ์๋ ํด๋์ค๋ฅผ ๊ฐ๋ณ์ ์ผ๋ก ๋ค์ ์์ฑํ์ง ์์๋,ย ์ฌ๋ฌ ์๋ฃย ํ์ผ๋ก ์ฌ์ฉํ  ์ ์๋๋ก ํ๊ฒ ๋ง๋ค์ด ๋์ ํโ

</aside>

์๋ฐ์์์ ํํ๋ฆฟ๊ณผ ๋์ผํ๋ค...ใ

- ํด๋์ค ๋ด๋ถ์ ํจ์ ์ ์ธ ์ ๊ธฐ๋ณธ ์ ๊ทผ ์ ํ์๋ private
    
    ์์ ๊ฐ์ด ํจ์๋ฅผ ๋๋ฆฝ์ ์ผ๋ก ์ ์ธ ๋ฐ ์ ์ ์์๋ ํด๋น ํจ์๋ฅผ main์์ ์ ๊ทผํ  ์ ์๋ค. 
    
    ๊ทธ๋ฌ๋ ์๋์ฒ๋ผ ํด๋์ค ๋ด๋ถ์์ ์ ์ธํ๊ฒ ๋๋ฉด ๋ค์ ๊ท์น์ ์ํด ์ ๊ทผํ  ์๊ฐ ์๋ค.
    
    > A whole lot of C code exists, including libraries that were desired to work with C++ as well, that use structs. Classes were introduced in C++, and to conform with the OO philosophy of encapsulation,ย **their members are private by default.
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
    
    ์ด์ ๊ฐ์ ๊ฒฝ์ฐ๋ฅผ ์ํด C++์์๋ private์ผ๋ก ๋ง์๋์ ๋ณ์๋ค์ ๋ค๋ฅธ ํด๋์ค๊ฐ ์ ๊ทผํ  ์ ์๊ฒ๋ ํ๋ freind ํค์๋๋ฅผ ์ ๊ณตํ๋ค.
    
    ( freindํค์๋์ ๋ํด์๋ [์ฌ๊ธฐ๋ฅผ ์ฐธ๊ณ ](https://yeolco.tistory.com/116)ํด๋ณด์ )
    
- `template<typename T>` vs `template<class T> ??`
    
    `typename`ย andย `class`ย are interchangeable in the basic case of specifying a template:
    
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
    
    are equivalent. (์ด๋ ๊ฒ๋ง ์์๋์..ใ)
    
    - ***BUT! thereโs something more.***
        
        Having said that, there are specific cases where there is a difference betweenย `typename`ย andย `class`.
        
        The first one is in the case of dependent types.ย `typename`ย is used to declare when you are referencing a nested type that depends on another template parameter, such as theย `typedef`ย in this example:
        
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
        
        When specifying aย **template template**, theย `class`ย keyword MUST be used as above -- it isย **not**ย interchangeable withย `typename`ย in this caseย *(note: since C++17 both keywords are allowed in this case)*.
        
        You also must useย `class`ย when explicitly instantiating a template:
        
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

## Example Code : ๋ ์ ์ ์ขํ ๊ณ์ฐํ๊ธฐ

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

- [C++] template(ํํ๋ฆฟ) ์ ๊ดํ์ฌ 1 (ํํ๋ฆฟ์ด๋, ํจ์ ํํ๋ฆฟ)
    
    [https://blockdmask.tistory.com/43](https://blockdmask.tistory.com/43)