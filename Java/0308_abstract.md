# 추상 클래스 abstract

> 구현부 없이 선언부만 있는 추상 메소드를 포함하는 클래스

추상 클래스는 new (인스턴스화)할 수 없다. 구현부가 비어있으므로 불러냈을 때 바디화할 수 있는 부분이 없기 때문에 에러가 난다.

이와 대조하여 구현부가 있는 일반적인 클래스는 concrete class라고 할 수 있다. 자주 사용하는 용어는 아니다.

컴퓨터는 디스플레이가 있고 타자도 칠 수 있어야 한다. 하지만 이런 기능이 화면, 키보드, 마우스 등 모든 부품에 존재하는 것이 아니기 때문에 가장 중심인 `Computer` 에는 이를 추상 클래스로 선언은 하되 일단 바디를 구현하지 않는다. 그러고 구현의 책임을 하위 클래스에게 위임한다.

```java
public abstract class Computer {
	public abstract void display(); // 구현부가 없다
	public abstract void typing();
}
```

추상 메소드는 해당 클래스를 상속 받은 하위 클래스에서 필요에 따라 구현하여 사용하면 된다. 

```java
public class Desktop extends Computer {
	@Override
	public void display() {
		System.out.println("Desktop display");
	}

	@Override
	public void typing() {
		System.out.println("Desktop typing");
	}
}
```

`Desktop` 은 `Computer` 의 모든 추상메소드를 오버라이딩했으므로 더 이상 추상 클래스가 아니다. `abstract` 예약어가 없는 것을 확인할 수 있다.

```java
public abstract class Notebook extends Computer {
	@Override
	public void display() {
		System.out.println("Notebook display");
	}
}
```

반면, `Notebook` 처럼 모든 추상 메소드의 바디를 구현하지 않은 경우 여전히 추상 클래스다.

```java
public class MyNotebook extends Notebook {
	@Override
	public void typing() {
		System.out.println("Notebook typing");
	}
}
```

이처럼 또 `Notebook` 을 상속받아서 구현하지 못한 나머지 추상메소드들의 구현도 마무리할 수 있다.

어떨 때에는 모든 메소드가 구현이 되었음에도 abstract 키워드를 사용해 추상 클래스로 만들어버리기도 한다. 이는 상속에서 인스턴스화 시키고 싶지 않은 클래스가 있을 때 그런다고 한다.
