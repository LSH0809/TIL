# 강의 정리 🚀
___

> 2021.08.11 실리콘밸리에서 날아온 데이터베이스(3)

## 공부한 내용

- ### 실습환경 소개 ###
    - MySQL Workbench를 사용


- ### SELECT 살펴보기 ###
    - SELECT 사용하기 이전에
        - SHOW DATABASES;
        - USE [데이터베이스 이름];
        - SHOW TABLES;

    - 만약, USE [데이터베이스 이름]을 사용하지 않았다면 [데이터베이스 이름].[테이블명]을 사용할 수 있다.

    - DISTINCT : 중복 제거

    - CASE WHEN
        - 필드 값의 변환을 위해 사용 가능하다.
        - 형식
            - CASE WHEN 조건 THEN 참일때 값 ELSE 거짓일때 값 END 필드이름
        
    - NULL이란?
        - 값이 존재하지 않음을 나타내는 상수
    
    - WHERE
        - IN
        - LIKE
        - BETWEEN

    - String Functions
        - LEFT / REPLACE / UPPER / LOWER / LENGTH / LPAD / RPAD / SUBSTRING / CONCAT
    
    - ORDER BY
        - 디폴트 순서는 오름차순
        - NULL 값 순서는 ?
            - NULL 값들은 오름차순일 경우, 처음에 위치함
            - NULL 값들은 내림차순일 경우, 마지막에 위치함


- ### GROUP BY 살펴보기 ###

    - 그룹별로 다양한 정보를 계산
        1. 그룹핑을 할 피드를 결정
        2. Aggregate 함수를 사용 (COUNT, SUM, AVG, MIN,MAX)
    

