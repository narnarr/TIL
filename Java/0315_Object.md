### 참고

- java.lang <[https://ryan-han.com/post/java/java-lang/](https://ryan-han.com/post/java/java-lang/)>
- 네이티브 코드 <[http://blog.naver.com/PostView.nhn?blogId=ft1998&logNo=100001231979&parentCategoryNo=&categoryNo=2&viewDate=&isShowPopularPosts=false&from=postView](http://blog.naver.com/PostView.nhn?blogId=ft1998&logNo=100001231979&parentCategoryNo=&categoryNo=2&viewDate=&isShowPopularPosts=false&from=postView)>
- 객체 소멸자 <https://madplay.github.io/post/java-finalize>

# Object 클래스

> 모든 클래스의 최상위 클래스.

모든 클래스는 Object 클래스를 상속받는다. 내가 입력하지 않아도 컴파일러가 자동으로 `extends Object`해준다. (다중 상속 안 된다는데 Object는 기본으로 깔고 들어가는거라 예외로 치나보다?)

`java.lang.Object` 에 위치하는데 이 역시 `import java.lang` 하지 않아도 자동으로 import 해준다.

모든 클래스는 Object 클래스의 메소드를 사용할 수 있고, `final` 등으로 선언된 것을 제외한 Object 클래스의 일부 메소드를 재정의하여 사용할 수도 있다.

이제 Object 클래스의 메소드 중 오버라이딩을 하여 자주 사용되는 메소드들을 알아보자.

## 01_toString() 메소드

> 객체가 갖고 있는 정보나 값들을 문자열로 만들어 리턴하는 메소드

```java
class Student {
	int studentNum;
	String studentName;
	
	public Student(int studentNum, String studentName) {
		this.studentNum = studentNum;
		this.studentName = studentName;
	}
}

public class StudentTest {
	public static void main(String[] args) {
		Student stu = new Student(100, "Steven Yeun");
		System.out.println(stu.toString());
		// object.Student@6a5fc7f7 주소가 출력된다
	
		String str = new String("Steven Yeun");
		System.out.println(str.toString());
		// Steven Yeun이 출력된다
	}
}
```

위와 같이 `stu` , `str` 모두 `toString()` 메소드를 이용했는데 왜 전자는 주소가, 후자는 문자열이 그대로 출력될까?

내가 만든 `Student` 클래스는 `Object` 로부터 `toString()` 메소드를 그대로 상속받은 반면, 자바에 이미 정의되어 있는 `String` 클래스는 `toString()` 메소드를 오버라이딩이 되어 있기 때문이다.

즉 주소가 `toString()` 메소드의 원형이고, 어떻게 오버라이딩하느냐에 따라 원하는 문자열로 출력이 가능하다.

`Student` 클래스도 `toString()` 메소드를 통해 문자열을 출력하고자 한다면 아래와 같이 오버라이딩하면 된다.

```java
@Override
public String toString() {
	return studentNumber + ", " + studentName;
}
```

## 02_equals() 메소드

> 객체의 논리적 동일함을 판별하는 메소드

```java
Student stuYeun = new Student(100, "Steven Yeun");
Student stuYeun2 = stuYeun;
Student stuSteven = new Student(100, "Steven Yeun");
```

`stuYeun` 과 `stuYeun2` 는 힙 메모리 내에서 같은 주소(hashCode)를 갖는다. 즉, 물리적 위치가 동일하다. 반면, `stuSteven` 은 새로운 메모리를 할당 받았기 때문에 참조하는 주소는 다르지만 학번도 같고 이름도 같은, 누가 봐도 동일한 학생을 인스턴스화한 것이다. 

이처럼 물리적으로 다른 메모리에 위치한 객체라도 논리적으로 동일함을 판별하기 위해 사용하는 메소드가 `equals()` 메소드다.

논리적으로 동일한지 알아보기 위해서는 `equals()` 를 오버라이딩한 후 사용해보자. 학번만 동일하면 동일 학생으로 보겠다.

```java
@Override
public boolean equals(Object obj) {
	if (obj instanceof Student) {
		Student std = (Student) obj;
		return (this.studentNum == std.studentNum);
	}
	return false;
}
```

```java
System.out.println(stuYeun == stuSteven); // false
System.out.println(stuYeun.equals(stuSteven)); // true
```

## 03_hashCode() 메소드

> 인스턴스가 저장된 가상머신의 주소를 10진수로 반환하는 메소드

```java
System.out.println(stuYeun); // object.Student@6a5fc7f7
System.out.println(stuYeun.hashCode()); // 1784662007
System.out.println(stuSteven.hashCode()); // 997110508
```

위와 같이 `hashCode()` 를 이용하면 10진수로 된 주소값을 얻을 수 있다.

물리적인 주소값이기 때문에 아까 `equals()` 오버라이딩을 통해 논리적으로 동일함을 보인 `stuYeun` 과 `stuSteven` 이 다른 10진수 주소를 반환한다. 이들이 같은 주소를 반환하게 만들고 싶다면 `hashCode()` 메소드 역시 오버라이딩해주면 된다.

```java
@Override
public int hashCode() {
	return studentNum; // 학생의 학번을 10진수 주소로 갖게 될 것이다.
}
```

만약 개발자가 재정의한 해쉬코드 말고 원래의 해쉬코드를 알고 싶다면 `System.identifyHashCode(stuSteven);` 을 출력해보면 된다.

## 04_clone() 메소드

> 객체의 복사본을 만드는 메소드

기본 틀(prototype)으로부터 같은 속성을 가진 객체의 복사본을 생성할 수 있다.

객체지향 프로그래밍의 정보은닉에 위배되는 가능성이 있으므로 복제할 객체는 Cloneable 인터페이스를 명시해야 한다. 즉 'Cloneable` 키워드가 적힌 객체만 복제 가능하다.

앞에 N이 붙은 메소드는 native code가 들어간다는 것. CPU나 OS가 직접 실행할 수 있는 코드. 이에 관해서는 정리하지 않고 가볍게 참고할만한 링크를 남기겠다.

```java
class Student implements Cloneable {
	// ...코드 생략
	@Override
	public Object clone() throws CloneNotSupportedException {
		return super.clone();
	}
}
```

```java
public class StudentTest {
	public static void main(String[] args) throws CloneNotSupportedException{
		Student stu = new Student(100, "Steven Yeun");
		Student stu2 = (Student) stu.clone();
	}
}
```

## 05_finalize() 메소드
> 더 이상 사용하지 않는 자원에 대한 정리 작업을 진행하기 위해 호출되는 종료자 메소드.

이전처럼 사용자가 호출하는 것이 아니라 인스턴스가 힙 메모리에서 해체될 때 garbage collector에서 호출한다. 이게 정의가 되어 있으면 가비지 콜랙터가 실행 한다. 객체 소멸자라고도 한다.
참고하기 좋은 블로그 링크를 위에 걸어두겠다.
