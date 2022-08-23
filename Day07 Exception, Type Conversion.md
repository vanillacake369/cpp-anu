# Day07 Exception, Type Conversion

# Try-Catch

```cpp
try {
  int age = 15;
  if (age >= 18) {
    cout << "Access granted - you are old enough.";
  } else {
    throw (age);
  }
}
catch (int myNum) {
  cout << "Access denied - You must be at least 18 years old.\n";
  cout << "Age is: " << myNum;
}
```

Java의 try-catch와 별 다를 것이 없다.

다만 catch()문의 그것과는 다르다

<aside>
💡 Java : catch(Exception e) 를 쓰는 대신에 C++에서는 catch(int num)을 사용한다.

</aside>

throw(age)를 통해 예외발생 변수age를 던진다. 나는 여태껏 문자열만을 던져 char*만 던지고 받는 줄 알았거늘, 어떠한 변수든 던지고 받을 수 있나보다

- 어떤 변수든 throw가능하다.
    
    **Throwing Exceptions**
    
    Exceptions can be thrown anywhere within a code block using **throw** statement. 
    
    The operand of the throw statement determines a ***type for the exception and can be any expression and the type of the result of the expression*** determines the type of exception thrown.
    

catch(int myNum)를 통해 던진 age를 받아 예외에 대한 메세지를 콘솔에 출력한다.

# **C++ Standard Exceptions**

![Untitled](Day07%20Exception,%20Type%20Conversion%205d5caeca39ef40e3bbd8ada15610e26c/Untitled.png)

C++에서는 우리가 프로그램 내에서 쓸 수 있는 <excpetion>이라는 기준 예외처리 리스트를 정의해두었다. (각 Exception들의 역할에 대한 설명을 참조하려면 [여기](https://www.tutorialspoint.com/cplusplus/cpp_exceptions_handling.htm#:~:text=A%20C%2B%2B%20exception%20is%20a,try%2C%20catch%2C%20and%20throw.)를 보시라)

<exception>을 쓰게 되면 맨 위 소스코드처럼 그저 예외발생 시 단순 예외처리를 하는 것이 아닌 각 예외에 따른 handling을 세분화할 수 있다.

다음 소스코드 예시를 보자.

```cpp
#include <iostream>
#include <exception>
using namespace std;

struct MyException : public exception {
   const char * what () const throw () {
      return "C++ Exception";
   }
};
 
int main() {
   try {
      throw MyException();
   } catch(MyException& e) {
      std::cout << "MyException caught" << std::endl;
      std::cout << e.what() << std::endl;
   } catch(std::exception& e) {
      //Other errors
   }
}
```

위 코드는 다음과 같은 결과를 출력한다.

```cpp
MyException caught
C++ Exception
```

---

# Reference

- **C++ Exception Handling**

[https://www.tutorialspoint.com/cplusplus/cpp_exceptions_handling.htm#:~:text=A C%2B%2B exception is a,try%2C catch%2C and throw](https://www.tutorialspoint.com/cplusplus/cpp_exceptions_handling.htm#:~:text=A%20C%2B%2B%20exception%20is%20a,try%2C%20catch%2C%20and%20throw).