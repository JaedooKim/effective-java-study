식품 포장의 영양정보 클래스

```java
public class NutritionFacts {
    private final int servingSize;  // (ml, 1회 제공량)     필수
    private final int servings;     // (회, 총 n회 제공량)  필수
    private final int calories;     // (1회 제공량당)       선택
    private final int fat;          // (g/1회 제공량)       선택
    private final int sodium;       // (mg/1회 제공량)      선택
    private final int carbohydrate; // (g/1회 제공량)       선택
}

public NutritionFacts(int servingSize, int servings) {
    this(servingSize, servings, 0);
}

public NutritionFacts(int servingSize, int servings, int calories) {
    this(servingSize, servings, calories, 0);
}

public NutritionFacts(int servingSize, int servings, int calories, int fat) {
    this(servingSize, servings, calories, fat, 0);
}

public NutritionFacts(int servingSize, int servings, int calories, int fat, int sodium) {
    this(servingSize, servings, calories, fat, sodium, 0);
}

public NutritionFacts(int servingSize, int servings, int calories, int fat, int sodium, int carbohydrate) {
    this.servingSize    = servingSize;
    this.servings       = servings;
    this.calories       = calories;
    this.fat            = fat;
    this.sodium         = sodium;
    this.carbohydrate   = carbohydrate;
}
```
점층적 생성자 패턴 : 선택 매개변수를 전부 다 받는 생성자까지 늘려가는 방식.
이런 생성자는 사용자가 설정하길 원치 않는 매개변수까지 포함하기 쉽다.

점층적 생성자 패턴도 쓸 수는 있지만, 매개변수 개수가 많아지면 클라이언트 코드를 작성하거나 읽기 어렵다.   

```java
public class NutritionFacts {
    // 매개변수들은 (기본값이 있다면) 기본값으로 초기화된다.
    private int servingSize     = -1;    // 필수; 기본값 없음
    private int servings        = -1;       // 필수; 기본값 없음
    private int calories        = 0;     
    private int fat             = 0;          
    private int sodium          = 0;       
    private int carbohydrate    = 0;

    public NutritionFacts(){ }
    //세터 메서드들
    public void setServingSize(int val) { servingSize = val;}
    public void setServings(int val)    { servings = val;}
    public void setCalories(int val)    { calories = val;}
    public void setFat(int val)         { fat = val;}
    public void setSodium(int val)      { sodium = val;}
    public void setCarbohydrate(int val) { carbohydrate = val;}
}
```
자바빈즈 패턴 : 세터 메서드들을 호출해 원하는 매개변수의 값을 설정하는 방식.
자바빈즈 패턴에서는 객체 하나를 만들려면 메서드를 여러 개 호출해야 하고, 객체가 완전히 생성되기 전까지는 일관성이 무너진 상태에 놓이게 된다.
자바빈즈 패턴에서는 클래스를 불변으로 만들 수 없다.


```java 
public class NutritionFacts {
    private final int servingSize;
    private final int servings;
    private final int calories;
    private final int fat;
    private final int sodium;
    private final int carbohydrate;

    public static class Builder {
        // 필수 매개변수
        private final int servingSize;
        private final int servings;

        // 선택 매개변수 - 기본값으로 초기화한다.
        private int calories    = 0;
        private int fat         = 0;
        private int sodium      = 0;
        private int carbohydrate= 0;

        public Builder(int servingSize, int servings) {
            this.servingSize = servingSize;
            this.servings    = servings;
        }

        public Builder calories(int val) {
            calories = val;
            return this;
        }

        public Builder fat(int val) {
            fat = val;
            return this;
        }

        public Builder sodium(int val) {
            sodium = val;
            return this;
        }

        public Builder carbohydrate(int val) {
            carbohydrate = val;
            return this;
        }

        public NutritionFacts builder() {
            return new NutritionFacts(this);
        }
    }

    private NutritionFacts(Builder builder) {
        servingSize    = builder.servingSize;
        servings       = builder.servings;
        calories       = builder.calories;
        fat            = builder.fat;
        sodium         = builder.sodium;
        carbohydrate   = builder.carbohydrate;
    }
}

```
빌더 패턴 : 명명된 선택적 매개변수를 흉내 낸 것이다.
빌더 패턴은 계층적으로 설계된 클래스와 함께 쓰기에 좋다.

계층적으로 설계된 클래스와 잘 어울리는 빌더패턴  
추상 클래스 -> 추상 빌더, 구체 클래스 -> 구체 빌더를 갖게 한다.

피자의 다양한 종류를 표현하는 계층구조의 루트에 놓인 추상 클래스..
```java
public abstract class Pizza {

    public enum Topping {HAM, MUSHROOM, ONION, PEPPER, SAUSAGE}
    final Set<Topping> toppings;
    
    abstract static class Builder<T extends Builder<T>> {
        EnumSet<Topping> toppings = EnumSet.noneOf(Topping.class);
        public T addTopping(Topping topping) {
            toppings.add(Objects.requireNonNull(topping));
            return self();
        }
        
        abstract Pizza build();
        
        // 하위 클래스는 이 메서드를 재정의(overriding)하여
        // "this"를 반환하도록 해야 한다.
        protected abstract T self();
    }

    Pizza(Builder<?> builder) {
        toppings = builder.toppings.clone(); // 아이템 50 참조
    }

}
```

크기(size) 매개변수 필수로 받는 뉴욕피자..  
```java
public class NyPizza extends Pizza {
    public enum Size {SMALL, MEDIUM, LARGE}
    private final Size size;

    public static class Builder extends Pizza.Builder<Builder> {
        private final Size size;

        public Builder(Size size) {
            this.size = Objects.requireNonNull(size);
        }

        @Override
        public NyPizza build() {
            return new NyPizza(this);
        }

        @Override
        protected Builder self() {
            return this;
        }
    }

    private NyPizza(Builder builder) {
        super(builder);
        size = builder.size;
    }
}
```

소스를 안에 넣을지 선택(sauceInside)하는 매개변수를 필수로 받는 칼초네피자..
```java
public class Calzone extends Pizza {
    private final boolean sauceInside;

    public static class Builder extends Pizza.Builder<Builder> {
        private boolean sauceInside = false;

        public Builder sauceInside() {
            sauceInside = true;
            return this;
        }

        @Override
        public Calzone build() {
            return new Calzone(this);
        }

        @Override
        protected Builder self() {
            return this;
        }
    }

    private Calzone(Builder builder) {
        super(builder);
        sauceInside = builder.sauceInside;
    }
}
```

각 하위 클래스의 빌더가 정의한 build 메서드는 해당하는 구체 하위 클래스를 반환하도록 선언한다.
NyPizza.Builder -> NyPizza, Calzone.Builder -> Calzone 를 반환한다는 뜻이다.

```java
// 클라이언트 측 코드 예
NyPizza pizza = new NyPizza.Builder(NyPizza.Size.SMALL)
            .addTopping(Pizza.Topping.SAUSAGE)
            .addTopping(Pizza.Topping.ONION).build();  
Calzone calzone = new Calzone.Builder()
            .addTopping(Pizza.Topping.HAM)
            .sauceInside().build();
```

빌더 패턴은 상당히 유연하다. 빌더 하나로 여러 객체를 순회하면서 만들 수 있고, 빌더에 넘기는 매개변수에 따라 다른 객체를 만들 수도 있다.