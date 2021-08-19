# 강의 정리 🚀
___

> 2021.08.19 SpringBoot Part1

## 공부한 내용

- ### Environment & Properties ###
    - ApplicationContext는 Environment를 상속받는다.
    - ApplicationContext는 Bean들을 관리한다.

    - AppConfig에 @PropertySource를 사용해서 properties 파일 이름을 지정해야한다.
    
    - application.properties는 key-value의 형태로 작성한다.
        - .을 이용해서 중첩해서 사용할 수 있다.
    - applicationContext에서 getProperty를 이용해서 해당하는 것을 가져올 수 있다.
    - 생성자를 만들지 않아도 @Value()을 이용해서 값을 할당할 수 있다.
    - @Value를 사용했는데 만약 properties에 없는 값이면 : 을 이용해서 default값을 지정할 수 있다. 만약 있으면 해당하는 값을, 없으면 default값을 반환한다.
    - 키를 가져올 때 우선순위
        1. JVM System properties
        2. JVM System envrionment
        3. properties 값
    
    ```java
    @PropertySource(value = "application.yaml",factory = YamlPropertiesFactory.class)
    @EnableConfigurationProperties
    public class AppConfiguration {
    }
    ```

    ```java
    public class YamlPropertiesFactory implements PropertySourceFactory {
    @Override
    public PropertySource<?> createPropertySource(String s, EncodedResource encodedResource) throws IOException {
        var yamlPropertiesFactoryBean = new YamlPropertiesFactoryBean();
        yamlPropertiesFactoryBean.setResources(encodedResource.getResource());

        var properties = yamlPropertiesFactoryBean.getObject();
        return new PropertiesPropertySource(encodedResource.getResource().getFilename(),properties);
        }
    }
    ```
- ### YAML로 프로퍼티 작성 ###
    - YAML이라는 이름은 마크업 언어가 아니다. 원래는 또 다른 마크업 언어(Yet Another Markup Language)였으나 YAML의 핵심은 데이터 중심에 있다는 것을 보여주기 위해 이름을 바꾸었다. 오늘날, XML과 JSON이 데이터 직렬화에 주로 쓰이기 시작하면서 많은 사람들이 YAML을 '가벼운 마크업 언어'로 사용하려 하고 있다.
    - : 을 사용하며 들여쓰기에 주의해야한다.(nested 표현)
    - @PropertySource는 yaml을 지원하지 않는다.(스프링 부트는 지원 O / 스프링 프레임워크는 지원 X)
        - 그러므로 PropertySourceFactory를 이용해서 작성해야한다.

- ### Resource ###
    - Spring Application을 만들다 보면 외부 리소스를 읽을 필요가 있다. 외부 리소스라면 이미지파일, 텍스트 파일, 암복호화를 위한 키파일 등이 있다.
    - Resurce와 ResourceLoader 인터페이스를 제공함으로써 하나의 API로 제공한다.
    - 스프링에서는 다양한 구현체를 제공한다.(공식문서 참조)
    - getResource를 한 후, 파일이름을 적으면 워킹 디렉토리에서 부터 찾는다.
    - URL 리소스는 getFiles가 아닌 getURL로 가져와야한다.
    - 요점은, 원하는 리소스를 프로젝트로 가져와서 사용할 수 있으며 그러한 방법을 익히는 것이다.

    ```java
    public class OrderTester {
    public static void main(String[] args) throws IOException {
        var applicationContext = new AnnotationConfigApplicationContext(AppConfiguration.class);

        var environment = applicationContext.getEnvironment();    
        var orderProperties = applicationContext.getBean(OrderProperties.class);
    //        System.out.println(MessageFormat.format("version {0}", orderProperties.getVersion()));
    //        System.out.println(MessageFormat.format("minimumOrderAmount {0}", orderProperties.getMinimumOrderAmount()));
    //        System.out.println(MessageFormat.format("supportVendors {0}", orderProperties.getSupportVendors()));
    //        System.out.println(MessageFormat.format("description {0}", orderProperties.getDescription()));


    //        var resource = applicationContext.getResource("application.yaml");
            var resource = applicationContext.getResource("classpath:application.yaml");
            var resource2 = applicationContext.getResource("file:sample.txt");
            var resource3 = applicationContext.getResource("https://stackoverflow.com/");
            var readableByteChannel = Channels.newChannel(resource3.getURL().openStream());
            var bufferedReader = new BufferedReader(Channels.newReader(readableByteChannel, StandardCharsets.UTF_8));
            var lines = bufferedReader.lines();
            var collect = lines.collect(Collectors.joining("\n"));
            System.out.println(collect);

            System.out.println(MessageFormat.format("Resource {0}", resource.getClass().getCanonicalName()));
            var strings = Files.readAllLines(resource.getFile().toPath());
            var strings2 = Files.readAllLines(resource2.getFile().toPath());

            System.out.println(strings.stream().reduce("",(a,b) -> a + "\n" + b));
            System.out.println(strings2.stream().reduce("",(a,b) -> a + "\n" + b));

            applicationContext.close();
        }
    }

    ```