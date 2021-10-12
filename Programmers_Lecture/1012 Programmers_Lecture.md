# 강의 정리 🚀
___
 
> 2021.10.12 협업

## 공부한 내용

- ### 모든 것은 공식문서와 함께!!! ###

- ### DB Pro Tips ###
    - ### 문자열 ###
        - CHAR(100)에 'abc'가 들어가는 경우 -> 계속 용량이 100으로 점유하고 있다.
        - VARCHAR(100)에 'abc'가 들어가는 경우 -> 길이를 3으로 줄여서 점유. 즉, 용량을 그만큼 아낄 수 있다.
        - VARCHAR는 resize 하는 과정이 포함되므로 insert 시간이 늘어난다.
        - TEXT 타입류는 제약이 많다.
        - ### 결론 ###
            - 주민번호, 전화번호 등 길이의 편차가 작은 문자열에는 CHAR
            - 이름, 주소, 게시글 제목/내용 등 길이의 편차가 큰 문자열에는 VARCHAR
            - TEXT 타입류는 제약이 많아서 되도록 CHAR, VARCHAR 사용하자.

    - ### 숫자 ###
        - INT UNSIGNED : UNSIGNED를 붙이면 음수 표현을 위한 비트를 아껴서 양수에 대한 범위가 확장된다.
            -> 예시 : INT AUTO_INCREMENT가 이에 해당된다.
        - INT(11) 의 의미: 숫자 크기가 아니라, ZEROFILL 옵션이 들어가 있을 때 0을 어디까지 채울지를 명시하는 것이다.
        - MySQL에 BOOL 타입은 없다.
            - 대신 BIT(1) 타입을 쓰는 것을 추천.
    - ### PK ###
        - 자연 KEY에서 선택(유니크한지 확인)
        - 대체 KEY 는 자연 KEY에서 쓸만한 것이 없을 때 사용
            - AUTO_INCREMENT도 하나의 예시
    - ### TIME ###
        - 시간은 UTC 기준으로 하는 것을 추천
        - 팀원들끼리의 기준을 정하는 것이 중요하다.
        - UNIX TIMESTAMP를 사용하는 것도 추천
    - ### SOFT DELETE ###
        - 쿼리로 DELETE 날리는 것은 HARD DELETE라고 한다.
        - SOFT DELETE는 STATUS, DELETED 같은 BOOL 컬럼을 두고, UPDATE 쿼리를 날려서 수정하는 것이다.
        - 쉽게 복구할 수 있다는 장점이 있지만, 항상 WHERE 절을 신경써야 한다는 단점이 있다.
    - ### Online DDL ###
        - LOCK을 좀 더 효율적으로 사용
            - ALTER TABLE 문 뒤에 ALGORITHM, LOCK 옵션을 넣으면 된다.
        1. 카피본을 만들고, 카피본에 ALTER 문을 수행
        2. 그동안 들어오는 INSERT / UPDATE / DELETE 문을 로그를 따로 모아두거나 원본에 반영함
        3. 이렇게 만들어진 새로운 테이블로 참조를 바꿔치기 한다.는 방식이다.
        - 모든 조작에 대해 유효한 것은 아니다.
        - backfill 작업은 규모를 작게 여러번 하는 것이 좋다.
    - ### INDEX ###
        - PK, FK, UQ 사실은 모두 INDEX이다.(자동으로 Index가 걸린다.)
        - MYSQL에서 INDEX == KEY 이다.


    ---

- ### API Specification ###
    -  HTTP의 장점을 최대한 활용할 수 있는 아키텍쳐
    - 복수 조회 : /posts
    - 단일 조회 : /posts/{id}
                    
    - ### Idempotence ###
        - Single request의 결과와 2번 이상 요청했을 때의 side effect가 동일하면 Idempotent하다.
        - POST /posts : 1번 요청이 들어오면 하나가 생기겠지만, 2번, 3번 요청하면 그만큼 더 생성되므로 not idempotent하다.
        - DELET / posts : 1번 요청하든, 2번 요청하든 게시물이 삭제되는 것은 똑같으므로 idempotent하다.
        - GET : Idempotent / POST : Not Idempotent / PUT : 싱글 리소스에만 사용. Idempotent . PUT은 create도 지원한다. / Patch : Idempotent . 싱글 리소스에만 사용. / DELETE : Idempotent . 싱글 리소스에만 사용한다.
    
    - ### 정리 ###
        - POST의 경우 201 created와 Location 헤더를 기억하자. (Location 헤더에는 post url을 넣어주면 좋다.)

            


