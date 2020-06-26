---
title: Class - const
author: RUKA SPROUT
date: 2020-06-26 11:11:00 +0900
categories: [C++]
tags: [programming]
---

## Const 멤버 변수

- 선언 시에 붙일 수도 있고 (필드), 파라미터로 받아 올 때 붙일 수도 있다.
- 멤버 변수의 값을 변경시킬 수 없다고 선언하는 것이다.
- **객체가 const 메소드만 호출할 수 있다.**

```cpp
const int x; // 필드 선언 시에 const 를 붙임

void func(const Point& pt) // 파라미터에 const 를 붙임
{
		pt.setXY(1, 1); // 에러. const 메소드를 사용하지 않음
		pt.getY(); // 성공. const 메소드를 사용함
}
```

## Const 메소드

- 메소드 안에서 어떤 멤버의 값도 바꿀 수 없다고 선언하는 것이다.
- **함수 내부에서 const 메소드만 호출할 수 있다.**
- 멤버가 const 일 필요는 없다.

```cpp
int getX() const // const 메소드 선언
{
		setXY(1, 1); // 에러. const 메소드를 사용하지 않음
		getY(); // 성공. const 메소드를 사용함
}
```