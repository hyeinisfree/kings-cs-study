# Abstract Factory Pattern
![Abstract_Factory_Pattern](https://user-images.githubusercontent.com/46441723/171158436-276892dc-02fd-4bb5-b687-8aeec2f95455.png)

## Overview

- concrete class들을 특정짓지 않고 관련된 독립적인 객체들을 생성할 수 있는 인터페이스를 제공할 수 있는 것이 Abstract factory patter이다.

## Participants

- AbstractFactory
    - abstract product 객체들을 생성하는 작업(operation)들에 대한 인터페이스를 정의한다.
- ConcreteFactory
    - concrete product 객체들을 생성하는 작업들을 구현한다.
- AbstractProduct
    - product 객체의 인터페이스를 정의한다.
- ConcreteProduct
    - concrete factory가 생성하는 product 객체를 정의한다.
    - AbstractProduct 인터페이스를 구현한다.
- Client
    - abstract factory와 abstract product가 정의해놓은 인터페이스를 사용한다.

## Benefits & Liabilities

1. concrete class를 isolate 시킬 수 있다. 
    - factory가 product object 생성 과정과 생성에 대한 책임(responsibility)를 encapsulate 하기 때문에 클라이언트는 클래스 구현에 대한 것을 몰라도 된다. → 클라이언트는 abstract interface를 통해 인스턴스들을 manipulate 할 수 있다.
    - concrete factory 내에 product class name들이 isolate 되어 있기 때문에 클라이언트 코드들에서는 product class의 이름이 등장하지 않는다.
2. product family 사이의 exchanging을 쉽게 만든다.
3. product들 사이의 일관성(consistency)을 도모한다.
4. 새로운 종류의 product를 제공하는 것이 힘들 수 있다.
    - AbstractFactory 인터페이스가 생성할 수 있는 product들을 정해놓았기 때문에, 새로운 product 생성에 대한 인터페이스 확장이 수반 돼야한다.