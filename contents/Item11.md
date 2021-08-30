# 🔗 아이템 11. equals를 재정의하려거든 hashCode도 재정의하라.

PhoneNumber 클래스의 인스턴스를 HashMap의 원소로 사용한다고 해보자.

```java
Map<PhoneNumber, String> m = new HashMap<>();
m.put(new PhoneNumber(707,867,5309), "제니");
```

이 코드 다음에 m.get(new PhoneNumber(707,867,5309))를 실행하면 "제니"가 나와야 할 것 같지만, 실제로는 null을 반환한다. 여기에는 2개의 PhoneNumber인스턴스가 사용되었다. 하나는 HashMap에 "제니"를 넣을 때 사용됐고, (논리적 동치인) 두 번째는 이를 꺼내려할 때 사용됐다. PhoneNumber 클래스는 hashCode를 재정의하지 않았기 때문에 논리적 동치인 두 객체가 서로 다른 해시코드를 반환하여 규약을 지키지 못한다. 그 결과 get 메서드는 엉뚱한 해시 버킷에 가서 객체를 찾으려 한 것이다. HashMap은 해시코드가 다른 엔트리끼리는 동치성 비교를 시도조차 하지 않도록 최적화되어 있기 때문이다.


## 💎 올바른 `hashCode` 메서드의 모습

- **적법하게 구현했지만, 절대 사용해서는 안되는 코드**
    ```java 
    @Override public int hashCode() { return 42; }
    ```
    동치인 모든 객체에서 똑같은 해시코드를 반환하니 적법하다.
    하지만 끔찍하게도 모든 객체에게 똑같은 값만 내어주므로 모든 객체가 해시테이블의 버킷 하나에 담겨 마치 연결 리스트(linked list)처럼 동작한다.

&nbsp;

- **좋은 hashCode를 작성하는 간단한 요령**
   1. int 변수 result를 선언한 후 값 c로 초기화한다. 이때 c는 해당 객체의 첫번째 핵심 필드를 단계 2.a방식으로 계산한 해시코드가(여기서 핵심 필드란 equals 비교에 사용되는 필드를 말한다.)    
   2. 해당 객체의 나머지 핵심 필드 f각각에 대해 다음 작업을 수행한다.
      1. 해당 필드의 해시코드 c를 계산한다.
         1. 기본 타입 필드라면, Type.hashCode(f)를 수행한다. 여기서 Type은 해당 기본 타입의 박싱 클래스다.
         2. 참조 타입 필드면서 이 클래스의 equals 메서드가 이 필드의 equals를 재귀적으로 호출해 비교한다면, 이 필드의 hashCode를 재귀적으로 호출한다. 필드의 값이 null이면 0을 사용한다.
         3. 필드가 배열이라면, 핵심 원소 각각을 별도 필드처럼 다룬다. 모든 원소가 핵심  원소라면 Arrays.hashCode를 사용한다.
       1. 단계 2.a에서 계산한 해시코드 c로 result를 갱신한다. 코드로는 다음과 같다
      
            result = 31 * result + c;
    1. result를 반환한다.      

&nbsp;

- **PhoneNumber 클래스에 적용**
    ```java
    @Override public int hashCode() {
        int result = Short.hashCode(areaCode);
        result = 31 * result + Short.hashCode(prefix);
        result = 31 * result + Short.hashCode(lineNum);
        return result;
    }
    ```
 &nbsp;

- **Object의 hash 메서드 사용**
    hashCode 함수를 단 한 줄로 작성할 수 있다.
    단, 속도는 더 느리다.
    ```java
    @Override public int hashCode() {
        return Objects.hash(lineNum, prefix, areaCode);
    }
    ```

 &nbsp;

- **해시코드를 지연 초기화하는 hashCode 메서드 - 스레드 안정성까지 고려해야 한다.**
    ```java
    private int hashCode; // 자동으로 0으로 초기화된다.

    @Override public int hashCode() {
        int result = hashCode;
        if (result == 0) {
            result = Short.hashCode(areaCode);
            result = 31 * result + Short.hashCode(prefix);
            result = 31 * result + Short.hashCOde(lineNum);
            hashCode = result;
        }
    }
    ```
    성능을 높인답시고 해시코드를 계산할 때 핵심 필드를 생략해서는 안 된다.


&nbsp;

## 💎 결론

`equals`를 재정의할 때는 hashCode도 반드시 재정의해야 한다. 그렇지 않으면 프로그램이 제대로 동작하지 않을 것이다. 재정의한 hashCode는 Object의 API 문서에 기술된 일반 규약을 따라야 하며, 서로 다른 인스턴스라면 되도록 해시코드도 서로 다르게 구현해야 한다. 이렇게 구현하기가 어렵지는 않지만 조금 따분한 일이긴 하다. 아이템 10에서 이야기한 AutoValue 프레임워크를 사용하면 멋진 equals와 ahshCode를 자동으로 만들어준다. IDE들도 이런 기능을 일부 제공한다.
