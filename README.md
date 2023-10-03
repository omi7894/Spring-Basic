# Spring-Basic
✨인프런 김영한 스프링핵심원리기본편

### 예제만들기
- member
	- (C)Memeber (id, name grade)
	- (I)MemberService (join(), findMember())
	- (C)MemberServiceImpl
	- (I)MembserRepository (save(), findById())
	- (C)MemoryMemberRepository

- discount
	- (I)DiscountPolicy (discount)
	- (C)FixDiscountPolicy
	- (C)RateDiscountPolicy

- order
	- (C)Order (memberId, itemName, itemPrice, discountPrice)
	- (I)OrderService (createOrder())
	- (C)OrderServiceImpl

### main 구성

```c
//멤버서비스 선언
//주문서비스 선언

//new 멤버 생성
//멤버서비스.join(...)

//Order order = 주문서비스.createOrder(...)

//sout(order.calculatePrice())
```

<br/>

🚨**DIP위반** 왜?? OrderServiceImpl이 DiscountPolicy만 의존하는게 아니라, FixDiscountPolicy와 RateDiscountPolicy에도 의존한다.   
> private final DiscountPolicy discountPolicy = new FixDiscountPolicy();  
> private final DiscountPolicy discountPolicy = new RateDiscountPolicy();  
> -> 추상에만(인터페이스에만) 의존하도록 변경

<br/>

### AppConfig 등장
MemberServiceImplc, OrderServiceImpl에서는 인터페이스만 접근하고(memberRepository, discountPolicy) 생성자 주입은 AppConfig 클래스에서 해준다.   
✏️생성자를 통해 참조 주입 (생성자 주입)  
✏️의존관계를 외부에서 주입한다. DI(Dependency Injection) : **의존성 주입**  
<br/>

### 정리 : 좋은 객체지향 설계
**✅SRP**  
한 클래스는 하나의 책임만 가져야한다. (단일 책임 원칙)

**✅DIP**   
프로그래머는 "추상화에 의존해야지, 구체화에 의존하면 안된다." (의존성 주입)

**✅OCP**  
소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다. 

<br/>

- IoC 
	- 제어의 역전
	- 프로그램 제어 흐름은 AppConfig가 가져간다.

- DI
	- 의존관계 주입
	1. 정적인 클래스 의존관계
	2. 동적인 객체 인스턴스 의존관계

<br/>

### 스프링 컨테이너와 스프링 

**@Configuration**  
구성정보(AppConfig)에 붙여준다.

**@Bean**  
스프링 컨테이너에 등록이 된다. 

**[스프링컨테이너]**
- ApplicationContext를 스프링 컨테이너라 한다. 
- ApplicationContext는 인터페이스다. 
- @Configuration이 붙은 AppConfig를 설정 정보로 사용한다.
- @Bean이 붙은 메서드를 호출해서 스프링 컨테이너에 등록한다. 
- 스프링 빈은 applicationContext.getBean()메서드를 사용해서 찾을 수 있다.

 **BeanFactory**
- 스프링 컨테이너의 최상위 인터페이스
- 스프링 빈을 관리하고 조회

**ApplicationContext**
- BeanFactory의 기능을 상속받아 제공
- 부가기능 갖고있음

**BeanDefinition**
- 스프링 빈 설정 메타 정보

<br/>

### 싱글톤
스프링 없는 순수한 DI 컨테이너인 AppConfig는 요청할 때 마다 객체를 새로 생성한다. 

싱글톤 패턴 : 생성자를 private로 막아서 외부에서 객체가 생성된는것을 막는다. 

싱글톤 패턴은 귀찮고 문제가 있기 때문에 싱글톤 컨테이너를 사용한다!!

싱글톤 방식은 무상태로 설계해야 한다!!  
ex)가격실수

@Bean이 붙은 메서드마다 이미 스프링 빈이 존재하면 존재하는 빈을 반환하고, 스프링 빈이 없으면 생성해서 스프링 빈으로 등록한다.  
-> 싱글톤 보장  
-> @Configuration 없이 @Bean만 사용하면 싱글톤을 보장하지 않는다. 


