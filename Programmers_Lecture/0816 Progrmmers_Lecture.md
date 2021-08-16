# 강의 정리 🚀
___

> 2021.08.16 강의 소개 및 스프링 부트 프로젝트 만들기

## 공부한 내용

- ### 프로젝트 생성 및 환경 설정 ###

    - Build Tool 선택하기
         - packing된 파일을 artifacts라고 부른다.
            - Build Tool은 Task들을 자동화하게 해주고 그러한 Task를 기술할 수 있게 도와줍니다.
            - 이렇게 기술된 파일을 빌드 스크립트라고 합니다.
            - Apache Maven -> XML / Gradle -> Groovy or Kotlin
        1. Maven
            - XML 기반으로 설정 모델을 제공하고 pom.xml 파일로 작성할 수 있습니다.
            - POM : Project Object Model의 약어
            - archetypes라는 프로젝트 템플릿을 제공해서 매번 같은 설정을 반복하지 않게 도와줍니다. 
            - 외부 라이브러리인 dependency를 관리해줍니다. 
            - groupId : 주로 회사나 단체명을 작성
            - artifactId : 주로 프로젝트 명을 작성
            - version : 프로젝트의 버전을 작성
            - Maven은 Multiple Module을 지원합니다. 즉 하나의 프로젝트에 여러 프로젝트를 관리할 수 있습니다.

            ___
            - build lifecycle
                - 프로젝트를 빌드하고 배포하는 일련의 절차를 의미합니다.
                ![image](https://user-images.githubusercontent.com/73347933/129563694-cdc60439-4349-44c8-b5c5-fee4d11996d0.png)

            - Transitive Dependencies (Transitive 의존성)
                - 의존성의 의존성을 의미한다.
                - 버전간,라이브러리 간 충돌이 발생할 수 있습니다.

            - Dependency Scope(의존 범위)
                - compile : ```<scope></scope>```을 지정하지 않는 경우, 기본값으로 설정된다. 컴파일 의존성은 프로젝트의 컴파일,테스트,실행에 라이브러리가 필요할 때 사용합니다.
                - provided : JDK 또는 컨테이너가 해당 라이브러리를 제공할 때 설정합니다. 
                - runtime : 컴파일 시에는 사용되지 않으나, 실행과 테스트 시에는 필요할 때 설정합니다.
                - test : 어플리케이션의 실행에는 사용하지 않으나, 테스트 컴파일 및 실행 시에 필요할 때 설정합니다.(junit이 대표적인 예입니다.)
                - system : provided 의존성과 비슷하지만, 사용자가 jar 파일의 위치를 지정한다는 부분이 다르다.

        
        2. Gradle
            - Groovy 기반으로 빌드 스크립트를 작성할 수 있게 도와준다.
            - 최근에는 코틀린도 지원한다. 
            - 하나의 프로젝트는 하나 이상의 Task로 구성된다.
            - Task는 일반적으로 Plugin에 의해서 제공된다.

- ### Spring Boot CLI ###
    - ![W3D1 느슨한 의존성](https://user-images.githubusercontent.com/73347933/129566256-173a5a1b-fe43-42e2-a880-94301ad6e7b3.png)





  