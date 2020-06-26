---
title: Class - Dynamic Bind
author: RUKA SPROUT
date: 2020-06-26 10:11:00 +0900
categories: [C++]
tags: [programming]
---

- 객체가 포인터로 선언되었을 때 자신의 타입이 아닌, 포인터에 들어간 객체의 타입의 함수가 호출되게 할 수 있다.

## 선언 방법

```cpp
class Base
{
public:
	virtual void print(); // 오버라이딩될 함수
}
class Derived : public Base
{
public:
	virtual void print() override; // 함수 오버라이딩
}
```

## main 에서의 활용

```cpp
Base base;
Derived dr;

Base* b1;

b1 = &base; // b1에 Base 클래스 객체 할당
b1->print(); // Base 함수 호출

b1 = &dr; // b1에 Derived 클래스 객체 할당
b1->print(); // Derived 함수 호출
```