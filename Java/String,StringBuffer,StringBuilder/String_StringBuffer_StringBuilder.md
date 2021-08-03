# String,StringBuffer 그리고 StringBuilder의 차이

## **\[String, StringBuffer 그리고 StringBuilder의 차이를 알아야 하는 이유\]**

 위 3가지 문자열 클래스는 Java를 사용하면 자주 접하게 되는 문자열 클래스입니다. 이는 모두 문자열을 저장하기도 하고 관리합니다. 하지만, 하는 역할이 비슷하다면 굳이 3가지가 존재해야 할까요? 당연히, 각각의 성능이 다르며 상황에 맞게 사용해야 합니다. 그러므로 하나씩 각 특징과 차이를 알아보겠습니다.


***

## | String vs StringBuffer/StringBuilder

 먼저, String의 특징을 살펴보겠습니다.

 **String**과 **StringBuffer/StringBuilder**의 기본적인 차이는 __<span style = "color : red">Immutable(불변)/mutable(가변)</span>__입니다. String 객체는 생성이 될 경우, 할당된 메모리 공간에 대한 변화는 일어나지 않습니다. 아래의 코드를 한번 살펴보겠습니다.

```java
String str = "Hello World";
str += "!!";
```

(그림 추가 예정)

 기존에 있던 __"Hello World"__는 없어지지 않고 새롭게 **"Hello World!!"**이 Heap 메모리 영역내의 **String Constant Pool**에 쌓이게 됩니다. 이후, GC(Garbage Collector)가 **"Hello World"**를 처리해주게 됩니다. 즉, 생성된 객체는 변하지 않고 새로운 객체가 계속 생성되는 것입니다.

 그렇다면, **StringBuilder**와 **StringBuffer**는 어떨까요?

앞서, **String**이 불변의 특성을 가지고 있다면 **StringBuilder**와 **StringBuffer**는 가변적인 특징을 지니고 있다고 말씀드렸습니다.

```java
StringBuffer sb = new StringBuffer("Hello World");
sb.append("!!");
```

(그림 추가 예정)

 가변적인 특징을 지니고 있기 때문에 처음 생성된 **"Hello World"**는 append() 메소드를 통해 **"Hello World!!"**로 변하게 됩니다. 즉, 앞서 확인한 **String**과는 다르게 새롭게 Heap 영역에 메모리를 쌓지 않고 기존에 있는 객체를 변화시킵니다.

단순히 한 두번의 연산과정일 경우에는 객체가 힙메모리에 쌓이는 것에 대한 우려가 없지만 이러한 예시를 생각해보겠습니다. 이렇게 + 연산과정(추가,삭제,수정)을 1000번하게 되면 String 인스턴스 1000개가 힙메모리에 쌓이게 됩니다. 하지만, **StringBuffer**나 **StringBuilder**를 사용하게 되면 하나만 생성하면 되므로 **훨씬 효율적이고 힙메모리에 부담이 적을것**입니다.

```java
String str = "";
for(int i= 0; i< 1000; i++){
    str += i;
}
```

### | StringBuffer vs StringBuilder

그렇다면, 가변성을 지니고 있는 **StringBuffer**와 **StringBuilder**의 차이는 무엇이 있을까요? 

가장 큰 차이는 **동기화 여부**입니다. **StringBuffer**는 동기화 키워드를 지원하여 멀티쓰레드 환경에서 안전하다는 특징(thread-safe)이 있습니다. 반대로, **StringBuilder**는 동기화를 지원하지 않기 때문에 멀티쓰레드 환경에서 사용하는 것은 적절하지 않지만, 그렇기 때문에 **StringBuilder**는 단일쓰레드 환경에서 **StringBuffer**보다 뛰어난 성능을 지니고 있습니다.

\- **String**은 동기화 키워드를 지원하기 때문에 멀티쓰레드 환경에서 안전하게 사용할 수 있습니다.

**\*** **동기화란?**

\- 프로세스 혹은 쓰레드들이 수행되는 시점을 조절하여 **서로가 알고 있는 정보가 일치하는 것**을 의미합니다.

\- 보다 쉽게 예시를 들어서 설명해보겠습니다. 만약, A 쓰레드와 B 쓰레드가 하나의 객체에 대해서 작업을 할 때 A가 객체의 값을 변경할 경우, B 쓰레드는 잘못된 값을 이용하여 작업을 할 수 있습니다. 그렇기에 이를 방지하기 위해 데이터의 무결성을 보장하는 것, A 쓰레드와 B 쓰레드가 알고 있는 객체의 정보를 일치시키는 것이 **동기화**입니다.

(동기화에 대한 공부도 추가적으로 해보겠습니다.)

### | Conclusion

 각 클래스들을 정리해보겠습니다. 물론, 최적화로 인하여 상이한 성능이 나올 수 있지만, 일반적인 경우에는 아래의 경우를 생각하며 사용하면 됩니다.

<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft"><tbody><tr><td style="width: 25%; text-align: center;">&nbsp;</td><td style="width: 25%; text-align: center;"><b>String</b></td><td style="width: 25%; text-align: center;"><b>StringBuffer</b></td><td style="width: 25%; text-align: center;"><b>StringBuilder</b></td></tr><tr><td style="width: 25%; text-align: center;"><b>연산 과정</b></td><td style="width: 25%; text-align: center;">String 인스턴스가<br>반복적으로 생성</td><td style="width: 25%; text-align: center;">하나의 객체를<br>가변적으로 사용</td><td style="width: 25%; text-align: center;">하나의 객체를<br>가변적으로 사용</td></tr><tr><td style="width: 25%; text-align: center;"><b>동기화 여부</b></td><td style="width: 25%; text-align: center;">O</td><td style="width: 25%; text-align: center;">O</td><td style="width: 25%; text-align: center;">X</td></tr></tbody></table>

**\[추가적인 의문\]**

 그렇다면 **String**은 왜 불변성을 지니도록 만들어진 것일까요?

\-> 재사용 가능성이 높을 경우 하나의 **String** 객체만을 생성하여 JVM의 힙 메모리를 절약함과 동시에 **캐싱 기능을 통한 속도 향상**에 있습니다.

\-> **String**은 불변성을 지니고 있기 때문에 중요한 데이터를 다룰 경우, 강제로 해당 레퍼런스에 대한 데이터 값을 바꾸는 것을 방지하기 위함입니다. 이는 멀티 쓰레드 환경에서도 불변성의 특징으로 인해 **데이터를 안전하게 유지**할 수 있습니다.

**\* JDK 버전 관련**

**\-** **JDK 1.5 버전 이전일 경우** 문자열 연산 이후 만들어진 문자열을 새로운 메모리에 할당하므로 성능상의 이슈가 있습니다.

**\- JDK 1.5 버전 이후일 경우** 컴파일 과정에서 String 객체를 사용하더라도 StringBuilder로 컴파일 되도록 변경되었습니다. 즉, 성능상의 이슈가 해소된 것입니다. 다만, 반복 루프문을 통해 문자열을 더하는 경우 여전히 객체를 메모리에 추가되는 점은 변경되지 않았습니다. 

(참고한 블로그)

[https://12bme.tistory.com/42](https://12bme.tistory.com/42)

[https://ifuwanna.tistory.com/221](https://ifuwanna.tistory.com/221)

[https://velog.io/@doghqkr13/String-StringBuilder-StringBuffer](https://velog.io/@doghqkr13/String-StringBuilder-StringBuffer)