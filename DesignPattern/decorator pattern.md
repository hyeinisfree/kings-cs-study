# decorator pattern

### **구조패턴**

프로그램 내의 자료구조나 인터페이스 구조 등 프로그램 구조를 설계하는데 활용 될 수 있는 패턴.

클래스, 객체들의 구성을 통해서 더 큰 구조를 만들 수 있게 해준다. 큰 규모의 시스템에서는 많은 클래스들이 서로 의존성을 가지게 되는데 이런 복잡한 구조를 개발하기 쉽게 만들어주고 유지 보수하기 쉽게 만들어준다. 

### **decorator pattern**

데코레이터 패턴은 기존 뼈대(클래스)는 유지하면서, 이후 필요한 형태로 꾸밀 때 사용한다. 확장이 필요한 경우 상속의 대안으로도 활용한다. SOLID중에서 개방패쇄 원칙(OCP)과 의존 역전 원칙(DIP)를 따른다.

<img width="782" alt="구조" src="https://user-images.githubusercontent.com/46683113/172127508-ae356ca7-4eec-4260-a82b-564d29a3bf87.png">


- 의존 역전 원칙 DIP(Dependency Inversion Principle)
    
    자신보다 변하기 쉬운 것에 의존하면 안 된다. 어떤 객체의 구성품이 변하기 쉬운 것이라면 그 구성품의 추상적인 상위클래스를 만들어 그 상위클래스에 의존하게 해야한다. 
    
    예) 스노우 타이어와 자동차  
    

### **왜 데코레이터 패턴이 필요할까**

- **클래스를 그냥 상속받을 경우  : 작은 규모일 때는 간편하지만 규모가 커지면 클래스의 개수가 너무 많아진다.**

<img width="400" alt="beverage" src="https://user-images.githubusercontent.com/46683113/172127575-87b2e025-5a13-492e-ab39-4bfc91fd2207.jpeg">


<img width="400" alt="expand_menu" src="https://user-images.githubusercontent.com/46683113/172127629-97c3e4e1-9d28-4b8c-a5ce-efd0cd9905b4.jpeg">


- **멤버변수와 슈퍼 클래스를 이용해 상속받는 경우**
    
    ![add_method](https://user-images.githubusercontent.com/46683113/172127670-926f2778-f9cc-4fd7-b81a-64abd2693f5b.jpeg)

    

만약 새로운 인스턴스변수가 생성되거나 메서드의 동작이 바뀐다면 기존 클래스의 코드를 수정해야 한다. 이는 개방폐쇄 원칙에 어긋난다. 

- OCP(Open Close Principle)
    - 클래스는 확장에 대해서는 열려 있어야 하지만 코드 변경에 대해서는 닫혀 있어야 한다.
    - 즉 기존 코드는 건드리지 않은 채로 확장을 통해서 새로운 행동을 간단하게 추가할 수 있도록 하면,새로운 기능을 유연하게 추가할 수 있어, 주변 환경에 잘 적응할 수 있으면서도 강하고 튼튼한 디자인을 만들 수 있다.
    
- **데코레이터를 따로 만드는 경우**

![decorator_image](https://user-images.githubusercontent.com/46683113/172127795-21e2c93f-1af4-4b06-95ba-10e68b06a16e.jpeg)


ConcreteComponent 클래스: HouseBlend, DarkRoast, Espresso,Decaf

-인스턴스 생성가능

ConcreteDecorator : Milk, Mocha,Soy,Whip … 

```java
//다크로스트 커피 + 모카+ 모카 + 휘핑크림
    Beverage darkRoast = new DarkRoast();  //다크로스트 커피
    darkRoast = new Mocha(darkRoast);	    //모카 추가
    darkRoast = new Mocha(darkRoast);	    //모카 한번 더 추가
    darkRoast = new Whip(darkRoast);	    //휘핑크림 추가		
    System.out.println(darkRoast.getDescription()+ 
        " : $"+darkRoast.cost());
```

다형성을 이용해 모든 음료를 Beverage 로 만들 수 있다

### 예시

java I/O 

![javaIO](https://user-images.githubusercontent.com/46683113/172127876-23253b54-0c8f-4a2c-86f9-e4a0a12de515.jpeg)

```java
//test.txt 파일을 읽어 오는데 BufferInputStream으로 wrapping 해서 byte 단위로 파일을 읽어옴
// 속도 향상
InputStream in= new BufferInputStream(new FileInputStream("test.txt"))
```

출처 : [http://wiki.gurubee.net/pages/viewpage.action?pageId=1507398](http://wiki.gurubee.net/pages/viewpage.action?pageId=1507398)