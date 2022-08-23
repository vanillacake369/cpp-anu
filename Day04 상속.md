# Day04 상속

# Contents

### Exmple Code : Tri,Rectangle using Inheritance

```cpp
#include <iostream>
using namespace std;

class CPoly{
protected:
    int w, h;
};
class CRect: public CPoly{
public:
    CRect(int x, int y){w=x; h=y;}
    int Area(){ return w*h;}
};
class CTry : public CPoly{
public:
    CTry(int x, int y){w=x; h=y;}
    int Area(){ return w*h/2;}
};

int main()
{
  CRect r(2,3);
  CTry t(2,3);
  cout << r.Area() << endl;
  cout << t.Area();
}
```