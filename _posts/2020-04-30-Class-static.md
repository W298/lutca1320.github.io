---
title: Class - static
author: RUKA SPROUT
date: 2020-04-30 11:11:00 +0900
categories: [C++]
tags: [programming]
---

## Static 변수

- 모든 객체가 공유하는 변수이다.
- **항상 클래스 밖에서 초기화되어야 한다.**

```cpp
class Point
{
public:
    static int count; // static variable 선언
}
```

```cpp
int Point::count = 0; // 초기화하지 않을 시 링커 오류 발생
```

```cpp
int main()
{
    cout << ++Point::count << endl; // public 이기 때문에 접근 가능
}
```

## Static 함수

- 객체를 만들지 않고 호출할 수 있는 함수이다.
- 클래스 멤버 중 static 변수만을 사용할 수 있다.
- `Class::Function()` 으로 호출할 수 있다.

```cpp
class Point
{
public:
    static void printCount(); // static function 선언
}
```

```cpp
int main()
{
    Point::printCount(); // static function 호출
}
```
