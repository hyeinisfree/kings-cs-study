# 브릿지 패턴(Bridge Pattern)
GoF 디자인 패턴 중 **구조** 패턴

## 개념
구현부를 기능과 구현 두 개의 별도 클래스로 구현하여 각자 독립적으로 변형이 가능하고 확장이 가능하도록 한다.

1. 새로운 기능(=새로운 메서드)을 추가하고 싶은 경우
  - ![bridge_2](https://user-images.githubusercontent.com/60397314/172101491-3227842b-358a-4e13-a0bd-f8618f9b0489.jpg)  
  - `Something`을 상속한 자식 클래스로 `SomethingGood` 클래스 생성
  - 상위 클래스는 기본적인 기능을 갖고 있고 하위 클래스에 새로운 기능 추가
  - 상위 클래스와 하위 클래스의 역할 분담에 의해 부품으로서의 가치(교환 가능성)가 높은 클래스 생성 가능
2. 새로운 구현을 추가하고 싶은 경우
    - ![bridge_3](https://user-images.githubusercontent.com/60397314/172101496-4847bba5-d8b6-4510-b350-9cf1ef3e648f.jpg)
    - 상위 클래스는 추상 메서드에 의한 인터페이스(API)를 규정, 하위 클래스는 구체적인 메서드에 의해 그 인터페이스를 구현
    - 새로운 구현을 만들기 위해서는 `AbstractClass`의 하위 클래스를 만들어 추상 메서드 구현

만약 클래스 계층이 한개라면 기능 클래스 계층과 구현 클래스 계층이 하나의 계층 구조 안에 섞임
따라서 이를 두 개의 독립된 클래스 계층으로 분리해 그 사이에 bridge 연결

## 구조
![bridge](https://user-images.githubusercontent.com/60397314/172100591-69355874-2e35-4785-b4e7-555b4011a1fb.png)  
- Abstraction: 기능 계층의 최상위 클래스로 추상 인터페이스
- RefinedAbstraction: 기능 계층에서 새로운 부분을 확장한 클래스
- Implementor: Abstraction의 기능을 구현하기 위한 인터페이스 정의
- ConcreteImplementor: 실제 기능을 구현하는 클래스

## 구현
![images_cham_post_20d9a039-df07-4981-bfce-22958c2e608b_image](https://user-images.githubusercontent.com/60397314/172102939-4dd09092-fdee-410a-8962-2d6898ff73ad.png)  
### Abstraction
```javascript
public class Animal {

    private Hunting_Handler hunting;

    public Animal(Hunting_Handler hunting)
    {
        this.hunting=hunting;
    }
    public void Find_Quarry()
    {
        hunting.Find_Quarry();
    }
    public void Detected_Quarry()
    {
        hunting.Detected_Quarry();
    }
    public void attack()
    {
        hunting.attack();
    }
    public void hunt()
    {
        Find_Quarry();
        Detected_Quarry();
        attack();
    }
}
```
- 객체 생성과 기능에 대한 method 정의
---
### RefinedAbstraction
```javascript
public class Bird extends Animal
{
    public Bird(Hunting_Handler hunting)
    {
        super(hunting);
    }
    public void hunt()
    {
        System.out.println("새의 사냥방식");
        Find_Quarry();
        Detected_Quarry();
        attack();
    }
}
```
```javascript
public class Tiger extends Animal
{
    public Tiger(Hunting_Handler hunting)
    {
        super(hunting);
    }
    public void hunt()
    {
        System.out.println("호랑이의 사냥방식");
        Find_Quarry();
        Detected_Quarry();
        attack();
    }
}
```
- 각 기능들을 조합하여 구현
---
### Implementor
```javascript
public interface Hunting_Handler {
    void Find_Quarry();
    void Detected_Quarry();
    void attack();
}
```
- 사냥법 Method에 대한 인터페이스 정의
---
### ConcreteImplementor
```javascript
public class Hunting_Method1 implements Hunting_Handler {
    public void Find_Quarry()
    {
        System.out.println("물 위에서 찾는다");
    }
    public void Detected_Quarry()
    {
        System.out.println("물고기 발견!");
    }
    public void attack()
    {
        System.out.println("낚아챈다.");
    }
}
```
```javascript
public class Hunting_Method2 implements Hunting_Handler {
    public void Find_Quarry()
    {
        System.out.println("지상에서 찾는다");
    }
    public void Detected_Quarry()
    {
        System.out.println("노루 발견");
    }
    public void attack()
    {
        System.out.println("물어뜯는다.");
    }
}
```
- 사냥법에 대한 실제 출력 기능들 정의
---
### Main
```javascript
public static void main(String argsp[]){
    Animal tiger = new Tiger(new Hunting_Method2());
    Animal bird = new Bird(new Hunting_Method1());

    tiger.hunt();
    System.out.println("--------------");
    bird.hunt();
    }
```
```markdown
호랑이의 사냥방식
지상에서 찾는다
노루 발견
물어뜯는다.
--------------
새의 사냥방식
물 위에서 찾는다
물고기 발견!
낚아챈다.
```

<br><br>
**출처**  
- [07 브릿지 패턴 (Bridge Pattern)](https://lktprogrammer.tistory.com/35)
- [[디자인 패턴] Bridge 패턴 (기능계층과 구현계층 분리하기)](https://m.blog.naver.com/tradlinx0522/220928963011)
- [[Design Pattern] 브릿지 패턴(Bridge Pattern)](https://velog.io/@cham/Design-Pattern-%EB%B8%8C%EB%A6%BF%EC%A7%80-%ED%8C%A8%ED%84%B4Bridge-Pattern)
