---
title: Data Structure - SortedList
author: RUKA SPROUT
date: 2020-10-17 16:54:00 +0900
categories: [Data Structure]
tags: [cpp, programming]
---

**`SortedList` 는 정렬되어 있는 List 자료구조이다.**

`UnsortedList` 와 거의 비슷하지만, `Add()` 함수가 다르다.
- 삽입 정렬을 사용하기 때문에 `Add()` 함수에서 어디에 Element 를 추가할 지 고려해야 한다.
- `List` 가 정렬되어 있으므로 처음부터 탐색하는 `Get()` 함수 말고도, 이진 탐색을 사용하는 `GetBinS()` 함수를 구현할 수 있다.

정적 사이즈를 가진 `SortedList` 는 동적 사이즈 `SortedList` 와 거의 동일하기 때문에 굳이 넣지 않았다.

#### 동적 사이즈를 가진 SortedList

<script src="https://gist.github.com/lutca1320/49a6ef8b21481aa97cbb9d910e3e07ad.js"></script>
