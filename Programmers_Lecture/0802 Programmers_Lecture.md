# 강의 정리 🚀
___

> 2021.08.02 Java 이야기

## 공부한 내용

- Java 개발환경
    - JRE : javac는 없으며 java만 포함되어 있다.
    - JDK : JRE + 개발툴 = 개발환경

- Gradle 직접 설치
    - Build Tool : Ant, Maven, Gradle
    - gradle 명령어
        - gradle init : 프로젝트를 생성
        - gradle tasks : 테스크 목록 확인
        - gradle build : 빌드
        - gradle run : 실행

- 통합개발환경

- Coding Convention(팀이나 회사에서 정하지 않는 일반적인 경우)
    - 클래스 명은 대문자로 시작한다. 
    - 메소드나 변수명은 소문자로 시작한다.
    ```java
    public class Application{
        public static void main(String[] args){
            int myVariable = 0;
            //int MyVarialbe (x)
        }
    }
    ```
    - Indent : 들여쓰기
        - Tab,Space 둘다 사용가능하지만 섞어서 쓰면 안된다.
- Reference
    - Java에는 포인터 대신 Reference라는 개념이 존재한다.
    - Java는 Primitive 값을 제외하고 모두 Reference 값이다.
        - primitive : boolean, byte,int,short,float,double,long,character
        - 단, 배열의 경우 reference로 취급한다.

- Constant Pool
    - '=='의 경우 reference가 같은지 비교하는 것이다. 
    ```java
    public class Application{
        public static void main(String[] args){
            String a = "Hello World";
            String b = "Hello World";
            System.out.println(a == b);
            //true 반환
        }
    }
    ```
    - String, StringBuffer, StringBuilder의 사용
    
- Object
    - 모든 객체의 최상위 객체이다.
    - 대표적인 메소드
        - toString() / equals() / hashCode()

- Git
    - Git에 익숙해져야 한다.
    - 어떻게 사용하는지, 어떠한 원리로 활용되는지를 이해해야 한다.
    - .gitignore를 잘 활용하기
        - 포함되지 않아야 할 파일들이 있으면 안된다. ex) 빌드결과, 바이너리...
    - gitignore.io 사이트 활용해보기 : <https://www.toptal.com/developers/gitignore>


## 보다 자세히

- [String, StringBuffer, StringBuilder의 차이 - 깃헙](https://github.com/LSH0809/TIL/blob/master/Java/String,StringBuffer,StringBuilder/String_StringBuffer_StringBuilder.md)
- [String, StringBuffer, StringBuilder의 차이 - 티스토리](https://today-retrospect.tistory.com/91)
- [Object 객체 탐구하기(toString(), equals(), hashCode())](https://today-retrospect.tistory.com/92)
