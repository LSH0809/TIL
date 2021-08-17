# 강의 정리 🚀
___

> 2021.08.17 SpringBoot Part1

## 공부한 내용

- ### IoC ###
    - Inversion of Control 은 제어의 역전을 의미한다.
    - IoC 상황에서는 객체가 자신이 사용할 객체를 스스로 선택하지 않고 생성도 하지 않는다.
    - 프레임워크가 흐름을 주도하면서 개발자가 만든 Application 코드를 사용하는 것이다. -> Application 코드가 프레임워크가 만들어 놓은 틀에서 수동적으로 동작하는 것이다. (Hollywood Principle)
    <br>

    ![SpringBoot1 IoC 구조](https://user-images.githubusercontent.com/73347933/129742447-b37ec282-0fb8-4560-9e50-a84a1aca82f2.png)


- ### DDD ###
    - 마이크로소프트 DDD 관련
  
    ![Microsoft DDD 관련 인프라 지속성 계층 디자인](https://user-images.githubusercontent.com/73347933/129745108-4e10e460-4a32-4f1c-a11c-f562c834dcfd.PNG)


    - Aggregate는 일종의 Entity라고 생각하기.

- ### ApplicationContext ###
    - Bean은 IoC 컨테이너에서 관리한다는 의미이다.
    - IoC 컨테이너에서는 register 요청이 들어오면 개별 객체들의 의존관계 설정이 자동으로 이루어지고 객체들의 생성과 파기 조합을 관장한다.
    - ApplicationContext는 BeanFactory를 상속받는다.

    - Configuration MetaData
        - 스프링의 ApplicationContext는 실제 만들어야 할 빈 정보를 Configuration MetaData로 부터 받아온다. 
        - 이를 XML 기반으로 하거나 혹은 Java 기반으로 작성할 수 있다. 
        - XML 기반으로 할 경우, GenericXmlApplicationContext를 구현체로 사용.
        - Java 기반의 설정을 할 경우, AnnotationConfigApplicationContext 구현체를 사용한다.
- ### Dependency Injection ###
    - 생성자 주입 패턴
    - 세터 기반의 의존관계 주입 지원
    