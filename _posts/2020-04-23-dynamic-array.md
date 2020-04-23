---
title: Dynamic Array
author: RUKA SPROUT
date: 2020-04-23 12:23:00 +0900
categories: [C++]
tags: [programming]
---

## 1차원 배열

### 변수 선언 (메모리 할당)

```cpp
int* arr = new int[size];
```

### 변수 제거 (메모리 해제)

```cpp
delete[] arr;
```

## 2차원 배열

- 2차원에서는 이중 포인터(`**`) 를 사용한다.
- 포인터가 변수의 주소를 담았다면, 이중 포인터는 포인터의 주소를 담는다.

```cpp
int** mat = new int*[size]
-------
mat[0] = 포인터
mat[1] = 포인터
...
```

### 변수 선언 (메모리 할당)

- n x m (n = 행, m = 열) 행렬은 다음과 같이 선언한다.

```cpp
int** mat = new int*[n]; // mat 을 동적 배열로 할당한다.

for (int i = 0; i < n; i++)
{
    mat[i] = new int[m]; // mat 의 원소들을 동적 배열로 할당한다.
}
```

### 변수 제거 (메모리 해제)

```cpp
for (int i = 0; i < n; i++)
{
    delete[] mat[i]; // mat 의 원소들의 메모리를 해제한다.
}

delete[] mat; // mat 의 메모리를 해제한다.
```
