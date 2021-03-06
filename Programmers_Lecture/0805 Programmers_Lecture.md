# ๊ฐ์ ์ ๋ฆฌ ๐
___

> 2021.08.05 Java Collection ์ด์ผ๊ธฐ

## ๊ณต๋ถํ ๋ด์ฉ

- ### Collection ###
    - ์ฌ๋ฌ ๋ฐ์ดํฐ์ ๋ฌถ์์ Collection์ด๋ผ๊ณ  ํ๋ค.
    - Collection์ ์ถ์์ฒด์ด๋ค. 
        - Collection์ ๊ตฌ์์ฒด๋ ๋ค์๊ณผ ๊ฐ๋ค.
            - List
                - LinkedList
                - ArrayList
                - Vector
                - Stack
            - Set
    
    <br>

    ```java
    public class Main {
        public static void main(String[] args) {
            MyIterator<String> iter =
                    new MyCollection<>(Arrays.asList("A", "CA", "DSB", "ASDC", "ASDFE"))
                            .iterator();

            while(iter.hasNext()) {
                String s = iter.next();
                int len = s.length();
                if(len % 2 == 0) continue;
                System.out.println(s);
            }
        }
    }

    ```
    
<br>

- ### Iterator ###
    - ๋ฐ์ดํฐ์ ๋ฌถ์์ ํ์ด์ ํ๋์ฉ ์ฒ๋ฆฌํ  ์ ์๋๋ก ํ๋ ์๋จ์ ์ ๊ณตํ๋ค.
    - next() ๋ฉ์๋๋ฅผ ํตํด ๋ค์ ๋ฐ์ดํฐ๋ฅผ ํธ์ถํ  ์ ์๋ค. 
    - ์ญ์์ผ๋ก ๋ฐ์ดํฐ๋ฅผ ์ ๊ทผํ  ์ ์๋ค.(previous ๊ฐ ์กฐํ X)
    - ๋ง์ฝ, ์ถ๊ฐ์ ์ธ ๋ฐ์ดํฐ๊ฐ ์์ ๋, next()๋ฉ์๋๋ฅผ ์ง์์ ์ผ๋ก ํธ์ถํ  ๊ฒฝ์ฐ Exception์ด ๋ฐ์ํ๋ค.
    <br>
    
    ```java
    public class Main {
        public static void main(String[] args) {
            MyIterator<String> iter =
                    new MyCollection<>(Arrays.asList("AB", "CAD", "DSBDD", "ASEADC", "ASAFSDFE"))
                            .iterator();

            while(iter.hasNext()) {
                String s = iter.next();
                int len = s.length();
                if(len % 2 == 0) continue;
                System.out.println(s);
            }
        }
    }

    ```
<br>

- ### Stream ###
    - Stream์ ๋์ด์ง์ง ์๋ ๋ฐ์ดํฐ์ ํ๋ฆ์ ์๋ฏธํ๋ค.
    - Java 8 ์ด์์์๋ถํฐ ์ฌ์ฉ๊ฐ๋ฅํ๋ค. (Collections.stream()์ ์ ๊ณตํด์ค๋ค.)
    - ์ฐ๋ฆฌ๊ฐ ํํ ์ฐ๊ณ  ์๋ System.in๊ณผ System.out๋ ์คํธ๋ฆผ์ด๋ค.(InputStream, OutputStream)
    - filter,map,forEach์ ๊ฐ์ ๊ณ ์ฐจํจ์(ํจ์๋ฅผ ์ธ์๋ก ๋ฐ๋ ํจ์)๊ฐ ์ ๊ณต์ด ๋๋ค.
    - Stream์ ์์ฑํ  ๋๋ generate์ iterate๋ฅผ ์ด์ฉํ์ฌ ๋ง๋ค ์ ์๋ค.
    - Stream์ ์ฌ์ฉํ๋ฉด ์ฐ์๋ ๋ฐ์ดํฐ์ ๋ํด ๊ณ ์ฐจํจ์๋ฅผ ์ฌ์ฉํ์ฌ ๋ณด๋ค ๊ฐ๋ ฅํ ๊ธฐ๋ฅ์ ์ฌ์ฉ ๋ฐ ํํ์ด ๊ฐ๋ฅํ๋ค.
    <br>

    ```java
    public class Main {
        public static void main(String[] args) {
            Arrays.asList("A","BD","CDE","EFEWF")
                    .stream()
                    .map(String::length)
                    .filter(i -> i% 2 == 1)
                    .forEach(System.out::println);
        }
    }
    ```

    ```java
    public class Main {
        public static void main(String[] args) {
            Stream<Integer> stream = Arrays.asList(1, 2, 3).stream();
        //        ์์ stream์ List์ ์๋ ๊ธฐ๋ฅ์ด๋ค.
        //        Primitive ํ์์ ์ ๋ค๋ฆญ์ ์ฌ์ฉ ํ  ์ ์๋ค.

                Arrays.stream(new int[]{1, 2, 3})
                        .map(i -> Integer.valueOf(i))
                        .boxed();
        //        ์ด์ฒ๋ผ, boxed() ๋ฉ์๋๋ฅผ ์ด์ฉํ๋ฉด Wrapper ํด๋์ค์ํํ๋ก ๋ง๋ค ์ ์๋ค.

                Arrays.stream(new int[]{1,2,3}).boxed();
                Arrays.stream(new int[]{1,2,3}).boxed().toArray();
                Arrays.stream(new int[]{1,2,3}).boxed().toArray(Integer[]::new);
                Arrays.stream(new int[]{1,2,3}).boxed().collect(Collectors.toList());
        //        -> toArray()๋ฅผ ํ๋ฉด Intstream์ ์ด์ฉํ๊ฑฐ๋ ํน์ Integer๋ฅผ ์ด์ฉํด์ ๋์ค๊ฑฐ๋ ๋์ค ํ๋, ๊ทธ๋ฌ๋ฏ๋ก ์ง์ ํด์ค ์ ์๋ค.
        //      ๋ฐฐ์ด์ ๊ฐ์ฒด๊ฐ ์๋๊ธฐ ๋๋ฌธ์ Stream์ด ์๋์ง๋ง, Arrays์ ๊ธฐ๋ฅ์ ๋ฐฐ์ด์ ์ด์ฉํ์ฌ stream์ ๋ง๋ค ์ ์๋ ๊ธฐ๋ฅ์ด ์๋ค.

        //        Stream.generate(() -> 1)
        //                .forEach(System.out::println);
        //        Stream์ ๋ฐ์ดํฐ์ ์ฐ์์ด๊ธฐ ๋๋ฌธ์ ๋ฐ์ดํฐ๊ฐ ์์ด์ง๋๊น์ง ๊ณ์ ์ถ๋ ฅํ๋ค. ๊ทธ๋ฌ๋ฏ๋ก 1์ด ๊ณ์ ์ฐํ๋ ๊ฒ์ด๋ค.

                Random r = new Random();
                Stream.generate(r::nextInt)
                        .limit(10)
                        .forEach(System.out::println);
        //      limit()์ ๋ฐ์ดํฐ์ ๊ฐ์๋ฅผ ์ ํํ๋ ์ญํ ์ ํ๋ค.

                Stream.iterate(0,(i) -> i + 1)
                        .limit(10)
                        .forEach(System.out::println);
        //        iterate๋ ์ด๊ธฐ๊ฐ๊ณผ ์ด๊ธฐ๊ฐ ์ดํ ์ด๋ป๊ฒ ๋ง๋ค ๊ฒ์ธ์ง ํ์ฉํ  ์ ์๋ค.
        }
    }

    ```
<br>

- ### Optional ###

    - NPE(Null Pointer Exception) : ๊ฐ์ฅ ๋ง์ด ๋ฐ์ํ๋ ์๋ฌ์ค ํ๋์ด๋ค. Java์์๋ ๋ ํผ๋ฐ์ค๊ฐ ๋ง๊ธฐ ๋๋ฌธ์ null ์๋ฌ์ ๋ํด ์ฃผ์ํด์ผํ๋ค.
    - ๊ทธ๋์ null์ ์ฐ์ง ์๋ ๋ฐฉ๋ฒ์ ๋ง๋ค์ด๋๋ค.
        1. EMPTY ๊ฐ์ฒด๋ฅผ ์ฌ์ฉํ๋ ๋ฐฉ๋ฒ
        2. Optional์ ์ฌ์ฉํ๋ ๋ฐฉ๋ฒ

    - EMPTY ๊ฐ์ฒด๋ฅผ ์ฌ์ฉํ๋ ๋ฐฉ๋ฒ
    <br>

        ![image](https://user-images.githubusercontent.com/73347933/128376817-1e0be74c-d2c7-4ee2-ad6d-ced6837aef63.png)

    - Optional์ ์ฌ์ฉํ๋ ๋ฐฉ๋ฒ
        - null ๋ฐ์ดํฐ : Optional.empty()
        - ํ์ธํ๋ ๋ฐฉ๋ฒ : .isEmpty(), .isPresent()
    <br>

    ```java
    public class Main {
        public static void main(String[] args) {
            Optional<User> optionalUser = Optional.empty();
    //        Optional ์ด ๋ฐ๊ตฌ๋๊ฐ ๋๋ ๊ฑฐ์. null์ด ๋๋ฉด null์ด ๋ด๊ธด Optional ๋ฐ๊ตฌ๋๋ฅผ ๋ฐํํ๋ ๊ฒ์ด๋ค.
            optionalUser = Optional.of(new User(28, "Java"));

            optionalUser.isEmpty();
    //        ๊ฐ์ด ์์ผ๋ฉด true
            optionalUser.isPresent();
    //        ๊ฐ์ด ์์ผ๋ฉด true

            if (optionalUser.isPresent()) {

            } else {

            }
    //        ๊ฐ์ด ์์ผ๋ฉด true๋ฐํ

            if (optionalUser.isEmpty()) {

            } else {

            }
    //        ๊ฐ์ด ์์ผ๋ฉด false๋ฐํ

            optionalUser.ifPresent(user -> {
    //           do 1
            });
            
            optionalUser.ifPresentOrElse(user -> {
    //            do 1
            }, () -> {
    //            do 2
            });
        }
    }

    ```