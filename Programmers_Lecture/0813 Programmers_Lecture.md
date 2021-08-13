# 강의 정리 🚀
___

> 2021.08.13 실리콘밸리에서 날아온 데이터베이스(4)

## 공부한 내용

- ### 트랜잭션 소개 ###
    - Atomic하게 실행되어야 하는 SQL들을 묶어서 하나의 작업처럼 처리하는 방법
        - DDL이나 DML 중 레코드를 수정/추가/삭제한 것에만 의미가 있다.
        - SELECT에는 트랜잭션을 사용할 이유가 없다.
        - BEGIN과 END OR BEGIN과 COMMIT 사이에 SQL문을 사용한다.
        - ROLLBACK을 할경우 이전 상태로 돌린다.
            - END와 COMMIT은 같다.
    - AUTOCOMMIT 모드
        - TRUE / FALSE에 따라서 COMMIT을 마지막에 해주거나 안해줘도된다.
        - SET autocommit= 0(혹은 1)의 실행으로 변경가능하다. 
            - 0은 False / 1은 True
    - TRUNCATE는 트랜잭션을 지원하지 않는다.


- ### VIEW 소개와 실습 ###
    - VIEW란?
        - 자주 사용하는 SQL쿼리(SELECT문)에 이름을 주고 그 사용을 쉽게 하는 것이다.
        - 이름이 있는 쿼리가 VIEW로 DB에 저장된다.
    
    
- ### Stored Procedure, Trigger 소개와 실습 ### (심화 공부 필요)
    - Stored Procedure란?
        - MySQL 서버단에 저장되는 SQL 쿼리들
            - CREATE PROCEDURE 사용
            - DROP PROCEDURE [IF EXISTS]로 제거
        - 함수처럼 인자를 넘기는 것이 가능
        - 리턴되는 값은 레코드들의 집합
        
        - DELIMITER // 를 이용해서 작성한다.

        - IN 파라미터 / INOUT 파라미터
    - Stored Function이란?
        - 값을 하나 리턴해주는 서버쪽 함수
        - 모든 함수의 인자는 IN 파라미터
        - Stored Procedure와 가장 다른 차이점 : SQL안에서 사용가능하다.

    - Trigger란?
        - CREATE TRIGGER 명령문을 사용한다.
        - INSERT, DELETE / UPDATE 실행 전, 후에 특정한 작업을 수행하는 거이다.
        - 중요 테이블의 경우 audit(감사)가 필요하다.



- ### Explain SQL과 Index 튜닝과 실습 ### (심화 공부 필요)
    - Explain SQL
        - SELECT / UPDATE / DELETE / INSERT 등의 쿼리가 어떻게 수행하는지 내부를 보여주는 SQL 명령
        - MySQL이 해당 쿼리를 어떻게 실행할지 Execution Plan을 보여준다.
        - 보통 느린 쿼리의 경우 문제가 되는 테이블에 인덱스를 붙이는 것이 일반적이다.

    - Index
        - Index는 테이블에서 특정 찾기 작업을 빠르게 수행하기 위해서 MySQL이 별도로 만드는 데이터 구조를 말한다.
        - INDEX 와 KEY는 같은 말이다.
        