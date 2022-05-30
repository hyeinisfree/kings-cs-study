## 생성패턴

생성 패턴은 인스턴스를 만드는 절차를 추상화하는 패턴입니다.

생성 패턴에 속하는 패턴들은 객체를 생성, 합성하는 방법이나 객체의 표현 방법을 시스템과 분리해줍니다.

다시말해, 생성 패턴을 이용하면 무엇이 생성되고, 누가 무엇을 생성하며, 이것이 어떻게 생성되는지, 언제 생성할 것인지 결정하는 데 유연성을 확보할 수 있게 됩니다. (뭔말인지..모르겠고 대충 그런걸 생성 패턴에서 관여하기 때문에 신경쓰지 않아도 된다는 소리인듯)

## 프로토타입 패턴

생성 패턴 중 하나인 프로토타입 패턴은 객체를 생성할 때 우리가 흔히 사용하는 new를 사용해서 새로운 객체를 생성하지 않고, 기존에 있는 객체(이게 프로토타입)으로부터 (깊은)복사해서 객체를 생성하는 방법론이다.

### 프로토타입 패턴을 사용하기에 적절한 경우

- 객체를 새로 생성하는 데 시간과 노력이 많이 들고, 이미 유사한 객체가 존재하는 경우
- 유사한 객체를 많이 만들어야 하는 경우
- 적은 자원으로 많은 객체를 생성해야 하는 경우


### 프로토타입 패턴을 사용하는 이유

- 일반적인 방법으로 (new 키워드 사용) 객체를 생성할 경우, 생성할 때 마다 자원(메모리)의 소모가 비교적 크다.
- 객체를 많이 생성하거나, 객체 생성 과정이 복잡할수록 부하와 자원의 소모가 커짐
- 이 대신, 이미 만들어진 객체를 ‘깊은복사’하여 또 다른 객체를 생성하면 객체를 새로 생성하는 데에 필요한 처리시간과 자원을 아낄 수 있음


### 자바에서 프로토타입 패턴을 적용한 예

자바에서 프로토타입 패턴을 적용할 때에는 Cloneable 인터페이스를 구현하여 사용하는 clone() 메서드를 사용한다.

1. 우선 프로토타입 패턴을 적용할 클래스가 **`Cloneable`** 인터페이스의 구현클래스여야 함
2. 깊은복사를 하기 위해 clone() 메서드를 재정의함 (clone() 재정의 함수에 원하는 깊은복사 코드 포함)
3. 실제 사용시 new 대신 이미 만들어져 있는 객체의 clone() 메서드를 호출하여 생성

```
public class Prototype implements Cloneable{
 
    private String name;
	
    public Prototype(){
        name = "name";
    }
    
    public Prototype(String name){
      this.name = name;
    }
    
    @Override
    public Object clone() throws CloneNotSupportedException {
        String temp = this.name;
        return new Prototype(temp);
    }
	
}
```

```
public class PrototypePatternDemo {
 
    public static void main(String[] args) throws CloneNotSupportedException {
        Prototype proto = new Prototype();
		
        //clone() 메서드 사용하여 객체 생성
        Prototype proto1 = (Prototype) proto.clone();
        Prototype proto2 = (Prototype) proto.clone();
    }
 
}
```
