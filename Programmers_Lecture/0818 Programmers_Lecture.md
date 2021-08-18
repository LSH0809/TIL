# 강의 정리 🚀
___

> 2021.08.18 SpringBoot Part1

## 공부한 내용

- ### IoC ###
    - new AnnotationConfigApplicationContext 라고 하면 ApplicationContext의 구현체이다. 또한 AppConfiguration.class는 메타데이터 이며 이를 전달하는 것이다.
    - AppConfiguration 안에 Description이 @Bean으로 낭려되어있는 것이다.
    
    - 주의해야할 부분
        - Circular Dependencies(순환 참조)

- ### 컴포넌트 스캔 ###
    - 컴포넌트 스캔은 스프링이 직접 클래스를 검색해서 빈으로 등록해주는 기능이다.(우리가 직접 등록 안해도 된다.)
    - 스프링은 자동으로 등록될 빈을 어떻게 찾는가?
        - Stereotype 어노테이션을 이용하면 스캔 대상을 지정할 수 있다.
        - 스트레오 타입이란?
            - UML 다이어그램을 확장시켜주는 도구로서 특정 요소를 상황이나 도메인에 맞게 분류해주는 것이다.
            - @Component, @Repository, @Controller, @Service 등이 있다.

    - 인터페이스가 아닌 구현체에 해줘야한다.
    - @ComponentScan을 하면 패키지 기준으로 등록할 것을 모두 찾는다.
        - @ComponentScan에서 basePackages 를 이용해서 원하는 패키지를 입력할 수 있다.
        - basePackageClasses을 이용해도 된다. 그러면 입력한 클래스를 기준으로 찾는다.
        - excludeFilters를 이용해서 제외할 것을 정할 수도 있다.
        ```java
        @ComponentScan(basePackages = {"org.programmers.order","org.programmers.voucher"})
        @ComponentScan(basePackageClasses ={Order.class, Voucher.class})
        @ComponentScan(excludeFilters = {@ComponentScan.Filter(type = FilterType.ANNOTATION, value = MemoryVoucherRepository.class)})
        ```

- ### Autowired ###
    - 자동으로 의존관계 주입하는 역할을 한다.
    1. Autowired를 사용
    2. Setter 메소드를 이용
    3. 생성자 이용

    - 이 중, 생성자 기반 의존관계 주입을 선택해야한다. 왜???
        - 초기화 시에 필요한 모든 의존관계가 형성되기 때문에 안전하다.
        - 잘못된 패턴을 찾을 수 있게 도와준다.
        - 테스트를 쉽게 해준다.
        - 불변성을 확보한다.
    
    - 만약, 하나의 인터페이스의 구현체가 두개 이상일 경우에는 어떻게 하나?
        - @Primary 어노테이션을 사용해서 우선시 되는 것을 지정해준다.
        - 혹은, @Qualifier 어노테이션을 사용해서 이름을 지정해준다.

- ### Bean Scope ###
    ```java
    @Scope(value = ConfigurableBeanFactory.SCOPE_PROTOTYPE)
    ```
    - 이러한 어노테이션을 활용해서 scope를 지정할 수 있다.
    - 디폴트는 싱글톤이다.

- ### Lifes Cycle ###
    - 생성이 있으면 소멸도 있다. 
    - ApplicationContext에서 close()라는 메소드가 있다. 이것을 사용하면 소멸된다.
    - close() 메소드를 사용하면 컨테이너에 있는 빈이 모두 없어진다.
    - Bean 생성 생명주기 콜백
        1. @PostConstruct 어노테이션이 적용된 메소드 호출
        2. Bean이 InitializingBean 인터페이스 구현시 afterPropertiesSet 호출
        3. @Bean 어노테이션의 initMethod에 설정한 메소드 호출
    - Bean 소멸 생명주기 콜백
        1. @PreDestroy 어노테이션이 적용된 메소드 호출
        2. Bean이 DisposableBean 인터페이스 구현시 destroy 호출
        3. @Bean 어노테이션의 destroyMethod에 설정한 메소드 호출