---
title: Exception Handle
author: RUKA SPROUT
date: 2020-06-26 18:11:00 +0900
categories: [C++]
tags: [programming]
---

## throw 가 없는 try-catch

```cpp
try
{
    cout << v.at(3);
}
catch (std::exception& ex) // 타입을 std::exception& 으로 받는다.
{
    cout << ex.what() << endl; // what() 메소드로 에러 내용을 표시한다.
}
```

## throw 를 이용한 try-catch

- throw 를 한 객체와 받는 catch 문의 타입이 동일해야 한다.

```cpp
try
{
    cin >> n;

    if (n > v.size())
	throw n; // n 값을 던짐
}
catch (int ex) // ex 값으로 받음
{
    cout << n << " is out of range" << endl;
}
```
