# κ°μ μ λ¦¬ π
___

> 2021.08.27 SpringBoot Part1

## κ³΅λΆν λ΄μ©

- ### λͺ¨λ  κ²μ κ³΅μλ¬Έμμ ν¨κ»!!! ###

- ### AOP ###
    - AOP μ μ© λ°©λ²
        1. μ»΄νμΌ μμ 
        2. ν΄λμ€ λ‘λ© μμ 
        3. λ°νμ μμ 

    - μ€νλ§μ AOP Proxies λ°©λ²μ μ¬μ©νλ€. 


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
            // νλ‘μλ Calculator μΈν°νμ΄μ€μ λͺ¨μ΅μ΄λ€.

            var result = proxyInstance.add(1, 2);
            logger.info("Add -> {} ", result);
        }
    }

    ```

    - AOPλ₯Ό μ¬μ©νλ €λ©΄ pom.xmlμ μμ‘΄μ± μΆκ°
    ```xml
        <dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-aop</artifactId>
		</dependency>
    ```

    - νκ² (Target)
        - ν΅μ¬ κΈ°λ₯μ λ΄κ³  μλ λͺ¨λλ‘μ λΆκ°κΈ°λ₯μ λΆμ¬ν  λμ
    - μ‘°μΈ ν¬μΈνΈ (Join Point)
        - μ΄λλ°μ΄μ€κ° μ μ©λ  μ μλ μμΉ
        - νκ² κ°μ²΄κ° κ΅¬νν μΈν°νμ΄μ€μ λͺ¨λ  λ©μλ
    - ν¬μΈνΈ μ»· (Pointcut)
        - μ΄λλ°μ΄μ€λ₯Ό μ μ©ν  νκ²μ λ©μλλ₯Ό μ λ°νλ μ κ·ννμ
        - ν¬μΈνΈμ»· ννμμ executionμΌλ‘ μμνκ³  λ©μλμ Signatureλ₯Ό λΉκ΅νλ λ°©λ²μ μ£Όλ‘ μ΄μ©ν¨
    - μ μ€ν©νΈ (Aspect)
        - μ μ€ν©νΈ = μ΄λλ°μ΄μ€ + ν¬μΈνΈμ»·
        - Springμμλ Aspectλ₯Ό λΉμΌλ‘ λ±λ‘ν΄μ μ¬μ©νλ€.
    - μ΄λλ°μ΄μ€ (Advice)
        - μ΄λλ°μ΄μ€λ νκ²μ νΉμ  μ‘°μΈνΈν¬μΈνΈμ μ κ³΅ν  λΆκ°κΈ°λ₯
        - Adviceμλ @Before, @After, @Around, @AfterRetruning, @AfterThrowing λ±μ΄ μλ€.

    - Springμ AOPλ λΉμΌλ‘ μμ±λ κ°μ²΄μ λν΄μλ§ νλ‘μκ° λ§λ€μ΄μ Έμ μ€ν κ°λ₯νλ€. λΉμΌλ‘ μλ§λ€μ΄μ§λ©΄ μ¬μ© X

    - μ΄λΈνμ΄μμΌλ‘ νμ©ν  μ μκ³ , λ³λμ ν΄λμ€μ λ©μλνμμΌλ‘ μ§μ μμΉλ₯Ό λ§λ€μ΄λ μ λ μλ€.

    - @Transactional μ΄λΈνμ΄μμ νμ©ν΄μ μμμ±μ μλ¬κ° λ°μν  κ²½μ°μ λ°μ΄ν° μμμ±?μ λ³΄μ₯ν  μ μλ€.

    - ### μ€μ΅ νμΈ ###

- ### νΈλμ μ μ ν ###
    - νΈλμ μ μ ν μ’λ₯ ν νμΈν  κ²
    - @Transactional(propagation = ?)μΌλ‘ μ€μ κ°λ₯νλ€.
    - νΈλμ μ κ²©λ¦¬
