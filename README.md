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


