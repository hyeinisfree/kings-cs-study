# 커맨드 패턴 / Command Pattern

명령을 추상화 하여 객체로 사용한다. 명령을 오브젝트처럼 관리하면서 특정 명령을 대기시키거나 순서를 바꾸는 것을 쉽게 할 수 있음. 

<img width="936" alt="command" src="https://user-images.githubusercontent.com/46683113/174586407-05cf0ea0-a44a-4229-83aa-8db32ece7144.png">

- Invoker : 만들어둔 command들을 실행시킬 수 있는 클래스 아래 OkGoogle
- receiver : 명령을 실행하는 객체 클래스 . 아래 Heater, Lamp 등

```java
public class Heater {
    public void powerOn(){
        System.out.println("Heater on");
    }
}
```

```java
public class OKGoogle {
    private Heater heater;

    public OKGoogle(Heater heater){
        this.heater = heater;
    }

    public void talk(){
        heater.powerOn();
    }
}
```

```java
public class Client {
    public static void main(String args[]){
        Heater heater = new Heater();
        OKGoogle okGoogle = new OKGoogle(heater);
        okGoogle.talk();
    }
}
```

### lamp 기능 추가

```java
public class Lamp {
    public void turnOn(){
        System.out.println("Lamp on");
    }
}
```

```java
public class OKGoogle {
    private static String[] modes = {"heater", "lamp"};

    private Heater heater;
    private Lamp lamp;
    private String mode;

    OKGoogle(Heater heater, Lamp lamp){
        this.heater = heater;
        this.lamp = lamp;
    }

    public void setMode(int idx){
        this.mode = modes[idx];
    }
//분기가 늘어남
    public void talk(){
        switch(this.mode){
            case "heater":
                this.heater.powerOn();
                break;
            case "lamp":
                this.lamp.turnOn();
                break;
        }

    }
}
```

```java
public class Client {
    public static void main(String args[]){
        Heater heater = new Heater();
        Lamp lamp = new Lamp();
        OKGoogle okGoogle = new OKGoogle(heater, lamp);

        // 램프 켜짐
        okGoogle.setMode(0);
        okGoogle.talk();

        // 알람 울림
        okGoogle.setMode(1);
        okGoogle.talk();
    }
}

```

### 커맨드 패턴 적용

<img width="518" alt="okgoogle" src="https://user-images.githubusercontent.com/46683113/174586565-2774b230-624f-4437-84c2-c01c9e14f219.png">


```java
public interface Command {
    public void run();
}
```

```java
public class HeaterOnCommand implements Command{
    private Heater heater;

    public HeaterOnCommand(Heater heater){
        this.heater = heater;
    }

    public void run(){
        heater.powerOn();
    }
}
```

```java
public class LampOnCommand implements Command{
    private Lamp lamp;

    public LampOnCommand(Lamp lamp){
        this.lamp = lamp;
    }

    public void run(){
        lamp.turnOn();
    }
}
```

```java
public class OKGoogle {
    private Command command;

    public void setCommand(Command command){
        this.command = command;
    }

    public void talk(){
        command.run();
    }
}
```

```java
public class Client {
    public static void main(String args[]){
        Heater heater = new Heater();
        Lamp lamp = new Lamp();

        Command heaterOnCommand = new HeaterOnCommand(heater);
        Command lampOnCommand = new LampOnCommand(lamp);
        OKGoogle okGoogle = new OKGoogle();

        // 히터를 켠다
        okGoogle.setCommand(heaterOnCommand);
        okGoogle.talk();

        // 램프를 켠다
        okGoogle.setCommand(lampOnCommand);
        okGoogle.talk();

    }
}
```

- 출처

[https://victorydntmd.tistory.com/295](https://victorydntmd.tistory.com/295) (**커맨드 패턴( Command Pattern ))**
