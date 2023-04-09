# 필수 정리 내용 
## 1. 의존과 의존성

다음과 같은 코드가 있다.

```
public class MemberService {

  private final MemberRepository memberRepository = new MemoryMemberRepository();
  
  ...
}
```
MemberService는 클라이언트가 회원 가입, 회원 조회 등의 기능을 사용할 수 있도록 지원한다. 이때, 회원 정보를 등록하거나 
등록되어있는 회원들의 목록을 화면에 나타내기 위해서는 데이터가 저장되어있는 곳의 정보가 필요하다. 즉, MemberRepository를 사용해야 한다.

MemberService에는 회원 객체 저장에 대한 정보가 존재하지 않는다. 그렇기 때문에 MemberRepository가 필요하고, 이때 MemberService와 MemberRepository에 
의존관계가 있다, MemberService가 MemberRepository에 의존한다 등으로 이야기할 수 있다.

스프링은 의존성 주입(DI)을 지원한다. 객체 의존관계를 외부에서 넣어주는 것을 의존성 주입이라고 한다. 다음과 같은 코드를 의존성 주입이라고 할 수 있다.
```
public class MemberService {

  private final MemberRepository memberRepository;
  
  public MemberService(MemberRepository memberRepository) {
    this.memberRepository = memberRepository;
  }  
  ...
}
```

## 2. @Autowired 의존성 주입
스프링에서는 생성자에 @Autowired 애노테이션을 사용하면 스프링이 연관된 객체를 스프링 컨테이너에서 찾아서 넣어준다. 
참고로 생성자가 1개만 있으면 @Autowired는 생략할 수 있다.

```
public class MemberService {

  private final MemberRepository memberRepository;
  
  @Autowired
  public MemberService(MemberRepository memberRepository) {
    this.memberRepository = memberRepository;
  }  
  ...
}
```

또한, @Autowired를 통한 DI는 스프링이 관리하는 객체에서만 동작하기 때문에 개발자가 직접 생성한 객체를 DI에 활용하고 싶은 경우, 스프링 빈으로 등록해주어야 한다.
DI에는 필드 주입, setter 주입, 생성자 주입 이렇게 3가지 방법이 있다.

- 필드 주입 : 필드에 바로 @Autowired 애노테이션을 사용한다. 스프링이 실행되고 나서 바꿀 수 있는 방법이 없기 때문에 추천되지 않는다.
- setter 주입 : setter에 @Autowired 애노테이션을 사용한다. 이렇게 하려면 setter가 public으로 열려있어야 하므로 setter가 public에 노출된다는 단점이 있다.
- 생성자 주입 : 위의 예시 코드와 같이 생성자를 통해 의존관계를 주입한다.

## 3. DIP 
DIP는 클린코드로 유명한 로버트 마틴이 정리한 좋은 객체지향 설계의 5가지 원칙(SOLID) 중 하나이다.
- SRP : 단일 책임 원칙
- OCP : 개방-폐쇄 원칙
- LSP : 리스코프 치환 원칙
- ISP : 인터페이스 분리 원칙
- DIP : 의존관계 역전 원칙

의존관계 역전 원칙(DIP, Dependenc Inversion Principle)은 구체화에 의존하지 않고 추상화에 의존해야 한다는 원칙이다.
쉽게 말해 클라이언트가 구현 클래스가 아닌 인터페이스에 의존할 수 있게 하라는 의미로, 의존관계 역전 원칙이 잘 지켜진다면 클라이언트는 구현 클래스를 몰라도 
기능을 사용하는데 아무 문제가 없다.

예를 들어, 운전자는 자동차에 대해서만 알고 있으면 그 자동차가 기름차거나 전기차거나 상관없이 운전할 수 있어야 한다.

## 4. 스프링 빈과 스프링 컨테이너란?
- 스프링 빈 : 스프링이 관리하는 객체

스프링 빈은 @Component 애노테이션을 통해 자동 등록할 수도 있고, 자바 코드로 직접 등록할 수도 있다.

- 스프링 컨테이너 : 스프링 빈을 생성하고 관리하는 역할

## 5. JDBC와 JPA?
- JDBC : 애플리케이션 서버와 DB를 연결할 때 필요한 기술

JDBC를 사용하면 애플리케이션에서 DB에 접속하여 데이터를 넣고 뺄 수 있다. DB에 접속한 후 데이터를 처리하는 SQL문은 직접 작성해야 한다.

- JPA : JDBC에서 한 단계 더 나아가 기본적인 SQL도 직접 만들어서 실행해주는 기술

JPA는 인터페이스만 제공하고, 구현 기술은 hibernate 등이 따로 있다.
