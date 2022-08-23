# STL algorithm

# Vector

---

![Untitled](STL%20algorithm%20c58c055a1bbe46969f53232e28d3c50e/Untitled.png)

- **front() :**

첫 번째 원소

- **back() :**

마지막 원소

- **begin() :**

첫번째 위치

- **end() :**

마지막의 다음 위치

- **size() :**

원소의 개수

- **capacity() :**

할당된 공간의 크기

## #1

```cpp
/*
vector 복습
1) vector me에 {3,4,5}를 넣으세요.
2) 가장 뒤에 8을 넣어 주세요.
3) 처음에 1을 넣어 주세요.
4) 출력해 주세요.
*/

// Example program
#include <iostream>
#include <vector>
using namespace std;
int main()
{
  vector <int > v = {1,2,3};
	// v.push_back(1);
  // v.push_back(2);
  // v.push_back(3);
	v.push_back(8);
  for(unsigned int i=0;i<v.size();i++){
    //cout << v.at(i) << endl;
    cout << v[i] << endl;
    // v.at(i)
    // v[i]
    // v.begin()
    // v.end() - 1
  }
}
```

## #2

```cpp
/*
크기5의 모든 초기값이 3인 벡터 생성한 뒤, 반복자를 통해 접근하여 출력해보아라.
*/
#include <iostream>
#include <vector>
using namespace std;
int main(){
	**vector<int> v(5,3); //{3,3,3,3,3}
	//vector<int> v = {1,2,3};
	vector<int>::iterator i;
	for(i=v.begin(); i!=v.end();i++){
		cout << *i << endl;
	}**
}
```

# Stack

---

- empty()
- size()
- top()
- push(g)
- pop()

## #1

```cpp
/*
	1. 0~4까지 스택에 입력
	2. 비워질 때까지 while문을 사용하여 꺼내기
*/

#include <iostream>
#include <stack>
using namespace std;
int main(){
	stack<int> stck;
	for(int i=0;i<5;i++){
		stck.push(i);
	}
	**while(!stck.empty()){
		cout << stck.top() << endl;
		stck.pop();
	}**
	return 0;
}
```

## #2

```cpp
/*
스택을 활용하여 10진수를 16진수로 변환하기
*/
#include <stack>
#include <iostream>
#include <string>
using namespace std;

int main(){
	stack<char> stck;
	string converter("0123456789ABCDEF");
	string hexadecimal;
	int decimal;
	
	do{
		cout<<"양의정수 입력"
		cin>>decimal;
	}while(decimal <=0);
	while(decimal!=0){
		stck.push(converter[decimal%16]);
		decimal = decimal;
	}
}
```

# Quick Sort() vs STL Sort()

---

## 1. Sort using STL

```cpp
// https://www.geeksforgeeks.org/sort-algorithms-the-c-standard-template-library-stl/ //

// C++ program to sort an array
#include <algorithm>
#include <iostream>
 
using namespace std;

// Driver code
int main()
{
   int a[] = { 1, 3, 5, 4, 2};
   
   // size of the array
   int asize = sizeof(a) / sizeof(a[0]);
   cout << "The array before sorting is : \n";
 
   // sort the array
   sort(a, a + asize);
   /*
   		sort (시작주소, 끝 주소)
   		 a
		   -> address of first element of array
		   a + asize(sizeof(a)/sizeof(a[0])
		   -> addrest of next contiguous locatoin of last element of array 
   */
 
   //size of a[0] -> size of int -> 4
   cout << sizeof(a[0]) << endl; 
   return 0;
}
```

## 2. Quick Sort

---

```cpp
// https://www.programiz.com/cpp-programming/library-function/cstdlib/qsort //

#include <iostream>
#include <cstdlib>
using namespace std;

**int compare(const void* a, const void* b)
{
	const int* x = (int*) a;
	const int* y = (int*) b;

	if (*x > *y)
		return 1;
	else if (*x < *y)
		return -1;
	else
		return 0;
}**

int main()
{
	const int num = 10;
	int arr[num] = {9,4,19,2,7,9,5,15,23,3};

	cout << "Before sorting" << endl;
	for (int i=0; i<num; i++)
		cout << arr[i] << " ";

	**qsort(arr,num,sizeof(int),compare);**

	cout << "After sorting" << endl;
	for (int i=0; i<num; i++)
		cout << arr[i] << " ";

	return 0;
}
```

# Appendices

---

- C++ : 고성능 응용 프로그램을 만드는 데 사용할 수 있는 교차 플랫폼 언어입니다.
- C++/WinRT : 헤더 파일 기반 라이브러리로 구현된 WinRT(Windows 런타임) API용 최신의 완전한 표준 C++17 언어 프로젝션
- Windows App SDK : Windows App 개발 플랫폼의 다음 진화를 나타내는 새로운 개발자 구성 요소 및 도구 집합
- WinUI 3 is the next generation of microsoft's windows ui library. it is based on windows app sdk
- React : 사용자 인터페이스 구축을 위한 선언적이고 효율적이며 유연한 JavaScript 라이브러리
- Rust : 성능 및 안전, 특히 안전한 동시성을 위해 설계된 다목적 프로그래밍 언어이다.
- **Direct3D** is a graphics [application programming interface](https://en.wikipedia.org/wiki/Application_programming_interface) (API) for [Microsoft Windows](https://en.wikipedia.org/wiki/Microsoft_Windows). Part of [DirectX](https://en.wikipedia.org/wiki/DirectX), Direct3D is used to render [three-dimensional graphics](https://en.wikipedia.org/wiki/3D_computer_graphics) in applications where performance is important, such as games.
- STL algorithm의 종류
1. 읽기 알고리즘(algorithm 헤더 파일)
2. 변경 알고리즘(algorithm 헤더 파일)
3. 정렬 알고리즘(algorithm 헤더 파일)
4. 수치 알고리즘(numeric 헤더 파일)