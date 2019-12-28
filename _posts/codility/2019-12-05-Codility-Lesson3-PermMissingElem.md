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
연속된 숫자를 찾기위해서 정렬이후, N번째 값과 N+1번째 값의 차이가 1이 아닌경우 이를 리턴하면 될 것으로 생각하여 적용함.
이때 문제에서 배열은 1부터 시작한다는 전제를 깔고 개발하면 다소 쉽게 풀 수 있으나
그렇지 않으면 `ArrayIndexOutOfBoundsException` 을 방어하기 위한 입력값 검증이 추가 될 수 도 있음

약간의 함정이 있는데 1~N 사이의 값중 빈 값이 없다면 N+1을 반환하여야 한다는 점을 고려해야한다.


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
