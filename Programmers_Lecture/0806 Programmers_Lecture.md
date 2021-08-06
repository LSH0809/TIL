# 강의 정리 🚀
___

> 2021.08.06 Java 실습프로젝트

## 공부한 내용

- ### Dependency ###
    - Gradle을 통해 Dependency를 가져올 수 있으며 Gradle은 사용환경을 만들어줄 수 있다. 
    - 원하는 라이브러리를 찾아서 가져오며 또 잘 사용하는 것도 중요한 능력이다.

<br>

    ```java
        plugins {
        id 'java'
    }

    group 'com.programmers.java.baseball'
    version '1.0.0'

    repositories {
        mavenCentral()
    }

    dependencies {
        testImplementation 'org.junit.jupiter:junit-jupiter-api:5.7.0'
        testRuntimeOnly 'org.junit.jupiter:junit-jupiter-engine:5.7.0'

        // Lombok
        compileOnly 'org.projectlombok:lombok:1.18.20'
        annotationProcessor 'org.projectlombok:lombok:1.18.20'

        testCompileOnly 'org.projectlombok:lombok:1.18.20'
        testAnnotationProcessor 'org.projectlombok:lombok:1.18.20'
    }

    test {
        useJUnitPlatform()
    }
    ```

    - Lombok을 활용하면 생성자, getter(),setter() 메소드 혹은 toString() 등 코드의 작성을 대신할 수 있다.
<br>

    ```java
    @어노테이션명
    public class User {
        private int age;
        private String name;
    }
    ```

    - @NoArgsConstructor : 기본 생성자를 대신 생성해주는 어노테이션
    - @AllArgsConstructor :  모든 인자가 들어가있을 경우의 생성자를 만들어준다.
    - @ToString : 클래스의 변수들을 활용하여 toString() 메소드를 재정의한다. 
        - 만약, 출력을 원하지 않는 변수가 있다면, @ToString.Exclude()를 사용하면 된다.
    - @EqualsAndHashCode : equals() 메소드와 hashCode() 메소드를 재정의 한다.
    - @Getter, @Setter : getter(), setter() 메소드를 생성한다.
    - @Data : @Getter, @Setter, @RequiredArgsConstructor, @ToString, @EqualsAndHashCode 이 모든 어노테이션을 대신하는 역할을 한다.


- ### 프로젝트 설계 ###
    - 숫자 야구 게임 설계의 과정
        1. 요구사항 파악하기
            - 게임의 룰을 이해
            - 동작환경, 데이터의 범위를 설정

        2. OOP에서의 설계
            - 일을 객체로 나누기
            - 나눈 객체를 연관짓기

        3. 핵심로직 설계하기
            - Flow Chart 그린다고 생각하며 설계하기

### 프로젝트구현 엔진레이어 ###
- 핵심 비즈니스 로직은 외부 Dependency가 없도록 해야한다.
- 핵심 비즈니스 로직이기 때문에 외부에 의해 수정되거나 흔들릴 여지가 있으면 안되기 때문이다.
- 완성된 프로젝트를 기반으로 다시 그려봤다.
- 이러한 설계를 하는 것, 코드를 생각하는 것, 모두 쉽지 않은 부분이다. 강의에서 나온 것처럼 꾸준한 복습이 필요하다.

<br>

![0806 프로젝트 구성도](https://user-images.githubusercontent.com/73347933/128494677-e76d60c6-b941-45f1-9608-c6aa7f1dae60.png)
