---
title:  "BinaryGap"

categories:
  - Coding
tags:
  - Coding
  - Codility
  - BinaryGap
  - 코딜리티
last_modified_at: 2019-12-20T03:00:00

 
#toc : true
#toc_label : Contents
#toc_icon: #

---

코딜리티의 첫번째 문제. 
주어진 정수값에 대해서 이진 변환 후 연속적으로 가장 많이 발생한 0의 개수를 구하는 문제였다.

여러가지 풀이 방법이 있겠지만 `Integer.toBinaryString()` 을 이용하여 풀어냈다.


```java
    public int solution(int num) {
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
 
```
 

이진변환에 대해서도 직접 대충 구현해 보았다.

```java
    @Test
    public void testBinary() {
        int data = 10;
        int remain = 0;
        
        List<Integer> arr = new ArrayList<>();

        while (data > 0) {
            remain = data % 2;
            data = data / 2;
            arr.add(remain);
        }

        for (int i = arr.size() - 1; i >= 0; i--) {
            System.out.print(arr.get(i));
        }
    }
```