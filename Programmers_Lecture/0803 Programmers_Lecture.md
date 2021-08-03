# TIL(Today I Learned) 🚀
___

> 2021.08.03 Java OOP 이야기

## 공부한 내용

- ### 객체지향프로그래밍 : 프로그램을 객체로 구성하는 것 ###
    - 프로그램의 동작을 객체들에게 나눠서 수행
    - 개념적인 용어 : 객체 / 기술적인 용어 : class, instance
    - 객체를 서로 구분할 필요가 있다. -> Type(형)으로 구분한다.
    <br>

    ```java
    String str = "Hello World";
    (형)   (변수)   (인스턴스)
    ```
    

- ### 객체지향의 특성 ###
    1. **캡슐화**
        - 캡슐처럼 완성도가 있다. 
            - 기능을 수행하는 단위로써 객체는 완전함을 갖는다. 
        - 정보가 은닉되어 있다.
            - 객체의 정보를 밖에서 접근하지 못하게 한다.

        - 접근지정자 사용
            - private : 객체 소유
            - protected : 상속된 객체에서도 접근 가능
            - friendly : 같은 패키지 내에서 접근 가능
            - public : 모두 접근 가능

            ```java
            public class Car{
                private Wheel wheel;
                private Door door;
                protected Engine engine;
            }
            ```

    2. **상속**
        - 상위, 부모, super, 추상
        - 하위, 자식, this, 구체
        - 잘못된 이해 : 공통된 기능을 여러 객체에게 전달하고 싶을 때 사용한다.

    3. **추상화**
        - 객체간의 관계에서 상위에 있는 것이 항상 하위에 있는 것보다 추상적이어야 한다.

        ```java
        // 의미적 추상체
        class Login{
            void login(){}
        }

        class KakaoLogin extends Login{
            void login(){}
        }
        ```

        ```java
        //추상기능을 가진 객체
        abstract class Login{
            abstract void login();
        }

        class KakaoLogin extends Login{
            void kakao(){}

            @Override
            void login(){}
        }
        ```

        ```java
        // 객체 자체가 추상적
        interface Login{
            void login();
        }

        class KakaoLogin implements Login{
            void kakao(){}
            
            @Override
            void login(){}
        }
        ```

    4. **다형성**
        - 형(type)을 여러가지로 표현할 수 잇다.
        - 객체가 어떻게 구체화되냐에 따라 필터링 된 기능을 사용할 수 있다.

<br>

- ### UML
    - UML : 객체가 어떻게 구분되고 연관관계가 설정되어 있는지 설명하기 위한 도구
        - Usecase Diagram
        - Sequence Diagram
        - Package Diagram
        - <strong>Class Diagram</strong>

<br>

- ### 객체지향설계
    - 객체지향 설계를 하는 5가지 원칙(SOLID)
        - S : SRP -> 수정이 필요한 경우 수정되는 이유는 하나여야한다.
        - O : OCP -> 수정에는 닫히고, 확장에는 열려야 한다.
        - L : LSP -> 추상객체로 사용되는 부분에 구상객체가 들어가도 아무 문제 없어야 한다.
        - I : ISP -> 한 클래스는 자신이 사용하지 않는 인터페이스는 구현하지 않아야 한다.
        - D : DIP -> 추상화에 의존해야지, 구체화에 의존하면 안된다.
    
    - 공통점을 모아놓음 => 디자인 패턴(23가지 패턴)
    - (https://refactoring.guru/)[https://refactoring.guru/]


        


## 보다 자세히

- 디자인 패턴 23가지
