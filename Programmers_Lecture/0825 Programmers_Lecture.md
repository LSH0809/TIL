# 강의 정리 🚀
___

> 2021.08.25 SpringBoot Part1

## 공부한 내용

- ### 모든 것은 공식문서와 함께!!! ###

- ### Spring JDBC ###

    - DataSource 
        - DateSource를 통해 데이터를 가져올 수 있다.
    - DataBase Connection Pool
        - 풀에 커넥션을 가져와서 쌓아두고 사용할 때 커넥션을 가져와서 사용하는 것이다.
    - DataSource - HikariCp
        - 빠르고 안정적인 JDBC라고 알려져 있다.
        - setter method는 비즈니스적으로 작성해야한다.

        - null 처리를 위해서 Optional을 사용해서 하는 것을 항상 고민하기
        - sql문에서 show status를 통해 쓰레드에 커넥션이 쌓이는 것을 확인할 수 있다.
    - @TestInstance.LifeCycle.PER_CLASS라고 하면 클래스별이므로 인스턴스가 한개이다. 이렇게 할경우 @BeforeAll의 메소드는 static을 사용하지 않아도 된다.
    - 테스트를 하면 내가 코드를 작성한 순서대로 테스트 코드가 돌아가지 않는다. 그러므로 @Order 어노테이션을 활용해야한다.
        - @TestMethodOrder(MethodOrderer.OrderAnnotation.class) 이부분을 테스트 클래스에 추가해줘야한다.
        - 단, @BeforeAll은 이 Order 어노테이션 이전에 실행한다.

- ### JdbcTemplate ###
    - 반복적인 부분을 템플릿 형식으로 제공하고 수정해야할 부분만 수정할 수 있게 도와준다.
    - 7장 너무 어렵다. JdbcTemplate 구조 분석 및 복습 필요
    - 한건의 데이터의 값은 - > queryForObject를 통해 얻을 수 있다. 
    - update / insert / delete는 jdbcTemplate의 update 메소드를 이용할 수 있다.
    - JdbcTemplate / Callback의 기본적인 원리와 동작 파악하기
<br>

- ### 실습과 관련한 것이 대부분이라 실습이 보다 중요함! ###