---
title:  "바이너리갭"
excerpt: "코딜리티"

categories:
  - Coding
tags:
  - Coding
  - Coldilty
  - BinaryGap
  - 코딜리티
last_modified_at: 2019-12-20T03:00:00

 
#toc : true
#toc_label : Contents
#toc_icon: #

---

코딜리티의 첫번째 문제. 
여러가지 풀이 방법이 있겠지만 `Integer.toBinaryString()` 을 이용하여 풀어냈다.


```java

public class No01_BinaryGap {

    public static void main(String[] args) {
        int solution = solutionByBinaryTransform(1041);
        System.out.print(solution);
    }


    public static int solutionByBinaryTransform(int num) {
        String s = Integer.toBinaryString(num);
        System.out.println("binary : " + s);

        int count = 0;
        int countTemp = 0;

        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '1') {
                if (count < countTemp) {
                    count = countTemp;
                }
                countTemp = 0;
            }
            if (s.charAt(i) == '0') {
                countTemp++;
            }
        }

        return count;

    }
}
```

다른 문제풀이를 검색해보면 여러 방법이 존재하는데 그중 `String.strip()`을 이용한 방법이 흥미로웠다.
여기서 `String.strip()` 이라는 메서드를 또 배워간다.

```java
String.strip 사용법

```


`Integer.toBinary` 이진변환법에 대해서도 직접 구현해 보았다.
```java

```