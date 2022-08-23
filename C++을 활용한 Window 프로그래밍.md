# C++을 활용한 Window 프로그래밍

# WinUI3 세팅

## Initial Setting

---

- 설치 대화 상자의 **워크로드** 탭에서 적절하게 선택합니다.
- UWP(유니버설 Windows 플랫폼) 앱 개발의 경우 **유니버설 Windows 플랫폼 개발을** 선택합니다.
- 그런 다음 해당 워크로드에 대한 설치 대화 상자의 **설치 세부 정보** 창에서 **C++(v143) 유니버설 Windows 플랫폼 도구**가 선택되어 있는지 확인합니다.
- C++ 앱 개발의 경우 **C++를 사용하여 데스크톱 개발을** 선택합니다.
- 그런 다음 설치 대화 상자의 **설치 세부 정보** 창에서 **Windows 앱 SDK C++ 템플릿**(목록 하단)을 선택합니다.
- 설치 대화 상자의 **개별 구성 요소** 탭에 있는 **SDK, 라이브러리 및 프레임워크** 섹션에서 **Windows 10 SDK(10.0.19041.0)**가 선택되어 있는지 확인합니다.

## 새 프로젝트 구성

![Untitled](C++%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%92%E1%85%AA%E1%86%AF%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A1%E1%86%AB%20Window%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%80%E1%85%B3%E1%84%85%E1%85%A2%E1%84%86%E1%85%B5%E1%86%BC%207c07d72984b94c6e889aadb1d4c404a6/Untitled.png)

이 때 *솔루션 및 프로젝트를 같은 디렉토리에 배치* 를 선택해준다~

## 대화상자기반 애플리케이션 생성

![Untitled](C++%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%92%E1%85%AA%E1%86%AF%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A1%E1%86%AB%20Window%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%80%E1%85%B3%E1%84%85%E1%85%A2%E1%84%86%E1%85%B5%E1%86%BC%207c07d72984b94c6e889aadb1d4c404a6/Untitled%201.png)

***위와 같이 여러 문서가 아닌 아래와 같은 대화상자 기반 애플리케이션을 생성한다!***

![Untitled](C++%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%92%E1%85%AA%E1%86%AF%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A1%E1%86%AB%20Window%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%80%E1%85%B3%E1%84%85%E1%85%A2%E1%84%86%E1%85%B5%E1%86%BC%207c07d72984b94c6e889aadb1d4c404a6/Untitled%202.png)

## 도구 상자 pin

![Untitled](C++%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%92%E1%85%AA%E1%86%AF%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A1%E1%86%AB%20Window%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%80%E1%85%B3%E1%84%85%E1%85%A2%E1%84%86%E1%85%B5%E1%86%BC%207c07d72984b94c6e889aadb1d4c404a6/Untitled%203.png)

## 대화상자 편집기

edit control 2개

button 1개

![Untitled](C++%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%92%E1%85%AA%E1%86%AF%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A1%E1%86%AB%20Window%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%80%E1%85%B3%E1%84%85%E1%85%A2%E1%84%86%E1%85%B5%E1%86%BC%207c07d72984b94c6e889aadb1d4c404a6/Untitled%204.png)

## 속성 입력 // edit control

### 캡션

![Untitled](C++%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%92%E1%85%AA%E1%86%AF%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A1%E1%86%AB%20Window%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%80%E1%85%B3%E1%84%85%E1%85%A2%E1%84%86%E1%85%B5%E1%86%BC%207c07d72984b94c6e889aadb1d4c404a6/Untitled%205.png)

### 글꼴

![Untitled](C++%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%92%E1%85%AA%E1%86%AF%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A1%E1%86%AB%20Window%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%80%E1%85%B3%E1%84%85%E1%85%A2%E1%84%86%E1%85%B5%E1%86%BC%207c07d72984b94c6e889aadb1d4c404a6/Untitled%206.png)

# WinUI3 Coding

## button 더블클릭 → 코드 입력

![Untitled](C++%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%92%E1%85%AA%E1%86%AF%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A1%E1%86%AB%20Window%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%80%E1%85%B3%E1%84%85%E1%85%A2%E1%84%86%E1%85%B5%E1%86%BC%207c07d72984b94c6e889aadb1d4c404a6/Untitled%207.png)

- ** xaml파일이란??
    
    화면 디자인 영역을 담당하는 파일이다.
    

## Code

---

```cpp
void CCalcDlg::OnBnClickedButton1()
{
	// TODO: 여기에 컨트롤 알림 처리기 코드를 추가합니다.
	int a = GetDlgItemInt(IDC_EDIT1);
	int b = **GetDlgItemInt(IDC_EDIT2);
	SetDlgItemInt(IDC_EDIT3, a + b);**
}
```

숫**자를 입력 받고자 할 때**

- **방법1.**

```cpp
CString str;
GetDlgItemText(IDC_EDIT, str);
int age = atoi(str);　　　// atoi : array to integer, (예- 문자 "23"을 정수 23으로)
```

- **방법2.**

```cpp
int age = GetDlgItemInt(IDC_EDIT);
```

- **숫자 입력시**

```cpp
SetDlgItemInt(EDIT의 ID값, 숫자);
```

## Methods

---

- `stoi()`

convert string to integer 

- `to_string()`

get data from screen

- `to_hstring()`

print data of memory to screen

## Code

---

`MainWindow.xaml`

```xml
<Window
    x:Class="App1.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:App1"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d">

    <StackPanel Orientation="Horizontal" HorizontalAlignment="Center">
        <TextBox x:Name="a"></TextBox>
        <TextBlock>+</TextBlock>
        <TextBox x:Name="b"></TextBox>
        <Button x:Name="add" Click="myAdd">=</Button>
        <TextBlock x:Name="c">???</TextBlock>
    </StackPanel>
</Window>
```

`MainWindow.xaml.cpp`

```cpp
/* *Print "i love anu" to console*

void MainWindow::myButton_Click()
{
	myButton().Content(box_value(L"i love anu")); //L : for support unicode 
}
*/

void winrt::App1::implementation::MainWindow::myAdd(winrt::Windows::Foundation::IInspectable const& sender, winrt::Microsoft::UI::Xaml::RoutedEventArgs const& e)
{
	int va = stoi(to_string(a().Text()));
	int vb = stoi(to_string(b().Text()));
	int vc = va + vb;
	c().Text(to_hstring(vc));
}
```

## Reference

---

**11강 윈도우 프로그래밍, MFC, WINUI**

[https://cafe.naver.com/simplecpp?iframe_url_utf8=%2FArticleRead.nhn%253Fclubid%3D30636140%2526page%3D1%2526menuid%3D2%2526boardtype%3DL%2526articleid%3D73%2526referrerAllArticles%3Dfalse](https://cafe.naver.com/simplecpp?iframe_url_utf8=%2FArticleRead.nhn%253Fclubid%3D30636140%2526page%3D1%2526menuid%3D2%2526boardtype%3DL%2526articleid%3D73%2526referrerAllArticles%3Dfalse)

****첫 번째 WinUI 3 프로젝트 만들기****

[https://docs.microsoft.com/ko-kr/windows/apps/winui/winui3/create-your-first-winui3-app](https://docs.microsoft.com/ko-kr/windows/apps/winui/winui3/create-your-first-winui3-app)

**Building a Native Windows on Arm App with WinUI 3**

[https://developer.arm.com/documentation/102767/0100/Create-a-WinUI-3-0-application](https://developer.arm.com/documentation/102767/0100/Create-a-WinUI-3-0-application)

**CEdit, CButton, CListBox**

[http://www.tipssoft.com/bulletin/board.php?bo_table=story&wr_id=3581&sca=������ũ&page=8](http://www.tipssoft.com/bulletin/board.php?bo_table=story&wr_id=3581&sca=%C6%C1%BE%D8%C5%D7%C5%A9&page=8)