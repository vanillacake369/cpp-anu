# Why use “const(...)&" rather than “(...)&” ?

# Contents

# 그냥 주소를 받으면 되지, const를 통해 받는 이유가 무엇인가?

## Opinion #1

> Even though the `const` is keeping you from changing the value of your parameter, it's better to send a reference to it, rather than send it by value, because, in large objects, sending it by value would require copying it first, which is not necessary when calling by reference
> 

## Opinion #2

> It speeds up the code execution, it offers usage simplicity and it also ensures the caller that you can not change the value of the variable by setting `const`
 keyword. It maybe have some other benefits, but I think the performance is the main reason. In [this article](https://www.geeksforgeeks.org/references-in-c/) and related articles, there are many useful things about References in C++.
> 

```
void printStudent(const Student &s)
{
    cout << s.name << "  " << s.address << "  " << s.rollNo;
}

int main(){
    Student s1;
    printStudent(s1);
    return 0;
}

```

Benefits are:

1. Work easily with object(don't think about pointers)
2. It does not copy the Student object(so it is fast)
3. You can not create a new student and assign it to s variable. if you write `s=new Student();` the compiler error will happen. So the caller can pass the variable with more confidence.
4. The parameter can not be null.

# 정리

즉, 다음과 같은 효과를 나타낸다는 것이다.

- 크기가 큰 Obejct를 shallow copy를 하지 않고 참조를 통해 받을 수 있다.
- `const`키워드를 통해 parameter가 인자로 넘어온 주소값 이외의 값을 참조할 수 없게 제한한다
    
    (= 오로지 인자주소값만 참조하게 강제한다)
    

# Reference

**[Why put const (...)& in C++](https://stackoverflow.com/questions/44795308/why-put-const-in-c)**