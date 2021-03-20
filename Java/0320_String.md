### 참고

- String 짱 <[https://github.com/wjdrbs96/Today-I-Learn/blob/master/Java/Java_lang/String vs StringBuffer vs StringBuilder.md](https://github.com/wjdrbs96/Today-I-Learn/blob/master/Java/Java_lang/String%20vs%20StringBuffer%20vs%20StringBuilder.md)>

# String

String을 선언하는 방식으로 아래와 같이 두 가지가 있다.

```java
String str1 = new String("abc");
String str2 = "abc";
```

첫번째 방식은 `new` 로 String을 인스턴스화하여 힙메모리를 할당 받아 해당 주소값을 담는 방식이고, 두번째 방식은  `""` 리터럴을 이용해 상수풀에 있는 문자열을 가리키는 방식이다. 

## String은 변경 불가immutable한 클래스다

한번 선언되거나 생성된 String 문자열은 변경할 수 없다. 아래 소스를 보자.

```java
public class StringTest {
 public static void main(String[] args {
		String str1 = "Hello";
		System.out.println(System.identityHashCode(str1)); //1435804085
		str1 += ", World";
		System.out.println(System.identityHashCode(str1)); //1784662007
	}
}
```

위의 코드를 보고난 후 "Hello"에 ", World"를 이어붙인 게 기존의 데이터를 대체할 것이라고 생각할지도 모른다. 하지만 해쉬코드를 보면 알 수 있듯이 첫번째 `str1` 와 두번째 `str1` 는 완전히 다른 곳을 가리키고 있다. 즉, 기존의 데이터를 수정한 것이 아니라, 상수풀에 아예 새로운 문자열이 생성된 것이다.

`java.lang.String` declaration을 살펴보면 `private final byte[] = value;` 가 있는 걸 볼 수 있다. 이처럼 `final` 로 선언되었기 때문에 String은 불변하다.

### String 클래스가 적절한 경우

- 문자열 연산이 적고 자주 참조(조회)하는 경우
- 멀티쓰레드 환경에서 동기화Synchronization 신경쓰지 않아도 됨(불변 클래스이므로)

### String 클래스가 적절하지 않은 경우

- `+` 나 `concat()` 메소드를 이용해서 계속 새로운 문자열을 만들면 기존의 문자열이 Garbage Collector에 의해 제거되어야 함.
- 실무에서는 서버에서 클라이언트로 응답을 보낼 때 등 문자열을 연결하는 경우가 많다. 이때 String을 사용하는 것은 연결되기 전의 문자열들이 쓸데없이 공간을 계속 차지하게 되어 메모리의 관점에서 비효율적이다.

→ 이럴 때 StringBuilder와 StringBuffer를 사용하면 된다.

# StringBuilder & StringBuffer

`final` 배열을 갖고 있던 String과 달리, 가변적인 char[] 배열을 멤버변수로 갖고 있는 클래스다. 문자열을 변경하거나 연결하는 경우에 용이하다.

```java
public class StringBuilderTest {
	public static void main(String[] args) {
		StringBuilder sb1 = new StringBuilder("Hello");
		System.out.println(System.identityHashCode(sb1)); //1435804085
		sb1.append(", World");
		System.out.println(System.identityHashCode(sb1)); //1435804085
```

StringBuilder와 StringBuffer는 쓰레드의 동기화를 지원하느냐를 제외하고는 모두 동일하다.

StringBuffer는 멀티쓰레드에 안전하도록 동기화가 지원된다. 단일쓰레드의 경우에 StringBuffer의 동기화는 불필요하게 성능만 떨어트리게 된다. 따라서 단일 쓰래드 프로그래밍에서는 StringBuilder를 사용하는 것이 더 좋다.
