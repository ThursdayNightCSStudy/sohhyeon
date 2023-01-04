# Design smells 또는 Code smells

디자인 냄새는 마틴 파울러의 리팩토링 책에서 사용된 코드냄새에서 기인한다. 디자인 냄새는 기본 디자인 원칙을 위반하고 디자인 품질에 부정적인 영향을 미치는 구조이다.

디자인 냄새에는 4가지 종류가 있다.

### Rigidity 경직성

시스템이 변경하기 어렵다. 하나의 변경을 위해 다른 것들을 변경해야할때 경직성이 높다고 한다.

### Fragility 취약성

취약성이 높다면 시스템은 어떤 부분을 수정하였는데 관련이 없는 부분에도 영향을 미친다.

### Immobility 부동성

다른 부분에서 사용할 수 있는 컴포넌트를 떼어내는 것이 어렵다. 주로 개발자가 이전에 구현되었던 모듈과 비슷한 기능을 하는 모듈을 만드려고 할때 문제점을 발견한다.

### Viscosity 점착성

개발자가 디자인을 보존하는 코드를 시스템에 추가할 수 있는 용이성을 나타낸다. 프로그램 설계에 맞는 코드를 추가하는 것보다 해킹을 추가하는 것이 더 쉽다면 시스템의 점착성(점도)가 높은 것이다. 디자인을 유지하면서 프로그램에 새 코드를 추가하는 것이 쉽다면 점착성이 낮은 것이다.

# SOLID

디자인 냄새, 코드 냄새를 없애기 위해서 지켜야할 원칙이 있는데, 이는 5가지 원칙의 앞글자를 따서 SOLID로 표현한다.

## Single Responsibility Principal

<b>클래스는 오직 하나의 이유로 수정되어야 한다.</b>

<hr>

## Open Closed Principal

<b>클래스는 확장에는 열려있고 수정에는 닫혀있어야 한다.</b>

여기서 키워드는 확장과 수정이다.

- 확장에 대해 열려있다: 애플리케이션의 요구사항이 변경될 때 이 변경에 맞게 새로운 동작을 추가해서 애플리케이션을 확장할 수 있다.

- 수정에 대해 닫혀있다: 기존의 코드를 수정하지 않고도 애플리케이션의 동작을 추가하거나 변경할 수 있다.

사실 OCP는 런타임 의존성과 컴파일타임 의존성에 관한 이야기다. 런타임 의존성이란, 실행시에 협력에 참여하는 객체들 사이의 관계다. 컴파일 의존성은 코드에서 드러나는 클래스 사이의 관계다.

<img src="../images/ocp.png">

영화의 할인정책을 표현한 다이어그램이다. 컴파일타임 의존성 관점에서 Movie 클래스는 추상 클래스인 DiscountPolicy에 의존한다. 런타임 의존성 관점에서 Movie 인스턴스는 AmountDiscountPolicy와 PercentDiscountPolicy 인스턴스에 의존한다. 컴파일타임 의존성과 런타임 의존성은 동일하지 않다.

위의 설계는 이미 OCP를 따르고 있다. 위의 설계에서 중복할인 정책을 추가하는 케이스를 생각해보자.

<img src="../images/ocp2.png">

위의 이미지와 마찬가지로 새로운 할인 정책을 추가해서 기능을 확장할 수 있다. 현재의 설계는 기존 코드를 수정할 필요 없이 새로운 클래스를 추가하는 것만으로 새로운 할인 정책을 확장할 수 있다. 이것이 OCP이다.

OCP를 수용하는 코드는 컴팡리타임 의존성을 수정하지 않고도 런타임 의존성을 쉽게 변경할 수 있다. 중복할인 정책을 구현하는 OverlappedDiscountPolicy 클래스를 추가하더라도 Movie 클래스는 여전히 DiscountPolicy 클래스에만 의존한다. 따라서 컴파일타임 의존성은 변하지 않는다. 하지만 런타임에 Movie 인스턴스는 OverlappedDiscountPolicy 인스턴스와 협력할 수 있다. 따라서 런타임 의존성은 변경되지 않는다. <b>의존성 관점에서 OCP를 따르는 설계란 컴파일 타임 의존성은 유지하면서 런타임 의존성의 가능성을 확장하고 수정할 수 있는 구조라고 할 수 있다.</b>

<hr>

## Liskov Substitution Principal

<b>베이스 클래스에서 파생된(상속한) 클래스는 베이스 클래스를 대체해서 사용할 수 있어야 한다.</b>

> 상속의 두 가지 목적

- 서브클래싱<br>
  다른 클래스의 코드를 재사용할 목적으로 상속을 사용하는 경우이다. 자식 클래스와 부모 클래스의 행동이 호환되지 않기 때문에 자식 클래스의 인스턴스가 부모 클래스의 인스턴스를 대체할 수 없다. 서브클래싱을 구현상속(implementation inheritance) 또는 클래스 상속(class inheritance)이라고 부르기도 한다.

- 서브타이핑<br>
  타입 계층을 구성하기 위해 상속을 사용하는 경우를 가리킨다. 서브타이핑에서는 자식 클래스와 부모 클래스의 행동이 호환되기 때문에 자식 클래스의 인스턴스가 부모 클래스의 인스턴스를 대체할 수 있다. 이때 부모 클래스는 자식 클래스의 슈퍼타입이 되고 자식 클래스는 부모 클래스의 서브타입이 된다. 서브타이핑을 인터페이스 상속(interface inheritance)이라고 부르기도 한다.

리스코프 치환 원칙을 한마디로 정리하면 "서브타입은 그것의 기반 타입에 대해 대체 가능해야 한다."는 것으로 클라이언트가 "차이점을 인식하지 못한 채 기반 클래스의 인터페이스를 통해 서브클래스를 사용할 수 있어야한다"는 것이다.

리스코프 치환 원칙에 따르면 자식 클래스가 부모 클래스와 행동 호환성을 유지함으로써 부모 클래스를 대체할 수 있도록 구현된 상속 관계만을 서브타이핑이라고 불러야한다.

<hr>

## Interface Segregation Principal

사용하지 않는 메소드에 의존하면 안된다.

<hr>

## Dependency Inversion Principal

<b>자신보다 변하기 쉬운 모듈에 의존해서는 안된다.</b>

> 고수준과 저수준?

- 고수준: 의미있는 단일 기능을 제공하는 상위 모듈로 쉽게 변화하지 않는다.
- 저수준: 고수준의 기능을 구현하기 위해 하위기능을 구현한 저수준 모듈이 필요하다. 비교적 자주 변경된다.

앞서 말한 것처럼 고수준 모듈이 잘 동작하려면 저수준 모듈을 사용해야한다. 다시 말하면, 고수준 모듈이 저수준 모듈에 의존하게 된다.

> 고수주이 저수준에 의존할때 생기는 문제

고수준 모듈이 저수준 모듈에 의존하게 되면 다음과 같은 세가지 문제점이 발생한다.

- 첫째, 테스트가 어렵다.<br>
  고수준 모듈을 테스트하기 위해서는 저수준 모듈이 모두 구현되어야만 한다.

- 둘째, 재사용성이 떨어진다.<br>
  고수준 모듈을 사용하기 위해서는 저수준 모듈도 함께 재사용해야한다.

- 셋째, 변경에 취약하다.<br>
  저수준 모듈을 변경하면 고수준 모듈도 함께 변경되어야한다.

이러한 문제를 해결하기 위한 방법이 바로 <b>추상화<b>이다.

> 추상화한 인터페이스를 활용한다.

다음 예시는 '가격할인 계산'이라는 기능을 구현하는 고수준 모듈 CalculateDiscountService이 추상화한 인터페이스인 RuleDiscounter를 의존하도록 의존성을 역전시킨 예시이다.

```java
// 고객 정보와 구매 정보에 룰을 적용해서 할인 금액을 구하는 규칙을 추상화한 인터페이스 (고수준!!)
public interface RuleDiscounter {
  Money applyRules(Customer customer, List<OrderLine> orderLines);
}

// 고수준 모듈이 추상화한 인터페이스에 의존하도록 변경 (고수준!!)
public class CalculateDiscountService {
  private RuleDiscounter ruleDiscounter;

  public CalculateDiscountService(RuleDiscounter ruleDiscounter) {
    this.ruleDiscounter = ruleDiscounter;
  }

  public Money calculateDiscount(List<OrderLine> orderLines, String customerId) {
    Customer customer = findCustomer = findCustomer(customerId);
    return ruleDiscounter.applyRules(customer, orderLines);
  }
}


// 고수준 모듈인 RuleDiscounter의 구현한 모듈 (저수준 모듈!!)
public class DroolsRuleDiscounter implements RuleDiscounter {
  private KieContainer kContainer;

  public DroolsRuleEngine() {
    KieServices ks = KieServices.Factory.get();
    kContainer = ks.getKieClasspathContainer();
  }

  @Override
  public Money applyRules(Customer customer, List<OrderLine> orderLines) {
    KieSession kSession = kContainer.newKieSession("discountSession");
    try {
      //코드 생략
      kSession.fireAllRules();
    } finally {
      kSession.dispose();
    }
    return money.toImmutalbeMoney();
  }
}
```
