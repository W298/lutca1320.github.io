---
title: Generic Programming
author: RUKA SPROUT
date: 2020-06-04 11:47:00 +0900
categories: [C++]
tags: [programming]
---

- 특정 타입이 아닌 Generic 한 타입을 사용하기 위해 사용한다.
- 한 `template` 에 여러 타입을 명시할 수 있다.
- `class` = `typename`

```cpp
template <class T>
template <class T, class U>

template <typename T>
```

## Generic 함수

- 선언

```cpp
template <class T>
void func(T p1, T p2);
```

- 중복 함수가 존재할 시 그 중복 함수를 호출한다.

```cpp
template <class T>
void func(T p1, T p2); // Generic 함수

void func(int p1, int p2); // 중복 함수

// func(1, 2)은 중복 함수가 호출된다.
```

## Generic 클래스

- 선언

```cpp
template <class T>
class Base
{
    T ary[100];
	...
}
```

- 객체 생성 시 타입을 명시해 주어야 한다.

```cpp
Base<int> bClass;
```
