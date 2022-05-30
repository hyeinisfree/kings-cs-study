# 빌더 패턴(Builder Pattern)
GoF 디자인 패턴 중 **생성** 패턴
---
## GoF(Gang of Four) 디자인 패턴
### 디자인 패턴?
소프트웨어를 설계할 때 자주 발생하는 문제들에 대한 재사용 가능한 해결책  
디자인 패턴을 통해 설계 문제, 해결 방법, 해결 방법을 언제 적용해야 할지, 그 결과를 알 수 있음  

### GoF
**목적**에 따라 분류할 시 `생성` 패턴 5개, `구조` 패턴 7개, `행위` 패턴 11개  
**범위**에 따라 분류할 시 `클래스` 패턴 3개, `객체` 패턴 19개 혼용 패턴 1개  
총 23개의 패턴으로 구성

- 생성 패턴(Creational Patterns)
  - 객체의 생성 과정에 관여를 해서 유연성을 높이고 코드의 유지/보수를 쉽게함
- 구조 패턴(Structural Patterns)
  - 클래스나 객체들을 조합해서 더 큰 구조로 만들어줌
- 행위 패턴(Behavioral Patternss)
  - 클래스나 객체들이 서로 상호작용하는 방법, 어떤 작업이나 알고리즘을 적합한 객체에 할당하는 것을 정의
  - 즉, 객체와 클래스의 **교류 방법**에 대해 정의
  <br><br>
- 클래스 패턴
  - 클래스와 서브 클래스 간의 관련성, 주로 상속과 관련. 컴파일 때 정적으로 결정
- 객체 패턴
  - 객체간의 관계 또는 관련성. 런타임에 변경될 수 있는 동적인 성격
---
### 개념
복잡한 객체를 생성하는 클래스와 표현하는 클래스를 분리하여, 서로 다른 표현이라도 이를 생성하는 절차는 동일하게 제공하는 패턴
빌더 패턴을 통해 많은 Optional한 멤버 변수(혹은 파라미터)나 지속성 없는 상태 값들에 대해 처리해야 하는 문제 해결 가능  

- 생성 패턴인 `팩토리 패턴`이나 `추상 팩토리 패턴`에서 발생하는 이슈
  1. 클라이언트 프로그램으로부터 팩토리 클래스로 많은 파라미터를 넘겨줄 때 타입, 순서 등에 대한 관리가 어려워져 에러가 발생할 확률 높음
  2. 경우에 따라 필요 없는 파라미터들에 대해서 팩토리 클래스에 일일이 null 값을 넘겨줘야 함
  3. 생성해야 하는 sub class가 무거워지고 복잡해짐에 따라 팩토리 클래스 또한 복잡해짐
-> 위의 문제들을 해결하기 위해 **별도의 Builder 클래스**를 만들어 필수 값에 대해서는 `생성자`를 통해, 선택적인 값들에 대해서는 `메소드`를 통해 step-by-step으로 값을 입력받은 후에 build() 메소드를 통해 최종적으로 하나의 인스턴스 리턴  

### 사용법
- 객체의 생성 알고리즘이 조립 방법에 독립적일 때
- 합성할 객체들의 표현이 서로 다르더라도 생성 절차에서 표현 과정을 지원해야할 때

### 구조
- `Builder(건축자)`
  - 인스턴스 생성을 위한 인터페이스(API) 선언
- `ConcreteBuilder(구체적인 건축자)`
  - Builder 인터페이스 구현
- `Director(감독자)`
  - Builder 인터페이스(API)를 사용해 인스턴스 사용
- `Productor(제품)`
  - 만들어질 제품의 속성과 기능을 가짐
![builder](https://user-images.githubusercontent.com/60397314/170934093-20f5cfe9-27b3-468e-a6fb-42ec13169715.png)
- Builder `추상클래스`를 정의하고 이를 상속받은 ConcreteBuilder `서브클래스`를 구현
- Product의 일부가 build될 때마다 Director는 Builder에 통보
- Builder는 Director의 요청을 처리해 Product에 부품을 추가

### 장점
- 표현을 다양하게 변경할 수 있음
- 생성과 표현 코드를 분리함
- 복합 객체를 생성하는 절차를 세밀하게 나눌 수 있음


<br><br>
**출처**  
- [GoF Design Pattern 이란](https://velog.io/@wooko5/GoF-Design-Pattern-%EC%9D%B4%EB%9E%80)
- [[Design Pattern] GoF(Gang of Four) 디자인 패턴](https://4z7l.github.io/2020/12/25/design_pattern_GoF.html)  
- [[Design Pattern] GoF 생성 패턴 - 빌더 패턴(Builder Pattern)](https://4z7l.github.io/2021/01/19/design_pattern_builder.html)  
- [[생성 패턴] 빌더 패턴(Builder pattern) 이해 및 예제](https://readystory.tistory.com/121)