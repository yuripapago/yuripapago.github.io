---
title:  "디자인패턴::커맨드패턴"
categories:
  - DesignPattern
tags:
  - DesignPattern
  - 디자인패턴
  - Command
  - 커맨드
---

커맨드(Singleton)패턴은 어떤 이벤트가 발생했을 때, 실행해야할 기능이 다양한 경우 인터페이스를 활용하여
그 기능을 제어 수 있도록 하는 패턴이다.
설명으로는 매우 추상적이고 전략(Strategy)패턴과 무슨차이가 있는지 감이 잘 오지 않는다.
전략패턴과의 차이점에 대해서는 전략패턴 글에서 설명하기로 하고
이 곳에서는 커맨드 패턴의 예제 코드를 살펴본다.

[커맨드패턴 코드보기](https://github.com/yuripapago/cote/tree/master/src/main/java/yuripapago/designpattern/command)

```java
public class DownloadCommand implements FtpCommand {
    @Override
    public void execute() {
        System.out.println("put file from remote ftp server");
    }
}


public class UploadCommand implements FtpCommand {
    @Override
    public void execute() {
        System.out.println("put file to remote ftp server");
    }
}



public interface FtpCommand {
    void execute();
}


public class FtpClient {

    private FtpCommand ftpCommand;

    public FtpClient() {

    }

    public FtpClient(FtpCommand ftpCommand) {
        this.ftpCommand = ftpCommand;
    }

    public void setFtpCommand(FtpCommand ftpCommand) {
        this.ftpCommand = ftpCommand;
    }


    public void execute() {
        ftpCommand.execute();
    }
}

```
```java

public class FtpClientTest {

    @Test
    public void test() {
        FtpClient client = new FtpClient();
        client.setFtpCommand(new UploadCommand());
        client.execute();


        client.setFtpCommand(new DownloadCommand());
        client.execute();

    }
}
```
너무나 단순하다. 조금만 코드를 읽어으면 이해할 수 있는 수준의 코드이다.

한가지 응용할 부분은 인터페이스에 구현할 메서드가 하나만 있는 경우 `FunctionalInterface` 라고도 한다.
구현해야할 인터페이스가 하나도 없는 경우 `MakerInterface` 라고 한다.
두 가지 주제에 대해서는 따로 한번 다룰 예정이다.

`FunctionalInterface` 는 자바1.8에서 미리 선언되어있는 인터페이스를 이용하여 별도의 클래스 구현 없이도 간단하게 사용할 수 있다
```java
  @Test
    public void test2() {
        FtpClient client = new FtpClient();
        client.setFtpCommand(() -> System.out.println("put file to remote ftp server"));
        client.execute();

        client.setFtpCommand(() -> System.out.println("get file from remote ftp server"));
        client.execute();
    }
```
