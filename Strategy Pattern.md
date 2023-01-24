## Strategy Pattern

---
> 어떤 동작을 하는 로직을 정의하고, 이것들을 하나로 묶어(캡슐화) 관리하는 패턴  
> 
> 로직에 들어가는 행동을 클래스로 선언하고, 인터페이스와 연결하는 방식으로 구성하는 것!

![Strategy_Pattern](https://velog.velcdn.com/images%2Fy_dragonrise%2Fpost%2F01b02920-5e7d-4a90-b5be-7cdfe0f6091d%2Fimage.png)

- **Strategy**: 인터페이스나 추상 클래스로 외부에서 동일한 방식으로 알고리즘을 호출하는 방법을 명시  

- **Concreate Strategy 1, 2, 3**: 스트래티지 패턴에서 명시한 알고리즘을 실제로 구현한 클래스  

- **Context**: 스트래티지 패턴을 이용하는 역할 수행. 필요에 따라 동적으로 구체적인 전략을 바꿀 수 있도록 setter 메서드 제공  

**장점**
새로운 로직을 추가하거나 변경할 때, 한번에 효율적으로 변경이 가능하다.  


### 예시

![Strategy_Pattern_Example](https://velog.velcdn.com/images%2Fy_dragonrise%2Fpost%2F7257712b-7f85-4fc6-9de8-a20c60b17a44%2Fimage.png)
- 추상 클래스 Robot의 자식 클래스: TaekwonV 클래스, Atom 클래스
- 추상 클래스 Robot의 추상 메서드 정의: attack method(), move method()

#### Robot 추상 클래스
```java
public abstract class Robot{
  private String name;
  private MovingStrategy movingStrategy;
  private AttackStrategy attackStrategy;

  public Robot(String name){
    this.name = name;
  }

  public String getName(){
    return name;
  }

  public void move(){
    movingStrategy.move();
  }

  public void attack(){
    attackStrategy.attack();
  }

  public void setMovingStrategy(MovingStrategy movingStrategy){
    this.movingStrategy = movingStrategy;
  }

  public void setAttackStrategy(AttackStrategy attackStrategy){
    this.attackStrategy = attackStrategy;
  }
}
```

#### TaekwonV 구현 클래스
```java
public class TaekwonV extends Robot{
  public TaekwonV(String name){
    super(name);
  }
}
```


#### Atom 구현 클래스
```java
public class Atom extends Robot{
  public Atom(String name){
    super(name);
  }
}
```

#### MovingStrategy 인터페이스
```java
interface MovingStrategy{
  public void move();
}
```    

#### FlyingStrategy 구현체
```java
public class FlyingStrategy implements MovingStrategy{
    public void move(){
      System.out.println("I can fly.");
    }
}
```

#### WalkingStrategy 구현체
```java
public class WalkingStrategy implements MovingStrategy{
    public void move(){
    System.out.println("I can only walk.");
    }
}
```

#### AttackStrategy 인터페이스
```java
interface AttackStrategy{
  public void attack();
}
```

#### MissileStrategy 구현체
```java
public class MissileStrategy implements AttackStrategy{
    public void attack(){
      System.out.println("I have Missile and can attack with it.");
    }
}
```

#### PunchStrategy 구현체
```java
public class PunchStrategy implements AttackStrategy{
    public void attack(){
      System.out.println("I have strong punch and can attack with it.");
    }
}
```
