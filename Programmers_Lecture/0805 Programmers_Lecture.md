# TIL(Today I Learned) 🚀
___

> 2021.08.05 Java Collection 이야기

## 공부한 내용

- ### Collection ###
    - 여러 데이터의 묶음을 Collection이라고 한다.
    - Collection은 추상체이다. 
        - Collection의 구상체는 다음과 같다.
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
    

- ### Iterator ###
    - 데이터의 묶음을 풀어서 하나씩 처리할 수 있도록 하는 수단을 제공한다.
    - next() 메소드를 통해 다음 데이터를 호출할 수 있다. 
    - 역순으로 데이터를 접근할 수 없다.(previous 값 조회 X)
    - 만약, 추가적인 데이터가 없을 때, next()메소드를 지속적으로 호출할 경우 Exception이 발생한다.
    
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

- ### Stream ###
    - Stream은 끊어지지 않는 데이터의 흐름을 의미한다.
    - Java 8 이상에서부터 사용가능하다. (Collections.stream()을 제공해준다.)
    - 우리가 흔히 쓰고 있는 System.in과 System.out도 스트림이다.(InputStream, OutputStream)
    - filter,map,forEach와 같은 고차함수(함수를 인자로 받는 함수)가 제공이 된다.
    - Stream을 생성할 때는 generate와 iterate를 이용하여 만들 수 있다.
    - Stream을 사용하면 연속된 데이터에 대해 고차함수를 사용하여 보다 강력한 기능을 사용 및 표현이 가능하다.

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
        //        위의 stream은 List에 있는 기능이다.
        //        Primitive 타입은 제네릭에 사용 할 수 없다.

                Arrays.stream(new int[]{1, 2, 3})
                        .map(i -> Integer.valueOf(i))
                        .boxed();
        //        이처럼, boxed() 메소드를 이용하면 Wrapper 클래스의형태로 만들 수 있다.

                Arrays.stream(new int[]{1,2,3}).boxed();
                Arrays.stream(new int[]{1,2,3}).boxed().toArray();
                Arrays.stream(new int[]{1,2,3}).boxed().toArray(Integer[]::new);
                Arrays.stream(new int[]{1,2,3}).boxed().collect(Collectors.toList());
        //        -> toArray()를 하면 Intstream을 이용하거나 혹은 Integer를 이용해서 나오거나 둘중 하나, 그러므로 지정해줄 수 있다.
        //      배열은 객체가 아니기 때문에 Stream이 안되지만, Arrays의 기능에 배열을 이용하여 stream을 만들 수 있는 기능이 있다.

        //        Stream.generate(() -> 1)
        //                .forEach(System.out::println);
        //        Stream은 데이터의 연속이기 때문에 데이터가 없어질때까지 계속 출력한다. 그러므로 1이 계속 찍히는 것이다.

                Random r = new Random();
                Stream.generate(r::nextInt)
                        .limit(10)
                        .forEach(System.out::println);
        //      limit()은 데이터의 개수를 제한하는 역할을 한다.

                Stream.iterate(0,(i) -> i + 1)
                        .limit(10)
                        .forEach(System.out::println);
        //        iterate는 초기값과 초기값 이후 어떻게 만들 것인지 활용할 수 있다.
        }
    }

    ```

- ### Optional ###

    - NPE(Null Pointer Exception) : 가장 많이 발생하는 에러중 하나이다. Java에서는 레퍼런스가 많기 때문에 null 에러에 대해 주의해야한다.
    - 그래서 null을 쓰지 않는 방법을 만들어냈다.
        1. EMPTY 객체를 사용하는 방법
        2. Optional을 사용하는 방법

    - EMPTY 객체를 사용하는 방법
        ![image](https://user-images.githubusercontent.com/73347933/128376817-1e0be74c-d2c7-4ee2-ad6d-ced6837aef63.png)

    - Optional을 사용하는 방법
        - null 데이터 : Optional.empty()
        - 확인하는 방법 : .isEmpty(), .isPresent()
    
    ```java
    public class Main {
        public static void main(String[] args) {
            Optional<User> optionalUser = Optional.empty();
    //        Optional 이 바구니가 되는 거임. null이 되면 null이 담긴 Optional 바구니를 반환하는 것이다.
            optionalUser = Optional.of(new User(28, "Java"));

            optionalUser.isEmpty();
    //        값이 없으면 true
            optionalUser.isPresent();
    //        값이 있으면 true

            if (optionalUser.isPresent()) {

            } else {

            }
    //        값이 있으면 true반환

            if (optionalUser.isEmpty()) {

            } else {

            }
    //        값이 있으면 false반환

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