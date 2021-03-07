# 캐스팅 Casting

캐스팅이란 타입을 변환하는 것, 즉 형변환이다. 상속 관계에 있는 부모와 자식은 서로 간의 형변환이 가능하다.

## 01_업캐스팅

업캐스팅이란 상위 클래스로의 묵시적 형변환이다. 비유를 들자면 "사람(하위)은 포유류(상위)다", "연필(하위)은 필기구(상위)다" 등과 같다. 

업캐스팅의 방법은 상위클래스형으로 변수를 선언하고 하위클래스 인스턴스를 생성하면 된다. 단, 그 역은 성립이 불가하다.

```java
Customer vc = new VIPCustomer();
List<Student> students = new ArrayList<Student>();
```

## 02_다운캐스팅

업캐스팅된 인스턴스를 원래 자료형(하위클래스)로 복구시켜주는 것을 다운캐스팅이라고 한다. 다운캐스팅은 명시적으로 타입을 지정해야 한다.

```java
Customer vc = new VIPCustomer(); //묵시적 업캐스팅
VIPCustomer vCustomer = (VIPCustomer) vc; // 명시적 다운캐스팅
```

근데 여기서 문제는, 컴파일 시 양변의 VIPCustomer가 일치하는지만 확인하고 넘어간다는 점이다.  따라서 무분별하게 다운캐스팅을 하다 보면 컴파일 시점에는 오류가 발생하지 않아도 런타임 오류가 발생할 가능성이 있다.

```java
GoldCustomer vCustomer = (GoldCustomer)vc; // 런타임 오류 발생
```

### +) instanceof 연산자

런타임 오류를 방지하고 싶으면 `instanceof` 연산자를 사용하면 된다. 객체가 실제로 어떤 타입인지 확인(true/false)한 후에 코드를 실행시켜서 안정적 형변환이 가능하다. 단, 참조형에서만 사용 가능하다.

```java
if (vCustomer instanceof GoldCustomer) {
	GoldCustomer vCustomer = (GoldCustomer)vc;
}
```
