---
title: Class - Friend
author: RUKA SPROUT
date: 2020-06-26 13:11:00 +0900
categories: [C++]
tags: [programming]
---

- 예외적으로 private, protected 를 무시하고 public 으로 인식시킨다.
- 친구의 자식, 친구의 친구는 friend 키워드로 명시하지 않은 경우 친구 관계가 형성되지 않는다.

## Friend 클래스

- 특정 클래스가 다른 클래스를 친구로 선언한다.
- 양방향이 아닌 단방향이다.

```cpp
class Civil
{
  	friend Spy;	
};

class Spy;

// Civil -> Spy
// Civil 은 Spy 에게 모든 정보를 제공하지만, Spy 는 Civil 에게 public 정보만 제공한다.
```

## Friend 메소드

- 범위를 전체 클래스가 아닌 특정 메소드로 한정시킨다.

```cpp
class Civil
{
private:
		int sendInfo();

public:
		friend void Spy::CollectInfo(Civil& c);
};

class Spy
{
private:
		int info;

public:
		void CollectInfo(Civil& c)
		{
				this->info += c.sendInfo();
		}
};

// Civil 은 Spy 의 CollectInfo 에게만 모든 정보를 제공한다.
// 그렇기 때문에 Spy 는 Civil 의 sendInfo 를 호출할 수 있다.
```

## Friend 전역 함수

- 클래스 외부의 함수가 모든 정보에 접근할 수 있도록 한다.

```cpp
class Civil
{
private:
		friend void showMoney(Civil& c);
};

void showMoney(Civil& c);
```