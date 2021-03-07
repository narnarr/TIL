**참고**

- 다형성 <[http://www.tcpschool.com/java/java_polymorphism_interface](http://www.tcpschool.com/java/java_polymorphism_interface)>
- 오버로딩과 this 1 <[https://seeminglyjs.tistory.com/170](https://seeminglyjs.tistory.com/170)>

# 다형성 Polymorphism

> 하나의 코드가 여러 자료형으로 구현되어 실행되는 것을 다형성이라고 한다.

객체지향 프로그래밍의 유연성, 재활용성, 유지보수성에 기본이 되는 특징이다.

### 장점

- 코드 간소화: if문이 많이 사라짐
- 유지보수에 편리

## 01_오버라이딩 Overriding

> 부모의 메소드를 자식에서도 사용하고 싶은데 구현 내용을 좀 달리 하고 싶을 때 메소드를 재정의, 즉 오버라이딩한다.

```java
public class Customer {
	protected int customerID;
	protected String grade;
	double bonusPoint;

	public void calcBonus(int price) {
		bonusPoint += price * 0.01;
	}
}
```

```java
public class VIPCustomer extends Customer {
	@Override
	public void calcBonus(int price) {
		bonusPoint = price * 0.05;
	}	
}
```

위와 같이 오버라이딩을 하는 메소드 위에 `@Override` 라는 annotation을 적어주면 된다.

나중에 인터페이스와 추상 클래스를 배운 이후에 자주 사용될 예정이다. 

### +) 어노테이션 annotation

컴파일러에게 몇가지 정보 전달해주어 컴파일 오류를 막아준다. annotation은 직접 만들 수도 있다. 아래는 대표적인 annotation이다.

- Override: 재정의된 메소드다
- FunctionalInterface: 함수형 인터페이스다
- Deprecated: 이후 버전에서 사용되지 않을 수 있는 변수, 메소드다
- SuppressWarnings: 특정 경고가 나타나지 않도록 한다

    ex) `@SuppressWarnings("deprecation")`는 @Deprecated가 나타나지 않도록 함

## 02_오버로딩 Overloading

> 하나의 객체에서 같은 이름을 가진 메소드를 여러 개 정의함으로써 다양한 유형의 호출에 응답하게 하는 것을 오버로딩이라 한다.

단, 각 메소드 인자의 조합(매개변수의 타입, 개수, 순서)를 다르게 해야 한다. 이를 메소드 시그니처(method signature)라고 한다.

작은 일부를 제외하고 거의 유사한 일을 수행하는 메소드들에게 매번 다른 이름을 붙이는 일이 번거롭기도 하고 코드를 읽는 사람이 이해하기도 힘들기 때문에 오버로딩을 통해 이런 비효율을 해결한다.

메소드 오버로딩뿐만 아니라 객체의 초기화를 담당하는 생성자 오버로딩도 있다. 구글링하다가 오버로딩과 관련하여 생성자에서 반복적인 this를 처리하는 새로운 방식을 발견해서 생성자 오버로딩 예제를 퍼와봤다.

```java
public class Overloading {
	String name;
	String sex;
	int age;
	
	public Overloading() {}
	
	public Overloading(String name) {
		this(name, "default", 0);
	}
	
	public Overloading(String name, String sex) {
		this(name, sex, 0);
	}
	
	public Overloading(String name, String sex, int age) {
		this.name = name;
		this.sex = sex;
		this.age = age;
		
		// this(name, sex, age); 위의 코드 대신 이를 넣으면 오류 발생
	}
}
```

마지막 생성자에서 모든 인스턴스 변수를 초기화하고, 다른 생성자들은 `this` 를 이용해 마지막 생성자를 호출함으로써 역시 모든 인스턴스 변수를 초기화를 시킨다. 이렇게 코드 간소화가 가능하다는 것!
