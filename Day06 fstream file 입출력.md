# Day06 fstream :: file 입출력

# Contents

---

# 파일 입출력의 과정

1. 입출력 헤더파일을 포함시킨다.
2. 입출력 스트림 관리객체를 선언한다.
3. 선언된 객체를 통해 입출력을 실행한다.
4. 입출력 스트림 관리객체를 닫음으로서 열었던 파일을 닫는다.

# **C언어 파일입출력과 C++ 파일입출력 차이가 무엇일까요?**

## **[C언어]**

C언어의 경우 [위 포스팅](https://jhnyang.tistory.com/196)에서 보았듯이 

*함수를 통해 스트림을 형성하고 필요한 정보를 파일구조체에다가 받아서 포인터로  접근*해 사용합니다. 

그리고 해당 파일로부터 읽고 싶거나, 또는 어떤 파일에 데이터를 쓰고 싶으면 *파일입출력 관련 함수를 이용해서 코드를 짜줘요. (fputs, fputc, fgets 등등)*

## **[C++언어]**

그런데 *C++은 이런 **스트림 관련 기능과 파일입출력 함수와 같은 관련 함수들을 묶어서 클래스로 제공***하고 있어요.

즉 FILE 구조체를 복잡한 포인터로 사용하지 않고 정보를 객체에 저장합니다. 

세부적인건 우리가 몰라도 되도록요!

또 기존 C++ 스탠다드 입출력 형식과 매우 유사하게 통일함으로써 헷갈림을 방지합니다!

# 파일 입출력 헤더

![Untitled](Day06%20fstream%20file%20%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%8E%E1%85%AE%E1%86%AF%E1%84%85%E1%85%A7%E1%86%A8%209151bd6e09b1424d8953fe344604fd86/Untitled.png)

## 각 파일 입출력 헤더 스트림 관리 객체 이름

(표준입력)istream → ifstream

(표준출력)ostream → ofstream

(표준입출력)iostream → fstream

즉! 

파일을 읽기만 할거면 ifstream객체를, 

파일이 쓰기만 할거면 ofstream객체를, 

읽고쓰는거 같이 할거면 fstream객체를 사용!!

# 파일로부터 문자열 읽기 - get,getline

## get()

```cpp
#include <iostream>
#include <fstream>
int main()
{
	ifstream fin("output.txt");
	char c;
	while (fin.get(c))   //파일입력
		std::cout << c;  //표준입출력 출력
	fin.close();
	return 0;
}
```

## getline()

```cpp
#include <iostream>
#include <fstream>
using namespace std;
int main()
{
	ifstream fin("output.txt");
	char line[100];
	while(fin.getline(line, sizeof(line)))
		cout << line << endl;
	fin.close();
	return 0;
}
```

---

# 수업에서 다룬 입출력 코드

## 1. File Write

```cpp
#include <iostream>
#include <fstream>
using namespace std;
int main() {
  ofstream MyFile("anu.txt"); // Create and open a text file
  MyFile << "Andong National Univ.";   // Write to the file
  MyFile.close();  // Close the file

	return 0;
}
```

### File Write

```cpp
ofstream MyFile("anu.txt"); // Create and open a text file
```

→ 표준출력(ostream)의 관리객체 ofstream 생성

```cpp
  MyFile << "Andong National Univ.";   // Write to the file
```

→ 출력실행

```cpp
  MyFile.close();  // Close the file
```

→ 출력스트림 관리객체 닫음

## 2. File Read

```cpp
#include <iostream>
#include <fstream>
using namespace std;
int main(){
	string myText;
	ifstream myFile("filename.txt");
	while (getline (myFile, myText)) {
	  cout << myText;
	}
	myFile.close();

	return 0;
}
```

### File Read

```cpp
string myText;
```

→ string 객체를 생성 

> 자바의 String과 같이 std에서 지원해주나 스펠링이 다르다. 자바에서는 String이나 C++에서는 string이다.
> 

```cpp
ifstream myFile("filename.txt");
```

→ istream(표준입력) 관리객체 생성

```cpp
while (getline (myFile, myText)) {
  cout << myText;
}
```

→ getline(file,str)을 통해 파일로부터 문자열을 읽어옴

```cpp
	myFile.close();
```

→ 표준입력 관리객체 닫음

## anu.txt에서 둘째 줄의 두 수를 읽고 더하여라

```cpp
MyFile << "Andong National Univ.\n";
MyFile << "20 30"<<endl;

myFile
1줄: Andong National Univ.
2줄: 20 30

#include <iostream>
#include <fstream>
#include <cstring>
using namespace std;
int main() {
	int n=0, a, b;
	string myText;
	ifstream myFile("anu.txt");
	while (getline (myFile, myText)) {
		n++;
		if(n==2){
		sscanf(myText.c_str(), "%d%d", &a,&b);
			cout << a + b << endl;
	}
	}
	myFile.close();
}
```

---

# Reference

- C++ 프로그래밍 기초 - 성윤정,김태은 공저, 한빛미디어
    
    : p.534~
    
- C언어와 C++ 파일입출력 차이 / 파일입출력 헤더 / 파일로부터 문자열 읽기 - get,getline
[https://jhnyang.tistory.com/363](https://jhnyang.tistory.com/363)