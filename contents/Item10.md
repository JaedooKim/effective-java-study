# π μμ΄ν 10. equalsλ μΌλ° κ·μ½μ μ§μΌ μ¬μ μ νλΌ
> `equals`λ₯Ό λ€ κ΅¬ννλ€λ©΄ μΈ κ°μ§λ§ μλ¬Έν΄λ³΄μ.  
*λμΉ­μ μΈκ°? μΆμ΄μ±μ΄ μλκ°? μΌκ΄μ μΈκ°?*

`equals` λ©μλλ₯Ό μ¬μ μνμ§ μκ³  κ·Έλ₯ λλ©΄, κ·Έ ν΄λμ€μ μΈμ€ν΄μ€λ μ€μ§ μκΈ° μμ κ³Όλ§ κ°κ² λλ€.

&nbsp;

## π `equals`λ₯Ό μ¬μ μ νλ©΄ μ λλ κ²½μ°

1. κ° μΈμ€ν΄μ€κ° λ³Έμ§μ μΌλ‘ κ³ μ ν  λ  
κ° ν΄λμ€(`Integer`λ `String`μ²λΌ κ°μ νννλ ν΄λμ€)κ° μλ λμνλ κ°μ²΄λ₯Ό νννλ ν΄λμ€  
ex) `Thread`

2. μΈμ€ν΄μ€μ 'λΌλ¦¬μ  ν΅μΉμ±'μ κ²μ¬ν  μΌμ΄ μμ λ  
ex) `java.util.regax.Pattern`μ `equals`λ₯Ό μ¬μ μν΄ λ `Pattern`μ μ κ·ννμμ λΉκ΅

3. μμ ν΄λμ€μμ μ¬μ μν `equals`κ° νμ ν΄λμ€μλ λ± λ€μ΄λ§μ λ  
ex) `Set`μ `AbstractSet`μ΄ κ΅¬νν `equals`λ₯Ό μμ, `List`λ `AbstractList`, `Map`μ `AbstractMap`

4. ν΄λμ€κ° *private*μ΄λ *package-private*μ΄κ³  `equals`λ₯Ό νΈμΆν  μΌμ΄ μμ λ  
μλμ κ°μ΄ κ΅¬νν΄ `equals`κ° μ€μλ‘λΌλ νΈμΆλλ κ±Έ λ§μ μ μλ€.  
```java
@Override public boolean equals(Object o) {
	throw new AssertionError(); // νΈμΆ κΈμ§!
}
```

&nbsp;

## π `equals`λ₯Ό μ¬μ μ ν΄μΌ νλ κ²½μ°

κ°μ²΄ μλ³μ±(object identity; λ κ°μ²΄κ° λ¬Όλ¦¬μ μΌλ‘ κ°μκ°)μ΄ μλ 'λΌλ¦¬μ  λμΉμ±'μ νμΈν΄μΌ νλλ°,  
μμ ν΄λμ€μ `equals`κ° λΌλ¦¬μ  λμΉμ±μ λΉκ΅νλλ‘ μ¬μ μ λμ§ μμμ λ (μ£Όλ‘ κ° ν΄λμ€)

ex) λ κ° κ°μ²΄λ₯Ό `equals`λ‘ λΉκ΅νλ κ²½μ°, κ°μ²΄κ° κ°μμ§κ° μλλΌ κ°μ΄ κ°μμ§λ₯Ό μκ³ μΆμ κ²μ΄λ€.  
`equals`κ° λΌλ¦¬μ  λμΉμ±μ νμΈνλλ‘ μ¬μ μνλ©΄, κ° λΉκ΅λ λ¬Όλ‘  `Map`μ ν€μ `Set`μ μμλ‘ μ¬μ© κ°λ₯.  
*but,* κ° ν΄λμ€μ¬λ, κ°μ μΈμ€ν΄μ€κ° λ μ΄μ λ§λ€μ΄μ§μ§ μλ *μΈμ€ν΄μ€ ν΅μ  ν΄λμ€*λΌλ©΄ μ¬μ μνμ§ μμλ λ¨.

&nbsp;

## π `equals` λ©μλ μ¬μ μ μΌλ° κ·μ½: λμΉκ΄κ³

**λμΉ ν΄λμ€(equivalent class): μ§ν©μ μλ‘ κ°μ μμλ€λ‘ μ΄λ£¨μ΄μ§ λΆλΆμ§ν©μΌλ‘ λλλ μ°μ°**  
β `equals` λ©μλκ° μΈλͺ¨ μμΌλ €λ©΄ λͺ¨λ  μμκ° κ°μ λμΉλ₯μ μν μ΄λ€ μμμλ κ΅νμ΄ κ°λ₯ν΄μΌ νλ€.

- **λ°μ¬μ±(reflexivity)**  
: `null`μ΄ μλ λͺ¨λ  μ°Έμ‘° κ° xμ λν΄, `x.equals(x)`λ `true`λ€.
- **λμΉ­μ±(symmetry)**  
: `null`μ΄ μλ λͺ¨λ  μ°Έμ‘° κ° x, yμ λν΄, `x.equals(y)`κ° `true`λ©΄ `y.equals(x)`λ `true`λ€.
- **μΆμ΄μ±(transitivity)**  
: `null`μ΄ μλ λͺ¨λ  μ°Έμ‘° κ° x, y, zμ λν΄, `x.equals(y)`κ° `true`μ΄κ³ , `y.equals(z)`λ `true`λ©΄ `x.equals(z)`λ `true`λ€.
- **μΌκ΄μ±(consistency)**  
: `null`μ΄ μλ λͺ¨λ  μ°Έμ‘° κ° x, yμ λν΄, `x.equals(y)`λ₯Ό λ°λ³΅ν΄μ νΈμΆνλ©΄ ν­μ `true`μ΄κ±°λ `false`λ€.
- `**null`-μλ**  
: `null`μ΄ μλ λͺ¨λ  μ°Έμ‘° κ° xμ λν΄, `x.equals(null)`μ `false`λ€.

### λ°μ¬μ±(reflexivity)

> κ°μ²΄κ° μκΈ° μμ κ³Ό κ°μμΌ νλ€.

```java
public class ProgrammingLanguage{
  private String name;

  public Fruit(String name){
    this.name = name;
  }

  public static void main(){
    Set<ProgrammingLanguage> set = new HashSet<>();
    ProgrammingLanguage language = new ProgrammingLanguage("java");
    set.add(language);
    System.out.println(set.contains(language)); // falseμΌ κ²½μ°, λ°μ¬μ±μ λ§μ‘±νμ§ λͺ»νλ κ²½μ°μ΄λ€.
  }
}
```

### λμΉ­μ±(symmetry)

> λ κ°μ²΄λ μλ‘μ λν λμΉ μ¬λΆμ λκ°μ΄ λ΅ν΄μΌ νλ€.

##### μλͺ»λ μ½λ - λμΉ­μ± μλ°°!

```java
// λμΉ­μ±μ μλ°ν ν΄λμ€
public final class CaseInsensitiveString{
  private final String s;

  public CaseInsensitiveString(String s){
    this.s = Obejcts.requireNonNull(s);
  }

  // λμΉ­μ± μλ°°!
  @Override public boolean equals(Object o){
    if(o instanceof CaseInsensitiveString)
      return s.equalsIgnoreCase(((CaseInsensitiveString) o).s);
    if(o instanceof String) // νλ°©ν₯μΌλ‘λ§ μλνλ€.
      return s.equalsIgnoreCase((String) o);
    return false;
  }
}
```

λ¬Έμ λ `CaseInsensitiveString`μ `equals`λ `String`μ μκ³  μμ§λ§, `String`μ `equals`λ `CaseInsensitiveString`μ μ‘΄μ¬λ₯Ό λͺ¨λ₯Έλ€λ λ° μλ€. λμΉ­μ±μ λͺλ°±ν μλ°νλ€.

```java
CaseInsensitiveString cis = new CaseInsensitiveString("Polish");
String s = "polish";

cis.equals(s); // true
s.equals(cis); // false
```

##### ν΄κ²° - `CaseInsensitiveString`λΌλ¦¬λ§ λΉκ΅νλλ‘ νλ€.

```java
//λμΉ­μ±μ λ§μ‘±νκ² μμ 
@Override public boolean equals(Object o){
  return o instanceof CaseInsensitiveString && ((CaseInsensitiveString) o).s.equalsIgnoreCase(s); 
}
```

### μΆμ΄μ±(transitivity)

> μ²« λ²μ§Έ κ°μ²΄μ λ λ²μ§Έ κ°μ²΄κ° κ°κ³ , λ λ²μ§Έ κ°μ²΄μ μΈ λ²μ§Έ κ°μ²΄κ° κ°μλ©΄, μ²« λ²μ§Έ κ°μ²΄μ μΈ λ²μ§Έ κ°μ²΄λ κ°μμΌ νλ€.

μμ ν΄λμ€μ μλ μλ‘μ΄ νλλ₯Ό νμ ν΄λμ€μ μΆκ°νλ©° `equals`λ₯Ό μ¬μ μν  λ μμ£Ό λ°μνλ λ¬Έμ λ€.

```java
public class Point {
	private final int x;
	private final int y;

	public Point(int x, int y) {
		this.x = x;
		this.y = y;
	}

	@Override public boolean equals(Object o) {
		if(!o instanceof Point)
			return false;
		Point p = (Point) o;
		return p.x == x && p.y == y;
	}
}
```

```java
public class ColorPoint extends Point {
	private final Color color;
	
	public ColorPoint(int x, int y, Color color) {
		super(x, y);
		this.color = color;
	}

	...
}
```

##### 1. μλͺ»λ μ½λ - λμΉ­μ± μλ°°!  

```java
    @Override public boolean equals(Object o) {
    	if(!o instanceof ColorPoint)
    		return false;
    	return super.equals(o) && ((ColorPoint) o).color == color;
    }
```

```java
    public static void main(){
      Point p = new Point(1,2);
      ColorPoint cp = new ColorPoint(1,2, Color.RED);
      p.equals(cp);    // true
      cp.equals(p);    // false
    }
```

`ColorPoint`μ `equals`λ μλ ₯ λ§€κ°λ³μμ ν΄λμ€ μ’λ₯κ° λ€λ₯΄λ€λ©° λ§€λ² `false`λ§ λ°νν  κ²μ΄λ€. 

##### 2. μλͺ»λ μ½λ - μΆμ΄μ± μλ°°!  

```java
    @Override public boolean equals(Obejct o){
      if(!(o instanceof Point))
        return false;
      if(!(o instanceof ColorPoint))
        return o.equals(this);
      return super.equals(o) && ((ColorPoint) o).color == color;
    }
```

```java
    public static void main(){
      ColorPoint p1 = new ColorPoint(1,2, Color.RED);
      Point p2 = new Point(1,2);
      ColorPoint p3 = new ColorPoint(1,2, Color.BLUE);
      p1.equals(p2);    // true 
      p2.equals(p3);    // true 
      p1.equals(p3);    // false
    }
```

`p1.equals(p2);`μ `p2.equals(p3);`λ `true`λ₯Ό λ°ννλλ°, `p1.equals(p3);`λ `false`λ₯Ό λ°νν΄ μΆμ΄μ±μ μλ°°λλ€.  
μ΄ λ°©μμ **λ¬΄ν μ¬κ·**μ λΉ μ§ μνλ μλ€.  

```java
    //SmellPoint.javaμ equals
    @Override public boolean equals(Obejct o){
      if(!(o instanceof Point))
        return false;
      if(!(o instanceof SmellPoint))
        return o.equals(this);
      return super.equals(o) && ((SmellPoint) o).color == color;
    }
```

```java
    public static void main(){
      ColorPoint p1 = new ColorPoint(1,2, Color.RED);
      SmellPoint p2 = new SmellPoint(1,2);
      p1.equals(p2);
      // 1. ColorPointμ equals: 2λ²μ§Έ ifλ¬Έ λλ¬Έμ SmellPointμ equalsλ‘ λΉκ΅
      // 2. SmellPointμ equals: 2λ²μ§Έ ifλ¬Έ λλ¬Έμ ColorPointμ equalsλ‘ λΉκ΅
      // 3. 1~2 λ¬΄ν μ¬κ·λ‘ μΈν StackOverflow Error
    }
```

κ΅¬μ²΄ ν΄λμ€λ₯Ό νμ₯ν΄ μλ‘μ΄ κ°μ μΆκ°νλ©΄μ `equals` κ·μ½μ λ§μ‘±μν¬ λ°©λ²μ μ‘΄μ¬νμ§ μλλ€.

##### 3. μλͺ»λ μ½λ - λ¦¬μ€μ½ν μΉν μμΉ μλ°°!  

κ·Έλ λ€κ³  `instanceof` κ²μ¬ λμ  `getClass` κ²μ¬λ₯Ό νλΌλ κ²μ μλλ€.

```java
    @Override public boolean equals(Object o){
      if(o == null || o.getClass() != getClass())
        return false;
      Point p = (Point) o;
      return p.x == x && p.y == y;
    }
```

μμ μ½λλ κ°μ κ΅¬ν ν΄λμ€μ κ°μ²΄μ λΉκ΅ν  λλ§ `true`λ₯Ό λ°ννλ€.  
λ¦¬μ€μ½ν μΉν μμΉ: μ΄λ€ νμμ μμ΄ μ€μν μμ±μ΄λΌλ©΄ κ·Έ νμ νμμμλ λ§μ°¬κ°μ§λ‘ μ€μνλ€.  
= `Point`μ νμ ν΄λμ€λ μ¬μ ν `Point`μ΄λ―λ‘ μ΄λμλ  `Point`λ‘μ¨ νμ©λ  μ μμ΄μΌ νλ€.  

**ν΄κ²° 1 - μμ λμ  μ»΄ν¬μ§μμ μ¬μ©νλΌ (`equals` κ·μ½μ μ§ν€λ©΄μ κ° μΆκ°νκΈ°)**

```java
public class ColorPoint{
  private final Point point;
  private final Color color;

	public ColorPoint(int x, int y, Color color) {
		point = new Point(x, y);
		this.color = Objects.requireNonNull(color);
	}

	/* μ΄ ColorPointμ Point λ·°λ₯Ό λ°ννλ€. */
  public Point asPoint(){ // view λ©μλ ν¨ν΄
    return point;
  }

  @Override public boolean equals(Object o){
    if(!(o instanceof ColorPoint)){
      return false;
    }
    ColorPoint cp = (ColorPoint) o;
    return cp.point.equals(point) && cp.color.equals(color);
  }
}
```

> **μ»΄ν¬μ§μ**: κΈ°μ‘΄ ν΄λμ€κ° μλ‘μ΄ ν΄λμ€μ κ΅¬μ± μμλ‘ μ°μΈλ€.  
**κΈ°μ‘΄ ν΄λμ€λ₯Ό νμ₯νλ λμ , μλ‘μ΄ ν΄λμ€λ₯Ό λ§λ€κ³  *private* νλλ‘ κΈ°μ‘΄ ν΄λμ€μ μΈμ€ν΄μ€λ₯Ό μ°Έμ‘°νκ² νλ€.**  
μ»΄ν¬μ§μμ ν΅ν΄ μ ν΄λμ€μ μΈμ€ν΄μ€ λ©μλλ€μ **κΈ°μ‘΄ ν΄λμ€μ λμνλ λ©μλλ₯Ό νΈμΆν΄ κ·Έ κ²°κ³Όλ₯Ό λ°ν**νλ€.

`Point`λ₯Ό μμνλ λμ  `Point`λ₯Ό `ColorPoint`μ *private* νλλ‘ λκ³ , `ColorPoint`μ κ°μ μμΉμ μΌλ° `Point`λ₯Ό λ°ννλ λ·°(view λ©μλ)λ₯Ό *public*μΌλ‘ μΆκ°νλ μμ΄λ€.  

- `ColorPoint` vs. `ColorPoint`: `ColorPoint`μ `equals`λ₯Ό μ΄μ©νμ¬ colorκ°κΉμ§ λͺ¨λ λΉκ΅
- `ColorPoint` vs. `Point`: `ColorPoint`μ `asPoint`λ₯Ό μ΄μ©νμ¬ `Point`λ‘ λ°κΏ, `Point`μ `equals`λ₯Ό μ΄μ©ν΄ x, yλΉκ΅
- `Point` vs. `Point`: `Point`μ `equals`λ₯Ό μ΄μ©ν΄ x, yκ° λͺ¨λ λΉκ΅

ex) `java.sql.Timestamp`: `java.util.Date` νμ₯ ν `nanoseconds` νλ μΆκ°.  
β `Timestamp`μ `equals`λ λμΉ­μ±μ μλ°°νλ©°, `Date`μ μμ΄ μΈ λ μλ±νκ² λμν  μ μλ€.

**ν΄κ²° 2 - μΆμ ν΄λμ€μ νμ ν΄λμ€ μ¬μ©νκΈ°**

μΆμ ν΄λμ€μ νμ ν΄λμ€μμλ `equals` κ·μ½μ μ§ν€λ©΄μλ κ°μ μΆκ°ν  μ μλ€.  
μμ ν΄λμ€μ μΈμ€ν΄μ€λ₯Ό μ§μ  λ§λλ κ² λΆκ°λ₯νκΈ° λλ¬Έμ, νμ ν΄λμ€λΌλ¦¬μ λΉκ΅κ° κ°λ₯νλ€.

### μΌκ΄μ±(consistency)

> λ κ°μ²΄κ° κ°λ€λ©΄ (μ΄λ νλ νΉμ λ κ°μ²΄ λͺ¨λκ° μμ λμ§ μλ ν) μμΌλ‘λ μμν κ°μμΌ νλ€.

- κ°λ³ κ°μ²΄μ κ²½μ° λΉκ΅ μμ μ λ°λΌ μλ‘ λ€λ₯Ό μλ νΉμ κ°μ μλ μλ€.
- λΆλ³ κ°μ²΄λ νλ² λ€λ₯΄λ©΄ λκΉμ§ λ¬λΌμΌ νλ€.
- ν΄λμ€κ° λΆλ³μ΄λ  κ°λ³μ΄λ  `equals`μ νλ¨μ μ λ’°ν  μ μλ μμμ΄ λΌμ΄λ€κ² ν΄μλ μ λλ€.  
ex) `java.net.URL`μ `equals`λ μ£Όμ΄μ§ URLκ³Ό λ§€νλ νΈμ€νΈμ IPμ£Όμλ₯Ό μ΄μ©ν΄ λΉκ΅νλλ°,  
νΈμ€νΈ μ΄λ¦μ IPμ£Όμλ‘ λ°κΎΈλ €λ©΄ λ€νΈμν¬λ₯Ό ν΅ν΄μΌ νλ―λ‘ κ·Έ κ²°κ³Όκ° ν­μ κ°λ€κ³  λ³΄μ₯ν  μ μλ€.  
β `equals`λ ν­μ λ©λͺ¨λ¦¬μ μ‘΄μ¬νλ κ°μ²΄λ§μ μ¬μ©ν κ²°μ μ (deterministic) κ³μ°λ§ μνν΄μΌ νλ€.

### null-μλ

λͺ¨λ  κ°μ²΄κ° `null`κ³Ό κ°μ§ μμμΌ νλ€.

**μλͺ»λ λͺμμ  null κ²μ¬**

```java
@Override
public boolean equals(Object o) {
  if(o == null) { 
      return false;
  }
}
```

**μ¬λ°λ₯Έ λ¬΅μμ  null κ²μ¬ - μ΄μͺ½μ΄ λ«λ€.**

```java
@Override
public boolean equals(Object o) {
  if(!(o instanceof MyType)) { 
      return false;
  }
  MyType myType = (MyType) o;
}
```

λμμ±μ κ²μ¬νλ €λ©΄ `equals`λ κ±΄λ€λ°μ κ°μ²΄λ₯Ό μ μ ν νλ³νν ν νμ νλλ€μ κ°μ μμλ΄μΌ νλ€.  
λ°λΌμ, νλ³νμ μμ `instanceof` μ°μ°μλ‘ μλ ₯ λ§€κ°λ³μκ° μ¬λ°λ₯Έ νμμΈμ§ κ²μ¬ν΄μΌ νλ€.  
μλ ₯μ΄ `null`μ΄λ©΄ νμ νμΈ λ¨κ³μμ `false`λ₯Ό λ°ννλ―λ‘ `null` κ²μ¬λ₯Ό λͺμμ μΌλ‘ νμ§ μμλ λλ€.

## π μ λ¦¬: μμ§μ `equals` λ©μλ κ΅¬ν λ°©λ²

1. `==`μ°μ°μλ₯Ό μ¬μ©ν΄ μλ ₯μ΄ μκΈ° μμ μ μ°Έμ‘°μΈμ§ νμΈνλ€.  
μκΈ° μμ μ΄λ©΄ `true`λ₯Ό λ°ννλ€. λ¨μν μ±λ₯ μ΅μ νμ©μΌλ‘ λΉκ΅ μμμ΄ λ³΅μ‘ν μν©μΌ λ κ°μ΄μΉλ₯Ό νλ€.
2. `instanceof` μ°μ°μλ‘ μλ ₯μ΄ μ¬λ°λ₯Έ νμμΈμ§ νμΈνλ€.  
κ°λ ν΄λΉ ν΄λμ€κ° κ΅¬νν νΉμ  μΈν°νμ΄μ€λ₯Ό λΉκ΅ν  μλ μλ€.  
μ΄λ° μΈν°νμ΄μ€λ₯Ό κ΅¬νν ν΄λμ€λΌλ©΄ `equals`μμ (ν΄λμ€κ° μλ) ν΄λΉ μΈν°νμ΄μ€λ₯Ό μ¬μ©ν΄μΌνλ€.  
ex) `Set`, `List`, `Map`, `Map.Entry` λ± μ»¬λ μ μΈν°νμ΄μ€λ€
3. μλ ₯μ μ¬λ°λ₯Έ νμμΌλ‘ νλ³ν νλ€.  
2λ²μμ `instanceof` μ°μ°μλ‘ μλ ₯μ΄ μ¬λ°λ₯Έ νμμΈμ§ κ²μ¬ νκΈ° λλ¬Έμ μ΄ λ¨κ³λ 100% μ±κ³΅νλ€.
4. μλ ₯ κ°μ²΄μ μκΈ° μμ μ λμλλ 'ν΅μ¬' νλλ€μ΄ λͺ¨λ μΌμΉνλμ§ νλμ© κ²μ¬νλ€.  
λͺ¨λ μΌμΉν΄μΌ `true`λ₯Ό λ°ννλ€.

## π `equals` κ΅¬ν μ μ£Όμν  μΆκ° μ¬ν­

- **κΈ°λ³Έ νμ**  
: `==` μ°μ°μ λΉκ΅
- **μ°Έμ‘° νμ**  
: `equals` λ©μλλ‘ λΉκ΅
- **float, double νλ**  
: μ μ  λ©μλ `Float.compare(float, float)`μ `Double.compare(double, double)`λ‘ λΉκ΅  
`Float.equals(float)`λ `Double.equals(double)`μ μ€ν  λ°μ±μ μλ°ν΄ μ±λ₯μ μ’μ§ μλ€.
- **λ°°μ΄ νλ**  
: μμ κ°κ°μ μ§μΉ¨λλ‘ λΉκ΅νλ€. λͺ¨λκ° ν΅μ¬ νλλΌλ©΄ `Arrays.equals()`λ₯Ό μ¬μ©νλ€.
- **null μ μκ° μ·¨κΈ λ°©μ§**  
: `Object.equals(object, object)`λ‘ λΉκ΅νμ¬ `NullPointException` λ°μμ μλ°©νλ€.
- λΉκ΅νκΈ° **λ³΅μ‘ν νλλ₯Ό κ°μ§ ν΄λμ€**  
: νλμ νμ€ν(canonical form)μ μ μ₯ν ν νμ€νλΌλ¦¬ λΉκ΅
- **νλμ λΉκ΅ μμλ `equals` μ±λ₯μ μ’μ°νλ€.**  
: λ€λ₯Ό κ°λ₯μ±μ΄ ν¬κ±°λ λΉκ΅νλ λΉμ©μ΄ μΌ νλλΆν° λΉκ΅  
νμ νλκ° κ°μ²΄ μ μ²΄ μνλ₯Ό λννλ κ²½μ°, νμ νλλΆν° λΉκ΅
- `**equals`λ₯Ό μ¬μ μν  λ `hashCode`λ λ°λμ μ¬μ μνμ**
- **λλ¬΄ λ³΅μ‘νκ² ν΄κ²°νλ € λ€μ§ λ§μ.**
- **Object μΈμ νμμ λ§€κ°λ³μλ‘ λ°λ `equals` λ©μλλ μ μΈνμ§ λ§μ.**  
`public boolean equals(MyClass o)`: μλ ₯ νμμ΄ Objectκ° μλλ―λ‘ μ€λ²λ‘λ©ν κ²μ΄λ€.

### μ κ΅¬νλ μ

```java
public class PhoneNumber {
    private final short areaCode, prefix, lineNum;

    public PhoneNumber(int areaCode, int prefix, int lineNum) {
        this.areaCode = rangeCheck(areaCode, 999, "μ§μ­μ½λ");
        this.prefix = rangeCheck(prefix, 999, "νλ¦¬ν½μ€");
        this.lineNum = rangeCheck(lineNum, 9999, "κ°μμ λ²νΈ");
    }

    private static short rangeCheck(int val, int max, String arg) {
        if(val < 0 || val > max) {
            throw new IllegalArgumentException(arg + ": " + val);
        }
        return (short) val;
    }

    @Override
    public boolean equals(Object o) {
        if(o == this) {
            return true;
        }

        if(!(o instanceof PhoneNumber)) {
            return false;
        }

        PhoneNumber pn = (PhoneNumber) o;
        return pn.lineNum == lineNum && pn.prefix == prefix
                && pn.areaCode == areaCode;
    }
}
```

&nbsp;

## π `AutoValue` νλ μμν¬

`equals`(`hashCode`λ λ§μ°¬κ°μ§)λ₯Ό μμ±νκ³  νμ€νΈνλ μμμ λμ ν΄μ€ μ€ν μμ€.  
ν΄λμ€μ μ λνμ΄μ νλλ§ μΆκ°νλ©΄ AutoValueκ° μ΄ λ©μλλ€μ μμμ μμ±ν΄μ€λ€.

&nbsp;

## π κ²°λ‘ 

κΌ­ νμν κ²½μ°κ° μλλ©΄ `equals`λ₯Ό μ¬μ μνμ§ λ§μ. λ§μ κ²½μ°μ `Object`μ `equals`κ° μ¬λ¬λΆμ΄ μνλ λΉκ΅λ₯Ό μ νν μνν΄μ€λ€. μ¬μ μν΄μΌ ν  λλ κ·Έ ν΄λμ€μ ν΅μ¬ νλ λͺ¨λλ₯Ό λΉ μ§μμ΄, λ€μ― κ°μ§ κ·μ½μ νμ€ν μ§μΌκ°λ©° λΉκ΅ν΄μΌ νλ€.
