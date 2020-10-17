---
title: Reversi 게임 제작기 - 보드, 돌 구현
author: RUKA SPROUT
date: 2020-10-17 14:22:00 +0900
categories: [Game Dev - Reversi]
tags: [Unity]
---

#### 개발 목적
Unity로 간단하게 Reversi (오델로) 보드게임을 만들고, Reversi AI 를 구축하는 데에 목적을 둘 것이다. 그렇기 때문에 게임 구현에 많은 시간을 쏟기 보다는, AI에 더 중점을 두어 개발할 것이다.

게임 메커니즘은 기존 Reversi 보드게임을 그대로 가져올 것이며, Unity 2D로 개발할 것이고, 애셋은 픽셀 아트를 직접 찍어 제작할 것이다.

지금까지는 서론이였고, 아래부터는 실제 개발을 진행할 것이다.

---

### Piece (돌) & Board (보드) 구성
Reversi 게임은 8X8 보드에서 이루어진다.

![스크린샷 2020-10-17 오후 2.35.24](https://i.imgur.com/FWiES9H.png)

#### Board
가로로 8칸, 세로로 8칸이기 때문에 구성할 때 **2차원 배열**을 사용할 것이다. 보드의 크기가 게임 도중 바뀌는 일은 없기 때문에 List 가 아닌 Array 를 사용할 것이다.

#### Grid
Board 를 구성하는 Element 들은 Grid 라는 클래스로 구성할 것이다. 위 그림에서도 보는 것처럼 그리드로 나누어져 있어서 이름을 Grid 라고 지었다.

Grid 가 가지고 있는 정보는 다음과 같이 구성하였다.
- stat : 현재 그리드 위에 어떤 Piece 가 올려져 있는지를 말한다.
    - Status (Enum) : Black = -1, None = 0, White = 1
- index : 현재 그리드가 보드에서 어느 위치에 있는지를 말한다.
- piece : 실제 Sprite 를 가지고 있는 오브젝트이다. 없을 경우 null 이다.

Status 라는 Enum 을 따로 정의했는데, 각각의 Element 에 특정 숫자를 정의해 주었다.
**Black 과 White 가 -1, 1인 이유는 값을 반전시킬 때 -1을 곱해서 하기 위함이다.**

#### Piece
*모든 Grid 가 Piece 를 가지고 있는 것은 아니지만, 모든 Piece 는 반드시 Grid 에 지정되어 있어야만 한다.*
Piece 클래스는 단지 Sprite 를 표현해 주는 용도로만 쓰이기 때문에 SpriteRenderer 컴포넌트를 조작하는 일을 맡는다.

---

### 코드 구현
아래 코드들은 정말 딱 구현만 해 둔 것이기 때문에, 서로 연결되어 있지도, 초기화되어 있지도 않다.
**이는 추후 GameMode 를 구현하면서 할 것이다.**

*참고로 필자가 C++ 스타일에 익숙해져서 그런지 자꾸 C++ 코드처럼 구현한다. 별로 상관은 없겠지만...*

#### Piece
```csharp
// Instantiate 해야 하므로 MonoBehaviour 를 상속하였다.
public class Piece : MonoBehaviour  
{
    public Sprite BlackSprite;  // 흑돌 Sprite
    public Sprite WhiteSprite;  // 백돌 Sprite

    private SpriteRenderer SR;  // Sprite 를 적용할 랜더러

    // color 파라미터 색상 Sprite 로 변경한다.
    public void SetColor(Grid.Status color)
    {
        // SpriteRenderer 를 아직 불러오지 못했을 때를 방지해 명시적으로 호출한다.
        Start();

        // Sprite 변경
        if (color == Grid.Status.Black)
        {
            SR.sprite = BlackSprite;
        }
        else if (color == Grid.Status.White)
        {
            SR.sprite = WhiteSprite;
        }
        else
        {
            // color 가 None 인 경우, Piece 가 올라와 있으면 안되기 때문에 현재 오브젝트를 제거한다.
            Destroy(this.gameObject);
        }
    }

    void Start()
    {
        // SpriteRenderer 컴포넌트를 가져온다.
        SR = GetComponent<SpriteRenderer>();
    }
}
```

#### Grid
```csharp
// 편의를 위해 보드에서의 위치를 표현해주는 Index 를 정의하였다.
using Index = System.Tuple<int, int>;

public class Grid
{
    public enum Status { Black = -1, None = 0, White = 1 }

    private Index index;    // 그리드에서의 위치
    private Status stat;    // 현재 상태 (어떤 Piece 가 올라가 있는가?)
    private Piece piece;    // Piece 오브젝트

    // Constructor
    public Grid()
    {
        index = new Index(-1, -1);
        stat = Status.None;
    }

    public Status GetStat() { return stat; }

    public Index GetIndex() { return index; }

    public void SetStat(Status stat) { this.stat = stat; }

    public void SetPiece(Piece piece) { this.piece = piece; }

    public void SetIndex(int i, int j) { this.index = new Index(i, j); }

    // 디버깅을 위해 현재 상태를 Print 한다.
    public void Print()
    {
        UnityEngine.Debug.LogWarning(index.Item1 + " / " + index.Item2 + " / " + stat.ToString());
    }
}
```

#### Matrix (보드)
```csharp
// 편의를 위해 보드에서의 위치를 표현해주는 Index 를 정의하였다.
using Index = System.Tuple<int, int>;

public class Matrix
{
    private Grid[,] data;   // Grid 배열

    // Constructor
    public Matrix()
    {
        data = new Grid[8, 8];  // 8X8 크기 지정

        for (var i = 0; i < 8; i++)
        {
            for (var j = 0; j < 8; j++)
            {
                data[i, j] = new Grid();    // 각각의 Grid 를 초기화 해주어야 한다.
                data[i, j].SetIndex(i, j);  // 각각의 Grid 에 Index 를 지정해준다.
            }
        }
    }

    public Grid[,] GetData() { return data; }

    // Index 에 있는 Grid 를 가져온다.
    public Grid GetGrid(Index index)
    {
        return data[index.Item1, index.Item2];
    }
}
```

---

#### 다음 포스트에서는...
위 클래스들은 초기화하고 연결하는 GameMode 클래스를 구현할 것이다.
