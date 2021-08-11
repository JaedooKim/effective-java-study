String.matches는 정규표현식으로 문자열 형태를 확인하는 가장 쉬운 방법이지만, 성능이 중요한 상황에서는 반복해 사용하기엔 적합하지 않다.

```java
// 값비싼 객체를 재사용해 성능을 개선한다.
public class RomanNumerals {
    private static final Pattern ROMAN = Pattern.compile(".....");

    static boolean isRomanNumeral(String s) {
        return ROMAN.matcher(s).matches();
    }
}
```

오토박싱은 프로그래머가 기본 타입과 박싱된 기본 타입을 섞어 쓸 때 자동으로 상호 변환해주는 기술이다. 오토박싱은 기본 타입과 그에 대응하는 박싱된 기본 타입의 구분을 흐려주지만, 완전히 없애주는 것은 아니다.

```java 
private static long sum() {
    Long sum = 0L;
    for (long i = 0; i <= Integer.MAX_VALUE; i++) 
        sum += i;
    
    return sum;
}
```
모든 양의 정수의 총합을 구하는 메서드로, int는 충분히 크지 않으니 long을 사용해 계산하고 있다.
정확한 답을 내기는 한다. 하지만 제대로 구현했을 때보다 훨씬 느리다. sum 변수를 long이 아닌 Long으로 선언해서 불필요한 Long 인스턴스가 약 2^31개나 만들어진 것이다.
박싱된 기본 타입보다는 기본 타입을 사용하고, 의도치 않은 오토박싱이 숨어들지 않도록 주의하자.