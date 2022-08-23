# Day08 Stack,Vector

# HOW TO USE?

- Stack이든 Vector이든 `#include`를 통해 inclue해줘야함
- stack<`type`> 변수명 / vector<`type`> 변수명
    
    Ex) stack<int> me;
    
- stack에서는...
    - push()
    - empty()
    - pop()
- vector에서는...
    - at
    - front
    - back

# Stack

```cpp
#include <iostream>
#include <stack>
using namespace std;
int main(){
	stack<int> me;
	for(int i=0;i<5;i++) me.push(i);
	cout << "Popping out elements...";
	while(!me.empty()){
		cout << ' ' << me.top();
		me.pop();
	}
	cout << '\n';
	return 0;
}
```

# Vector

```cpp
#include <iostream>
#include <vector>
using namespace std;
int main(){
	vector<int> v;
	v.push_back(7);
	v.push_back(3);
	for(int i=0; i< v.size() ; i++)
		cout << v.at(i) << endl;
}
```

- 초기화 시, {n1,n2 ...}으로 초기화 하지 않도록 주의한다.
    
    If your compiler supports C++11, you can simply do:
    
    ```cpp
    std::vector<int> v = {1, 2, 3, 4};
    ```
    
    This is available in GCC [as of version 4.4](http://gcc.gnu.org/projects/cxx0x.html). Unfortunately, VC++ 2010 seems to be lagging behind in this respect.
    

# Reference

- vector

[https://www.cplusplus.com/reference/vector/vector/](https://www.cplusplus.com/reference/vector/vector/)

- vector initialization

[https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/)

- **What is the easiest way to initialize a std::vector with hardcoded elements?**

[https://stackoverflow.com/questions/2236197/what-is-the-easiest-way-to-initialize-a-stdvector-with-hardcoded-elements](https://stackoverflow.com/questions/2236197/what-is-the-easiest-way-to-initialize-a-stdvector-with-hardcoded-elements)