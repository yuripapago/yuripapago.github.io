---
title:  "CyclicRotation"

categories:
  - Coding
tags:
  - Coding
  - Codility
  - CyclicRotation
  - 코딜리티
---

주어진 배열에서 특정 개수만큼 오른쪽 시프트하여 그 결과 값을 리턴하는 문제이다.
단순하게 생긴대로 `deque` 를 이용하면 쉽게 풀 수 있다.

* 데큐 자료 구조는 따로 한번 정리해야겠다.

주어진 배열을 데큐로 변환하고
마지막에 들어간 값을 꺼내어 (pollLast)
가장 첫번째 자리로 넣는다. (addFirst)


```java
 public int[] solution2(int[] arr, int k) {
        //deque
        if (arr == null) {
            int empty[] = {};
            return empty;
        }
        if (k == 0) {
            return arr;
        }

        //deque
        BlockingDeque<Integer> queue = new LinkedBlockingDeque<>();
        for (int i = 0; i < arr.length; i++) {
            queue.add(arr[i]);
        }

        for (int r = 0; r < k; r++) {
            Integer peek = queue.pollLast();
            queue.addFirst(peek);
        }

        return queue.stream().mapToInt(q -> Integer.valueOf(q)).toArray();

    }
```

다른 풀이방법은 나머지 연산자를 이용하여 배열의 위치값을 한번에 결정하는 것인데,
알면 쉬운 방법이나 번뜩하게 생각하기엔 다소 어려운 알고리즘 같다.


```java
    public int[] solution(int[] arr, int k) {
        if (arr == null) {
            int empty[] = {};
            return empty;
        }
        if (k == 0) {
            return arr;
        }

        int[] ret = new int[arr.length];

        for (int i = 0; i < arr.length; i++) {
            int idx = (i + k) % arr.length;
            ret[idx] = arr[i];
        }

        return ret;
    }
```


