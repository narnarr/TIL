# 상속

상위 클래스(부모)의 변수, 메소드 등을 하위 클래스(자식)가 물려받는 것. 접근제어자 `protected` 미만일 경우 상속받지 못한다.

- 상위 클래스: 보다 일반적인 개념 및 기능
- 하위 클래스: 보다 구체적인 개념 및 기능

c++은 클래스의 다중 상속이 가능하지만 자바는 불가능하다.

부모가 존재해야 자식도 존재한다. 사용자가 자식 인스턴스를 생성하고자 하면 자식의 생성자보다 부모의 생성자가 먼저 호출된다. 따라서 자식의 생성자에서는 무조건 부모의 생성자를 호출해야 한다. 

자식에서 부모 생성자 호출하는 코드가 없을 경우 컴파일러는 자동으로 부모의 기본 생성자를 호출하기 위한 `super();`를 추가한다. 하지만 만약 부모에게 기본 생성자가 없는 경우(= 매개변수가 있는 생성자만 존재하는 경우) 자식은 명시적으로 부모의 생성자 호출해야 한다.

```java
public class Customer {
	protected int customerID;
	protected String name;
	protected String grade;

	//기본 생성자가 없기 때문에 자식에서는 이를 명시적으로 호출해야 한다
	public Customer(String name) {
		this.name = name;
		grade = "SILVER";
	}

}
```

```java
public class VIPCustomer extends Customer {
	
	public VIPCustomer(String name) {
		//명시적으로 호출한 부모의 생성자
		super(String name);
		grade = "VIP";
	}
}
```
