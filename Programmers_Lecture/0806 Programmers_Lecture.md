# κ°μ μ λ¦¬ π
___

> 2021.08.06 Java μ€μ΅νλ‘μ νΈ

## κ³΅λΆν λ΄μ©

- ### Dependency ###
    - Gradleμ ν΅ν΄ Dependencyλ₯Ό κ°μ Έμ¬ μ μμΌλ©° Gradleμ μ¬μ©νκ²½μ λ§λ€μ΄μ€ μ μλ€. 
    - μνλ λΌμ΄λΈλ¬λ¦¬λ₯Ό μ°Ύμμ κ°μ Έμ€λ©° λ μ μ¬μ©νλ κ²λ μ€μν λ₯λ ₯μ΄λ€.


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

    <br>


    - Lombokμ νμ©νλ©΄ μμ±μ, getter(),setter() λ©μλ νΉμ toString() λ± μ½λμ μμ±μ λμ ν  μ μλ€.

    ```java
    @μ΄λΈνμ΄μλͺ
    public class User {
        private int age;
        private String name;
    }
    ```

    - @NoArgsConstructor : κΈ°λ³Έ μμ±μλ₯Ό λμ  μμ±ν΄μ£Όλ μ΄λΈνμ΄μ
    - @AllArgsConstructor :  λͺ¨λ  μΈμκ° λ€μ΄κ°μμ κ²½μ°μ μμ±μλ₯Ό λ§λ€μ΄μ€λ€.
    - @ToString : ν΄λμ€μ λ³μλ€μ νμ©νμ¬ toString() λ©μλλ₯Ό μ¬μ μνλ€. 
        - λ§μ½, μΆλ ₯μ μνμ§ μλ λ³μκ° μλ€λ©΄, @ToString.Exclude()λ₯Ό μ¬μ©νλ©΄ λλ€.
    - @EqualsAndHashCode : equals() λ©μλμ hashCode() λ©μλλ₯Ό μ¬μ μ νλ€.
    - @Getter, @Setter : getter(), setter() λ©μλλ₯Ό μμ±νλ€.
    - @Data : @Getter, @Setter, @RequiredArgsConstructor, @ToString, @EqualsAndHashCode μ΄ λͺ¨λ  μ΄λΈνμ΄μμ λμ νλ μ­ν μ νλ€.

<br>

- ### νλ‘μ νΈ μ€κ³ ###
    - μ«μ μΌκ΅¬ κ²μ μ€κ³μ κ³Όμ 
        1. μκ΅¬μ¬ν­ νμνκΈ°
            - κ²μμ λ£°μ μ΄ν΄
            - λμνκ²½, λ°μ΄ν°μ λ²μλ₯Ό μ€μ 

        2. OOPμμμ μ€κ³
            - μΌμ κ°μ²΄λ‘ λλκΈ°
            - λλ κ°μ²΄λ₯Ό μ°κ΄μ§κΈ°

        3. ν΅μ¬λ‘μ§ μ€κ³νκΈ°
            - Flow Chart κ·Έλ¦°λ€κ³  μκ°νλ©° μ€κ³νκΈ°

### νλ‘μ νΈκ΅¬ν μμ§λ μ΄μ΄ ###
- ν΅μ¬ λΉμ¦λμ€ λ‘μ§μ μΈλΆ Dependencyκ° μλλ‘ ν΄μΌνλ€.
- ν΅μ¬ λΉμ¦λμ€ λ‘μ§μ΄κΈ° λλ¬Έμ μΈλΆμ μν΄ μμ λκ±°λ νλ€λ¦΄ μ¬μ§κ° μμΌλ©΄ μλκΈ° λλ¬Έμ΄λ€.
- μμ±λ νλ‘μ νΈλ₯Ό κΈ°λ°μΌλ‘ λ€μ κ·Έλ €λ΄€λ€.
- μ΄λ¬ν μ€κ³λ₯Ό νλ κ², μ½λλ₯Ό μκ°νλ κ², λͺ¨λ μ½μ§ μμ λΆλΆμ΄λ€. κ°μμμ λμ¨ κ²μ²λΌ κΎΈμ€ν λ³΅μ΅μ΄ νμνλ€.


![0806 νλ‘μ νΈ κ΅¬μ±λ](https://user-images.githubusercontent.com/73347933/128494677-e76d60c6-b941-45f1-9608-c6aa7f1dae60.png)
