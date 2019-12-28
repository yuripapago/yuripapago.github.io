---
title:  "TapeEquilibrium"

categories:
  - Coding
tags:
  - Coding
  - Codility
  - TapeEquilibrium
  - 코딜리티
---
문제 이해가 다소 어려웠었다. 주어진 배열을 차례로 쪼개어 잘랐을때 왼쪽과 오른쪽의 합계의 차이가 가장 적은 값을 구하는 것이다.
아래는 코딜리티 예제인에 갑자기 10이 뜬금 등장하여 혼란스러웠다.

[3, 1, 2, 3, 4]
    | 3 - 10 | = 7
    | 4 - 9  | = 5
    | 6 - 7  | = 1
    | 9 - 4  | = 5
3과 1,2,3,4 의 합인 3-10의 차이는 7,
3,1과 2,3,4 의 합인 4-9의 차이는 5 ...

이런식으로 풀어가는 문제였다. 문제가 이해되면 코드는 쉽게 해결된다.
최초 루프에서 전체 합계를 구한후 다음 루프에서는 하나씩 빼주면서 계산해 나가면 된다.

다만 하나의 함정이 있었으니 마지막 배열은 굳이 합산안해도 되므로 `array.length -1` 을 적용해줘야 100% 목표달성이 된다.


```java
   public int solution(int[] arr) {
         int forwardSum = 0;
         int backwardSum = 0;
         int result = Integer.MAX_VALUE;
         int tmp;

         for (int i = 0; i < arr.length; i++) {
             backwardSum += arr[i];
         }

         for (int i = 0; i < arr.length - 1; i++) { //이 부분이 다소 함정?
             forwardSum += arr[i];
             backwardSum -= arr[i];
             tmp = Math.abs(forwardSum - backwardSum);

             if (result > tmp) {
                 result = tmp;
             }

         }
         return result;
     }
```
