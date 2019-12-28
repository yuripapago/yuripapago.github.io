---
title:  "FrogJump"

categories:
  - Coding
tags:
  - Coding
  - Codility
  - FrogJump
  - 코딜리티
---

출발지 x 에서 목적지 y 까지 d 거리만큼 개구리가 연속해서 점프하는 경우 몇 번을 점프해야 도착할 수 있는지를 물어보는 문제.
새삼 급 문제 난이도가 쉬워서 외려 함정이 있을까 생각한 문제였다.


```java
 public int solution(int x, int y, int d) {
         if (x == y) {
             return 0;
         }

         int distance = (y - x);
         if (distance <= d) {
             return 1;
         }

         return distance % d == 0 ? distance / d : (distance / d) + 1;
     }
```
