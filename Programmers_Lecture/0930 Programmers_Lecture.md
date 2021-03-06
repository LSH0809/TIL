# 강의 정리 🚀
___

> 2021.09.30 SpringBoot Part

## 공부한 내용

- ### 모든 것은 공식문서와 함께!!! ###
- 스프링 데이터 JPA에 대해 소개
- Native Query (QueryDSL)

- ### Spring Data JPA ###
    - 데이터 소스 및 엔티티 매니저 트랜젝션 매니저 설정을 자동으로 해준다.
    - 스프링에서 JPA를 편리하게 사용할 수 있도록 지원하는 프로젝트이다.
    - 인터페이스를 가져와 사용한다면 CRUD를 간편하게 구현할 수 있다.
        - 메소드를 호출해서 실행
        
    - 이를 통해 우리는 엔티티 객체에 좀 더 집중할 수 있다.
    - 메소드 쿼리
        - docs 확인
            - 명시되어있는 키워드를 이용해서 구현 가능하다.
        - 만약, 메소드만으로 구현하기 힘들다면, @Query 어노테이션을 이용해서 구현할 수 있다.(JPQL)
        - QueryDSL (빌더패턴을 이용해서 구현) - 실제 Native Query는 QueryDSL을 많이 이용한다.

    - Spring Data JPA를 사용하면 쿼리 작성하는 데 집중하기 보다 엔티티 자체에 좀 더 신경을 쓸 수 있다.
    - 쿼리 지향 개발이 아닌 객체 지향 개발을 하게 도와준다.

- ### REST-API ###
    - MockMvc을 이용해서 Controller 테스트 코드 실습
    - Service Layer 테스트 코드 실습