---
title: Processing 3 드로잉
author: RUKA SPROUT
date: 2020-04-09 19:23:00 +0900
categories: [Others]
tags: [processing3]
---
[Processing 3](https://processing.org/) 를 이용해 미니언즈 (라고 주장하는) 를 그려 보았다.

### 스크린샷
![스크린샷 2020-04-09 오후 7.22.16](/assets/스크린샷%202020-04-09%20오후%207.22.16.png)

### 소스코드
s 값을 이용해 캐릭터의 크기를 조절할 수 있다.
```c
void setup()
{
  size(1000, 1000);
  background(255);

  face(width/2, height/2, 2);
  eyes(width/2, height/2, 2);
  mouth(width/2, height/2, 2);
  hair(width/2, height/2, 2);
  body(width/2, height/2, 2);
}

void eyes(int x, int y, float s)
{
  fill(76, 76, 98);
  stroke(0, 0);
  rect(x - 195*s, y - 15*s, 390*s, 30*s, 20);

  fill(129, 129, 129);
  stroke(0, 0);
  circle(x, y, 160*s);

  fill(255, 255, 255);
  stroke(0, 0);
  circle(x, y, 100*s);

  fill(76, 80, 97);
  stroke(0, 0);
  circle(x, y, 50*s);

  fill(245, 223, 109);
  stroke(0, 0);
  arc(x, y, 100*s, 100*s, PI+PI/12, 2*PI-PI/12, OPEN);
}

void face(int x, int y, float s)
{
  fill(245, 223, 109);
  stroke(0, 0);
  circle(x, y+50*s, 380*s);
}

void mouth(int x, int y, float s)
{
  fill(76, 76, 98);
  stroke(0, 0);
  rect(x - 60*s, y + 130*s, 120*s, 18*s, 20);
}

void hair(int x, int y, float s)
{
  noFill();
  stroke(76, 80, 97);
  strokeWeight(15*s);
  arc(x - 50*s, y - 120*s, 100*s, 100*s, 2*PI-PI/2.5, 2*PI-PI/10, OPEN);

  noFill();
  stroke(76, 80, 97);
  strokeWeight(15*s);
  arc(x + 50*s, y - 120*s, 100*s, 100*s, PI+PI/10, PI+PI/2.5, OPEN);
}

void body(int x, int y, float s)
{
  fill(84, 146, 228);
  stroke(0, 0);
  arc(x, y+50*s, 380*s, 380*s, PI/4, PI-PI/4, OPEN);

  fill(84, 146, 228);
  stroke(0, 0);
  rect(x-85*s, y+50*s-25*s+140*s, 170*s, 50*s, 30);

  fill(61, 113, 187);
  stroke(0, 0);
  circle(x+60*s, y+195*s, 20*s);

  fill(61, 113, 187);
  stroke(0, 0);
  circle(x-60*s, y+195*s, 20*s);
}
```
