# 강의 정리 🚀
___

> 2021.09.25 SpringBoot Part

## 공부한 내용

- ### 모든 것은 공식문서와 함께!!! ###
- EntityManagerFactory, EntityManager에 대해 학습
- 영속성 컨텍스트에 대해 학습
- 엔티티의 생명주기에 대해 학습
- 영속성 컨텍스트의 특징에 대해 학습
- 실습을 통해 영속성 컨텍스트에 대해 이해

- ### EntityManagerFactory, EntityManager
    - JPA는 테이블과 Java의 Object를 연결하는 ORM 프레임워크이다.
    - Entity는 RDB의 테이블과 매핑되는 관계이다.
    
    - EntityManagerFactory
        - Entity를 관리하는 EntityManager를 생산하는 공장이다.
        - Thread Safe하다.
    - EntityManager
        - EntityManager는 Entity를 저장하고, 수정하고, 삭제하고, 조회하는 (CRUD) 등, Entity와 관련된 모든 일을 처리한다.(엔티티 관리역할)
        - Thread Safe하지 않다. 여러 쓰레드에서 접근할 경우 동시성 이슈가 발생할 수 있다. 
    
    - 추가
        - EntityManager는 실제로 DB 데이터값을 가지고 올때 Connection을 획득해서 사용하게 된다. (즉, 실제 사용할 때 Connection을 획득한다.는 의미이다./ 트랜젝션을 시작할 때 Connection을 획득한다.)

- ### 영속성 컨텍스트 ###
    - 영속성 컨텍스트
        - JPA를 이용하는데 가장 중요한 요소이다.
        - 엔티티 매니저는 엔티티를 영속성 컨텍스트에 보관하고 관리한다.
        - persist() -> 영속화를 시켜주겠다라는 의미이다. -> 엔티티 객체를 영속성 컨텍스트 안에서 관리하겠다는 의미이다.
        - Entity는 EntityManager에 의해 영속성 컨텍스트에서 관리된다.

    - 영속성 컨텍스트의 특징 (Persistence Context)
        1. 영속성 컨텍스트와 식별자 값
            - 영속성 컨텍스트 안에서 관리되는 엔티티는 식별자 값을 가진다.
                - 왜냐하면, key -value로 엔티티를 관리하기 때문이다. (1차 캐시로 관리되기때문에 식별자 값이 필요하다.)
        2. 영속성 컨텍스트와 데이터 베이스 저장
            - 커밋하는 순간, 영속성 컨텍스트에 저장된 엔티티를 DB에 반영한다.(이를, Flush라고 부른다.)
                - flush는 변경 내용을 DB에 동기화 하는 작업이다.
        3. 영속성 컨텍스트가 엔티티를 관리함으로 얻는 이점
            - 1차 캐시
            - 동일성 보장(1차 캐시로 인해 벌어지는 현상)
            - 트랜젝션을 지원하는 쓰기 지연
            - 변경 감지
            - 지연 로딩

    - 엔티티 생명 주기
        - 영속성 컨텍스트는 모든 변경사항을 감지할 수 있다.

        - 특정한 life cycle이 있다. 즉, Entity는 생명 주기를 지니고 있다.
        1. 비영속(new) - 영속성 컨텍스트와 관계가 없는 상태 
        2. 영속(managed) - 영속성 컨텍스트에 저장된 상태
        3. 준영속(detached) - 영속성 컨텍스트에 저장되었다가 분리된 상태
        4. 삭제(removed) - 삭제된 상태

        - persist() 메소드를 통해 비영속 -> 영속상태가 된다. 이후 flush()를 통해 DB에 저장되는 것이다.
        - detach() / clear() / close() -> 준영속으로 만든다
        - merge() -> 영속화 한다.
        - remove() -> 영속성 컨텍스트 / DB 모두에서 삭제한다.

        - 엔티티를 영속성 컨텍스트에서 관리하기 위해서는 항상 트랜젝션을 시작 / 끝을 만들어야 한다. 그래서 실습과정에서 트랜젝션을 획득한다.
        - 트랜젝션이 commit 되는 순간 flush DB와 동기화가 된다.(엔티티를 영속화 한다라고 표현한다.)


    - 조회
        - 1차 캐시를 이용해서 조회를 할 경우, DB까지 쿼리를 날리지 않고 그냥 1차 캐시에 있는 정보를 바로 반환한다.(DB에 쿼리 안날림)
        - DB를 이용해서 조회를 할 경우, (영속성 컨텍스트를 초기화 한다음 실습(clear()-> 준영속 상태로 만든다.))쿼리가 DB에 날라간다.
        - [흐름 : 1차 캐시에 데이터가 없을 경우, DB에 쿼리를 날라서 조회를 한다. 이후 조회가 있을 경우 1차 캐시에 남아있는 기록을 확인한다.]

        - 궁금증 - 준영속 상태로 만들 경우, 1차 캐시는 비워지는 것인가?

    - 수정
        - flush()를 한 객체와 스냅샷을 이용해서 변경이 되었는지 비교한다.
            - 변경되었으면 업데이트를 한다.
        - 이를 변경 감지라고 한다.(dirty checking)
            - dirty checking
                - JPA는 엔티티를 영속성 컨텍스트에 보관할 때 최초 상태를 복사해서 저장해두는 데 이를 스냅샷이라고 한다. 그리고 flush 시점에 스냅샷과 엔티티를 비교해서 변경된 엔티티를 찾는다. 변경되어있으면 update 쿼리를 날린다.
                (더티 체킹은 영속성 컨텍스트가 관리하는 영속 상태의 엔티티에만 적용된다. -> 준영속, 비영속, 삭제 이런 상태인 것은 더티체킹되지 않는다.)

        - 궁금증 - flush가 일어나는 경우 다시 확인 (commit가 일어날 경우)
        - 영속상태로 만드는 것 : Transaction.BEGIN or persist() 
        - flush() 메소드는 Transaction.COMMIT / flush() 
    
- ### 엔티티 매핑 ###

    - AUTO DDL 옵션
        1. create : 기존 테이블을 사제하고 새로 테이블을 생성한다. (DROP + CREATE)
        2. create-drop : 어플리케이션 종료시 생성한 DDL을 제거한다. (DROP + CREATE + DROP) -> 테스트 코드를 작성할 때 DROP을 하므로 이후 영향이 없어서 좋다.
        3. update : 테이블, 엔티티 매핑 정보를 비교하며 변경상을 수정한다.
        4. validate : 테이블, 엔티티 매핑 정보를 비교해서 차이가 있으면 경도를 남겨 어플리케이션을 실행하지 않는다.
        5. none : 자동 생성 기능을 사용하지 않는다.
        - 개발 환경에서는 주로 1,2,3 번을 이용한다. 

    - @Column
        - @Column(name = ? , nullable = ? , length = ? , unique = ? )
            - name : RDB의 ? 에 해당하는 칼럼과 매핑을 하겠다는 의미이다.  
                - default값은 변수명을 따라간다. 만약 변수명이 nickName일 경우 자동으로 nick_name으로 변경해준다.
            - nullable : NOT NULL 옵션의 여부에 대한 것이다.
            - length : String 형에서만 사용가능하다. VARCHAR의 length를 얼마로 줄 것인지 결정한다.
            - unique : RDB의 유니크 제약 조건에 해당한다. 
            - insertable : 엔티티 저장시 필드도 같이 저장한다. false이면 읽기 전용으로 사용한다.

        - 이러한 옵션에 대한 것은 사용하지 않다 하더라도 다른 개발자들이 보는 편의성을 고려하여 작성하는 것을 권장한다.

    - 기본키 매핑 전략
        - 1차 캐시에서 사용할 수 있다.
        1. 직접할당
            - 개발자가 임의로 직접 할당
        2. SEQUENCE
            - 데이터베이스 시퀀스에서 식별자 값을 획득한 후 영속화
            - ORACLE, H2
        3. TABLE
            - 데이터 베이스 시퀀스 생성용 테이블에서 식별자 값을 획득한 후 영속화 (자주 사용x)
        4. IDENTITY
            - 데이터베이스 엔티티를 저장해서 식별자 값을 획득한 후 영속화
            - 엔티티가 영속화 되려면 식별자 값이 반드시 필요하기 때문에, persist() 시점에 INSERT 쿼리가 같이 수행된다.
            - MYSQL의 AUTO_INCREMENT와 같다.
        5. AUTO
            - dialect 방언에 따라서 자동으로 전략을 선택
            - 실무에서는 이 방법 자주 사용
        - 1번, 5번을 자주 사용
    
    - 기타 컬럼 매핑
        - @Column의 속성 columnDefinition = "TIMESTAMP" : LocalDateTime을 다루고 싶을 때 이렇게 입력하면 값이 입력된다.
        - @Enumerated(EnumType.STRING) : ENUM 값을 넣고 싶을 때 사용한다.
        - @Lob : VARCHAR(255)가 넘는 Long TEXT일 경우 사용한다.

- ### 단일 관계 매핑을 할 경우 문제 ###
    - 객체 중심설계를 고려했는데 단일 관계 매핑을 할 경우 FK를 이용할 때 객체 그래프 탐색을 하지 못한다. 
        - 즉, 객체 중심적이지 못한 상황이 나온다. -> 연관관계 매핑을 해야한다.