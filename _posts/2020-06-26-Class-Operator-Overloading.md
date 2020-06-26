---
title: Class - Operator Overloading
author: RUKA SPROUT
date: 2020-06-26 12:11:00 +0900
categories: [C++]
tags: [programming]
---

## 클래스 내부에서의 오버로딩

- `operator==`, `operator+` 등으로 사용한다.
- 메소드 형식으로 만들 수 있다.
- 클래스 내부에 있기 때문에 멤버 변수를 마음대로 사용할 수 있다.
- pt1.+(pt2) 와 같은 작동원리이다.
  - pt1이라는 객체가 +라는 메소드를 호출하는데, 파라미터로 pt2를 사용하는 원리이다.

```cpp
bool Point::operator==(Point pt2);
Point Point::operator+(Point pt2);
```

## 외부에서의 오버로딩

- 함수 형식으로 만들 수 있다.
- 제한된 멤버 변수 접근이 가능하다.
- +(pt1, pt2) 와 같은 작동원리이다.
  - +라는 함수가 있는데, 파라미터로 pt1, pt2 를 받는 것이다.

```cpp
bool operator==(Point pt1, Point pt2);
Point operator+(Point pt1, Point pt2);
```