---
title: Computer programming
date: 2020-07-06 10:10:44
categories:
- C, C++
- Basic
tags:
- C, C++
mathhax: true
---
# Day 1

## C와의 차이점

+ `#include <stdio.h>` -> `#include <iostream>`
  + 형식지정자 필요없어짐
+ `.h` 사라짐
  + 호환은 가능
+ `class`의 개념
  + object
+ `bool`의 개념
  + C
    + 참 : 0 이외의 값
  + C++
    + true : 1
    + false : 0
+ `string`의 개념

## Practice

> practice.cpp

~~~C++
#include <iostream>
using namespace std;

int main(){
    int a = 5;
    int b = 10;
    cout << "1. a + b / 3 * 3 = " << a + b / 3 * 3 << endl;
    cout << "2. b << 2 = " << (b << 2) << endl;
    cout << "3. a != b = " << (a != b) << endl;
    cout << "4. b % a = " << (b % a) << endl;
    cout << "5. (a > b) ? a : b = " << ((a > b) ? a : b) << endl;
    cout << "6. sizeof(a) = " << sizeof(a) << endl;
    int c;
    c = a++;
    cout << "7. C = a++ 이후 c의 값 : " << c << endl;
    a += b;
    cout << "8. a += b 이후 a의 값 : " << a << endl;
    cout << "9. a & b = " << (a & b) << endl;
    c = (a + b, a - b);
    cout << "10. c = (a + b, a - b) 이후 c의 값 : " << c << endl;
    return 0;
}
~~~

>> Output

~~~C++
1. a + b / 3 * 3 = 14
2. b << 2 = 40
3. a != b = 1
4. b % a = 0
5. (a > b) ? a : b = 10
6. sizeof(a) = 4
7. C = a++ 이후 c의 값 : 5
8. a += b 이후 a의 값 : 16
9. a & b = 0
10. c = (a + b, a - b) 이후 c의 값 : 6

Process finished with exit code 0
~~~

<!-- More -->

## 연산자

+ 산술 연산자
  + `*`, `/`, `%`
  + `+`, `-`
+ 비트 이동 연산자
  + `<<`, `>>`
+ 관계 연산자
  + `<`, `<=`, `>`, `>=`
  + `==`, `!=`
+ 논리 연산자
  + `&&`
  + `||`

## Plus

> plus.cpp

~~~C++
#include <iostream>
using namespace std;

int main(){
    int x = 10, y = 10;

    cout << "x = " << x << endl;
    cout << "++x = " << ++x << endl;
    cout << "x = " << x << endl;

    cout << "y = " << y << endl;
    cout << "y++ = " << y++ << endl;
    cout << "y = " << y << endl;

    return 0;
}
~~~

>> Output

~~~C++
x = 10
++x = 11
x = 11
y = 10
y++ = 10
y = 11

Process finished with exit code 0
~~~

## Switch

> switch.cpp

~~~C++
#include <iostream>
using namespace std;

int main(){
    int score;

    cout << "점수를 입력하세요 : ";
    cin >> score;

    score = score / 10;

    switch(score){
        case 10:
        case 9:
            cout << "A+ 입니다.";
            break;
        case 8:
            cout << "A 입니다.";
            break;
        case 7:
            cout << "B 입니다.";
            break;
        case 6:
            cout << "C 입니다.";
            break;
        default:
            cout << "F 입니다.";
            break;
    }

    return 0;
}
~~~

## Continue & Break

> continue_break.cpp

~~~C++
#include <iostream>
using namespace std;

int main(){
    int a;
    for(;;){
        cout << "정수 입력 : ";
        cin >> a;
        if(a == 0)
            break;
        if(a % 3 != 0){
            cout << "No" << endl;
            continue;
        }
        cout << "Yes" << endl;
    }

    return 0;
}
~~~

***

# Day 2

## Pointer

> pointer1.cpp

~~~C++
#include <iostream>
using namespace std;

int main(){
    int a = 10;
    int b = 12;
    int *pa; //Pointer 변수
    int *pb;
    pa = &a;
    pb = &b;
    cout << "Pointer of a : " << pa << " == " << &a << endl;
    cout << "Pointer of b : " << pb << " == " << &b << endl;

    return 0;
}
~~~

>> Output

~~~C++
Pointer of a : 0x7ffee6a4f958 == 0x7ffee6a4f958
Pointer of b : 0x7ffee6a4f954 == 0x7ffee6a4f954

Process finished with exit code 0
~~~

> pointer2.cpp

~~~C++
#include <iostream>
using namespace std;

int main(){
    int a[3] = {1, 2, 3};
    int *pa; //Pointer 변수
    pa = &a[0];
    cout << "*(pa + 1) = " << *(pa + 1) << endl;
    cout << "a[1] = " << a[1] << endl;

    return 0;
}
~~~

>> Output

~~~C++
*(pa + 1) = 2
a[1] = 2

Process finished with exit code 0
~~~

+ 포인터는 상수 - 변경 불가

## Function

> function.cpp

~~~C++
#include <iostream>
using namespace std;

int adder(int a, int b);

int main(){
    cout << adder(13, 14) << endl;
    return 0;
}

int adder(int a, int b){
    int sum;
    sum = a + b;
    return sum;
}
~~~

>> Output

~~~C++
27

Process finished with exit code 0
~~~

+ Call by Value
  + 값 복사 - 수정 불가
  + 전역변수 - 누구든지 접근 가능
+ Call by Address
+ Call by Reference

> call_by_value.cpp

~~~C++
#include <iostream>
using namespace std;

void swap(int x, int y);

int main(){
    int a = 2;
    int b = 3;

    cout << "a : " << a << "\tb : " << b <<endl;
    swap(a, b);
    cout << "a : " << a << "\tb : " << b <<endl;

    return 0;
}

void swap(int x, int y){
    int temp = x;
    x = y;
    y = temp;
}
~~~

>> Output

~~~C++
a : 2	b : 3
a : 2	b : 3

Process finished with exit code 0
~~~

> call_by_address.cpp

~~~C++
#include <iostream>
using namespace std;

void swap(int *x, int *y);

int main(){
    int a = 2;
    int b = 3;

    cout << "a : " << a << "\tb : " << b <<endl;
    swap(&a, &b);
    cout << "a : " << a << "\tb : " << b <<endl;

    return 0;
}

void swap(int *x, int *y){
    int temp = *x;
    *x = *y;
    *y = temp;
}
~~~

> call_by_reference.cpp

~~~C++
#include <iostream>
using namespace std;

void swap(int *x, int *y);

int main(){
    int a = 2;
    int b = 3;

    cout << "a : " << a << "\tb : " << b <<endl;
    swap(a, b);
    cout << "a : " << a << "\tb : " << b <<endl;

    return 0;
}

void swap(int &x, int &y){
    int temp = x;
    x = y;
    y = temp;
}
~~~

>> Output

~~~C++
a : 2	b : 3
a : 3	b : 2

Process finished with exit code 0
~~~

+ `swap(int, int)`는 기본 제공 함수

## 배열

~~~C++
int n[10]; // 정수 10개짜리 빈 메모리 공간
double d[] = [0.1, 0.2, 0.5, 3.9]; // d의 크기는 자동 4로 설정
n[10] = 20; // 인덱스 0~9까지만
n[-1] = 9.9; // 인덱스 음수 불가
int m[2][5]; // 2행 5열의 2차원 배열 선언
int grade[2][3] = {{10, 20, 30}, {40, 50, 60}};
~~~

+ 배열은 0부터 시작
+ 함수에 매개변수로 전달 시 배열의 크기도 함께 전달

> two_dimension_array.cpp

~~~C++
#include <iostream>
using namespace std;

int main(){
    int Ary[5][5];
    int i, j;
    for(i = 0; i < 5; i++){
            for(j = 0; j < 5; j++){
                if(i >= j){
                    Ary[i][j] = i + 1;
                }
                else{
                    Ary[i][j] = 0;
                }
            }
    }
    for(i = 0; i < 5; i++){
        for(j = 0; j < 5; j++){
            cout << Ary[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}
~~~

>> Output

~~~C++
1 0 0 0 0 
2 2 0 0 0 
3 3 3 0 0 
4 4 4 4 0 
5 5 5 5 5 

Process finished with exit code 0
~~~

## Calling a Function with an Array as a Parameter

~~~C++
#include <iostream>
using namespace std;

int addArray(int *a, int size);
void makeDouble(int a[], int size);
void printArray(int a[], int size);

int main(){
    int n[] = {1, 2, 3, 4, 5};

    int sum = addArray(n, 5);
    cout << "배열 n의 합은 " << sum << "입니다." << endl;
    makeDouble(n, 5);
    printArray(n, 5);

    return 0;
}

int addArray(int *a, int size){
    int su = 0;
    for(int i = 0; i < size; i++){
        su = su + a[i];
    }
    return su;
}
void makeDouble(int a[], int size){
    for(int i = 0; i < size; i++){
        a[i] = a[i] * a[i];
    }
}
void printArray(int a[], int size){
    for(int i = 0; i < size; i++){
        cout << a[i] << "\t";
    }
}
~~~

>> Output

~~~C++
배열 n의 합은 15입니다.
1	4	9	16	25	
Process finished with exit code 0
~~~

+ 배열이 함수의 파라미터로 들어갈 경우
  + `int *a`
  + `int a[]`

## Const and Pointer

> const_pointer.cpp

~~~C++
#include <iostream>
using namespace std;

int main(){
    int var1 = 1;
    int var2 = 2;

    const int *p1 = &var1;
    int *const p2 = &var2;

    //*p1 = 10; 오류
    var1 = 10;
    *p2 = 3;

    cout << var1 << endl;
    cout << var2 << endl;

    return 0;
}
~~~

>> Output

~~~C++
10
3

Process finished with exit code 0
~~~

+ `const int *pNum` - 포인터 자체의 값이 상수
+ `int *const pNum` - 포인터가 가리키는 값이 상수

> example.cpp

~~~C++
#include <iostream>
using namespace std;

#define N 4

void print_arr(int *arr);
void percentage(int *arr);

int main(){
    int count[N] = {42, 37, 83, 33};
    cout << "인원수 : ";
    print_arr(count);
    percentage(count);
    cout << "\n백분율 : ";
    print_arr(count);

    return 0;
}

void print_arr(int *arr){
    for(int i = 0; i < N; i++){
        cout << *(arr + i) << "\t";
    }
}
void percentage(int *arr){
    int sum = 0;
    for(int i = 0; i < N; i++){
        sum = sum + *(arr + i);
    }
    for(int i = 0; i < N; i++){
        *(arr + i) = *(arr + i) * 100 / sum;
    }
}
~~~

>> Output

~~~C++
인원수 : 42	37	83	33	
백분율 : 21	18	42	16	
Process finished with exit code 0
~~~

## String

> getline.cpp

~~~C++
#include <iostream>
using namespace std;

int main(){
    string song("Falling in love with you");
    string elvis("Elvis Presley");
    string singer;

    cout << song + "를 부른 가수는";
    cout << "(힌트 : 첫글자는 " << elvis[0] << ")?";

    getline(cin, singer);
    if(singer == elvis)
        cout << "맞았습니다." << endl;
    else
        cout << "틀렸습니다. " + elvis + "입니다." << endl;

    return 0;
}
~~~

>> Output

~~~C++
Falling in love with you를 부른 가수는(힌트 : 첫글자는 E)?Elvis Presley
맞았습니다.

Process finished with exit code 0

...

Falling in love with you를 부른 가수는(힌트 : 첫글자는 E)?asdf
틀렸습니다. Elvis Presley입니다.

Process finished with exit code 0
~~~

+ `char` - `' '`
+ `string` - `" "`

## Quiz

> quiz1.cpp

~~~C++
#include <iostream>
using namespace std;

int main(){
    string str;
    cout << "문자열 입력>>";

    getline(cin, str);
    int len = str.size();
    for(int i = 1; i <= len; i++){
        for(int j = 1; j <= i; j++){
            cout << str[j-1];
        }
        cout << endl;
    }

    return 0;
}
~~~

>> Output

~~~C++
문자열 입력>>Morning
M
Mo
Mor
Morn
Morni
Mornin
Morning

Process finished with exit code 0
~~~

> quiz2.cpp

~~~C++
#include <iostream>
using namespace std;

double biggest(double x[], int n){
    double big = x[0];
    for(int i = 0; i < n; i++){
        if(x[i] > big)
            big = x[i];
    }
    return big;
}

int main(){
    double a[5];
    cout << "5개의 실수를 입력하라>>";
    for(int i = 0; i < 5; i++)
        cin >> a[i];
    cout << "제일 큰 수 = " << biggest(a, 5) << endl;

    return 0;
}
~~~

>> Output

~~~C++
5개의 실수를 입력하라>>20.0
3.44
44.66
22.0
40.0
제일 큰 수 = 44.66

Process finished with exit code 0
~~~

***

# Day 3

## Namespace

~~~C++
namespace name{ // name이라는 이름 공간 생성
    // 이곳에 선언된 모든 이름은 name 이름 공간에 생성된 이름
    void function(){
        ...
    }
    ...
}
name::function()
~~~

+ 이름(Identifier) 충돌이 발생하는 경우
  + 여러 명이 서로 나누어 프로젝트를 개발하는 경우
  + 오픈 소스 혹은 다른 사람이 작성한 소스나 목적 파일을 가져와서 컴파일하거나 링크하는 경우
+ `namespace`
  + 이름 충돌 해결
  + 개발자가 자신만의 이름 공간을 생성할 수 있도록 함
+ `std`
  + ANSI C++ 표준에서 정의한 이름 공간(`namespace`) 중 하나
  + `<iostream>`

> namespace.cpp

~~~C++
#include <iostream>
using namespace std;

namespace Graphic{
    int maximum = 100;
}
namespace Math{
    int maximum = 65536;
    int add(int a, int b){return a + b;}
    int sub(int a, int b){return a - b;}
}

int main(){
    cout << "Radius Maximum = " << Graphic::maximum << endl;
    cout << "Integer Maximum = " << Math::maximum << endl;
    cout << "Integer Add = " << Math::add(2,4) << endl;
    cout << "Integer Sub = " << Math::sub(2,4) << endl;

    return 0;
}
~~~

>> Output

~~~C++
Radius Maximum = 100
Integer Maximum = 65536
Integer Add = 6
Integer Sub = -2

Process finished with exit code 0
~~~

## String

+ `cin.getline(char buf[], int size, char delimitChar)`
  + 공백이 낀 문자열을 입력 받는 방법
  + `buf`에 최대 `size-1`개의 문자 입력(끝에 `\0` 붙임)
  + `delimitChar`를 만나면 입력 중단(끝에 `\0` 붙임)
    + Default : `\n`(Enter)
+ `string` 클래스
  + 문자열의 크기에 따른 제약 없음
    + 스스로 문자열의 버퍼 조정
  + 문자열 복사, 비교, 수정 등을 위한 다양한 함수와 연산자 제공
  + 객체 지향적
  + `<string>` 헤더 파일에 선선

> cin_getline.cpp

~~~C++
#include <iostream>
using namespace std;

int main(){
    cout << "주소 입력 : ";

    char address[100];
    cin.getline(address, 100, '\n');
    cout << "주소는 " << address << "입니다.\n";

    return 0;
}
~~~

>> Output

~~~C++
주소 입력 : ㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅇㅇㅇㅇㅇㅇㅇㅇㅇㅇㅇㅇㅇㅇㅇㅇㅇㅇ
주소는 ㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋ입니다.

Process finished with exit code 0
~~~

> string_getline.cpp

~~~C++
#include <iostream>
#include <string>
using namespace std;

int main(){
    cout << "주소 입력 : ";

    string address;
    getline(cin, address);
    cout << "주소는 " << address << "입니다.\n";

    return 0;
}
~~~

>> Output

~~~C++
주소 입력 : asdfasdfasdfasdfasdfasdfasdfa
주소는 asdfasdfasdfasdfasdfasdfasdfa입니다.

Process finished with exit code 0
~~~

> search.cpp

~~~C++
#include <iostream>
#include <string>
using namespace std;

int main(){
    string str;
    int count = 0;
    cout << "문자들을 입력하라 : ";
    getline(cin, str);

    int i = 0;
    while(true){
        if(str[i] == 'o'){
            count += 1;
        }
        else if(str[i] == '\0'){
            break;
        }
        i += 1;
    }

    cout << 'o' << "의 개수는 " << count << endl;

    return 0;
}
~~~

>> Output

~~~C++
문자들을 입력하라 : Hello, World!
o의 개수는 2

Process finished with exit code 0
~~~

## Class & Object

~~~C++
class Name{
public:
    int value;
    void function();
    ...
};

void Name::function(){
    ...
}
~~~

+ `class`
  + 상태 정보(속성) : 멤버 변수
  + Action : 멤버 함수
  + 객체를 만들어내기 위해 정의된 설계도, 틀
  + 클래스는 객체가 아니며 실체도 아님
+ Object
  + 객체는 생성될 때 클래스의 모양을 그대로 가지고 탄생
  + 멤버 변수와 멤버 함수로 구성
  + 메모리에 생성, 실체(Instance)로도 불림
+ Why `class`?
  + Encapsulation
    + `public`
      + 외부에서 접근 가능
    + `protectected`
    + `private`
      + 외부에서 접근 불가
      + Default
    + 캡슐화
    + 클래스로 묶어둠
  + Inheritance
  + Polymorphism

> circle.cpp

~~~C++
#include <iostream>
using namespace std;

class Circle{
public:
    int radius;
    double getArea();
};
double Circle::getArea(){
    return 3.14*radius*radius;
}

int main(){
    Circle donut;
    donut.radius = 1;
    double area = donut.getArea();
    cout << "donut 면적은 " << area << "입니다." << endl;

    Circle pizza;
    pizza.radius = 30;
    area = pizza.getArea();
    cout << "pizza 면적은 " << area << "입니다." << endl;

    return 0;
}
~~~

>> Output

~~~C++
donut 면적은 3.14입니다.
pizza 면적은 2826입니다.

Process finished with exit code 0
~~~

> rectangle.cpp

~~~C++
#include <iostream>
using namespace std;

class Rectangle{
public:
    int width;
    int height;
    int getArea(){
        return width*height;
    }
};

int main(){
    Rectangle rect;
    rect.width = 3;
    rect.height = 5;
    cout << "사각형의 면적은 " << rect.getArea() << endl;

    return 0;
}
~~~

>> Output

~~~C++
사각형의 면적은 15

Process finished with exit code 0
~~~

## Constructor

+ 생성자
  + 객체가 생성되는 시점에서 자동으로 호출되는 멤버 함수
  + 생성자는 클래스의 이름과 같음
  + `public`으로 선언
+ 종류
  + 기본 생성자
    + 매개변수 없음
    + 생성자가 없으면 컴파일러가 자동으로 만들어줌
  + 사용자 정의 생성자
    + 매개변수 존재
    + 객체 생성 및 멤버 변수 초기값 정의
    + 기본 생성자 자동 생성 X

> constructor.cpp

~~~C++
#include <iostream>
using namespace std;

class Circle{
private:
    int radius;
public:
    Circle();
    Circle(int r);
    double getArea();
};

int main(){
    Circle donut;
    double area = donut.getArea();
    cout << "donut 면적은 " << area << "입니다." << endl;

    Circle pizza(30);
    area = pizza.getArea();
    cout << "pizza 면적은 " << area << "입니다." << endl;

    return 0;
}

double Circle::getArea(){
    return 3.14*radius*radius;
}

Circle::Circle(){
    radius = 1;
}

Circle::Circle(int r){
    radius = r;
}
~~~

>> Output

~~~C++
donut 면적은 3.14입니다.
pizza 면적은 2826입니다.

Process finished with exit code 0
~~~

## Quiz

> quiz2.cpp

~~~C++
#include <iostream>
using namespace std;

class Tower{
private:
    int height;
public:
    Tower();
    Tower(int h);
    int getHeight();
};

int main(){
    Tower myTower;
    Tower seoulTower(100);
    cout << "높이는 " << myTower.getHeight() << "미터" << endl;
    cout << "높이는 " << seoulTower.getHeight() << "미터" <<endl;
    return 0;
}

Tower::Tower(){
    height = 1;
}
Tower::Tower(int h){
    height = h;
}
int Tower::getHeight(){
    return height;
}
~~~

>> Output

~~~C++
높이는 1미터
높이는 100미터

Process finished with exit code 0
~~~

***

# Day 4

## Class Practice

> integer.cpp

~~~C++
#include <iostream>
using namespace std;

class Integer{
private:
    int val1;
public:
    Integer(int val);
    Integer(string val);
    void set(int val);
    int get();
    bool isEven();
};

int main(){
    Integer n(30);
    cout << n.get() << ' ';
    n.set(50);
    cout << n.get() << ' ';
    Integer m("300");
    cout << m.get() << ' ';
    cout << m.isEven();

    return 0;
}

Integer::Integer(int val){
    val1 = val;
}
Integer::Integer(string val){
    val1 = stoi(val);
}
void Integer::set(int val){
    val1 = val;
}
int Integer::get(){
    return val1;
}
bool Integer::isEven(){
    if(val1%2 == 0){
        return true;
    }
    else{
        return false;
    }
}
~~~

>> Output

~~~C++
30 50 300 1
Process finished with exit code 0
~~~

## Destructor

~~~C++
class name{
    ~name();
}
name::~name(){};
~~~

+ 객체가 소멸되는 시점에서 자동으로 호출되는 함수
+ 소멸자의 목적
  + 객체가 사라질 때 마무리 작업을 위함
  + 실행 도중 동적으로 할당 받은 메모리 해제, 파일 저장 및 닫기, 네트워크 닫기 등
+ 소멸자는 `return` 불가
+ 객체는 생성의 반대순으로 소멸
+ 동적 메모리 할당 사용 시 소멸자 이용

> destructor.cpp

~~~C++
#include <iostream>
using namespace std;

class Circle{
public:
    Circle();
    Circle(int r);
    int radius;
    double getArea();
    ~Circle();
};

int main(){
    Circle donut;
    double area = donut.getArea();
    cout << "donut 면적은 " << area << "입니다." << endl;
    donut.~Circle();

    Circle pizza(30);
    area = pizza.getArea();
    cout << "pizza 면적은 " << area << "입니다." << endl;
    pizza.~Circle();

    return 0;
}

Circle::Circle(){
    radius = 1;
    cout << "반지름 " << radius << " 원 생성" << endl;
}
Circle::Circle(int r){
    radius = r;
    cout << "반지름 " << radius << " 원 생성" << endl;
}
double Circle::getArea(){
    return 3.14*radius*radius;
}
Circle::~Circle(){
    cout << "반지름 " << radius << " 원 소멸" << endl;
}
~~~

>> Output

~~~C++
반지름 1 원 생성
donut 면적은 3.14입니다.
반지름 1 원 소멸
반지름 30 원 생성
pizza 면적은 2826입니다.
반지름 30 원 소멸
반지름 30 원 소멸
반지름 1 원 소멸

Process finished with exit code 0
~~~

## 접근 지정자

+ 캡슐화의 목적
  + 객체 보호, 보안
  + C++에서 객체의 캡슐화 전략
    + 객체의 상태를 나타내는 데이터 멤버(멤버 변수)에 대한 보호
    + 중요한 멤버는 다른 클래스나 객체에서 접근할 수 없도록 보호
    + 외부와으이 인터페이스를 위해서 일부 멤버는 외부에 접근 허용
+ 멤버에 대한 3가지 접근 지정자
  + `private`
    + 동일한 클래스의 멤버 함수에만 제한함
  + `public`
    + 모든 다른 클래스에 허용, 외부함수(`main()`)도 허용
  + `protected`
    + 클래스 자신과 상속받은 자식 클래스에만 허용

## Inline

+ 짧은 함수의 다수 호출로 인해 오버헤드가 일어남
+ 이를 `inline`을 통해 해결
+ 장점 : 시간 단축
+ 단점 : 코드가 길어짐
+ 클래스의 선언부에 구현된 멤버 함수는 자동 `inline` 함수

## Program

+ 바람직한 프로그램
  + `main.cpp`
  + `class.h` : 클래스 선언부 - 헤더 파일(`.h`)에 저장
  + `class.cpp` : 클래스 구현부 - `.cpp` 파일에 저장
+ 클래스를 헤더 파일과 `.cpp` 파일로 분리하여 작성
+ 목적 : 클래스 재사용

> main.cpp

~~~C++
#include <iostream>
#include "Box.h"
using namespace std;

int main(){
    Box b(10, 2);
    b.draw();
    cout << endl;
    b.setSize(7, 4);
    b.setFill('%');
    b.draw();

    return 0;
}
~~~

> Box.h

~~~C++
#ifndef UNTITLED_BOX_H // 조건 컴파일 역할, n은 not, 정의되어있지 않으면 정의, 정의되어있으면 실행 X
#define UNTITLED_BOX_H // 중복 include 실행방지

class Box {
private:
    int width, height;
    char fill;
public:
    Box(int w, int h);
    void setFill(char f);
    void setSize(int w, int h);
    void draw();
};

#endif // UNTITLED_BOX_H
~~~

> Box.cpp

~~~C++
#include <iostream>
#include "Box.h"
using namespace std;

Box::Box(int w, int h){
    setSize(w, h);
    fill = '*';
}

void Box::setFill(char f){
    fill = f;
}

void Box::setSize(int w, int h){
    width = w;
    height = h;
}

void Box::draw(){
    for(int n = 0; n < height; n++){
        for(int m = 0; m < width; m++)
            cout << fill;
        cout << endl;
    }
}
~~~

>> Output

~~~C++
**********
**********

%%%%%%%
%%%%%%%
%%%%%%%
%%%%%%%

Process finished with exit code 0
~~~

## Random

~~~C++
#include <cstdlib>
#include <ctime>

int rand(void);
void srand((unsigned int) time(NULL));

srand((unsigned) time(0)); // Seed 값 설정, 현재시간 이용 초기화
rand() % (End - Begin + 1) + Begin; // int 스케일링
rand() % (End - Begin) / RAND_MAX + Begin; // float 스케일링
~~~

+ `rand()` = $[0, 2^{15}-1]$

> random.cpp

~~~C++
#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

class EvenRandom{
public:
    EvenRandom();
    int next();
    int nextinRange(int low, int high);
};

int main(){
    EvenRandom r;
    cout << "-- 0에서 " << RAND_MAX << "까지의 랜덤 짝수 정수 10개 : " << endl;
    for(int i = 0; i < 10; i++){
        int n = r.next();
        cout << n << '\t';
    }
    cout << endl << endl << "-- 2에서 10까지의 랜덤 짝수 정수 10개 : " << endl;
    for(int i = 0; i < 10; i++){
        int n = r.nextinRange(2, 10);
        cout << n << '\t';
    }

    return 0;
}

EvenRandom::EvenRandom(){
    srand((unsigned int) time(0));
}

int EvenRandom::next(){
    int ran = rand();
    while(true){
        if(ran % 2 == 0){
            return ran;
        }
        ran = rand();
    }
}

int EvenRandom::nextinRange(int low, int high){
    int ran = rand() % (high - low + 1) + low;
    while(true){
        if(ran % 2 == 0){
            return ran;
        }
        ran = rand() % (high - low + 1) + low;
    }
}
~~~

>> Output

~~~C++
-- 0에서 2147483647까지의 랜덤 짝수 정수 10개 : 
754544228	1733691306	1091657446	454057686	268781690	2138855454	962661234	305563340	433726818	1087132208	

-- 2에서 10까지의 랜덤 짝수 정수 10개 : 
10	10	6	2	2	4	6	4	2	4	
Process finished with exit code 0
~~~

***

# Day 5

## Object

> oval.cpp

~~~C++
#include <iostream>
using namespace std;

class Oval{
    int width, height;
    double getArea();
public:
    Oval();
    Oval(int w, int h);
    ~Oval();
    int getWidth();
    int getHeight();
    void set(int w, int h);
    void show();
};

int main(){
    Oval a, b(3, 4);
    a.set(10, 20);
    a.show();
    b.show();

    return 0;
}

Oval::Oval(){
    width = 1;
    height = 1;
}

Oval::Oval(int w,int h){
    width = w;
    height = h;
}

Oval::~Oval(){
    cout << "Oval 소멸 ";
    show();
}

double Oval::getArea(){
    return 3.14*width*height;
}

int Oval::getWidth(){
    return width;
}

int Oval::getHeight(){
    return height;
}

void Oval::set(int w, int h){
    width = w;
    height = h;
}

void Oval::show(){
    cout << "width = " << width << ", height = " << height << ", Area = " << getArea() << endl;
}
~~~

>> Output

~~~C++
width = 10, height = 20, Area = 628
width = 3, height = 4, Area = 37.68
Oval 소멸 width = 3, height = 4, Area = 37.68
Oval 소멸 width = 10, height = 20, Area = 628

Process finished with exit code 0
~~~

## Object Pointer

+ 객체에 대한 포인터
  + 객체의 주소 값을 가지는 변수
+ 포인터로 멤버를 접근할 때
  + `객체포인터->멤버`

> circle1.cpp

~~~C++
#include <iostream>
using namespace std;

class Circle{
    int radius;
public:
    Circle(){radius = 1;}
    Circle(int r){radius = r;}
    double getArea();
};

int main(){
    Circle donut;
    double d = donut.getArea();

    Circle *p;
    p = &donut;
    double b = p->getArea();

    cout << d << "==" << b << endl;

    return 0;
}

double Circle::getArea(){
    return radius*radius*3.14;
}
~~~

>> Output

~~~C++
3.14==3.14

Process finished with exit code 0
~~~

> circle2.cpp

~~~C++
#include <iostream>
using namespace std;

class Circle{
    int radius;
public:
    Circle(){radius = 1;}
    Circle(int r){radius = r;}
    double getArea();
};

int main(){
    Circle donut;
    Circle pizza(30);

    cout << donut.getArea() << endl;

    Circle *p;
    p = &donut;
    cout << p->getArea() << endl;
    cout << (*p).getArea() << endl;

    p = & pizza;
    cout << p->getArea() << endl;
    cout << (*p).getArea() << endl;

    return 0;
}

double Circle::getArea(){
    return radius*radius*3.14;
}
~~~

>> Output

~~~C++
3.14
3.14
3.14
2826
2826

Process finished with exit code 0
~~~

## Object Array

+ 객체 배열 선언 가능
  + 기본 타이 배열 선언과 형식 동일
    + `Circle c[3];`
+ 객체 배열 선언
  + 객체 배열을 위한 공간 할당
  + 배열의 각 원소 객체마다 생성자 실행
    + 매개변수 없는 생성자 호출
    + 매개변수 있는 생성자를 한번에는 호출할 수 없음
  + `Circle c[3] = {Circle(10), Circle(20), Circle()};`
+ 배열 소멸
  + 배열의 각 객체마다 소멸자 호출
  + 생성의 반대순으로 소멸

> circle1.cpp

~~~C++
#include <iostream>
using namespace std;

class Circle{
    int radius;
public:
    Circle(){radius = 1;}
    Circle(int r){radius = r;}
    double getArea();
    void setRadius(int r){radius = r;}
};

int main(){
    Circle circleArray[3];
    circleArray[0].setRadius(10);
    circleArray[1].setRadius(20);
    circleArray[2].setRadius(30);

    for(int i = 0; i < 3; i++){
        cout << "Circle " << i << "의 면적은 " << circleArray[i].getArea() << endl;
    }

    Circle *p;
    p = circleArray;
    for(int i = 0; i < 3; i++){
        cout << "Circle " << i << "의 면적은 " << p->getArea() << endl;
        p++;
    }

    return 0;
}

double Circle::getArea(){
    return radius*radius*3.14;
}
~~~

>> Output

~~~C++
Circle 0의 면적은 314
Circle 1의 면적은 1256
Circle 2의 면적은 2826
Circle 0의 면적은 314
Circle 1의 면적은 1256
Circle 2의 면적은 2826

Process finished with exit code 0
~~~

> circle2.cpp

~~~C++
#include <iostream>
using namespace std;

class Circle{
    int radius;
public:
    Circle(){radius = 1;}
    Circle(int r){radius = r;}
    void setRadius(int r){radius = r;}
    double getArea(){return 3.14*radius*radius;}
};

int main(){
    Circle c[3] = {Circle(10), Circle(20), Circle()};
    Circle *p = c;

    for(int i = 0; i < 3; i++){
        cout << "c[" << i << "]의 면적은 " << c[i].getArea() << endl;
    }

    for(int i = 0; i < 3; i++){
        cout << "(c+" << i << ")의 면적은 " << (c+i)->getArea() << endl;
    }

    for(int i = 0; i < 3; i++){
        cout << "*(c+" << i << ")의 면적은 " << (*(c+i)).getArea() << endl;
    }

    for(int i = 0; i < 3; i++){
        cout << "p[" << i << "]의 면적은 " << p[i].getArea() << endl;
    }

    for(int i = 0; i < 3; i++){
        cout << "(p+" << i << ")의 면적은 " << (p+i)->getArea() << endl;
    }

    for(int i = 0; i < 3; i++){
        cout << "*(p+" << i << ")의 면적은 " << (*(p+i)).getArea() << endl;
    }

    for(int i = 0; i < 3; i++){
        cout << "p->" << i << "의 면적은 " << p->getArea() <<endl;
        p++;
    }

    return 0;
}
~~~

>> Output

~~~C++
c[0]의 면적은 314
c[1]의 면적은 1256
c[2]의 면적은 3.14
(c+0)의 면적은 314
(c+1)의 면적은 1256
(c+2)의 면적은 3.14
*(c+0)의 면적은 314
*(c+1)의 면적은 1256
*(c+2)의 면적은 3.14
p[0]의 면적은 314
p[1]의 면적은 1256
p[2]의 면적은 3.14
(p+0)의 면적은 314
(p+1)의 면적은 1256
(p+2)의 면적은 3.14
*(p+0)의 면적은 314
*(p+1)의 면적은 1256
*(p+2)의 면적은 3.14
p->0의 면적은 314
p->1의 면적은 1256
p->2의 면적은 3.14

Process finished with exit code 0
~~~

## Dynamic Memory

~~~C++
데이터타입 *포인터변수 = new 데이터타입;
데이터타입 *포인터변수 = new 데이터타입(초기값); // 배열의 초기화는 for문
delete 포인터변수;

데이터타입 *포인터변수 = new 데이터타입[배열의크기]; // 배열의 동적 할당
for(int i = 0; i < 배열의크기; i++){
    포인터변수[i] = 값;
}
delete [] 포인터변수;

클래스이름 *포인터변수 = new 클래스이름; // 객체의 동적 할당
클래스이름 *포인터변수 = new 클래스이름(생성자매개변수리스트);
delete 포인터변수;
~~~

+ 정적 할당
  + 변수 선언을 통해 필요한 메모리 할당
  + 많은 양의 메모리는 배열 선언을 통해 할당
+ 동적 할당
  + 필요한 양이 예측되지 않는 경우, 프로그램 작성 시 할당 받을 수 없음
  + 실행 중에 운영체제로부터 할당 받음
    + 힙(`heap`)으로부터 할당
    + 힙은 운영체제가 소유하고 관리하는 메모리, 모든 프로세스가 공유할 수 있는 메모리
+ `C`의 동적 메모리 할당
  + `malloc()`
  + `free()`
+ `C++`의 동적 메모리 할당, 반환
  + `new` 연산자
    + 기본 타입 메모리 할당, 배열 할당, 객체 할당, 객체 배열 할당
    + 객체의 동적 생성 - 힙 메모리로부터 객체를 위한 메모리 할당 요청
    + 객체 할당 시 생성자 호출
  + `delete`
    + `new`로 할당 받은 메모리 반환
    + 객체의 동적 소멸 - 소멸자 호출 뒤 객체를 힙에 반환

|Data Type|정적 할당|동적 할당|
|:--:|:--:|:--:|
|Integer|`int a = val; int *pa = &a;`|`int *p = new int(val);`|
|Array|`int arr[num];`|`int *parr = new int[100];`|
|Object|`Class instance(val); Class *pc = &instance;`|`Class *pc = new Class;`|

> circle.cpp

~~~C++
#include <iostream>
using namespace std;

class Circle{
    int radius;
public:
    Circle(){radius = 1; cout << "생성자 실행" << endl;}
    Circle(int r){radius = r; cout << "생성자 실행" << endl;}
    ~Circle(){cout << "소멸자 실행" << endl;}
    double getArea(){return 3.14*radius*radius;}
};

int main(){
    int radius;
    while(true){
        cout << "정수 반지름 입력(음수이면 종료 >> ";
        cin >> radius;
        if(radius < 0) break;
        Circle *p = new Circle(radius);
        cout << "원의 면적은 " << p->getArea() << endl;
        delete p;
    }
    return 0;
}
~~~

>> Output

~~~C++
정수 반지름 입력(음수이면 종료 >> 5
생성자 실행
원의 면적은 78.5
소멸자 실행
정수 반지름 입력(음수이면 종료 >> 9
생성자 실행
원의 면적은 254.34
소멸자 실행
정수 반지름 입력(음수이면 종료 >> -1

Process finished with exit code 0
~~~

## This Pointer

+ 현재의 실행중인 객체를 가리키는 `pointer` 변수
+ 포인터, 객체 자신 포인터
+ 클래스의 멤버 함수 내에서만 사용
+ 개발자가 선언하는 변수가 아닌 컴파일러가 선언한 변수
+ 용도
  + 매개변수 이름 == 멤버 변수 이름
  + 매개변수가 자신의 객체주소를 `return`
+ 사용범위
  + 멤버 함수

## Quiz

> quiz1.cpp

~~~C++
#include <iostream>
using namespace std;

class Sample{
    int *p;
    int size;
public:
    Sample(int n){
        size = n; p = new int[n];
    }
    void read();
    void write();
    int big();
    int getSize(){return size;}
    ~Sample(){delete [] p;}
};

int main(){
    Sample s(10);
    s.read();
    cout << "동적배열 정수 " << s.getSize() << "개를 출력합니다. ";
    s.write();
    cout << "가장 큰 수는 " << s.big() << endl;

    return 0;
}

void Sample::read(){
    cout << "입력하려는 정수의 개수는? ";
    cin >> size;
    cout << size << "개의 정수를 입력하시오. ";
    for(int i = 0; i < size; i++)
        cin >> p[i];
}
void Sample::write(){
    for(int i = 0; i < size; i++)
        cout << p[i] << ' ';
    cout << endl;
}
int Sample::big(){
    int b = p[0];
    for(int i = 0; i < size; i++){
        b = (b < p[i]) ? p[i] : b;
    }
    return b;
}
~~~

>> Output

~~~C++
입력하려는 정수의 개수는? 5
5개의 정수를 입력하시오. 11 22 44 55 23
동적배열 정수 5개를 출력합니다. 11 22 44 55 23 
가장 큰 수는 55

Process finished with exit code 0
~~~

> quiz2.cpp

~~~C++
#include <iostream>
using namespace std;

class Circle{
    int radius;
public:
    Circle(){radius = 1;}
    Circle(int r){radius = 1;}
    void setRadius(int r){radius = r;}
    int getRadius(){return radius;}
    double getArea(){return 3.14 * radius * radius;}
};

class Sample{
    Circle *p;
    int size;
public:
    Sample(int n){
        size = n; p = new Circle[n];
    }
    void read();
    void write();
    Circle big();
    int getSize(){return size;}
    ~Sample(){delete [] p;}
};

int main(){
    Sample s(10);
    s.read();
    cout << "각 원 객체의 반지름 " << s.getSize() << "개를 출력합니다. ";
    s.write();
    Circle big = s.big();
    cout << "가장 큰 원의 넓이 : " << big.getArea() << "\t 가장 큰 원의 반지름 : " << big.getRadius() << endl;

    return 0;
}

void Sample::read(){
    int num;
    cout << "입력하려는 원의 개수는? ";
    cin >> size;
    cout << size << "개의 원의 반지름을 입력하시오. ";
    for(int i = 0; i < size; i++){
        cin >> num;
        p[i].setRadius(num);
    }
}
void Sample::write(){
    for(int i = 0; i < size; i++)
        cout << p[i].getRadius() << ' ';
    cout << endl;
}
Circle Sample::big(){
    Circle b = p[0];
    for(int i = 0; i < size; i++){
        b.setRadius((b.getRadius() < p[i].getRadius()) ? p[i].getRadius() : b.getRadius());
    }
    return b;
}
~~~

>> Output

~~~C++
입력하려는 원의 개수는? 3
3개의 원의 반지름을 입력하시오. 3 16 2
각 원 객체의 반지름 3개를 출력합니다. 3 16 2 
가장 큰 원의 넓이 : 803.84	 가장 큰 원의 반지름 : 16

Process finished with exit code 0
~~~

***

# Day 6

## string

+ 문자열 생성
  + `string str0("name");`
  + `string str1 = "name";`
  + `string str2(str);` - 복사생성자
  + 주의 : 문자열 끝에 `'\0(NULL)`가 없음
+ 문자열 연산자
  + 산술 연산자
    + `+=`, `+`
  + 관계 연산자
    + `>=`, `<=`, `>`, `<`, `!=`, `==`
    + 비교는 사전식
  + 배열처럼 사용 가능
+ 문자열 변환 함수
  + 문자열 -> 숫자
    + `stoi();`
    + `stof();`
    + `stod();`
  + 숫자 -> 문자열
    + `to_string();`
  + 문자열 -> C언어 문자열(`\0`)
    + `str.c_str();`
+ 문자열 크기 함수
  + `str.size();`
  + `str.length();`
  + `str.capacity();` - 시스템이 정해줌
+ 문자열 조작 함수
  + `str.append(string);`
    + 문자열 뒤에 파라미터의 문자열 추가
  + `str.substr(시작 index, 크기);`
    + 시작부터 크기만큼 추출
  + `str.replace(index, length, string);`
    + `index`에서 `length`만큼 `string`으로 대체
  + `str.find(string, index);`
    + `index`부터 `string`이 시작하는 위치 `int`값으로 `return`
  + `str.resize(unsigned, char);`
    + 숫자만큼의 크기로 바꾸며 남는다면 `char`으로 채움

> string1.cpp

~~~C++
#include <iostream>
using namespace std;

int main(){
    string str;
    string address("서울시 서울시 서울시");
    string copyAddress(address);

    char text[] = {'L', 'O', 'V', 'E', ' ', 'C', '+', '+', '\0'};
    string title(text);

    cout << str << endl;
    cout << address << endl;
    cout << copyAddress << endl;
    cout << title << endl;

    return 0;
}
~~~

>> Output

~~~C+

서울시 서울시 서울시
서울시 서울시 서울시
LOVE C++

Process finished with exit code 0
~~~

> string2.cpp

~~~C++
#include <iostream>
using namespace std;

int main(){
    string str;

    cout << "문자열을 입력하세요 : ";

    getline(cin, str, '\n');
    int len = str.length();

    for(int i = 0; i < len; i++){
        string first = str.substr(0, 1);
        string sub = str.substr(1, len-1);
        str = sub + first;
        cout << str <<endl;
    }

    return 0;
}
~~~

>> Output

~~~C++
문자열을 입력하세요 : asdfasdfasdfasdf
sdfasdfasdfasdfa
dfasdfasdfasdfas
fasdfasdfasdfasd
asdfasdfasdfasdf
sdfasdfasdfasdfa
dfasdfasdfasdfas
fasdfasdfasdfasd
asdfasdfasdfasdf
sdfasdfasdfasdfa
dfasdfasdfasdfas
fasdfasdfasdfasd
asdfasdfasdfasdf
sdfasdfasdfasdfa
dfasdfasdfasdfas
fasdfasdfasdfasd
asdfasdfasdfasdf

Process finished with exit code 0
~~~

> string3.cpp

~~~C++
#include <iostream>
using namespace std;

class Date{
    string year;
    string month;
    string day;
public:
    Date(int y, int m, int d){year = to_string(y); month = to_string(m); day = to_string(d);}
    Date(string when);
    void show();
    string getYear(){return year;}
    string getMonth(){return month;}
    string getDay(){return day;}
};

int main(){
    Date birth(2014, 3, 20);
    Date independenceDay("1945/8/15");
    independenceDay.show();
    birth.show();
    cout << birth.getYear() << ',' << birth.getMonth() << ',' << birth.getDay() << endl;

    return 0;
}

Date::Date(string when){
    int where1;
    int where2;
    where1 = when.find('/');
    year = when.substr(0, where1);
    where2 = when.find('/', where1 + 1);
    month = when.substr(where1 + 1, where2 - where1 - 1);
    day = when.substr(where2 + 1, when.size());
}
void Date::show(){
    cout << year << "년" << month << "월" << day << "일" << endl;
}
~~~

>> Output

~~~C++
1945년8월15일
2014년3월20일
2014,3,20

Process finished with exit code 0
~~~

## Call by Reference

~~~C++
int n = 0;
int &refn = n;

class c;
class &refc = c;
~~~

+ 참조 변수
  + 참조자 `&`의 도입
  + 이미 존재하는 변수에 대한 다른 이름(별명)을 선언
    + 참조 변수는 이름만 존재
    + 참조 변수에 새로운 공간 할당 X
    + 초기화로 지정된 기존 변수 공유

> reference1.cpp

~~~C++
#include <iostream>
using namespace std;

int main(){
    cout << 'i' << '\t' << 'n' << '\t' << "refn" << endl;

    int i = 1;
    int n = 2;
    int &refn = n;
    n = 4;
    refn++;
    cout << i << '\t' << n << '\t' << refn << endl;

    refn = i;
    refn++;
    cout << i << '\t' << n << '\t' << refn << endl;

    int *p = &refn;
    *p = 20;
    cout << i << '\t' << n << '\t' << refn << endl;

    return 0;
}
~~~

>> Output

~~~C++
i	n	refn
1	5	5
1	2	2
1	20	20

Process finished with exit code 0
~~~

> reference2.cpp

~~~C++
#include <iostream>
using namespace std;

class Circle{
    int radius;
public:
    Circle(){radius = 1;}
    Circle(int radius){this->radius = radius;}
    void setRadius(int radius){this->radius = radius;}
    double getArea(){return 3.14*radius*radius;}
};

void readRadius(Circle &c);

int main(){
    Circle donut;
    readRadius(donut);
    cout << "donut의 면적 = " << donut.getArea() << endl;

    return 0;
}

void readRadius(Circle &c){
    int r;
    cout << "정수 값으로 반지름을 입력하세요 >> ";
    cin >> r;
    c.setRadius(r);
}
~~~

>> Output

~~~C++
정수 값으로 반지름을 입력하세요 >> 3
donut의 면적 = 28.26

Process finished with exit code 0
~~~

> reference3.cpp

~~~C++
#include <iostream>
using namespace std;

class MyintStack{
    int p[10];
    int tos;
public:
    MyintStack();
    bool push(int n);
    bool pop(int &refn);
};

int main(){
    MyintStack a;
    for(int i = 0; i < 11; i++){
        if(a.push(i))
            cout << i << '\t';
        else
            cout << endl << i + 1 << "번째 stack full" << endl;
    }
    int n;
    for(int i = 0; i < 11; i++){
        if(a.pop(n))
            cout << n << '\t';
        else
            cout << endl << i + 1 << "번째 stack empty" << endl;
    }

    return 0;
}

MyintStack::MyintStack(){
    tos = 0;
}
bool MyintStack::push(int n){
    if(tos == 10)
        return false;
    p[tos] = n;
    tos++;
    return true;
}
bool MyintStack::pop(int &refn){
    if(tos == 0)
        return false;
    tos--;
    refn = p[tos];
    return true;
}
~~~

>> Output

~~~C++
0	1	2	3	4	5	6	7	8	9	
11번째 stack full
9	8	7	6	5	4	3	2	1	0	
11번째 stack empty

Process finished with exit code 0
~~~

## Quiz

> quiz.cpp

~~~C++
#include <iostream>
#include <string>
#include <cstdlib>
#include <ctime>
using namespace std;

class Player{
    string name;
public:
    Player(string name = ""){
        this->name = name;
    }
    void setName(string name){this->name = name;}
    string getName(){return name;}
    void getEnterKey(){
        char buf[100];
        cin.getline(buf, 99);
    }
};

class GamblingGame{
    Player p[2];
    int num[3];
    bool matchAll();
public:
    GamblingGame();
    void run();
};

int main(){
    GamblingGame game;
    game.run();

    return 0;
}

GamblingGame::GamblingGame(){
    cout << "***** 갬블링 게임을 시작합니다. *****" << endl;
    srand((unsigned int) time(0));
    for(int i = 0; i < 3; i++)
        num[i] = 0;
    cout << "첫번째 선수 이름>>";
    string name;
    cin >> name;
    p[0].setName(name);
    cout << "두번째 선수 이름>>";
    cin >> name;
    p[1].setName(name);
}
void GamblingGame::run(){
    string n;
    int i = 0;
    for(;;){
        cout << p[i % 2].getName() << " : <Enter>";
        if(i == 0)
            cout << endl;
        p[i % 2].getEnterKey();
        if(this->matchAll()){
            cout << p[i % 2].getName() << "님 승리!!" << endl;
            break;
        }
        else
            cout << "아쉽군요!" << endl;
        i++;
    }
}
bool GamblingGame::matchAll(){
    cout << "\t";
    for (int i = 0; i < 3; i++){
        int n = rand() % 3;
        num[i] = n;
        cout << num[i] << "\t";
    }
    if (num[0] == num[1] && num[0] == num[2])
        return true;
    else
        return false;
}
~~~

>> Output

~~~C++
***** 갬블링 게임을 시작합니다. *****
첫번째 선수 이름>>Kim
두번째 선수 이름>>Park
Kim : <Enter>
	0	1	1	아쉽군요!
Park : <Enter>
	2	0	2	아쉽군요!
Kim : <Enter>
	1	2	1	아쉽군요!
Park : <Enter>
	1	1	1	Park님 승리!!

Process finished with exit code 0
~~~

***

# Day 7

## Dynamic Memory

> stack.cpp

~~~C++
#include <iostream>
using namespace std;

class MyintStack{
    int *parr;
    int tos;
public:
    MyintStack(int size);
    bool push(int n);
    bool pop(int &refn);
    ~MyintStack(){delete [] parr;}
};

int main(){
    MyintStack a(10);
    for(int i = 0; i < 11; i++){
        if(a.push(i))
            cout << i << '\t';
        else
            cout << endl << i + 1 << "번째 stack full" << endl;
    }
    int n;
    for(int i = 0; i < 11; i++){
        if(a.pop(n))
            cout << n << '\t';
        else
            cout << endl << i + 1 << "번째 stack empty" << endl;
    }

    return 0;
}

MyintStack::MyintStack(int size){
    tos = 0;
    parr = new int[size];
}
bool MyintStack::push(int n){
    if(tos == 10)
        return false;
    parr[tos] = n;
    tos++;
    return true;
}
bool MyintStack::pop(int &refn){
    if(tos == 0)
        return false;
    tos--;
    refn = parr[tos];
    return true;
}
~~~

>> Output

~~~C++
0	1	2	3	4	5	6	7	8	9	
11번째 stack full
9	8	7	6	5	4	3	2	1	0	
11번째 stack empty

Process finished with exit code 0
~~~

## Return Reference

> return_ref1.cpp

~~~C++
#include <iostream>
using namespace std;

char c = 'a';

char &find(){
    return c;
}

int main(){
    char a = find();
    cout << a << endl;

    char &ref = find();
    cout << ref << endl;

    find() = 'b';
    cout << find() << endl;

    return 0;
}
~~~

>> Output

~~~C++
a
a
b

Process finished with exit code 0
~~~

> return_ref2.cpp

~~~C++
#include <iostream>
using namespace std;

char &find(char s[], int index){
    return s[index];
}

int main(){
    char name[] = "Zerohertz";
    cout << name << endl;

    find(name, 0) = '5';
    cout << name << endl;

    char &ref = find(name, 2);
    ref = 't';
    cout << name << endl;

    return 0;
}
~~~

>> Output

~~~C++
Zerohertz
5erohertz
5etohertz

Process finished with exit code 0
~~~

> reference.cpp

~~~C++
#include <iostream>
using namespace std;

void addConst(int &x, int y){
    x = x + 200;
    y = y + 200;
    cout << "addConst" << endl;
    cout << "&x = " << &x << "\tx = " << x << endl;
    cout << "&y = " << &y << "\ty = " << y << endl;
}

int main(){
    int a = 100;
    int b = 100;
    addConst(a, b);
    cout << "Main" << endl;
    cout << "&a = " << &a << "\ta = " << a << endl;
    cout << "&b = " << &b << "\tb = " << b << endl;

    return 0;
}
~~~

>> Output

~~~C++
addConst
&x = 0x7ffee84d09a8	x = 300
&y = 0x7ffee84d0964	y = 300
Main
&a = 0x7ffee84d09a8	a = 300
&b = 0x7ffee84d09a4	b = 100

Process finished with exit code 0
~~~

> return_ref3.cpp

~~~C++
#include <iostream>
using namespace std;

int &addConst(int &x, int y){
    x = x + 200;
    y = y + 200;
    cout << "addConst" << endl;
    cout << "&x = " << &x << "\tx = " << x << endl;
    cout << "&y = " << &y << "\ty = " << y << endl;
    return x;
}

int main(){
    int a = 100;
    int b = 100;
    addConst(a, b) = 555;
    cout << "Main" << endl;
    cout << "&a = " << &a << "\ta = " << a << endl;
    cout << "&b = " << &b << "\tb = " << b << endl;

    return 0;
}
~~~

>> Output

~~~C++
addConst
&x = 0x7ffee834b9a8	x = 300
&y = 0x7ffee834b964	y = 300
Main
&a = 0x7ffee834b9a8	a = 555
&b = 0x7ffee834b9a4	b = 100

Process finished with exit code 0
~~~

## Shallow Copy & Deep Copy

+ Shallow copy
  + 객체 복사 시, 객체의 멤버를 1:1로 복사
  + 객체의 멤버 변수에 동적 메모리가 할당된 경우
    + 사본은 원본 객체가 할당 받은 메모리를 공유하는 문제 발생
+ Deep copy
  + 객체 복사 시, 객체의 멤버를 1:1로 복사
  + 객체의 멤버 변수에 동적 메모리가 할당된 경우
    + 사본은 원본이 가진 메모리 크기만큼 별도로 동적 할당
    + 원본의 동적 메모리에 있는 내용을 사본에 복사
  + 완전한 형태의 복사
    + 사본과 원본은 메모리를 공유하는데 문제 없음

> shallow1_copy.cpp

~~~C++
#include <iostream>
using namespace std;

int main(){
    int *a = new int(3);
    int *b = new int(5);
    cout << "a의 주소(복사전) : " << a << endl;
    cout << "b의 주소(복사전) : " << b << endl;

    a = b;

    cout << "a의 주소(복사후) : " << a << endl;
    cout << "b의 주소(복사후) : " << b << endl;

    cout << "a의 값 : " << *a << endl;
    cout << "b의 값 : " << *b << endl;

    delete a;
    delete b;

    return 0;
}
~~~

>> Output

~~~C++
untitled(997,0x11451edc0) malloc: *** error for object 0x7fefdc405980: pointer being freed was not allocated
untitled(997,0x11451edc0) malloc: *** set a breakpoint in malloc_error_break to debug
a의 주소(복사전) : 0x7fefdc405970
b의 주소(복사전) : 0x7fefdc405980
a의 주소(복사후) : 0x7fefdc405980
b의 주소(복사후) : 0x7fefdc405980
a의 값 : 5
b의 값 : 5

Process finished with exit code 6
~~~

> shallow2_copy.cpp

~~~C++
#include <iostream>
#include <cstring>
#pragma warning(disable:4996)
using namespace std;

class Person{
    char *name;
    int id;
public:
    Person(Person &p){
        this->name = p.name;
        this->id = p.id;
    }
    Person(int id, const char *name);
    ~Person();
    void changeName(const char *name);
    void show(){cout << id << ',' << name << endl;}
};

int main(){
    Person zerohertz(1, "zerohertz");
    Person zhz(zerohertz);

    cout << "***** zhz 객체 생성 후 *****" << endl;
    zerohertz.show();
    zhz.show();

    zhz.changeName("0Hz");
    cout << "***** zhz 이름 변경 후 *****" << endl;
    zerohertz.show();
    zhz.show();

    return 0; // zhz, zerohertz 순으로 소멸, zerohertz 소멸 시 오류
}

Person::Person(int id, const char *name){
    this->id = id;
    int len = strlen(name);
    this->name = new char[len + 1];
    strcpy(this->name, name);
}
Person::~Person(){
    delete [] name;
}
void Person::changeName(const char *name){
    if(strlen(name) > strlen(this->name))
        return;
    strcpy(this->name, name);
}
~~~

>> Output

~~~C++
untitled(1347,0x11c7dddc0) malloc: *** error for object 0x7f9184c05970: pointer being freed was not allocated
untitled(1347,0x11c7dddc0) malloc: *** set a breakpoint in malloc_error_break to debug
***** zhz 객체 생성 후 *****
1,zerohertz
1,zerohertz
***** zhz 이름 변경 후 *****
1,0Hz
1,0Hz

Process finished with exit code 6
~~~

## Copy Constructor

> copy_constructor1.cpp

~~~C++
#include <iostream>
#include <cstring>
#pragma warning(disable:4996)
using namespace std;

class Person{
    char *name;
    int id;
public:
    Person(Person &p);
    Person(int id, const char *name);
    ~Person();
    void changeName(const char *name);
    void show(){cout << id << ',' << name << endl;}
};

int main(){
    Person zerohertz(1, "zerohertz");
    Person zhz(zerohertz);

    cout << "***** zhz 객체 생성 후 *****" << endl;
    zerohertz.show();
    zhz.show();

    zhz.changeName("0Hz");
    cout << "***** zhz 이름 변경 후 *****" << endl;
    zerohertz.show();
    zhz.show();

    return 0;
}

Person::Person(Person &p){
    this->id = p.id;
    int len = strlen(p.name);
    this->name = new char[len + 1];
    strcpy(this->name, p.name);
    cout << "복사 생성자 실행, 원본 객체의 이름 : " << this->name << endl;
}
Person::Person(int id, const char *name){
    this->id = id;
    int len = strlen(name);
    this->name = new char[len + 1];
    strcpy(this->name, name);
}
Person::~Person(){
    delete [] name;
}
void Person::changeName(const char *name){
    if(strlen(name) > strlen(this->name))
        return;
    strcpy(this->name, name);
}
~~~

>> Output

~~~C++
복사 생성자 실행, 원본 객체의 이름 : zerohertz
***** zhz 객체 생성 후 *****
1,zerohertz
1,zerohertz
***** zhz 이름 변경 후 *****
1,zerohertz
1,0Hz

Process finished with exit code 0
~~~

> copy_constructor2.cpp

~~~C++
#include <iostream>
#pragma warning(disable:4996)
using namespace std;

class MyString{
    char *pBuf;
public:
    MyString(const char *s = NULL);
    MyString(MyString &MyStr);
    ~MyString();
    void print();
    int getSize();
};

int main(){
    MyString str1;
    MyString str2("Hello");
    MyString str3("World!");
    MyString str4(str3);
    str1.print();
    str2.print();
    str3.print();
    str4.print();

    return 0;
}

MyString::MyString(const char *s){
    if(s == NULL){
        pBuf = new char[1];
        pBuf[0] = NULL;
    }
    else{
        pBuf = new char[strlen(s) + 1];
        strcpy(pBuf, s);
    }
}
MyString::MyString(MyString &MyStr){
    int len = MyStr.getSize();
    this->pBuf = new char[len + 1];
    strcpy(this->pBuf, MyStr.pBuf);
}
MyString::~MyString(){
    if(pBuf) delete [] pBuf;
}
void MyString::print(){
    cout << pBuf << endl;
}
int MyString::getSize(){
    return strlen(pBuf);
}
~~~

>> Output

~~~C++

Hello
World!
World!

Process finished with exit code 0
~~~

**객체에서 동적 메모리 사용 시 복사 생성자 직접 생성**

***

# Day 9

## Polymorphism(다형성)

+ Overloading
  + 함수 중복
  + 연산자 중복
  + Default Parameter
+ Overriding
  + 함수 재정의

## Function Overloading

+ 다른 함수로 인식
+ 함수의 이름 동일
+ 함수의 매개변수 type, 개수 다름
+ return type 무관
+ 소멸자 불가 - 매개변수 X
+ 모호하지 않게 선언

> overloading.cpp

~~~C++
#include <iostream>
using namespace std;

int big(int a, int b){
    if(a > b) return a;
    else return b;
}

int big(int a[], int size){
    int res = a[0];
    for(int i = 1; i < size; i++)
        if(res < a[i]) res = a[i];
    return res;
}

int main(){
    int array[5] = {1, 9, -2, 8, 6};
    cout << big(2, 3) << endl;
    cout << big(array, 5) << endl;
    
    return 0;
}
~~~

>> Output

~~~C++
3
9

Process finished with exit code 0
~~~

## Default Parameter

+ 사전에 값을 선언한 함수의 매개변수
+ 생략 가능
+ 일반 매개변수 뒤에 존재

> default_param.cpp

~~~C++
#include <iostream>
using namespace std;

void f(char c=' ', int line = 1);

int main(){
    f();
    f('%');
    f('@', 5);

    return 0;
}

void f(char c, int line){
    for(int i = 0; i < line; i++){
        for(int j = 0; j < 10; j++){
            cout << c;
        }
        cout << endl;
    }
}
~~~

>> Output

~~~C++
          
%%%%%%%%%%
@@@@@@@@@@
@@@@@@@@@@
@@@@@@@@@@
@@@@@@@@@@
@@@@@@@@@@

Process finished with exit code 0
~~~

> myvec.cpp

~~~C++
#include <iostream>
using namespace std;

class MyVector{
    int *p;
    int size;
public:
    MyVector(int n = 100){p = new int[n]; size = n;}
    ~MyVector(){delete [] p;}
};

int main(){
    MyVector *v1, *v2;
    v1 = new MyVector();
    v2 = new MyVector();

    delete v1;
    delete v2;

    return 0;
}
~~~

>> Output

~~~C++
Process finished with exit code 0
~~~

## Static & Non-static

+ `static`
  + 변수와 함수에 대한 기억 부류의 한 종류
    + 생명 주기 : 프로그램이 시작될 때 생성, 프로그램 종료 시 소멸
    + 사용 범위 : 선언된 범위, 접근 지정에 따름
  + 전역 변수나 전역변수를 클래스에 캡슐화
    + 전역 변수나 전역 함수를 가능한 사용하지 않도록
    + 전역 변수나 전역 함수를 `static`으로 선언하여 클래스 멤버로 선언
  + 객체 사이에 공유 변수를 만들고자 할 때
    + `static` 멤버를 선언하여 모든 객체들이 공유
+ 클래스의 멤버
  + `static`
    + 프로그램이 시작할 때 생성
    + 클래스당 한번만 생성, 클래스 멤버라고 불림
    + 클래스의 모든 인스턴스(객체)들이 공유하는 멤버
  + non-`static`
    + 객체가 생성될 때 함께 생성
    + 객체마다 객체 내에 생성
    + 인스턴스 멤버라고 불림

> person.cpp

~~~C++
#include <iostream>
using namespace std;

class Person{
public:
    double money;
    void addMoney(int money){
        this->money += money;
    }
    static int sharedMoney;
    static void addShared(int n){
        sharedMoney += n;
    }
};

int Person::sharedMoney = 10;

int main(){
    Person han;
    han.money = 100;
    han.sharedMoney = 200;

    Person lee;
    lee.money = 150;
    lee.addMoney(200);
    lee.addShared(200);

    cout << han.money << '\t' << lee.money << endl;
    cout << han.sharedMoney << '\t' << lee.sharedMoney << endl;

    Person::sharedMoney = 1000;
    Person::addShared(20000);

    cout << han.money << '\t' << lee.money << endl;
    cout << han.sharedMoney << '\t' << lee.sharedMoney << endl;

    return 0;
}
~~~

>> Output

~~~C++
100	350
400	400
100	350
21000	21000

Process finished with exit code 0
~~~

> employee.cpp

~~~C++
#include <iostream>
using namespace std;

class Employee{
    string name;
    double salary;
    int static count;
public:
    Employee(string name = "", double salary = 0):name(name), salary(salary){
        this->count++;
    }
    int static getCount(){
        return count;
    }
    ~Employee(){
        this->count--;
    }
};

int Employee::count = 0;

int main(){
    Employee e1("김철수");
    Employee e2;
    Employee e3("김철호", 20000);

    int n = Employee::getCount();
    cout << "현재의 직원 수 : " << n << endl;

    return 0;
}
~~~

>> Output

~~~C++
현재의 직원 수 : 3

Process finished with exit code 0
~~~

> circle.cpp

~~~C++
#include <iostream>
using namespace std;

class Circle{
private:
    static int numOfCircles;
    int radius;
public:
    Circle(int r = 1):radius(r){numOfCircles++;}
    ~Circle(){numOfCircles--;}
    double getArea(){return 3.14*radius*radius;}
    static int getNumOfCircles(){return numOfCircles;}
};

int Circle::numOfCircles = 0;

int main(){
    Circle *p = new Circle[10];
    cout << "할당된 원의 개수 : " << Circle::getNumOfCircles() << endl;

    delete [] p;
    cout << "할당된 원의 개수 : " << Circle::getNumOfCircles() << endl;

    Circle a;
    cout << "할당된 원의 개수 : " << Circle::getNumOfCircles() << endl;

    Circle b;
    cout << "할당된 원의 개수 : " << Circle::getNumOfCircles() << endl;

    return 0;
}
~~~

>> Output

~~~C++
할당된 원의 개수 : 10
할당된 원의 개수 : 0
할당된 원의 개수 : 1
할당된 원의 개수 : 2

Process finished with exit code 0
~~~

### Timeline of Program

1. 프로그램 시작
   + 전역 변수
   + `static` 멤버
     + 멤버 변수
     + 멤버 함수
2. 객체
   + non-`static` 멤버
3. 객체 종료
   + non-`static` 멤버 종료
4. 프로그램 끝
   + 전역 변수 종료
   + `static` 멤버 종료

### Access

+ `static` 멤버 함수 -> `static` 멤버 변수 : 가능
+ `static` 멤버 함수 -> non-`static` 멤버 변수 : 불가능
+ `static` 멤버 함수 -> non-`static` 멤버 함수 : 불가능
+ non-`static` 멤버 함수 -> non-`static` 멤버 변수 : 가능
+ non-`static` 멤버 함수 -> `static` 멤버 변수 : 가능
+ non-`static` 멤버 함수 -> `static` 멤버 함수 : 가능
+ `static` 멤버 함수가 접근할 수 있는 것
  + `static` 멤버 함수
  + `static` 멤버 변수
  + 함수 내의 지역 변수

~~~C++
this->sharedMoney += n; // static 이후 객체 생성 - 오류
~~~

## Quiz

> quiz.cpp

~~~C++
#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

class Random{
public:
    void static seed(){srand(time(NULL));}
    int static nextInt(int start, int end);
    char static nextAlphabet();
    double static nextDouble();
};

int main(){
    Random::seed();
    cout << "1에서 100까지 랜덤한 정수 10개를 출력합니다." << endl;
    for(int i = 0; i < 10; i++) cout << Random::nextInt(1, 100) << '\t';
    cout << endl;

    cout << "알파벳을 랜덤하게 10개를 출력합니다." << endl;
    for(int i = 0; i < 10; i++) cout << Random::nextAlphabet() << '\t';
    cout << endl;

    cout << "랜덤한 실수를 10개 출력합니다." << endl;
    for(int i = 0; i < 5; i++) cout << Random::nextDouble() << '\t';
    cout << endl;
    for(int i = 0; i < 5; i++) cout << Random::nextDouble() << '\t';

    return 0;
}

int Random::nextInt(int start, int end){
    return rand() % (end - start + 1) + start;
}
char Random::nextAlphabet(){
    int num;
    while(true){
        num = nextInt(65, 122);
        if(num >= 91 && num <= 96){
            continue;
        }
        else{
            return num;
        }
    }
}
double Random::nextDouble(){
    return (double) rand() / RAND_MAX;
}
~~~

>> Output

~~~C++
1에서 100까지 랜덤한 정수 10개를 출력합니다.
47	98	79	68	45	18	87	76	88	15	
알파벳을 랜덤하게 10개를 출력합니다.
l	K	W	k	d	d	y	f	X	X	
랜덤한 실수를 10개 출력합니다.
0.891485	0.195258	0.707381	0.95967	0.167292	
0.673519	0.836099	0.318814	0.307098	0.397495
~~~

***

# Day 10

## Friend

+ 클래스의 멤버 함수가 아닌 외부 함수
  + 전역 함수
  + 다른 클래스의 멤버 함수
+ `friend`로 클래스 내에 선언된 함수
  + 클래스의 모든 멤버를 접근할 수 있는 권한 부여
  + 프렌드 함수라고 부름
+ friend
  + 전역 함수
  + 다른 클래스의 멤버 함수
  + 다른 클래스 전체

> friend1.cpp

~~~C++
#include <iostream>
using namespace std;

class Rect;
bool equals(Rect r, Rect s);

class Rect{
    int width, height;
public:
    Rect(int width, int height):width(width), height(height){};
    friend bool equals(Rect r, Rect s);
};

int main(){
    Rect a(3, 4), b(4, 5);
    if(equals(a, b)) cout << "equal" << endl;
    else cout << "not equal" << endl;

    return 0;
}

bool equals(Rect r, Rect s){
    if(r.width == s.width && r.height == s.height) return true;
    else return false;
}
~~~

> friend2.cpp

~~~C++
#include <iostream>
using namespace std;

class Rect;
bool equals(Rect r, Rect s);

class RectManager{
public:
    bool equals(Rect r, Rect s);
};

class Rect{
    int width, height;
public:
    Rect(int width, int height):width(width), height(height){};
    friend bool RectManager::equals(Rect r, Rect s);
};

int main(){
    Rect a(3, 4), b(4, 5);
    RectManager Man;
    if(Man.equals(a, b)) cout << "equal" << endl;
    else cout << "not equal" << endl;

    return 0;
}

bool RectManager::equals(Rect r, Rect s){
    if(r.width == s.width && r.height == s.height) return true;
    else return false;
}
~~~

> friend3.cpp

~~~C++
#include <iostream>
using namespace std;

class Rect;
bool equals(Rect r, Rect s);

class RectManager{
public:
    bool equals(Rect r, Rect s);
};

class Rect{
    int width, height;
public:
    Rect(int width, int height):width(width), height(height){};
    friend RectManager;
};

int main(){
    Rect a(3, 4), b(4, 5);
    RectManager Man;
    if(Man.equals(a, b)) cout << "equal" << endl;
    else cout << "not equal" << endl;

    return 0;
}

bool RectManager::equals(Rect r, Rect s){
    if(r.width == s.width && r.height == s.height) return true;
    else return false;
}
~~~

>> Output

~~~C++
not equal

Process finished with exit code 0
~~~

## Operator Overloading

~~~C++
리턴타입 operator연산자(매개변수)
~~~

+ `C++`에 본래 있는 연산자만 중복 가능
+ 피 연산자 타입이 다른 새로운 연산 정의
+ 연산자는 함수 형태로 구현 - 연산자 함수(Operator function)
  + 클래스의 멤버 함수로 구현
  + 외부 함수로 구현하고 클래스에 프렌드 함수로 선언
+ 반드시 클래스와 관계를 가짐
+ 피연산자의 개수를 바꿀 수 없음
+ 연산의 우선 순위 변경 안됨
+ 모든 연산자가 중복 가능하진 않음

> power_by_member_function.cpp

~~~C++
#include <iostream>
using namespace std;

class Power{
    int kick;
    int punch;
public:
    Power(int kick = 0, int punch = 0):kick(kick), punch(punch){}
    void show();
    Power operator+(Power op2);
};

int main(){
    Power a(3, 5), b(4, 6), c;
    c = a + b; // a.operator+(b)
    a.show();
    b.show();
    c.show();

    return 0;
}

void Power::show(){
    cout << "Kick = " << kick << ',' << " Punch = " << punch << endl;
}
Power Power::operator+(Power op2){
    Power tmp;
    tmp.kick = this->kick + op2.kick;
    tmp.punch = this->punch + op2.punch;
    return tmp;
}
~~~

> power_by_friend_function.cpp

~~~C++
#include <iostream>
using namespace std;

class Power{
    int kick;
    int punch;
public:
    Power(int kick = 0, int punch = 0):kick(kick), punch(punch){}
    void show();
    friend Power operator+(Power op1, Power op2);
};

int main(){
    Power a(3, 5), b(4, 6), c;
    c = a + b; // operator+(a, b)
    a.show();
    b.show();
    c.show();

    return 0;
}

void Power::show(){
    cout << "Kick = " << kick << ',' << " Punch = " << punch << endl;
}
Power operator+(Power op1, Power op2){
    Power tmp;
    tmp.kick = op1.kick + op2.kick;
    tmp.punch = op1.punch + op2.punch;
    return tmp;
}
~~~

>> Output

~~~C++
Kick = 3, Punch = 5
Kick = 4, Punch = 6
Kick = 7, Punch = 11

Process finished with exit code 0
~~~

> cpoint_by_member_function.cpp

~~~C++
#include <iostream>
using namespace std;

class CPoint{
    int x, y;
public:
    CPoint(int a = 0, int b = 0):x(a), y(b){}
    CPoint operator-();
    void Print(){cout << '(' << x << ',' << y << ')' << endl;}
};

int main(){
    CPoint P1(2, 2);
    CPoint P2 = -P1;
    CPoint P3 = -(-P1);

    P1.Print();
    P2.Print();
    P3.Print();

    return 0;
}

CPoint CPoint::operator-(){
    return(CPoint(-this->x, -this->y));
}
~~~

> cpoint_by_friend_function.cpp

~~~C++
#include <iostream>
using namespace std;

class CPoint{
    int x, y;
public:
    CPoint(int a = 0, int b = 0):x(a), y(b){}
    friend CPoint operator-(CPoint obj);
    void Print(){cout << '(' << x << ',' << y << ')' << endl;}
};

int main(){
    CPoint P1(2, 2);
    CPoint P2 = -P1;
    CPoint P3 = -(-P1);

    P1.Print();
    P2.Print();
    P3.Print();

    return 0;
}

CPoint operator-(CPoint obj){
    return CPoint(-obj.x, -obj.y);
}
~~~

>> Output

~~~C++
(2,2)
(-2,-2)
(2,2)

Process finished with exit code 0
~~~

> prefix_by_member_function.cpp

~~~C++
#include <iostream>
using namespace std;

class Power{
    int kick;
    int punch;
public:
    Power(int kick = 0, int punch = 0):kick(kick), punch(punch){}
    void show();
    Power operator++(); // 매개변수 존재 -> postfix
};

int main(){
    Power a(3, 5), b;
    a.show();
    b = ++a;
    a.show();
    b.show();

    return 0;
}

void Power::show(){
    cout << "Kick = " << kick << ',' << " Punch = " << punch << endl;
}
Power Power::operator++(){
    this->kick++;
    this->punch++;
    return *this;
}
~~~

>> Output

~~~C++

~~~

> postfix_by_friend_function.cpp

~~~C++
#include <iostream>
using namespace std;

class Power{
    int kick;
    int punch;
public:
    Power(int kick = 0, int punch = 0):kick(kick), punch(punch){}
    void show();
    friend Power operator++(Power &p, int x); // x 삭제 -> prefix
};

int main(){
    Power a(3, 5), b;
    a.show();
    b = a++;
    a.show();
    b.show();

    return 0;
}

void Power::show(){
    cout << "Kick = " << kick << ',' << " Punch = " << punch << endl;
}
Power operator++(Power &p, int x){
    p.kick++;
    p.punch++;
    return p;
}
~~~

>> Output

~~~C++
Kick = 3, Punch = 5
Kick = 4, Punch = 6
Kick = 4, Punch = 6

Process finished with exit code 0
~~~

> pre_post.cpp

~~~C++
#include <iostream>
using namespace std;

class Power{
    int kick;
    int punch;
public:
    Power(int kick = 0, int punch = 0):kick(kick), punch(punch){}
    void show();
    friend Power operator++(Power &p);
    friend Power operator++(Power &p, int x);
};

int main(){
    Power a(3, 5), b;
    a.show();
    b = ++a;
    a.show();
    b.show();
    Power c(3, 5), d;
    d = c++;
    c.show();
    d.show();

    return 0;
}

void Power::show(){
    cout << "Kick = " << kick << ',' << " Punch = " << punch << endl;
}
Power operator++(Power &p){
    p.kick++;
    p.punch++;
    return p;
}
Power operator++(Power &p, int x){
    p.kick++;
    p.punch++;
    return p;
}
~~~

>> Output

~~~C++
Kick = 3, Punch = 5
Kick = 4, Punch = 6
Kick = 4, Punch = 6
Kick = 4, Punch = 6
Kick = 4, Punch = 6

Process finished with exit code 0
~~~

> complex.cpp

~~~C++
#include <iostream>
using namespace std;

class Complex{
    friend ostream &operator<<(ostream &os, const Complex &v);
    double x, y;
public:
    Complex(double x = 0, double y = 0):x(x), y(y){}
    Complex operator+(const Complex &v2) const{
        Complex v(0.0, 0.0);
        v.x = this->x + v2.x;
        v.y = this->y + v2.y;
        return v;
    }
    void display(){
        cout << '(' << x << ',' << y << 'i' << ')' << endl;
    }
};

int main(){
    Complex v1(1.1,2.1), v2(12.12, 13.13), v3;
    v3 = v1 + v2;
    v1.display();
    v2.display();
    v3.display();
    cout << v1 << v2 << v3;

    return 0;
}

ostream &operator<<(ostream &os, const Complex &v){
    os << '(' << v.x << ',' << v.y << 'i' << ')' << endl;
    return os;
}
~~~

>> Output

~~~C++
(1.1,2.1i)
(12.12,13.13i)
(13.22,15.23i)
(1.1,2.1i)
(12.12,13.13i)
(13.22,15.23i)

Process finished with exit code 0
~~~

## Quiz

> quiz.cpp

~~~C++
#include <iostream>
using namespace std;

class Complex{
    double re, im;
public:
    Complex(double r):re(r), im(0){}
    Complex(double x = 0, double y = 0):re(x),im(y){}
    void Output(){
        cout << re << " + " << im << 'i' << endl;
    }
    Complex &operator+=(Complex com);
    Complex &operator-();
    friend Complex operator+(Complex &com1, Complex &com2);
    friend Complex operator++(Complex &com);
    friend Complex operator++(Complex &com, int x);
    friend ostream &operator<<(ostream &os, Complex &com){
        os << '(' << com.re << ',' << com.im << 'i' << ')' << endl;
        return os;
    }
};

int main(){
    Complex c1(1, 2), c2(3 ,4), c(9, 200);
    c1.Output(); c2.Output(); c1 += c2; c1.Output();
    Complex c3 = c1 + c2;
    Complex c4 = c1 += c2, c5, c6; c3.Output();
    c5 = ++c4; c4.Output(); c5.Output();
    c6 = c4++; c4.Output(); c6.Output();
    c2 = -c2; cout << c2; cout << c;

    return 0;
}

Complex &Complex::operator+=(Complex com){
    this->re = this->re + com.re;
    this->im = this->im + com.im;
    return *this;
}
Complex &Complex::operator-(){
    Complex com(-this->re, -this->im);
    return com;
}
Complex operator+(Complex &com1, Complex &com2){
    Complex com(com1.re + com2.re, com1.im + com2.im);
    return com;
}
Complex operator++(Complex &com){
    com.re++;
    com.im++;
    return com;
}
Complex operator++(Complex &com, int x){
    com.re++;
    com.im++;
    return com;
}
~~~

>> Output

~~~C++
1 + 2i
3 + 4i
4 + 6i
7 + 10i
8 + 11i
8 + 11i
9 + 12i
9 + 12i
(-3,-4i)
(9,200i)

Process finished with exit code 0
~~~

***

# Day 11

## Stack

> stack.cpp

~~~C++
#include <iostream>
using namespace std;

class Stack{
    int size;
    int *mem;
    int tos;
public:
    Stack(int size = 4){
        this->size = size;
        mem = new int[size];
        tos = -1;
    }
    ~Stack(){delete [] mem;}
    Stack &operator<<(int n);
    Stack &operator>>(int &n);
    bool operator!();
};

int main(){
    Stack stack(10);
    stack << 1 << 2 << 3 << 4 << 5;
    while(true){
        if(!stack) break;
        int x;
        stack >> x;
        cout << x << '\t';
    }
    cout << endl;

    return 0;
}

Stack &Stack::operator<<(int n){
    if(tos == size - 1){
        return *this;
    }
    this->tos++;
    this->mem[tos] = n;
    return *this;
}
Stack &Stack::operator>>(int &n){
    if(tos == -1){
        return *this;
    }
    n = this->mem[tos];
    this->tos--;
    return *this;
}
bool Stack::operator!(){
    if(tos == -1)
        return true;
    else
        return false;
}
~~~

>> Output

~~~C++
5	4	3	2	1	

Process finished with exit code 0
~~~

## Const Member & Const Object

+ `const` member variable : 객체 생성과 동시에 초기화 필요
  + 멤버 초기화 구문 사용
+ `const` member function : 멤버 변수의 값을 읽을 수 있으나 변경 불가능
  + 멤버 변수의 주소 반환 불가
  + 비`const` 멤버 함수의 호출 불가
+ `const` object
  + 객체 생성 시 `const` 접두사 추가
  + 멤버 변수의 값 변경 불가
  + `const` 멤버 함수 이외의 멤버 함수에 대한 호출 불가

## Inheritance

+ 기본 클래스(Base class) - 상속해주는 클래스, 부모 클래스
+ 파생 클래스(Derived class) - 상속받는 클래스, 자식 클래스

~~~C++
class Derived : public Base{ //public, private, protected
    ...
}
~~~

+ 간결한 클래스 작성
+ 클래스 간의 계층적 분류 및 관리의 용이함
+ 클래스 재사용과 확장을 통한 소프트웨어 생산성 향상

> inheritance.cpp

~~~C++
#include <iostream>
using namespace std;

class Point{
    int x, y;
public:
    void set(int x, int y){this->x = x; this->y = y;}
    void showPoint(){
        cout << '(' << x << ',' << y << ')' << endl;
    }
};

class ColorPoint : public Point{
    string color;
public:
    void setColor(string color){this->color = color;}
    void showColorPoint();
};

int main(){
    Point p;
    ColorPoint cp;
    cp.set(3, 4);
    cp.setColor("Red");
    cp.showColorPoint();

    return 0;
}

void ColorPoint::showColorPoint(){
    cout << color << " : ";
    showPoint();
}
~~~

>> Output

~~~C++
Red : (3,4)

Process finished with exit code 0
~~~

## Casting

+ 업 캐스팅(Up-casting)
  + 파생 클래스의 객체를 기본 클래스의 포인터로 가리키는 것
  + 포인터 : 기본
  + 객체 : 파생
+ 다운 캐스팅(Down-casting)
  + 기본 클래스 포인터가 가리키는 객체를 파생 클래스의 포인터로 가리키는 것
  + 명시적 형변환 필요
  + 포인터 : 파생
  + 객체 : 기본

## 접근 지정자

+ private 멤버
  + 선언된 클래스 내에서만 접근 가능
  + 파생 클래스에서도 기본 클래스의 private 멤버 직접 접근 불가
+ public 멤버
  + 선언된 클래스나 외부 어떤 클래스, 모든 외부 함수에 접근 허용
  + 파생 클래스에서 기본 클래스의 public 멤버 접근 가능
+ protected 멤버
  + 선언된 클래스에서 접근 가능
  + 파생 클래스에서만 접근 허용

> point.cpp

~~~C++
#include <iostream>
using namespace std;

class Point{
    int x, y;
protected:
    Point(int x, int y):x(x), y(y){}
    int getX(){return x;}
    int getY(){return y;}
    void move(int x, int y){this->x = x; this->y = y;}
};

class ColorPoint : public Point{
    string color;
public:
    ColorPoint():Point(0, 0){color = "BLACK";}
    ColorPoint(int x, int y):Point(x, y){}
    ColorPoint(int x, int y, string color):Point(x, y){this->color = color;}
    void setPoint(int x, int y){move(x, y);}
    void setColor(string color){this->color = color;}
    friend void show(ColorPoint &p);
};

int main(){
    ColorPoint zeroPoint;
    show(zeroPoint);
    ColorPoint cp(5, 5);
    cp.setPoint(10, 20);
    cp.setColor("BLUE");
    show(cp);
    ColorPoint cpRed(23, 33, "RED");
    show(cpRed);

    return 0;
}

void show(ColorPoint &p){
    cout << p.color << "색으로 " << '(' << p.getX() << ',' << p.getY() << ')' << "에 위치한 점입니다." << endl;
}
~~~

>> Output

~~~C++
BLACK색으로 (0,0)에 위치한 점입니다.
BLUE색으로 (10,20)에 위치한 점입니다.
RED색으로 (23,33)에 위치한 점입니다.

Process finished with exit code 0
~~~

## Quiz

> quiz.cpp

~~~C++
#include <iostream>
using namespace std;

class BaseArray{
    int capacity;
    int *mem;
protected:
    BaseArray(int capacity = 100):capacity(capacity){mem = new int[capacity];}
    ~BaseArray(){delete [] mem;}
    void put(int index, int val){mem[index] = val;};
    int get(int index){return mem[index];}
    int getCapacity(){return capacity;};
};

class MyQueue : BaseArray{
    int head;
    int tail;
    int size;
public:
    MyQueue(int capacity):BaseArray(capacity){head = 0; tail = -1; size = 0;}
    void enqueue(int n);
    int dequeue();
    int capacity(){return getCapacity();}
    int length(){return size;}
    void setSize(int S = 0){size = S;}
    int getSize(){return size;}
};

int main(){
    MyQueue mQ(100);
    int Size;
    cout << "큐의 사이즈를 입력하라>> ";
    cin >> Size;
    mQ.setSize(Size);
    int n;
    cout << "큐에 삽입할 "<< mQ.getSize() << "개의 정수를 입력하라>> ";
    for(int i = 0; i < mQ.getSize(); i++){
        cin >> n;
        mQ.enqueue(n);
    }
    cout << "큐의 용량 : " << mQ.capacity() << ",\t큐의 크기 : " << mQ.length() << endl;
    cout << "큐의 원소를 순서대로 제거하여 출력한다>> ";
    while(mQ.length() != 0){
        cout << mQ.dequeue() << ' ';
    }
    cout << endl << "큐의 현재 크기 : " << mQ.length() << endl;

    return 0;
}

void MyQueue::enqueue(int n){
    int he = head % getCapacity();
    put(he, n);
    head++;
}
int MyQueue::dequeue(){
    tail++;
    int ta = tail % getCapacity();
    size--;
    return get(ta);
}
~~~

>> Output

~~~C++
큐의 사이즈를 입력하라>> 5
큐에 삽입할 5개의 정수를 입력하라>> 12 34 44 33 22
큐의 용량 : 100,	큐의 크기 : 5
큐의 원소를 순서대로 제거하여 출력한다>> 12 34 44 33 22 
큐의 현재 크기 : 0

Process finished with exit code 0
~~~

***

# Day 12

## Constructor of Inheritance

> constructor.cpp

~~~C++
#include <iostream>
using namespace std;

class TV{
    int size;
public:
    TV(){size = 20;}
    TV(int size):size(size){}
    int getSize(){return size;}
};

class WideTV : public TV{
    bool videoIn;
public:
    WideTV(int size, bool videoIn) : TV(size){
        this->videoIn = videoIn;
    }
    bool getVideoIn(){return videoIn;}
};

class SmartTV : public WideTV{
    string ipAddr;
public:
    SmartTV(string ipAddr, int size) : WideTV(size, true){
        this->ipAddr = ipAddr;
    }
    string getipAddr(){return ipAddr;}
};

int main(){
    SmartTV htv("192.0.0.1", 32);
    cout << "size = " << htv.getSize() << endl;
    cout << "videoIn = " << htv.getVideoIn() << endl;
    cout << "IP = " << htv.getipAddr() << endl;

    return 0;
}
~~~

>> Output

~~~C++
size = 32
videoIn = 1
IP = 192.0.0.1

Process finished with exit code 0
~~~

## Virtual Function & Overriding

+ Virtual function
  + `virtual` 키워드로 선언된 멤버 함수
  + 동적 바인딩 지시어
  + 컴파일러에게 함수에 대한 호출 바인딩을 실행 시간까지 미루도록 지시
+ Function overriding
  + 파생 클래스에서 기본 클래스의 가상 함수와 동일한 이름의 함수 선언
  + 기본 클래스 : 가상 함수의 존재감 상실
  + 파생 클래스 : 오버라이딩한 함수가 호출되도록 동적 바인딩
  + 함수 재정의라고도 부름
  + 다형성의 한 종류
+ 조건
  + `virtual`으로 함수 선언(파생 클래스는 생략 가능)
  + upcasting
  + 함수 동일

> overriding.cpp

~~~C++
#include <iostream>
using namespace std;

class Base{
public:
    virtual void f(){cout << "Base" << endl;}
};

class Derived : public Base{
public:
    void f(){cout << "Derived" << endl;}
};

class GrandDerived : public Derived{
public:
    void f(){cout << "GrandDerived" << endl;}
};

int main(){
    Base *bp = new GrandDerived;
    bp->f();
    Derived *dp = new GrandDerived;
    dp->f();

    return 0;
}
~~~

>> Output

~~~C++
GrandDerived
GrandDerived

Process finished with exit code 0
~~~

> destructor1.cpp

~~~C++
#include <iostream>
using namespace std;

class Base{
public:
    ~Base(){cout << "~Base" << endl;}
};

class Derived : public Base{
public:
    ~Derived(){cout << "~Derived" << endl;}
};

class GrandDerived : public Derived{
public:
    ~GrandDerived(){cout << "~GrandDerived" << endl;}
};

int main(){
    Base *bp = new GrandDerived;
    Derived *dp = new GrandDerived;
    GrandDerived *gp = new GrandDerived;

    delete bp;
    delete dp;
    delete gp;

    return 0;
}
~~~

>> Output

~~~C++
~Base
~Derived
~Base
~GrandDerived
~Derived
~Base

Process finished with exit code 0
~~~

> destructor2.cpp

~~~C++
#include <iostream>
using namespace std;

class Base{
public:
    virtual ~Base(){cout << "~Base" << endl;}
};

class Derived : public Base{
public:
    ~Derived(){cout << "~Derived" << endl;}
};

class GrandDerived : public Derived{
public:
    ~GrandDerived(){cout << "~GrandDerived" << endl;}
};

int main(){
    Base *bp = new GrandDerived;
    Derived *dp = new GrandDerived;
    GrandDerived *gp = new GrandDerived;

    delete bp;
    delete dp;
    delete gp;

    return 0;
}
~~~

>> Output

~~~C++
~GrandDerived
~Derived
~Base
~GrandDerived
~Derived
~Base
~GrandDerived
~Derived
~Base

Process finished with exit code 0
~~~

## Overloading vs. Overrding

+ Overloading
  + 이름만 같은 함수 중복 작성
  + 하나의 클래스
+ Overriding
  + 모든 것이 완벽히 같은 함수 재작성
  + 상속

## Quiz

> quiz.cpp

~~~C++
#include <iostream>
using namespace std;

class BaseArray{
    int capacity;
    int *mem;
public:
    BaseArray(int capacity = 100):capacity(capacity){mem = new int[capacity];}
    ~BaseArray(){delete [] mem;}
    void put(int index, int val);
    int get(int index);
    int getCapacity(){return capacity;}
};

class MyStack : public BaseArray{
    int tos;
public:
    MyStack(int capacity) : BaseArray(capacity){tos = 0;}
    void push(int n);
    int pop();
    int capacity(){return getCapacity();}
    int length(){return tos;}
};

int main(){
    MyStack mStack(100);
    int n;
    cout << "스택에 삽입할 5개의 정수를 입력하라>> ";
    for(int i = 0; i < 5; i++){
        cin >> n;
        mStack.push(n);
    }
    cout << "스택 용량:" << mStack.capacity() << ", 스택 크기:" << mStack.length() << endl;
    cout << "스택의 모든 원소를 팝하여 출력한다>> ";
    while(mStack.length() != 0){
        cout << mStack.pop() << ' ';
    }
    cout << endl << "스택의 현재 크기 : " << mStack.length() << endl;
}

void BaseArray::put(int index, int val){
    mem[index] = val;
}
int BaseArray::get(int index){
    return mem[index];
}

void MyStack::push(int n){
    put(tos, n);
    tos++;
}
int MyStack::pop(){
    tos--;
    return get(tos);
}
~~~

>> Output

~~~C++
스택에 삽입할 5개의 정수를 입력하라>> 34 52 41 12 78
스택 용량:100, 스택 크기:5
스택의 모든 원소를 팝하여 출력한다>> 78 12 41 52 34 
스택의 현재 크기 : 0

Process finished with exit code 0
~~~

***

# Day 13

## Interface

+ 인터페이스만 선언하고 구현을 분리하여 작업자마다 다양한 구현 가능
+ 사용자는 구현의 내용을 모르지만 인터페이스에 선언된 순수 가상 함수가 구현되어있기 때문에 호출하여 사용하기만 하면 됨

> shape.cpp

~~~C++
#include <iostream>
using namespace std;

class Shape{
    Shape *next;
protected:
    virtual void draw() = 0; // 순수 가상 함수
public:
    Shape(){next = NULL;}
    virtual ~Shape(){}
    void paint(){draw();}
    Shape *add(Shape *p){this->next = p; return p;};
    Shape *getNext(){return next;}
};

class Circle : public Shape{
protected:
    void draw(){cout << "Circle" << endl;}
    ~Circle(){cout << "del Circle" << endl;}
};

class Rect : public Shape{
protected:
    void draw(){cout << "Rect" << endl;}
    ~Rect(){cout << "del Rect" << endl;}
};

int main(){
    Shape *pStart = NULL;
    Shape *pLast;
    pStart = new Circle();
    pLast = pStart;
    pLast = pLast->add(new Rect());
    pLast = pLast->add(new Rect());
    pLast = pLast->add(new Circle());
    pLast = pLast->add(new Rect());
    Shape *p = pStart;
    while(p != NULL){
        p->paint();
        p = p->getNext();
    }
    p = pStart;
    while(p != NULL){
        Shape *q = p->getNext();
        delete p;
        p = q;
    }

    return 0;
}
~~~

>> Output

~~~C++
Circle
Rect
Rect
Circle
Rect
del Circle
del Rect
del Rect
del Circle
del Rect

Process finished with exit code 0
~~~

## Abstract Class

+ 최소한 하나의 순수 가상 함수를 가진 클래스
+ 온전한 클래스가 아니므로 객체 생성 불가능
+ 추상 클래스의 포인터는 선언 가능
+ 순수 가상 함수를 통해 파생 클래스에서 구현할 함수의 형태(원형)을 보여주는 인터페이스 역할

> calculator.cpp

~~~C++
#include <iostream>
using namespace std;

class Calculator{
    void input(){
        cout << "정수 2개를 입력하세요>>";
        cin >> a >> b;
    }
protected:
    int a, b;
    virtual int calc(int a, int b) = 0;
public:
    void run(){
        input();
        cout << "계산된 값은 " << calc(a, b) << endl;
    }
};

class Adder : public Calculator{
protected:
    int calc(int a, int b){return a + b;}
};

class Subtract : public Calculator{
protected:
    int calc(int a, int b){return a - b;}
};

int main(){
    Calculator *c;
    c = new Adder;
    c->run();
    c = new Subtract;
    c->run();
    delete c;

    return 0;
}
~~~

>> Output

~~~C++
정수 2개를 입력하세요>>4 3
계산된 값은 7
정수 2개를 입력하세요>>4 3
계산된 값은 1

Process finished with exit code 0
~~~

## Generalization of Function

+ Generic 혹은 일반화
  + 함수나 클래스를 일반화시키고, 매개변수 타입을 지정하여 틀에서 찍어내듯이 함수나 클래스 코드를 생산하는 기법
+ Template
  + 함수나 클래스를 일반화하는 `C++` 도구
  + `template` 키워드로 함수나 클래스 선언
  + Generic type - 일반화를 위한 Data type

> sum.cpp

~~~C++
#include <iostream>
using namespace std;

template<class T>
T Sum(T a, T b){
    return a + b;
}

int main(){
    cout << Sum(1, 2) << endl;
    cout << Sum(1.1, 2.2) << endl;
    cout << Sum('1', '2') << endl;

    return 0;
}
~~~

>> Output

~~~C++
3
3.3
c

Process finished with exit code 0
~~~

> search.cpp

~~~C++
#include <iostream>
using namespace std;

template<class T>
bool search(T one, T arr[], int size){
    for(int i = 0; i < size; i++){
        if(arr[i] == one)
            return true;
    }
    return false;
}

int main(){
    int x[] = {1, 10, 100, 5, 4};
    if(search(100, x, sizeof(x) / 4))
        cout << "100이 배열 x에 포함되어 있다.";
    else
        cout << "100이 배열 x에 포함되어 있지 않다.";
    cout << endl;

    char c[] = {'h', 'e', 'l', 'l', 'o'};
    if(search('e', c, 5))
        cout << "e가 배열 x에 포함되어 있다.";
    else
        cout << "e가 배열 x에 포함되어 있지 않다.";
    cout << endl;

    return 0;
}
~~~

>> Output

~~~C++
100이 배열 x에 포함되어 있다.
e가 배열 x에 포함되어 있다.

Process finished with exit code 0
~~~

## Generalization of Class

+ 선언 : `template<class T>`
  + class의 정의 앞에 선언
  + 선언부, 구현부 - 멤버 함수 앞 선언
  + `T class<T>::function(T param);`
+ 일반화할 변수만 `T`로 선언

> generic.cpp

~~~C++
#include <iostream>
using namespace std;

class Point{
    int x, y;
public:
    Point(int x = 0, int y = 0):x(x), y(y){}
    void show(){cout << '(' << x << ',' << y << ')' << endl;}
};

template<class T>
class MyStack{
    int tos;
    T data[100];
public:
    MyStack();
    void push(T element);
    T pop();
};

int main(){
    MyStack<int *> ipStack;
    int *p = new int[3];
    for(int i = 0; i < 3; i++)
        p[i] = i * 10;
    ipStack.push(p);
    int *q = ipStack.pop();
    for(int i = 0; i < 3; i++)
        cout << q[i] << '\t';
    cout << endl;
    delete [] p;

    MyStack<Point> pointStack;
    Point a(2, 3), b;
    pointStack.push(a);
    b = pointStack.pop();
    b.show();

    MyStack<Point *> pStack;
    pStack.push(new Point(10, 20));
    Point *pPoint = pStack.pop();
    pPoint->show();

    MyStack<string> stringStack;
    string s = "C++";
    stringStack.push(s);
    stringStack.push("Zerohertz");
    cout << stringStack.pop() << '\t';
    cout << stringStack.pop() << endl;

    return 0;
}

template<class T>
MyStack<T>::MyStack(){
    tos = -1;
}
template<class T>
void MyStack<T>::push(T element){
    if(tos == 99){
        cout << "Stack full" << endl;
        return;
    }
    tos++;
    data[tos] = element;
}
template<class T>
T MyStack<T>::pop(){
    T Data;
    if(tos == -1){
        cout << "Stack empty" << endl;
        return 0;
    }
    Data = data[tos--];
    return Data;
}
~~~

>> Output

~~~C++
0	10	20	
(2,3)
(10,20)
Zerohertz	C++

Process finished with exit code 0
~~~

> gclass.cpp

~~~C++
#include <iostream>
using namespace std;

template<class T1, class T2>
class GClass{
    T1 data1;
    T2 data2;
public:
    GClass(){data1 = 0; data2 = 0;};
    void set(T1 a, T2 b){
        data1 = a; data2 = b;
    }
    void get(T1 &a, T2 &b){
        a = data1; b = data2;
    }
};

int main(){
    int a;
    double b;
    GClass<int, double> x;
    x.set(2, 0.5);
    x.get(a, b);
    cout << "a = " << a << "\tb = " << b << endl;

    char c;
    float d;
    GClass<char, float> y;
    y.set('m', 12.5);
    y.get(c, d);
    cout << "c = " << c << "\td = " << d << endl;

    return 0;
}
~~~

>> Output

~~~C++
a = 2	b = 0.5
c = m	d = 12.5

Process finished with exit code 0
~~~

## Quiz

> quiz.cpp

~~~C++
#include <iostream>
#include <string>
using namespace std;

class Shape{
protected:
    string name;
    int width, height;
public:
    Shape(string n = "", int w = 0, int h = 0){name = n; width = w; height = h;}
    virtual double getArea(){return 0;}
    string getName(){return name;}
};

class Oval : public Shape{
public:
    Oval(string n = "", int w = 0, int h = 0):Shape(n, w, h){}
    double getArea(){return 3.14 * width * height;}
};

class Rect : public Shape{
public:
    Rect(string n = "", int w = 0, int h = 0):Shape(n, w, h){}
    double getArea(){return width * height;}
};

class Triangular : public Shape{
public:
    Triangular(string n = "", int w = 0, int h = 0):Shape(n, w, h){}
    double getArea(){return width * height / 2;}
};

int main(){
    Shape *p[3];
    p[0] = new Oval("빈대떡", 10, 20);
    p[1] = new Rect("찰떡", 30, 40);
    p[2] = new Triangular("토스트", 30, 40);
    for(int i = 0; i < 3; i++)
        cout << p[i]->getName() << " 넓이는 " << p[i]->getArea() << endl;
    for(int i = 0; i < 3; i++) delete p[i];

    return 0;
}
~~~

>> Output

~~~C++
빈대떡 넓이는 628
찰떡 넓이는 1200
토스트 넓이는 600

Process finished with exit code 0
~~~

***

# Day 14

## STL

+ STL(Standard Template Library)
  + 표준 템플릿 라이브러리
  + 많은 제네릭 클래스와 제네릭 함수 포함
+ STL의 구성
  + 컨테이너 : 템플릿 클래스
    + 데이터를 담아두는 자료 구조를 표현한 클래스
    + 리스트, 큐, 스택, 맵, 셋, 벡터
  + iterator : 컨테이너 원소에 대한 포인터
    + 컨테이너의 원소들을 순회하면서 접근하기 위해 만들어진 컨테이너 원소에 대한 포인터
  + 알고리즘 : 템플릿 함수
    + 컨테이너 원소에 대한 복사, 검색, 삭제, 정렬 등의 기능을 구현한 템플릿 함수
    + 컨테이너의 멤버 함수 아님

> STL 컨테이너의 종류

|컨테이너 클래스|설명|헤더 파일|
|:-:|:-:|:-:|
|vector|동적 크기의 배열을 일반화한 클래스|`<vector>`|
|deque|앞뒤 모두 입력 가능한 큐 클래스|`<deque>`|
|list|빠른 삽입/삭제 가능한 리스트 클래스|`<list>`|
|set|정렬된 순서로 값을 저장하는 집합 클래스, 값은 유일|`<set>`|
|map|(key, value)쌍으로 값을 저장하는 맵 클래스|`<map>`|
|stack|스택을 일반화한 클래스|`<stack>`|
|queue|큐를 일반화한 클래스|`<queue>`|

> STL iterator의 종류

|iterator의 종류|iterator에 `++` 연산 후 방향|read/write|
|:-:|:-:|:-:|
|iterator|다음 원소로 전진|read/write|
|const_iterator|다음 원소로 전진|read|
|reverse_iterator|지난 원소로 후진|read/write|
|const_reverse_iterator|지난 원소로 후진|read|

> STL 알고리즘 함수들

+ copy
+ merge
+ random
+ rotate
+ equal
+ min
+ remove
+ search
+ find
+ move
+ replace
+ sort
+ max
+ partition
+ reverse
+ swap

## Vector

+ 가변 길이 배열을 구현한 `Generic` 클래스
+ 원소의 저장, 삭제, 검색 등 다양한 멤버 함수 지원
+ 벡터에 저장된 원소는 인덱스로 접근 가능

> vector.cpp

~~~C++
#include <iostream>
#include <vector>
using namespace std;

int main(){
    vector<int> v;

    v.push_back(1);
    v.push_back(2);
    v.push_back(3);

    for(int i = 0; i < v.size(); i++)
        cout << v[i] << '\t';
    cout << endl;

    v[0] = 10;
    int n = v[2];
    v.at(2) = 5;

    for(int i = 0; i < v.size(); i++)
        cout << v[i] << '\t';
    cout << endl;

    return 0;
}
~~~

>> Output

~~~C++
1	2	3	
10	2	5	

Process finished with exit code 0
~~~

## Iterator

+ 반복자라고도 부름
+ `*`, `++` 연산자 사용 가능
+ 컨테이너의 원소를 가리키는 포인터

> iterator.cpp

~~~C++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main(){
    vector<int> v;
    int n;

    cout << "5개의 정수를 입력하시오." << endl;
    for(int i = 0; i < 5; i++){
        cin >> n;
        v.push_back(n);
    }

    sort(v.begin(), v.end()); // sort(v.begin() + a, v.begin() + b) -> a에서 b - 1까지

    vector<int>::iterator it;

    for(it = v.begin(); it != v.end(); it++)
        cout << *it << '\t';
    cout << endl;

    return 0;
}
~~~

>> Output

~~~C++
5개의 정수를 입력하시오.
30 -7 250 6 120
-7	6	30	120	250	

Process finished with exit code 0
~~~

## Algorithm

+ 탐색(`find`) : 컨테이너 안에서 특정한 자료를 찾음
+ 정렬(`sort`) : 자료들을 크기 순으로 정렬
  + `param1` : 정렬을 시작한 원소의 주소
  + `param2` : 소팅 범위의 마지막 원소 다음 주소
+ 반전(`reverse`) : 자료들의 순서 역순
+ 삭제(`remove`) : 조건이 만족되는 자료 삭제
+ 변환(`transform`) : 컨테이너 요소들을 사용자가 제공하는 변환 함수에 따라 변환
 
> algorithm.cpp

~~~C++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class Circle{
    string name;
    int radius;
public:
    Circle(int radius = 1, string name = ""):radius(radius), name(name){}
    double getArea(){return 3.14 * radius * radius;}
    string getName(){return name;}
    bool operator<(Circle b);
    friend ostream &operator<<(ostream &os, vector<Circle> &b);
};

void printVector(vector<Circle> vec);

int main(){
    vector<Circle> v;
    v.push_back(Circle(2, "waffle"));
    v.push_back(Circle(3, "pizza"));
    v.push_back(Circle(1, "donut"));
    v.push_back(Circle(5, "pizzaLarge"));
    printVector(v);
    // int it = v.size() - 1;
    sort(v.begin(), v.end()); // sort(&v[0], &v[it]);
    printVector(v);
    cout << endl << "프렌드함수 operator<<로 출력하는 경우" << endl;
    cout << v << endl;

    return 0;
}

bool Circle::operator<(Circle b){
    if(this->radius < b.radius)
        return true;
    else
        return false;
}

ostream &operator<<(ostream &os, vector<Circle> &b){
    vector<Circle>::iterator it;
    os << "모든 원소를 출력한다.>>";
    for(it = b.begin(); it != b.end(); it++)
        os << it->getName() << '\t';
    os << endl;
    return os;
}

void printVector(vector<Circle> vec){
    cout << "모든 원소를 출력한다.>>";
    for(auto it = vec.begin(); it != vec.end(); it++) // auto는 자동형변환
        cout << it->getName() << '\t';
    cout << endl;
}
~~~

>> Output

~~~C++
모든 원소를 출력한다.>>waffle   pizza   donut   pizzaLarge
모든 원소를 출력한다.>>donut    waffle  pizza   pizzaLarge

프렌드함수 operator<<로 출력하는 경우
모든 원소를 출력한다.>>donut    waffle  pizza   pizzaLarge
~~~