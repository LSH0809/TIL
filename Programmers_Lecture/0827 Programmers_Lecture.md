# 강의 정리 🚀
___

> 2021.08.27 SpringBoot Part1

## 공부한 내용

- ### 모든 것은 공식문서와 함께!!! ###

- ### AOP ###
    - AOP 적용 방법
        1. 컴파일 시점
        2. 클래스 로딩 시점
        3. 런타임 시점

    - 스프링은 AOP Proxies 방법을 사용한다. 


    ```java
    class CalculatorImpl implements Calculator {

        @Override
        public int add(int a, int b) {
            return a + b;
        }
    }

    interface Calculator {
        int add(int a, int b);
    }

    class LoggingInvocationHandler implements InvocationHandler {
        private static final Logger logger = LoggerFactory.getLogger(LoggingInvocationHandler.class);

        private final Object target;

        public LoggingInvocationHandler(Object target) {
            this.target = target;
        }

        @Override
        public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
            logger.info("{} executed in {}", method.getName(), target.getClass().getCanonicalName());
            return method.invoke(target, args);
        }
    }

    public class JdkProxyTest {
        private static final Logger logger = LoggerFactory.getLogger(JdkProxyTest.class);

        public static void main(String[] args) {
            var calculator = new CalculatorImpl();
            Calculator proxyInstance = (Calculator) Proxy.newProxyInstance(LoggingInvocationHandler.class.getClassLoader(), new Class[]{Calculator.class}, new LoggingInvocationHandler(calculator));
            // 프록시는 Calculator 인터페이스의 모습이다.

            var result = proxyInstance.add(1, 2);
            logger.info("Add -> {} ", result);
        }
    }

    ```

    - AOP를 사용하려면 pom.xml에 의존성 추가
    ```xml
        <dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-aop</artifactId>
		</dependency>
    ```

    - 타겟 (Target)
        - 핵심 기능을 담고 있는 모듈로서 부가기능을 부여할 대상
    - 조인 포인트 (Join Point)
        - 어드바이스가 적용될 수 잇는 위치
        - 타겟 객체가 구현한 인터페이스의 모든 메소드
    - 포인트 컷 (Pointcut)
        - 어드바이스를 적용할 타겟의 메소드를 선발하는 정규표현식
        - 포인트컷 표현식은 execution으로 시작하고 메소드의 Signature를 비교한느 방법을 주로 이용함
    - 애스팩트 (Aspect)
        - 애스팩트 = 어드바이스 + 포인트컷
        - Spring에서는 Aspect를 빈으로 등록해서 사용한다.
    - 어드바이스 (Advice)
        - 어드바이스는 타겟의 특정 조인트포인트에 제공할 부가기능
        - Advice에는 @Before, @After, @Around, @AfterRetruning, @AfterThrowing 등이 있다.

    - Spring의 AOP는 빈으로 생성된 객체에 대해서만 프록시가 만들어져서 실행 가능하다. 빈으로 안만들어지면 사용 X

    - 어노테이션으로 활용할 수 있고, 별도의 클래스에 메소드형식으로 지정위치를 만들어둘 수 도 있다.

    - @Transactional 어노테이션을 활용해서 원자성을 에러가 발생할 경우의 데이터 원자성?을 보장할 수 있다.

    - ### 실습 확인 ###

- ### 트랜젝션 전파 ###
    - 트랜젝션 전파 종류 표 확인할 것
    - @Transactional(propagation = ?)으로 설정가능하다.
    - 트랜젝션 격리
