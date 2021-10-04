# 강의 정리 🚀
___

> 2021.10.04 SpringBoot Part

## 공부한 내용

- ### 모든 것은 공식문서와 함께!!! ###

- ### 기본 개념 ###
    - IaaS(Infrastructure as a Service)
        - IaaS는 서버, 네트워킹, 스토리지와 데이터 센터 공간 등의 컴퓨팅 자원을 종량제방식
    - PaaS(Platform as a Service)
        - 웹 기반 어플리케이션을 빌드하여 제공하는 전 과정을 지원하는데 갖춘 클라우드 기반 환경 제공
    - SaaS(Software as a Service)
        - 클라우드 기반 어플리케이션 혹은 SaaS는 모든 기능이 동작하는 SW를 제공

    - Public Cloud / Private Cloud / Hybrid Cloud
        - Deployment model로 구분

    - 클라우드 서비스 기본 개념
        - Virtualization(가상화)를 이용함
            - 리소스 효율성 / 관리 편의성 / 가동 중단 시간 최소화 / 프로비저닝 고소화 -> 장점
        - 가상머신(VM)
            - 가상화를 실행시킬 수 있는 환경
        - 하이퍼 바이저
            - VM을 구성하는 소프트웨어 계층

    - CDN(Content Delivery Network)
        - 서버와 사용자 사이의 물리적인 거리를 줄여 소요 시간을 최소화.
        - 지역별로 서버를 구축해서 빠르게 받을 수 있도록 함.(캐시서버(엣지서버) 이용)
            - 이렇게 하면 Origin server의 부하도 줄어듬

    - 스냅샷(Snapshot)
        - 특정 시점에 특정 파일을 포착해 보관하는 기술(이미지화)
        - 장애나 데이터 손상 시 스냅샷을 생성한 시점으로 데이터를 복구
        - 큰 스토리지 공간을 차지하지 않는다.
        - 장애도 해결 가능함

    - 데이터 센터 : 수많은 서버들을 한데 모아 네트워크로 연결해 놓은 시설

    - 지역(Region)
        - 데이터 센터가 위치한 지역
        - IT 리소스를 생성할 Region은 선택 가능
        - 고객의 지역과 자원을 생성할 Region은 최대한 가까워야함.

    - 가용영역(Availability Zone)
        - Region들을 두가지 이상들로 묶은 것
        - AZ로 표시

- ### AWS 기본 기능 ###
    - EC2(Elastic Cloud Compute)
        - 인스턴스 타입 : 메모리 / 용량 / 스토리지 등 다양한 속성의 성능을 통해서 설정
    - AMI(Amazon Machine Image)
        - 이미지 - OS,설치된 프로그램, 설정 등이 포함된 파일
    - Security Group
        - EC2 인스턴스에 대한 보안 설정
    - Key Pair
        - EC2 인스턴스에 접속하기 위한 암호화 된 파일
    - Elastic IP
        - EC2 인스턴스는 Private Ip와 Public IP를 보유

    - 그외 등등 (노션 강의 자료)
- ### 실습 시작 ###
