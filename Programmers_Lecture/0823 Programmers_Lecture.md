# κ°μ μ λ¦¬ π
___

> 2021.08.23 SpringBoot Part1

## κ³΅λΆν λ΄μ©

- ### λͺ¨λ  κ²μ κ³΅μλ¬Έμμ ν¨κ»!!! ###

- ### μννΈμ¨μ΄ νμ€ν ###
    - νμ€ν νΌλΌλ―Έλ
        - λ¨κ³λ³ νμ€ν μμ€ν
        ![image](https://user-images.githubusercontent.com/73347933/130394926-84628327-44fc-4d7c-9fcd-7658530e870e.png)
    - λ¨μ νμ€νΈ
        - μΌλ°μ μΌλ‘ κ°μ₯ λ§μ΄ μμ±νλ νμ€νΈ
        - νΉμ  λΆλΆμ κ³ λ¦½ν΄μ νλ νμ€νΈ(λΉ λ₯΄κ²)
        - SUT : νμ€νΈ νλ νλμ λ¨μ (μ΄ μμ μ¬λ¬κ°μ λ©μλλ€μ΄ μμ κ²μ΄λ€.)
        - GIVEN / WHEN / THENμ νλ¦
        - νμ€νΈ λλΈ
            - νμ€νΈ λλΈμ μμ‘΄ κ΅¬μ±μμλ₯Ό μ¬μ©ν  μ μμ λ νμ€νΈ λμ μ½λμ μνΈμμ©νλ κ°μ²΄μ΄λ€.
        - λͺ©μ 
            - μ§μμ μΌλ‘ λ³κ²½νμ λ νμ€νΈ μ½λλ₯Ό ν΅ν΄ κΈ°μ‘΄μ κΈ°λ₯μ λ³΄μ₯νλ€.
            - νμ€νΈ μΌμ΄μ€λ§ λ΄λ μ΄λ ν κΈ°λ₯μ΄ μλμ§ νμΈν  μ μλ€.(κΈ°λ₯ λͺμΈμ μ­ν )
    - ν΅ν© νμ€νΈ
        - κ°κ°μ λ¨μ νμ€νΈκ° λλ΄λ©΄ μ΄μ  μΈλΆ νΉμ λ΄λΆμ μ°κ²°μ νμΈνλ€.

- ### JUnit ###
    - λ§€ λ¨μ νμ€νΈμλ§λ€ νμ€νΈ ν΄λμ€μ μΈμ€ν΄μ€κ° μμ±λμ΄ λλ¦½μ μΈ νμ€νΈκ° κ°λ₯νκ² ν΄μ€λ€.
    - μ΄λΈνμ΄μμ μ κ³΅ν΄μ νμ€νΈ λΌμ΄ν μ¬μ΄ν΄μ κ΄λ¦¬νκ² ν΄μ£Όκ³  νμ€νΈ μ½λλ₯Ό κ°κ²°νκ² μμ±νλλ‘ μ§μνλ€.
    - νμ€νΈ λ¬λλ₯Ό μ κ³΅ν΄μ μΈνλ¦¬μ μ΄ / μ΄ν΄λ¦½μ€ λ±μμ νμ€νΈ μ½λλ₯Ό μ½κ² μ€ννκ² νλ€.
    - assertλ‘ νμ€νΈ μΌμ΄μ€μ μν κ²°κ³Όλ₯Ό νλ³νλ€.
    - κ²°κ³Όλ μ±κ³΅(λΉμ) / μ€ν¨(λΉ¨κ°μ)μ€ νλλ‘ νμλλ€.

    - JUnit4 -> JUnit5 
    - λ°ννμ λ¬΄μ‘°κ±΄ voidμ¬μΌ νλ€.
    - @DisplayNameμ μ΄μ©ν΄μ μ€λͺμ μΆκ°ν  μ μλ€.

    - @BeforeAllμ κ°μ²΄κ° μμ±λμμ λ μ΄κΈ°μ νλ² μ€ν
    - @BeforeEachλ λ§€ νμ€νΈ λ©μλλ§λ€ μ€νλλ€.
    - assertAll()μ μ¬μ©νλ©΄ μ¬λ¬κ°μ μ‘°κ±΄μ νμΈν  μ μλ€.
    - assertThorws()μ μ¬μ©νλ©΄ μμΈλ₯Ό νμΈν  μ μλ€.

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
            @DisplayName("μ¬λ¬ hamcrest mathcer νμ€νΈ")
            void hamcrestTest() {
                assertEquals(2, 1 + 1);
                assertThat(1 + 1, equalTo(2));
                assertThat(1 + 1, is(2));
                assertThat(1 + 1, anyOf(is(1), is(2)));

                assertNotEquals(1, 1 + 1);
                assertThat(1 + 1, not(equalTo(1)));
            }

            @Test
            @DisplayName("μ»¬λ μμ λν matcher νμ€νΈ")
            void hamcrestListMathcerTest() {
                var prices = List.of(2, 3, 4);
                assertThat(prices, hasSize(3));
                assertThat(prices, everyItem(greaterThan(1)));
                assertThat(prices, containsInAnyOrder(3, 4, 2));
        //        assertThat(prices,contains(2,4,3)); μ΄κ²μ μμλ₯Ό μ§μΌμ νμ€νΈν¨
                assertThat(prices, hasItem(greaterThanOrEqualTo(2)));
            }
        }

        ```
- ### Mock Object ###
    - Mock μ€λΈμ νΈλ νμ κ²μ¦μ μ¬μ©νκ³  stucbμ ν¬ν¨ν λ€λ₯Έ λμ­λ€μ μν κ²μ¦μ μ¬μ©νλ€.
        - Mockμ μ’ λ νμμ μ§μ€
        - μν κ²μ¦ : λ©μλκ° μνλ ν, κ°μ²΄μ μνλ₯Ό νμΈνλ©° μ¬λ°λ₯΄κ² λμνλμ§λ₯Ό νμΈνλ κ²μ¦λ²μ΄λ€.
        - νμ κ²μ¦ : λ©μλμ λ¦¬ν΄ κ°μΌλ‘ νλ¨ν  μ μλ κ²½μ° νΉμ  λμμ μννλμ§ νμΈνλ κ²μ¦λ²μ΄λ€.

    ```java
    class OrderServiceTest {

    class OrderRepositoryStub implements OrderRepository {

            @Override
            public Order insert(Order order) {
                return null;
            }
        }

        @Test
        @DisplayName("μ€λκ° μμ±λμΌ νλ€. (stub)")
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
        @DisplayName("μ€λκ° μμ±λμΌ νλ€. (Mock)")
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
    - Mockμ ν΅ν΄μ ν΄λΉνλ Mockκ°μ²΄μ λ©μλλ§μ λμμ νμΈν  μ μλ€.(ν΄λΉνλ λͺ© κ°μ²΄κ° μ λλ‘ μ΄ λ©μλλ₯Ό callνλμ§, μ¬μ©νλμ§, μ΄λ ν λ§€κ°λ³μλ₯Ό μ¬μ©νλμ§ λ±λ±) 
    - inOrderλ₯Ό μ¬μ©ν΄μ λ©μλμ μμλ νμΈν  μ μλ€.

- ### Spring Test ###
    - Springμμ μ κ³΅νλ μ΄λΈνμ΄μμ νμ©ν΄μ ν΅ν© νμ€νΈλ₯Ό μ€μ΅ν κ²°κ³Όμ΄λ€.
```java
//@ExtendWith(SpringExtension.class)
//@ContextConfiguration(classes = {AppConfiguration.class})
//μ λκ°μ§ μ΄λΈνμ΄μμ μλ νλμ μ΄λΈνμ΄μμΌλ‘ μ κ³΅ν¨
//@ActiveProfiles("test") μ΄λ κ² νλ©΄ test profile μ¬μ©λ¨
@SpringJUnitConfig(classes = {AppConfiguration.class})
public class KdtSpringContextTests {

    @Autowired
    ApplicationContext context;

    @Autowired
    OrderService orderService;

    @Autowired
    VoucherRepository voucherRepository;

    @Test
    @DisplayName("applicationContextκ° μμ±λμΌ νλ€.")
    public void testApplicationContext(){
        assertThat(context,notNullValue());
    }

    @Test
    @DisplayName("VoucherRepositoryκ° λΉμΌλ‘ λ±λ‘λμΌ νλ€.")
    public void testVoucherRepositoryCreation(){
        var bean = context.getBean(VoucherRepository.class);
        assertThat(bean,notNullValue());
    }

    @Test
    @DisplayName("OrderServiceλ₯Ό μ¬μ©ν΄μ μ£Όλ¬Έμ μμ±ν  μ μλ€.")
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