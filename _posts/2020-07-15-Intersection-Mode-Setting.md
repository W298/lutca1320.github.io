---
title: 도로 제작 - 1. 모드 설정
author: RUKA SPROUT
date: 2020-07-15 12:00:00 +0900
categories: [Game Dev - Intersection]
tags: [Unity]
---

이 게임은 꽤 복잡한 시스템을 가지고 있는데, 도로를 그리는 조작까지 복잡해지면 유저가 초반에 적응하기 힘들 것이다. 그래서 매우 직관적이고 간단한 조작을 만들기 위해 거의 모든 조작은 마우스 버튼의 누름(ButtonDown) 과 눌러져 있는 상태(Button), 그리고 땜(ButtonUp) 을 이용하여 설계하였다.

이러한 조작을 만들기 위해, '모드'를 정의하였다.

---

- `BUILD` (Default) : 도로를 스폰한다.
- `APPEND` : 도로를 이어 붙인다.
- `REMOVE` : 도로를 삭제한다.

![Intersection Mode System](https://i.imgur.com/xzsn8VT.png)

- 초기 값은 `BUILD` 모드로 되어 있고, 마우스 버튼을 누르는 순간 `runBuild` 함수가 호출된 후 모드를 `APPEND` 모드로 변경한다.
- `APPEND` 모드에서는 마우스 버튼을 누르고 있으면 `runAppendModeGrid` 함수가 호출되고, 마우스 버튼을 때는 순간 `BUILD` 모드로 돌아간다.

![Mode System](https://i.imgur.com/1dnwaDe.gif)

#### 스크립트

```csharp
if (current_mode == MODE.BUILD)
{
    if (Input.GetMouseButtonDown(0))
    {
        // BUILD MODE
        runBuildMode();
    }
    else if (current_mode == MODE.APPEND)
    {
        // APPEND MODE
        runAppendModeGrid();
    }
}
```

- `current_mode` : 현재 모드를 저장하는 변수
- `runBuildMode` : 도로 스폰 함수
- `runAppendModeGrid` : 현재 도로의 포인트 추가 (이어붙이기)

```csharp
void runBuildMode()
{
    UnityEngine.Debug.LogWarning("RunBuild!");

    new_index = 0;

    SpawnPath();

    if (current_spline)
    {
        current_spline.Rebuild(true);
    }

    AppendPath();
    new_index++;

    current_mode = MODE.APPEND;
}
```

- `SpawnPath` : 사전 정의한 `SplineComputer` 를 스폰
- `AppendPath` : 현재 `SplineComputer` 에 포인트 하나 추가 (Snapping 될 때 `true` 리턴)
- `new_index` : 다음 포인트 인덱스

```csharp
void runAppendModeGrid()
{
    if (Input.GetMouseButton(0))
    {
        if (AppendPath())
        {
            new_index++;
        }
    }
    else if (Input.GetMouseButtonUp(0))
    {
        new_index = 0;
        current_mode = MODE.BUILD;
    }
}
```
