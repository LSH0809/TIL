# 강의 정리 🚀
___

> 2021.09.25 SpringBoot Part

## 공부한 내용

- ### 모든 것은 공식문서와 함께!!! ###
- ApplicationLayer에서 Database Layer에 접근하는 방법에 대해 학습
    - JDBC Template, 쿼리매퍼(Mybatis)소개
    - ORM(JPA)
- JPA란 무엇인지 학습한다.
- JPA의 필요성에 대해서 학습한다.

- ### JDBC ###
    - Statment, ResultSet 객체를 이용하여 JDBC API / JDBC Template실습(기존의 실습 과정과 같다.)
    - Connection 획득
    - Statment를 이용한 질의
    - ResultSet을 이용하여 질의결과에 대한 사용
    - Statement, Connection 반납


- ### Mybatis ###
    - type-aliases-package : VO 파일의 경로를 설정하는 것이다.(쿼리 결과를 어떤 객체, 패키지에 매핑할지 결정)
    - map-underscore-camel-case : camelCase로 매핑시켜준다.
    - default-fetch-size : select All Query를 했을 때 한번에 몇개씩 가져올지 크기 결정
    - default-statement-timeout : statement는 API와 통신하는 객체인데 그러한 타임아웃을 설정하는 것이다.
    - mapper-locations: Mybatis는 쿼리를 xml 파일로 관리하는데 그러한 파일 경로를 설정할 수 있다.

    - @Mapper 어노테이션을 이용한 인터페이스를 통해서 관리할 수 있다.
    - JDBC 쿼리를 Java 코드와 분리하여 관리할 수 있다.
        - 즉, 메소드를 호출하면 해당하는 쿼리가 실행되는 것이다.

    - 간단한 예제 확인
- ### JPA ###
    - 이전 MyBatis는 쿼리 코드를 직접작성하며 메소드가 호출되는 것을 확인했다.
    - JPA는 @Entity라는 어노테이션을 이용해서 테이블과 매핑되게 한다.
    - @Table 어노테이션을 이용해서 어떤 테이블과 매핑되는지 정할 수 있다.
    - Java 객체의 변경을 통해 쿼리를 수행하는 장점을 지니고 있다.
    - ORM : 객체와 관계형 데이터베이스를 연결시켜준다는 의미를 지닌다.

    - JPA를 사용하는 이유
        - SQL에 의존적인 개발에서 탈피하여, 객체중심으로 생산적인 개발이 가능하다.(생산성 증진)
        - 객체지향 프로그래밍은 추상화,캡슐화, 상속, 다형성등을 제공한다.
        - 관계형 데이터베이스 데이터 중심으로 구조화 되어있으며, OOP의 특징을 지원하지 않는다. -> (객체와 관계형 테이블의 패러다임 불일치)