# Java-Spring



#오버라이딩
- 상위 클래스가 가지고 있는 메서드를 하위 클래스가 제정의

#다형성
- 하나의 객체가 여러 가지 타입을 가질 수 있다.
- 부모클래스 타입의 참조변수로 자식클래스 타입의 인스턴스를 참조할 수 있도록 해야함. (상위클래스가 하위클래스 참조가능)
- 다형성을 사용함으로써 유연하고, 변경이 용이한 개발 가능. 
- 확장 가능한 설계
- 클라이언트에 영향을 주지 않는 변경가능
- 스프링은 제어의 역전(IOC), 의존관계 주입(DI)은 다형성을 활용함.

#좋은 객체 지향 설계의 5가지 원칙 (SOLID)
1. SRP : 단일책임원칙, 하나의 클래스는 하나의 책임만 가져야 한다. 
2. OCP : 개방-폐쇄 원칙, 확장에는 열려있지만 변경에는 닫혀있어야함. 구현객체를 변경하려면 클라이언트 코드를 변경해야한다. 다형성은 o OCP가 깨짐.
         어떻게 문제를 해결해야하나? -> 별도의 조립, 설정자가 필요하다.
3. LSP : 리스코프 치환 원칙, 상위클래스의 기능을 하위클래스에서 정확하게 기능을 구현해야한다.
4. ISP : 인터페이스 분리 법칙, 인터페이스를 크게하지말고, 규모를 작게하여서 여러개의 인터페이스로 구분한다.
5. DIP : 의존관계 역전원칙, 클라이언트는 인터페이스만 바라보고, 인터페이스를 구현한 클래스에 의존하지마라. -> 인터페이스에만 의존하자.

결론 : 다형성 많으로는 OCP, DIP를 지킬수 없다, 역할과 구현을 분리하자.


* 클래스 다이어그램
클래스 다이어그램 : 시간에 따라 변하지 않는 시스템의 정적인 면을 보여주는 대표적인 UML 구조 다이어그램


<회원 클래스 다이어그램>

<img width="509" alt="스크린샷 2022-06-11 오후 10 46 12" src="https://user-images.githubusercontent.com/75271204/173190523-530b51d4-73f7-49ab-9bfc-8433b199212e.png">


JUnit 테스트
Given - When - Then 이란?
준비, 실행, 검증의 세부분으로 나눈다
준비 : 테스트에서 사용하는 변수의 값 설정 및 정의.
실행 : 변수의 값을 실제 메서드를 호출한다.
검증 : 실행값이 맞는지 검증한다.

@Test, @BeforeEach
@BeforeEach 사용시 @Test 돌아가기전에 먼저 코드를 실행시켜준다.

<img width="585" alt="스크린샷 2022-06-11 오후 11 05 25" src="https://user-images.githubusercontent.com/75271204/173191206-d363909e-5af6-4ecb-bbe5-a0f560154a34.png">


인터페이스뿐만아니라 구현클레스도 함께 의존하고 있다. "DIP" 위반
다른 구현클래스로 변경할려면 클라이언트코드도 변경해야한다. "OCP" 위반
<img width="578" alt="스크린샷 2022-06-12 오후 9 41 09" src="https://user-images.githubusercontent.com/75271204/173233687-6be4f3e6-3b1d-452a-9af8-e79783a80c16.png">

DIP와 OCP를 어떻게 해결할 것인가?
1. AppConfig를 사용하여 구현객체를 생성하고 연결하는 설정클래스
AppConfig를 사용하여서 DIP를 지킨다 즉 인터페이스만 바라보고있게함. 생성자를 통해 주입한다 -> 생성자주입
<img width="500" alt="스크린샷 2022-06-12 오후 9 59 19" src="https://user-images.githubusercontent.com/75271204/173234442-56068666-23e3-4ccb-827b-d2e00a3db615.png">

<img width="732" alt="스크린샷 2022-06-12 오후 10 17 12" src="https://user-images.githubusercontent.com/75271204/173235117-c6aa5d42-d386-4eeb-9e57-7d9d2fb3407d.png">


프로그래머는 "추상화에 의존해야지, 구체화에 의존해서는 안된다." 의존성 주입은 이 원칙을 따르는 방법중 하나

#프레임워크 vs 라이브러리
프레임워크 : 프레임워크가 내가 작성한 코드를 실행하고 대신 실행하면 프레임워크(JUnit).
라이브러리 : 내가 작성한 코드가 직접 제어의 흐름을 담당한다.

#의존관계 주입 DI(Dependency Injection)

객체를 직접 생성하는 게 아니라 외부에서 생성한 후 주입 시켜주는 방식이다.
정적인 클래스 의존관계와 실행시점에서 결정되는 동적인 객체 의존 관계 둘을 분리해서 생각해야함.
정적인 클래스 의존관계 -> 애플리케이션을 실행하지 않아도 쉽게 분석가능. 하지만 실제 어떤 구현객체가 들어올지는 모른다.
동적인 클래스 의존관계 -> 애플리케이션 실행시점에 외부에서 구현객체를 생성하고, 클라이언트에 전달해서 클라이언트와 서버의 실제 의존관계가 되는 것을 의존관계 주입이라 함.

* 즉 DI를 사용하면 정적인 클래스 의존관계 변경없이 돈적인 객체 인스턴스 의존관계를 쉽게 변경할 수 있다.

#IOC(Inversion of Control)
"제어의 역전" 이라는 의미로, 말 그대로 메소드나 객체의 호출작업을 개발자가 결정하는 것이 아니라, 외부에서 결정되는 것을 의미한다.
객체 간의 결합도를 줄이고 유연한 코드를 작성할 수 있게 하여 가독성 및 코드 중복, 유지 보수를 편하게 할 수 있게 한다.

#IOC 컨테이너 및 DI 컨테이너
객체를 생성하고 관리하면서 의존관계를 설정해주는 역할



@Bean & @Configuration


<img width="498" alt="스크린샷 2022-06-13 오후 11 31 11" src="https://user-images.githubusercontent.com/75271204/173377237-c121a84f-ae04-4660-b0a0-1aa9e4f09162.png">

<img width="793" alt="스크린샷 2022-06-13 오후 11 33 09" src="https://user-images.githubusercontent.com/75271204/173377657-086135d4-e0c0-4132-97f4-759efd7c4a26.png">


@Configuration을 통해 설정정보로 사용한다.
@Bean으로 하면 해당 인스턴스 스프링빈으로 등록이 된다.
꺼내서 사용할때에는 applicationContext.getBean("인스턴스이름", 반환타입);
applicationContext을 스프링 컨테이너라고 한다. -> AppConfig을 직접 사용하는 대신


<실제 Bean 으로 등록된걸 확인할 수 있다.>

<img width="549" alt="스크린샷 2022-06-13 오후 11 35 54" src="https://user-images.githubusercontent.com/75271204/173378258-263c9417-a039-4c58-a46e-ded43ce3bc41.png">




<Bean을 조회하는 과정>

<img width="770" alt="스크린샷 2022-06-15 오후 10 45 32" src="https://user-images.githubusercontent.com/75271204/173842760-310a2e49-31f2-4628-a936-557efeb6f5e0.png">

* Bean을 조회하는 과정에서 같은 타입의 빈이 둘이상일시 중복오류 발생.

<img width="811" alt="스크린샷 2022-06-15 오후 10 50 32" src="https://user-images.githubusercontent.com/75271204/173844226-df6a93d8-5404-4a86-8f6d-be5767e57d51.png">

<img width="522" alt="springframework beans factory NoUniqueBeanDefinitionException" src="https://user-images.githubusercontent.com/75271204/173844932-a9fa4c31-5a4c-4035-942a-8b97ea740be8.png">

중복의 타입이 존재시 해결법 -> 빈이름을 지정하면 된다.(메서드 이름)


* 부모와 자식의 상속관계에서 부모를 조회시 자식이 둘 이상이면 오류가 발생한다.


* BeanFactory는 스프링 컨테이너의 최상위 인터페이스이다 -> ApplicationContext는 BeanFactory의 모두 상속받아서 제공
ApplicationContext는 부가적으로 여러 기능을 제공

<img width="475" alt="스크린샷 2022-06-15 오후 11 20 44" src="https://user-images.githubusercontent.com/75271204/173850614-8152d371-c057-4dd0-91b5-fe5ad89ee3db.png">


* 스프링 컨테이너는 다양한 형식의 설정을 제공한다
1. Annotation 기반 자바코드 설정 (AnnotationConfigApplicationContext)
2. XML 설정 사용 (GenericXmlApplicationContext)


<XML을 통한 스프링 컨테이너에 빈 등록>

<img width="738" alt="ApplicationContext" src="https://user-images.githubusercontent.com/75271204/173855470-de11d6e6-9c30-415e-a2d1-5dec140014f7.png">

<img width="774" alt="스크린샷 2022-06-15 오후 11 41 32" src="https://user-images.githubusercontent.com/75271204/173855490-da0e68fb-896a-4a7d-a43b-37e591dcb9bc.png">


* 스프링은 빈 설정 메타정보를 BeanDefinition이라는 추상화를 사용
XML, 자바코드를 사용해도 @Bean, <bean>을 이용해 메타정보를 생성해낸다. 
-> 자세한거는 넘어가도됨.


* 웹어플리케이션 및 싱글톤

싱글톤이 아닌 순수한 컨테이너에서는 요청할때마다 새로운 객체를 생성한다.
이렇게 되면 웹사이트의 다수요청시 지속적인 객체를 생성해야해서 매우 비효율적이다.

<img width="475" alt="AppConfig appConfig = new AppConfig();" src="https://user-images.githubusercontent.com/75271204/174432389-dea3814f-e3bb-402a-b981-86c6e996d99e.png">


<img width="599" alt="스크린샷 2022-06-18 오후 3 02 55" src="https://user-images.githubusercontent.com/75271204/174432394-d04db78a-f5ea-475f-9203-1d2820ae1f5c.png">




#싱글톤 패턴(Singleton Pattern)
객체를 딱하나만 생성하여 그것을 공유하여 사용하는 디자인 패턴이다. 

<img width="607" alt="public static SingletonService getInstance(){" src="https://user-images.githubusercontent.com/75271204/174432401-2d7e737a-2ddd-4786-b1d3-a776b7e91c61.png">


<img width="589" alt="void singletonServiceTest(){" src="https://user-images.githubusercontent.com/75271204/174432404-b464a9c6-e4d1-4218-850a-a32b504b28ae.png">

 
<img width="632" alt="gstart singlet SingletonService931206beb" src="https://user-images.githubusercontent.com/75271204/174432410-88727a5f-9921-475c-8b2c-ceb77c4e5baa.png">
         

같은 인스턴스를 사용하게된다.
하지만 싱글톤 패턴은 단점들이 많다.
1. 싱글톤 패턴을 구현하는 코드가 많다
2. 구체클래스에 의존하게됨 -> DIP 위반
3. OCP위반
4. 유연성이 떨어진다.


#싱글톤 컨테이너
스프링은 싱글톤 패턴의 문제점을 해결하여, 객체 인스턴스를 싱글톤으로 관리해준다.

#Stateful(유지) vs Stateless(무상태) 설계
스프링 컨테이너는 같은 객체 인스턴스를 공유하기 때문에 싱글톤 객체는 상태를 stateful 하게 설계하면 안됨.
즉 stateless로 설계를 해야한다.
* 특정 클라이언트에 의존적인 필드 X
* 특정 클라이언트가 값을 변경할 수 있는 필드 X
* 가급적 수정보단 읽기만 가능하게 끔
* 공유되지 않은 지역변수, 파라미터, ThreadLocal 등을 사용해야함.


#@Configuration을 사용하지 않고 @Bean만 사용하게되면 어떻게될까?
@Bean인 메서드들이 스프링 빈으로 다 등록이 되지만, 싱글톤이 깨져버리게 된다.



#@Autowired @ComponentScan @Component
스프링은 스프링 빈 등록을 자동으로 해주는 컴포넌트 스캔이라는 기능을 제공한다.
@ComponentScan을 사용하면 @Component 로 되어있는걸 모두다 스캔한다.
@Component를 쓰면 해당 인스턴스를 스프링 빈으로 등록해준다.

일단 스프링빈으로 등록된 인스턴스에 
@Autowired를 생성자위에 쓰면 자동으로 의존관계 주입을 해줌 -> 이때 해당 타입이랑 같은 빈을 찾아서 주입해준다.
만약 빈에서 같은 타입을 찾아서 주입하려는데 똑같은 타입이 빈으로 여러게 등록이 되어있으면 어떻게하는가?



