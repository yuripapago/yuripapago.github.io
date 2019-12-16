---
layout: post
title: "Codility::BinaryGap"
subtitle: "바이너리갭"
date: 2019-12-10 00:00:00
background: '/img/bg-post.jpg'
category: jekyll/blog
---

# 바이너리 갭

코딜리티의 첫 번째 문제.
다른 알고리즘 사이트의 첫 번째 문제와는 달리 다소 난이도가 있다.
숫자가 주어지면 이진수로 변환하고 그 이진수의 0의 개수를 세는 프로그램을 만들어야 한다는 생각이 번뜩 드는데
'이진 변환을 어떻게 했더라?' 하는 급작스러운 의문이 당혹케 할 수 도 있다.

연습만이 살 길이고 당황하지 않는 첫 걸음이다.

좋은 알고리즘과 다른 풀이가 있겠지만 나는 이렇게 풀었다.

```java
class Solution {
     public int solution(int N) {

        String s = Integer.toBinaryString(N);
        //System.out.println("binary : " + s);

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

# 풀이
우선 int를 바이너리 String 으로 변환하고, `charAt()`을 이용하여 gap을 세어 풀어냈다.
