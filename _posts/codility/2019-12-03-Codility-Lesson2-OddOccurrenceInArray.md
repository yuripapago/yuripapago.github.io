---
title:  "OddOccurrencesInArray"

categories:
  - Coding
tags:
  - Coding
  - Codility
  - OddOccurrencesInArray
  - 코딜리티
---

주어진 정수 배열에서 짝이 없는 숫자를 찾아 리턴하는 문제이다.
매우 쉬운편이고 여러가지 풀이가 존재할 것 같다.

Set 자료구조를 이용하여 이미 데이터가 있는지 판단하여, 있으면 제거, 없으면 추가하여
마지막에 남은 하나를 리턴하는 형태이다.



```java
    public int solution(int[] arr) {

        Set<Integer> data = new HashSet<>();
        for (int i = 0; i < arr.length; i++) {
            if (data.contains(arr[i])) {
                data.remove(arr[i]);
            } else {
                data.add(arr[i]);
            }
        }
        return data.iterator().next();

    }
```

java8의 StreamAPI를 이용하여 원소별로 그룹핑하여 풀어보았다.
개인적으로는 이런 풀이가 더 이해하기 편하여 선호한다.

```java
    @Test
    public void testUseStreamAPI() {
        Map<Integer, Long> collect = Arrays.stream(arr)
                .boxed()
                .collect(Collectors.groupingBy(c -> c, Collectors.counting()));

        int result = collect.entrySet().stream()
                .filter(entry -> entry.getValue() % 2 != 0)
                .map(entry -> entry.getKey()).findAny().orElse(0);

        System.out.print(result);
    }
```

다른 답변으로는 XOR를 이용한 연산이 있는데 굳이 이렇게 까지 풀어야할 이유는 없어보인다.
성능을 매우 따져야하는 구간에서 적용해 볼 만할 것 같다.

