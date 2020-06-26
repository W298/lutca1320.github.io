---
title: Class - Inheritance
author: RUKA SPROUT
date: 2020-06-26 14:11:00 +0900
categories: [C++]
tags: [programming]
---

## 상속 접근 지정자

- **부모 클래스의 멤버 변수/함수 가 private 인 경우 접근 불가**

```cpp
class Derived : (접근 지정자) Base
```

- public : 부모 클래스의 멤버 변수/함수 를 public 으로 인식
  - public → public
  - protected → protected
  - **private → 접근 불가**
- protected : 부모 클래스의 멤버 변수/함수 를 protected 로 인식
  - public → protected
  - protected → protected
  - **private → 접근 불가**
- private : 부모 클래스의 멤버 변수/함수 를 private 으로 인식
  - public → private
  - protected → private
  - **private → 접근 불가**

## 오버라이딩

- 부모 클래스의 메소드와 같은 파라미터, 이름, 리턴을 가진 메소드를 재정의하는 것이다.
- virtual, override 등의 키워드를 사용하는 것이 명시적이지만, 동적 바인딩이 아닌 경우에는 사용하지 않아도 작동한다.

### 추상 클래스 / 순수 가상 함수

```cpp
class Abstract
{
public:
		virtual void func() = 0;
}
class Derived
{
public:
		virtual void func() override // virtual, override 키워드는 없어도 작동한다.
```

- 추상 클래스는 순수 가상 함수만을 가지고 있는 클래스이다.
- 추상 클래스는 객체를 생성할 수 없다.
- 순수 가상 함수는 `= 0` 을 통해 정의할 수 있으며, 상속 클래스에서 반드시 재정의되어야 한다.