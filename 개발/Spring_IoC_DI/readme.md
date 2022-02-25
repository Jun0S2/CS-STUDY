# Spring IoC / DI

스프링은 자바 엔터프라이즈 개발을 편하게 해주는 오픈소스 프레임워크이며, 코드의 가독성과 의존성을 해결하기 위해 Application Context 라는 컨테이너를 제공한다. 이 컨테이너에서 **Bean 등을 관리하며 각 클래스에서 사용할 수 있도록 Bean을 생성해주는 것을 DI** 라고 한다. 

개발자가 아닌 **컨테이너가 직접 bean을 생성, 관리하기 때문에 IoC(제어의 역전) 컨테이너**라고도 한다.

## DI (의존성 주입)

빈의 상호 연결은 의존성 주입이라고 알려진 패턴을 기반으로 수행된다.

- 컨테이너에서 모든 애플리케이션 컴포넌트를 생성, 관리하고 해당 컴포넌트를 필요로 하는 빈에 주입(연결)
- 일반적으로 생성자 인자 또는 속성의 접근자 메서드를 통해 처리됨
- 최신 버전에서는 @Configuration 애노테이션을 사용 → 각 빈을 컨테이너에서 제공하는 클래스라는걸 명시
- 이전 버전 - XML파일에서 연결

XML 설정

```java
<bean id="inventoryService" class="com.example.InventoryService" />
<bean id="productService" class="com.example.ProductService" />
  <constructor-arg ref="inventoryService" />
</bean>
```

 @Configuration Annotation 사용

```java
@Configuration
public class ServiceConfiguration {

  @Bean
  public InventoryService inventoryService() {
    return new InventoryService();
  }

  @Bean
  public ProductService productService() {
    return new ProductService(inventoryService());
  }
}
```

## IoC (제어의 역전)

![이미지 출처 : [https://yhmane.tistory.com/127](https://yhmane.tistory.com/127)](Spring%20IoC%200f4ea/Untitled.png)

이미지 출처 : [https://yhmane.tistory.com/127](https://yhmane.tistory.com/127)

- **객체에 대한 제어권이 개발자로부터 컨테이너**로 넘어간 것.
- 객체의 생성부터 생명주기 관리까지 전부 컨테이너가 맡아서 하기 때문에 제어를 컨테이너를 갖고 있음
- 컨테이너가 직접 빈을 생성 / 관리하기 때문에 개발자는 코드에 `new` 등으로 선언하지 않아도 되며 각 클래스의 **의존도를 낮추어준다.**

![Untitled](Spring%20IoC%200f4ea/Untitled%201.png)

기존 - 개발자가 직접 객체를 생성하여 코드를 제어함.

```java
public class A {
	private B b;
	public A(){b = new B();}
}
```

스프링 - 컨테이너에 의해 생성한 객체를 사용만 함

```java
public class A {
	@Autowired
	private B b;
}
```

## 정리

IoC는 객체의 흐름, 생명 주기 관리 등 독립적인 제 3자에게 역활과 책임을 위임하는 프로그래밍 모델 방식. 

DI는 인터페이스를 통해 다이나믹하여 객체를 주입하여 유연한 프로그래밍을 가능하게 하는 패턴

Reference

[https://biggwang.github.io/2019/08/31/Spring/IoC, DI란 무엇일까/](https://biggwang.github.io/2019/08/31/Spring/IoC,%20DI%EB%9E%80%20%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C/)

[https://bcp0109.tistory.com/226](https://bcp0109.tistory.com/226)

[https://yhmane.tistory.com/127](https://yhmane.tistory.com/127)