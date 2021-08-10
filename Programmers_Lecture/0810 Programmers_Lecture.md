# 강의 정리 🚀
___

> 2021.08.10 실리콘밸리에서 날아온 데이터베이스(2)

## 공부한 내용

- ### MySQL 소개 ###
    - MySQL 특징
        - **용량 증대 방식(Scaling)**
            - Scale - Up : 서버에 CPU와 Memory 추가
            - Scale - Out : Master - Slave 구성
                - 클러스터 방식도 존재하지만 MySQL은 이를 지원하지 못한다.

- ### 클라우드와 AWS 소개 ###
    - 클라우드 : 자원을 필요한만큼 실시간으로 할당하여 사용한 만큼 지불
        - 장점 
            - 초기 투자 비용이 크게 줄어듬
            - 리소스 준비를 위한 대기시간 대폭 감소
            - 노는 리소스 제거로 비용 감소
            - 글로벌 확장 용이
            - 소프트웨어 개발 시간 단축(Saas 이용)

    - **EC2(Elastic Cloud Comput)**
        -  AWS의 서버 호스팅 서비스
            - 리눅스 혹은 윈도우 서버를 론치하고 로그인 가능
            - 가상서버들이라 전용서버에 비해 성능이 떨어진다.
        - 3개의 옵션
            - On-Demand : 시간당 비용을 지불(가장 흔함)
            - Reserved : 1년이나 3년간 사용보장 -> 할인 옵션
            - Spot Instance : 경매방식으로 보다 싸게 사용
    
    - **S3(Simple Storage Service)**
        - 대용량 클라우드 스토리지 서비스
        - 데이터 저장관리르 위해 계층적 구조를 제공
        - 디렉토리 = 버킷
   

- ### MySQL 설치와 Docker ###
    - **도커(Docker)란?**
        - 다른 OS에서 설치하려면 다양한 변수가 존재
        - 특정 프로그램과 소프트웨어들을 하나의 패키지로 만듬으로써 해당 프로그램의 개발과 사용을 도와주는 오픈소스 플랫폼
        
        - **Docker Image** : 패키지를 파일 시스템 형태로 만든 것
        - **Docker Registry** : Docker Image 공유소
        - **Docker Container** : Docker Image를 실행시킨 것 (응용 프로그램)
            - 곧 인스턴스를 의미한다.

    - 설치방법 제공(강의자료)
    

- ### MySQL 설치와 AWS RDS ###
    - RDS란?
        - AWS가 제공해주는 다양한 관계형 데이터베이스 서비스
    
    - 설치방법 제공(강의자료)
    

- ### DDL과 예제 데이터 소개 ###
    ![image](https://user-images.githubusercontent.com/73347933/128841766-f6100ca4-9fd1-4d75-b94b-8280d9dda777.png)


    ![image](https://user-images.githubusercontent.com/73347933/128842007-4ab8d943-060c-40af-9d8c-0ace250f3784.png)
