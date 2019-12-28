---
title:  "PermMissingElem"

categories:
  - Coding
tags:
  - Coding
  - Codility
  - PermMissingElem
  - 코딜리티
---

연속된 숫자 배열에서 없는 수를 찾아 리턴하는 문제.
연속(N+1)된 숫자를 찾기위해서 정렬이후, N번째 값과 N+1번째 값의 차이가 1이 아닌경우 이를 리턴하면 될 것으로 생각하여 적용하였으나
의외로 쉽게 풀리지 않았음.

약간의 함정이 있는데 1~N 사이의 값중 빈 값이 없다면 N+1을 반환하여야 한다는 점
문제에서 배열은 1부터 시작한다는 전제를 깔고 있어 더욱 쉽게 풀 수 있었음.


```java
 public int solution(int[] arr) {

         Arrays.sort(arr);

         for (int i = 0; i < arr.length; i++) {

             if (arr[i] != i + 1) {
                 return i + 1;
             }
         }

         return arr.length + 1; //이 부분이 문제의 함정이라 생각
     }
```
