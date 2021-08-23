# 강의 정리 🚀
___

> 2021.08.23 SpringBoot Part1

## 공부한 내용

- ### 모든 것은 공식문서와 함께!!! ###

- ### 소프트웨어 테스팅 ###
    - 테스팅 피라미드
        - 단계별 테스팅 시스템
        ![image](https://user-images.githubusercontent.com/73347933/130394926-84628327-44fc-4d7c-9fcd-7658530e870e.png)
    - 단위 테스트
        - 일반적으로 가장 많이 작성하는 테스트
        - 특정 부분을 고립해서 하는 테스트(빠르게)
        - SUT : 테스트 하는 하나의 단위 (이 안에 여러개의 메소드들이 있을 것이다.)
        - GIVEN / WHEN / THEN의 흐름
        - 테스트 더블
            - 테스트 더블은 의존 구성요소를 사용할 수 없을 때 테스트 대상 코드와 상호작용하는 객체이다.
        - 목적
            - 지속적으로 변경했을 때 테스트 코드를 통해 기존의 기능을 보장한다.
            - 테스트 케이스만 봐도 어떠한 기능이 있는지 확인할 수 있다.(기능 명세의 역할)
    - 통합 테스트
        - 각각의 단위 테스트가 끝내면 이제 외부 혹은 내부의 연결을 확인한다.

- ### JUnit ###
    - 매 단위 테스트시마다 테스트 클래스의 인스턴스가 생성되어 독립적인 테스트가 가능하게 해준다.
    - 어노테이션을 제공해서 테스트 라이프 사이클을 관리하게 해주고 테스트 코드를 간결하게 작성하도록 지원한다.
    - 테스트 러너를 제공해서 인텔리제이 / 이클립스 등에서 테스트 코드를 쉽게 실행하게 한다.
    - assert로 테스트 케이스의 수행 결과를 판별한다.
    - 결과는 성공(녹색) / 실패(빨간색)중 하나로 표시된다.

    - JUnit4 -> JUnit5 
    - 반환형은 무조건 void여야 한다.
    - @DisplayName을 이용해서 설명을 추가할 수 있다.

    - @BeforeAll은 객체가 생성되었을 때 초기에 한번 실행
    - @BeforeEach는 매 테스트 메소드마다 실행된다.
    - assertAll()을 사용하면 여러개의 조건을 확인할 수 있다.
    - assertThorws()을 사용하면 예외를 확인할 수 있다.

    - Hamcrest Assertion Test
        - assertThat()
            - equalTo()
            - is()
            - anyOf()
        - assertNotEquals()
        - assertThat()
        ```java
        import static org.hamcrest.Matchers.*;
        import static org.hamcrest.MatcherAssert.*;

        import static org.junit.jupiter.api.Assertions.*;

        public class HamcrestAssertionTests {

            @Test
            @DisplayName("여러 hamcrest mathcer 테스트")
            void hamcrestTest() {
                assertEquals(2, 1 + 1);
                assertThat(1 + 1, equalTo(2));
                assertThat(1 + 1, is(2));
                assertThat(1 + 1, anyOf(is(1), is(2)));

                assertNotEquals(1, 1 + 1);
                assertThat(1 + 1, not(equalTo(1)));
            }

            @Test
            @DisplayName("컬렉션에 대한 matcher 테스트")
            void hamcrestListMathcerTest() {
                var prices = List.of(2, 3, 4);
                assertThat(prices, hasSize(3));
                assertThat(prices, everyItem(greaterThan(1)));
                assertThat(prices, containsInAnyOrder(3, 4, 2));
        //        assertThat(prices,contains(2,4,3)); 이것은 순서를 지켜서 테스트함
                assertThat(prices, hasItem(greaterThanOrEqualTo(2)));
            }
        }

        ```
- ### Mock Object ###
    - Mock 오브젝트는 행위 검증을 사용하고 stucb을 포함한 다른 대역들은 상태 검증을 사용한다.
        - Mock은 좀 더 행위에 집중
        - 상태 검증 : 메소드가 수행된 후, 객체의 상태를 확인하며 올바르게 동작했는지를 확인하는 검증법이다.
        - 행위 검증 : 메소드의 리턴 값으로 판단할 수 없는 경우 특정 동작을 수행하는지 확인하는 검증법이다.

    ```java
    class OrderServiceTest {

    class OrderRepositoryStub implements OrderRepository {

            @Override
            public Order insert(Order order) {
                return null;
            }
        }

        @Test
        @DisplayName("오더가 생성되야 한다. (stub)")
        void createOrder() {
            // given
            var voucherRepository = new MemoryVoucherRepository();
            var fixedAmountVoucher = new FixedAmountVoucher(UUID.randomUUID(), 100);
            voucherRepository.insert(fixedAmountVoucher);
            var sut = new OrderService(new VoucherService(voucherRepository), new OrderRepositoryStub());

            // when
            var order = sut.createOrder(UUID.randomUUID(), List.of(new OrderItem(UUID.randomUUID(), 200, 1)), fixedAmountVoucher.getVoucherId());

            // then
            assertThat(order.totalAmount(), is(100L));
            assertThat(order.getVoucher().isEmpty(), is(Boolean.FALSE));
            assertThat(order.getVoucher().get().getVoucherId(), is(fixedAmountVoucher.getVoucherId()));
            assertThat(order.getOrderStatus(), is(OrderStatus.ACCEPTED));
        }

        @Test
        @DisplayName("오더가 생성되야 한다. (Mock)")
        void createOrderByMock() {
            // given
            var voucherServiceMock = mock(VoucherService.class);
            var orderRepositoryMock = mock(OrderRepository.class);
            var fixedAmountVoucher = new FixedAmountVoucher(UUID.randomUUID(), 100);
            when(voucherServiceMock.getVoucher(fixedAmountVoucher.getVoucherId())).thenReturn(fixedAmountVoucher);
            var sut = new OrderService(voucherServiceMock, orderRepositoryMock);

            // when
            var order = sut.createOrder(UUID.randomUUID(), List.of(new OrderItem(UUID.randomUUID(), 200, 1)), fixedAmountVoucher.getVoucherId());

            // then
            assertThat(order.totalAmount(), is(100L));
            assertThat(order.getVoucher().isEmpty(), is(Boolean.FALSE));
            var inOrder = inOrder(voucherServiceMock, orderRepositoryMock);
            inOrder.verify(voucherServiceMock).getVoucher(fixedAmountVoucher.getVoucherId());
            inOrder.verify(orderRepositoryMock).insert(order);
            inOrder.verify(voucherServiceMock).userVoucher(fixedAmountVoucher);
        }
    }
    ```
    - Mock을 통해서 해당하는 Mock객체의 메소드만의 동작을 확인할 수 있다.(해당하는 목 객체가 제대로 이 메소드를 call하는지, 사용하는지, 어떠한 매개변수를 사용하는지 등등) 
    - inOrder를 사용해서 메소드의 순서도 확인할 수 있다.

- ### Spring Test ###
    - Spring에서 제공하는 어노테이션을 활용해서 통합 테스트를 실습한 결과이다.
```java
//@ExtendWith(SpringExtension.class)
//@ContextConfiguration(classes = {AppConfiguration.class})
//위 두가지 어노테이션을 아래 하나의 어노테이션으로 제공함
//@ActiveProfiles("test") 이렇게 하면 test profile 사용됨
@SpringJUnitConfig(classes = {AppConfiguration.class})
public class KdtSpringContextTests {

    @Autowired
    ApplicationContext context;

    @Autowired
    OrderService orderService;

    @Autowired
    VoucherRepository voucherRepository;

    @Test
    @DisplayName("applicationContext가 생성되야 한다.")
    public void testApplicationContext(){
        assertThat(context,notNullValue());
    }

    @Test
    @DisplayName("VoucherRepository가 빈으로 등록되야 한다.")
    public void testVoucherRepositoryCreation(){
        var bean = context.getBean(VoucherRepository.class);
        assertThat(bean,notNullValue());
    }

    @Test
    @DisplayName("OrderService를 사용해서 주문을 생성할 수 있다.")
    public void testOrderService(){
        // given
        var fixedAmountVoucher = new FixedAmountVoucher(UUID.randomUUID(),100);
        voucherRepository.insert(fixedAmountVoucher);

        // when
        var order = orderService.createOrder(UUID.randomUUID(), List.of(new OrderItem(UUID.randomUUID(),200,1)),fixedAmountVoucher.getVoucherId());

        // then
        assertThat(order.totalAmount(),is(100L));
        assertThat(order.getVoucher().isEmpty(),is(false));
        assertThat(order.getVoucher().get().getVoucherId(),is(fixedAmountVoucher.getVoucherId()));
        assertThat(order.getOrderStatus(),is(OrderStatus.ACCEPTED));
    }
}

```