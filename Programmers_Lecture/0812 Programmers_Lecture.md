# 강의 정리 🚀
___

> 2021.08.11 실리콘밸리에서 날아온 데이터베이스(3)

## 공부한 내용

- ### INSERT / UPDATE / DELETE 설명 ###
    - MySQL에서 지원하는 컬럼 타입
        - Numeric Type
            - INTEGER, INT, SMALLINT, TINYINT, MEDIUMINT, BIGINT
            - DECIMAL, NUMERIC
            - FLAOT, DOUBLE, BIT
        - Date and Time Type
            - DATE, DATETIME, TIMESTAMP, TIME, YEAR
        - String Type
            - CHAR, VARCHAR, BINARY, VARBINARY, BLOB, TEXT, ENUM, SET
        - JSON Type
            - 다양한 JSON 조작함수를 제공함
        - Spatial Type
            - 위치 관련 타입

    - TIP
        - 돈과 관련해서는 DECIMAL 타입을, 소수점 이하 신경을 쓰지 않을 때는 DECIMAL, NUMERIC
        - FLOAT과 DOUBLE의 차이
            - DOUBLE 타입의 precision이 더 좋다. 더 잘표현이 가능하다. 하지만, storage가 더 차지한다. 
            - FLOAT은 반대로 storage가 덜 차지한다.

        - VARCHAR vs CHAR
            - CHAR : 고정된 길이
            - 둘 다 텍스트 길이의 제한이 있기 때문에 긴 텍스트일 경우 TEXT 타입을 써야한다.

    - INSERT
        - EX)
            - INSERT INTO prod.vital(user_id, vital_id, date, weight) VALUES(100, 1, '2020-01-01', 75);
            - INSERT INTO prod.alert VALUES(1, 4, 'WeightIncrease', '2020-01-02', 101);

    - DELETE
        - EX)
            - DELETE FROM prod.vital WHERE weight <= 0;
        - DELETE vs TRUNCATE
            - DELETE는 WHERE 조건문을 사용할 수 있다. 대신 속도가 느리다.
            - TRUNCATE는 WHERE 조건문을 사용할 수 없다. 대신 속도가 빠르다. 또한 트랜젝션 사용시 롤백이 불가능하다.

    - UPDATE
        - EX)
            - UPDATE prod.vital SET weight = 92 WHERE vital_id = 4;


- ### INSERT/ UPDATE / DELETE 실습 ###
    - MySQL Workbench로 실습

- ### 다양한 JOIN 살펴보기
    - JOIN이란?
        - SQL 조인은 두 개 이상의 테이블들을 공통 필드를 가지고 통합
        - JOIN의 결과로 양쪽의 필드를 모두 가진 새로운 테이블이 만들어짐.

        ![image](https://user-images.githubusercontent.com/73347933/129161279-5743ebec-22af-485a-8f74-cc52507d948e.png)


    - JOIN 문법
        - MySQL은 FULL 조인을 지원하지 않는다.
        - SELECT A.*, B.* FROM raw_data.table1 A ____ JOIN raw_data.table2 B ON A. key1 = B.key1 and A.key2 = B.key2 WHERE A.ts >= '2019-01-01';

    - JOIN시 고려해야할 점
        - 중복 레코드가 없고 PK의 유일성이 보장되는 지를 체크
        - 조인하는 테이블들간의 관계를 명확하게 정의 -> 어느 테이블을 FROM 절에 사용할지 결정
    
    - JOIN 설명
        - INNER JOIN
            - 양쪽 테이블에서 매치가 되는 레코드만 리턴함
            - 양쪽 테이블의 필드가 모두 채워진 상태로 리턴된다.
        - LEFT JOIN
            - 왼쪽 테이블(BASE)(FROM 절에 사용)의 모든 레코드들을 리턴함
            - 오른쪽 테이블의 필드는 왼쪽 테이블의 레코드와 일치하는 경우에만 채워지고 나머지는 NULL로 리턴된다.
        - FULL JOIN
            - 왼쪽 테이블과 오른쪽 테이블의 모든 레코드들을 리턴함
            - 매칭되는 경우에만 채워지고 나머지는 NULL로 리턴함
        - CROSS JOIN
            - 왼쪽 테이블과 오른쪽 테이블의 레코드의 모든 조합을 리턴함
        - SELF JOIN
            - 동일한 테이블을 ALIAS를 다르게 해서 자기 자신과 조인함


- ### JOIN 실습 ###
    - MySQL workbench로 실습