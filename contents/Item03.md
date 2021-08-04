싱글턴이란 인스턴스를 오직 하나만 생성할 수 있는 클래스를 말한다. 그런데 클래스를 싱글턴으로 만들면 이를 사용하는 클라이언트를 테스트하기가 어려워질 수 있다.

### 싱글턴을 만드는 방식

**첫번째 public static 멤버가 final 필드`인 방식**
```java
public class Elvis {
    public static final Elvis INSTANCE = new Elvis();
    private Elvis() {...}

    public void leaveTheBuilding() {...}
}
```
private 생성자는 public static final 필드인 Elvis.INSTANCE를 초기화할 때 딱 한번만 호출된다.

장점1. 해당 클래스가 싱글턴임이 API에 명백히 드러난다는 것.
public static 필드가 final이니 절대로 다른 객체를 참조할 수 없다.

장점2. 간결함

**두번째 정적 팩터리 메서드를 public static 멤버로 제공한다.**
```java 
public class Elvis {
    private static final Elvis INSTANCE = new Elvis();
    private Elvis() {...}
    public static Elvis getInstance() { return INSTANCE; }

    public void leaveTheBuilding() {...}
}
```

장점1. 마음이 바뀌면 API를 바꾸지 않고도 싱글턴이 아니게 변경할 수 있다는 점.
유일한 인스턴스를 반환하던 팩터리 메서드가 예를들어 호출하는 스레드별로 다른 인스턴스를 넘겨주게 할 수 있다.

장점2. 원한다면 정적 팩터리를 제네릭 싱글턴 팩터리로 만들 수 있다.

장점3. 정적 팩터리의 메서드 참조를 공급자로 사용할 수 있다.
가령 Elvis::getinstance를 Supplier\<Elvis>로 사용하는 식.
이러한 장점들이 필요하지 않다면 public 필드 방식이 좋다.

둘 중 하나의 방식으로 만든 싱글턴 클래스를 직렬화하려면 Serializable을 구현한다고 성언하는 것만으로는 부족하다.
모든 인스턴스 필드를 일시적이라고 선언하고 readResolve 메서드를 제공해야한다.

    //싱글턴임을 보장해주는 readResolve 메서드
    private Object readResolve() {
        // '진짜' Elvis를 반환하고, 가짜 Elvis는 가비지 컬렉터에 맡긴다.
        return INSTANCE;
    }
   

**세번째 원소가 하나인 열거 타입을 선언하는 것**

```java 
public enum Elvis {
    INSTANCE;

    public void leaveTheBuilding(){...}
}
```
public 필드 방식과 비슷하지만, 더 간결하고, 추가 노력없이 직렬화할 수 있고, 리플렉션 공격에서도 제2의 인스턴스가 생기는 일을 막아준다.

조금 부자연스러워 보일 수는 있으나 대부분 상황에서는 원소가 하나뿐인 열거 타입이 싱글턴을 만드는 가장 좋은 방법이다. 단, 만들려는 싱글턴이 Enum 외의 클래스를 상속해야 한다면 이 방법은 사용할 수 없다.

(열거 타입이 다른 인터페이스를 구현하도록 선언할 수는 있다.)
