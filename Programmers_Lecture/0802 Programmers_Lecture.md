# ๊ฐ์ ์ ๋ฆฌ ๐
___

> 2021.08.02 Java ์ด์ผ๊ธฐ

## ๊ณต๋ถํ ๋ด์ฉ

- Java ๊ฐ๋ฐํ๊ฒฝ
    - JRE : javac๋ ์์ผ๋ฉฐ java๋ง ํฌํจ๋์ด ์๋ค.
    - JDK : JRE + ๊ฐ๋ฐํด = ๊ฐ๋ฐํ๊ฒฝ

- Gradle ์ง์  ์ค์น
    - Build Tool : Ant, Maven, Gradle
    - gradle ๋ช๋ น์ด
        - gradle init : ํ๋ก์ ํธ๋ฅผ ์์ฑ
        - gradle tasks : ํ์คํฌ ๋ชฉ๋ก ํ์ธ
        - gradle build : ๋น๋
        - gradle run : ์คํ

- ํตํฉ๊ฐ๋ฐํ๊ฒฝ

- Coding Convention(ํ์ด๋ ํ์ฌ์์ ์ ํ์ง ์๋ ์ผ๋ฐ์ ์ธ ๊ฒฝ์ฐ)
    - ํด๋์ค ๋ช์ ๋๋ฌธ์๋ก ์์ํ๋ค. 
    - ๋ฉ์๋๋ ๋ณ์๋ช์ ์๋ฌธ์๋ก ์์ํ๋ค.
    ```java
    public class Application{
        public static void main(String[] args){
            int myVariable = 0;
            //int MyVarialbe (x)
        }
    }
    ```
    - Indent : ๋ค์ฌ์ฐ๊ธฐ
        - Tab,Space ๋๋ค ์ฌ์ฉ๊ฐ๋ฅํ์ง๋ง ์์ด์ ์ฐ๋ฉด ์๋๋ค.
- Reference
    - Java์๋ ํฌ์ธํฐ ๋์  Reference๋ผ๋ ๊ฐ๋์ด ์กด์ฌํ๋ค.
    - Java๋ Primitive ๊ฐ์ ์ ์ธํ๊ณ  ๋ชจ๋ Reference ๊ฐ์ด๋ค.
        - primitive : boolean, byte,int,short,float,double,long,character
        - ๋จ, ๋ฐฐ์ด์ ๊ฒฝ์ฐ reference๋ก ์ทจ๊ธํ๋ค.

- Constant Pool
    - '=='์ ๊ฒฝ์ฐ reference๊ฐ ๊ฐ์์ง ๋น๊ตํ๋ ๊ฒ์ด๋ค. 
    ```java
    public class Application{
        public static void main(String[] args){
            String a = "Hello World";
            String b = "Hello World";
            System.out.println(a == b);
            //true ๋ฐํ
        }
    }
    ```
    - String, StringBuffer, StringBuilder์ ์ฌ์ฉ
    
- Object
    - ๋ชจ๋  ๊ฐ์ฒด์ ์ต์์ ๊ฐ์ฒด์ด๋ค.
    - ๋ํ์ ์ธ ๋ฉ์๋
        - toString() / equals() / hashCode()

- Git
    - Git์ ์ต์ํด์ ธ์ผ ํ๋ค.
    - ์ด๋ป๊ฒ ์ฌ์ฉํ๋์ง, ์ด๋ ํ ์๋ฆฌ๋ก ํ์ฉ๋๋์ง๋ฅผ ์ดํดํด์ผ ํ๋ค.
    - .gitignore๋ฅผ ์ ํ์ฉํ๊ธฐ
        - ํฌํจ๋์ง ์์์ผ ํ  ํ์ผ๋ค์ด ์์ผ๋ฉด ์๋๋ค. ex) ๋น๋๊ฒฐ๊ณผ, ๋ฐ์ด๋๋ฆฌ...
    - gitignore.io ์ฌ์ดํธ ํ์ฉํด๋ณด๊ธฐ : <https://www.toptal.com/developers/gitignore>


## ๋ณด๋ค ์์ธํ

- [String, StringBuffer, StringBuilder์ ์ฐจ์ด - ๊นํ](https://github.com/LSH0809/TIL/blob/master/Java/String,StringBuffer,StringBuilder/String_StringBuffer_StringBuilder.md)
- [String, StringBuffer, StringBuilder์ ์ฐจ์ด - ํฐ์คํ ๋ฆฌ](https://today-retrospect.tistory.com/91)
- [Object ๊ฐ์ฒด ํ๊ตฌํ๊ธฐ(toString(), equals(), hashCode())](https://today-retrospect.tistory.com/92)
