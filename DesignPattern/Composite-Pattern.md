# Composite Pattern

## Overview
* Composite 패턴은 structural pattern에 포함된다.
* Structural pattern은 클래스와 객체(object)들이 어떻게 구성되어(compose) 큰 structure를 형성하는지 고려하는 것이다.

## Composite Pattern의 목적
* `composite` 이라는 이름에서 알 수 있게 `composite pattern` 은 객체들이 part-whole hierarchy를 이룰 수 있도록 트리 구조로 객체들을 구성한다.
* 또, `composite pattern` 은 클라이언트가 각각의 객체와 여러 객체로 구성된 것을 동일한 인터페이스로 사용할 수 있게 한다.

## Composite Pattern은 언제 사용할까?
* 객체들의 part-whole hierarchy를 구성하고 싶을 때
* 클라이언트가 각각의 객체나 여러 객체로 구성된 것을 구분하지 않고 동일한 인터페이스로 사용하게 하고 싶을 때

## Composite Pattern의 구조
![CleanShot 2022-06-06 at 19 34 39@2x](https://user-images.githubusercontent.com/46441723/172144860-02dbf694-8177-4fe5-8a8d-fe7470c2f916.png)

* Component (위 그림의 Graphic)
    * composition에 포함될 객체들에 대한 일관된 인터페이스를 정의하는 역할이다.
    * 모든 클래스들이 가져야할 공통적인 행동(behavior)을 제공한다.
    * child component들에게 접근하고, 관리할 수 있는 인터페이스를 정의한다.
    * (optional) component의 부모에 접근할 수 있는 인터페이스를 정의한다.

* Leaf (Rectangle, Line, Text, etc.)
    * composition의 leaf 객체를 나타낸다. leaf에게는 당연히 자식이 없어야한다.
    * composition의 primitive 객체들에 대한 행동을 정의한다.

* Composite (위 그림의 Picture)
    * chilren을 갖는 component들에 대한 행동을 정의한다.
    * child component들을 저장(store)한다.
    * Component 인터페이스에 정의되어 있는 child 관련 operation들을 구현한다.

* Client
    * Component 인터페이스를 통해 composition의 객체들을 변경(manipulate)한다. 즉, Composition 객체들을 일관된 인터페이스(Component가 정의한 인터페이스)를 통해 사용하는 주체이다.

## Composition Pattern을 사용한 결과
* 클라이언트가 단순해진다.
    * 클라이언트는 primitive 객체와 composite structure를 동일한 인터페이스를 통해 사용할 수 있다.
    * 즉, 클라이언트는 지금 다루는 객체가 primitive인지 composite인지 몰라도 된다. 클라이언트측 코드가 단순해짐은 물론이고 재사용성 또한 높일 수 있는 것이다.

* 새로운 종류의 component를 추가하기 쉬워진다.
    * 새로운 composite나 leaf가 추가되더라고 기존의 클라이언트 코드에서 동일하게 사용될 수 있다.

* Overly general한 디자인이 적용될 수 있다.
    * 새로운 component를 추가하기 쉽게 만들면 composite을 이루는 구성원에 대한 제약을 걸기 힘들어진다. 
    * 어떤 상황에서는 특정 component들만 갖는 composite을 만들고 싶을 수 있다. 이때, composite의 사용만으로는 타입 시스템을 통한 제약을 둘 수 없다. 따라서 런타임 때 component의 타입을 체크해야한다.

