---
title:  "디자인패턴::싱글톤패턴"
categories:
  - DesignPattern
tags:
  - DesignPattern
  - 디자인패턴
  - Singleton
  - 싱글톤
---

싱글톤(Singleton)패턴 이라는 이름은 너무나 익숙하게 알려진 이름이다.
단순하게 객체를 사용할 때마다 매번 생성하지 않고 하나의 객체를 생성하는 패턴이며
아래 코드 처럼 생성자를 private 로 선언하여 객체생성을 제약하는 기술이 결합된 패턴이다.

```java
public class Singleton {
    private static Singleton instance = null;

    private Singleton() {
        System.out.println("singleton construct");
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }

}
```
다만 이 코드는 심각한 결함이 존재한다.
객체 생성과정에서 멀티스레드로 접근하는 경우 싱글톤 객체 생성을 보장하지 못한다. 즉 thread-safe 하지 못하는 것이고
이를 위해 생성자에 `synchronized` 키워드가 포함되어야 한다.
이때 `synchronized` 에 의한 성능 감소를 최소화하고자 `volatile` 을 이용한 방법을 사용하기도 했었다.

```java
public class Singleton {
    private volatile static Singleton instance = null;

    private Singleton() {
        System.out.println("instance construct");

    }

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null)
                    instance = new Singleton();
            }
        }
        return instance;
    }
}
```

최근에는 `Holder` 를 이용한 방식으로 jvm 내부에서 싱글톤을 원자적으로 처리할 수 있게 하는 방식이 사용된다.
덕분에 `synchronized` 도 보기싫던 `if` 구문도 모두 사라지고 안전한 싱글톤을 이용할 수 있게 되었다.


```java
public class Singleton {
    private Singleton() {
        System.out.println("instance construct");

    }

    private static class SingletonHolder {
        public static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getInstance() {
        return SingletonHolder.INSTANCE;
    }
}
```




한편, 싱글톤 패턴은 정적클래스(static class)와 유사하다.
흔히 사용하는 유틸리티 클래스가 그것인데 아래처럼 생겼다.

```java
public class DateUtil {
    private static int day = 1;
    public synchronized static void addDay() {
        day++;
        System.out.println("day : " + day);
    }
}
```
이렇게 사용한다면 굳이 싱글톤 객체를 만들 필요도 없으며, 정적 클래스가 단 한개의 인스턴스만 있음을 보장한다.
다만 유틸리티 처럼 사용하는 정적클래스가 아닌 인터페이스를 구현해야하는 과정에서는 위의 싱글톤 패턴 기법이 필요하다.


번외로 이펙티브자바에서는 `enum`을 사용한 싱글톤 기법도 소개하면서
원소가 하나뿐인 enum 자료형은 싱글톤을 구현하는데 가장 좋은 방법이라고 소개한다.
리플렉션에 의한 공격이나 직렬화에서 안전하기 때문이란다. 실제 써본적은 없다. 까먹지 않도록 적어둔다.

```java
public enum SingletonEnum {
    INSTANCE;
    static String init = "";

    public static SingletonEnum getInstance() {
        init = "test";
        return INSTANCE;
    }
}

```

