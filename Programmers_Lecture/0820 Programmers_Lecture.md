# 강의 정리 🚀
___

> 2021.08.20 SpringBoot Part1

## 공부한 내용

- ### 모든 것은 공식문서와 함께!!! ###

- ### 로깅 처리하기 ###
    - 로깅
        - 시스템을 작동할 때 시스템의 작동 상태의 기록과 보존, 이용자의 습성 조사 및 시스템 동작의 분석 등을 하기 위해 작동중의 각종 정보를 기록해둘 필요가 있다. 이 기록을 만드는 것을 <로깅>이라 한다.
    - System.out.println()을 쓰기 보다 로깅을 사용해야한다. System.out.println()은 성능에 부담이 많이 간다.
    - SLF4J 
        - Logging Framework들을 추상화해놓은 것이다.
        - Facade Pattern을 이용했다.
        - 퍼사드 패턴은 서브시스템(내부 구조)을 거대한 클래스(외벽)로 만들어 감싸서 편리한 인터페이스를 제공해준다.
        - SLF4J가 다양한 로깅 프레임워크를 지원하는데 이는 바인딩 모듈을 통해서 처리된다.
            - 바인딩 모듈은 로깅 프레임워크를 연결하는 역할을 한다.
        - Log Level
            1. trace
            2. debug
            3. info
            4. warn
            5. error
            ![image](https://user-images.githubusercontent.com/73347933/130193157-c9804881-709a-4d1d-b525-5a293c2a1f87.png)
                - effective level q 를 하면 level of request p의 범위를 제공한다.(ex. DEBUG 레벨을 하면 TRACE 빼고 전부 나온다.)

        - 로거는 이름 기반으로 기록된다.
        - 로거 팩토리가 필요한데 일반적으로 클래스 단위에서 생성된다.
        ```java
        private static final Logger logger = LoggerFactory.getLogger(OrderTester.class);
        ```
- ### logback 설정하기 ###
    - logback 설정파일 찾는 순서
        1. logback-test.xml 파일을 먼저 찾는다.
        2. 없다면 logback.groovy를 찾는다.
        3. 그래도 없다면 logback.xml을 찾는다.
        4. 모두 없다면 기본 설정 전략을 따른다. BasicConfiguration
    - Appender를 설정해서 로그 기록을 어디에 기록할지 정할 수 있다.

- ### Conversion Rule ###
    - logger를 보다 시각화하기 좋게 색깔을 변화할 수 있다.
    - 콘솔창과 FILE 등 각각 다른 설정을 줄 수 있다.

- ### SpringBoot ###
    - @SpringBootApplication
        - SpringBootConfiguration 이 하나, 별도로 Configuration 필요하면 생성 
        - SpringBootConfiguration은 하나여야한다.
        - ComponentScan 이 안에 있기 때문에 자동으로 스캔하게 된다.
        - CoC : 소프트웨어 개발자들이 결정할 갯수를 줄여서 단순하고도 유연하게 해 주는 소프트웨어 디자인 패러다임 이라고 한다.
    - SpringBanner Generator를 이용해서 배너도 만들 수 있다.
        - resource 폴더 밑에 banner.txt에 내용을 작성하면 자동으로 인식한다.
