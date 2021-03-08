### 참고

템플릿 메소드 패턴: <[https://niceman.tistory.com/142](https://niceman.tistory.com/142)>

# 템플릿 메소드

> 추상 메소드나 구현된 메소드를 활용하여 전체의 흐름(시나리오, 로직)을 정의해 놓은 메소드. 소프트웨어 디자인 패턴 중 하나다.

`final` 예약어로 선언하여 재정의할 수 없게 한다.

비유하자면 내가 하루 일과를 `기상> 아점> 공부> 저녁> 휴식> 취침` 이라고 짰으면 반드시 위의 순서대로 보내야 하는 것이다. 아점을 먹으라고 선언했기 때문에 아침 따로, 점심 따로 먹을 수 없다. 대신에 매일매일 메뉴의 선택이나 공부 내용 및 방법에 대해서는 선택 가능하다. 

추상 클래스로 선언된 상위 클래스에서 추상 메소드를 이용해 전체 구현의 흐름을 정의하고, 구체적인 구현에 대해서는 하위 클래스에 책임을 위임하는 것이다. 

### 장점

- 코드 간소화 (중복 감소)
- 자식 클래스의 역할 감소시면서 핵심 로직 관리에 용이
- 객체 추가 및 확장 용이

### 단점

- 추상 메소드가 너무 많아지면 클래스 관리가 복잡해짐
- 추상 클래스와 구현 클래스 간 복잡성 증대

이와 같이 하위 클래스에서 추상 메소드를 어떻게 구현했느냐와 상관 없이, 반드시 이 흐름대로 진행해!라고 으름장을 놓는 메소드를 템플릿 메소드라고 한다.

## final 예약어

`static` 과 함께 자주 쓰인다. 값이 잘 변하지  않기 때문이다.

final 변수는 값이 변경될 수 없는 상수다. 오직 한 번만 값을 할당할 수 있다.

```java
public static final double PI = 3.14;
```

final 메소드는 하위클래스에서 재정의overriding할 수 없다.

final 클래스는 더 이상 상속되지도 않는다. ex) 자바의 String 클래스

```java
public class Define (
	public static final int NIN = 1;
	public static final int MAX = 99999;
	public static final double PI = 3.14;
	public static final String HBD = "Happy Birthday!";
}
```

```java
public class DefineTest {
	public static void main(String[] args) {
	//static이기 때문에 new로 인스턴스화하지 않고도 바로 HBD 불러올 수 있다.
		System.out.println(Define.HBD);
	}
}
```
