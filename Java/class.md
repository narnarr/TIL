### 참고

- Class 클래스 <[https://heavyfive.tistory.com/entry/Class-클래스의-용도](https://heavyfive.tistory.com/entry/Class-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%9D%98-%EC%9A%A9%EB%8F%84)>
- Class 클래스 <[https://devyongsik.tistory.com/292](https://devyongsik.tistory.com/292)>
- Class 클래스 <[https://palpit.tistory.com/entry/Java-자바-기본-API-Class-Class](https://palpit.tistory.com/entry/Java-%EC%9E%90%EB%B0%94-%EA%B8%B0%EB%B3%B8-API-Class-Class)>
- reflection <[https://joont.tistory.com/165](https://joont.tistory.com/165)>
- 동적 로딩 <https://ubange.tistory.com/223?category=647815>

# Class 클래스

> 자바의 모든 클래스들에 대한 구조를 정의한 틀. 클래스와 인터페이스의 메타 데이터를 관리한다.

자바의 모든 클래스와 인터페이스는 컴파일 후 class 파일로 변환된다. 이 class 파일에는 객체의 클래스명, 생성자 정보, 필드 정보, 메소드 정보 등과 같은 **메타 데이터**가 포함되어 있는데, Class 클래스를 이용하면 컴파일된 class 파일에 접근하여 객체의 정보를 가져올 수 있다. Class 클래스는 java.lang 패키지에 소속되어 있다.

보통 라이브러리가 잘 되어 있어서 원하는 자료형을 찾아 사용하기 편리하기 때문에 굳이 Class 클래스를 가져다 사용하지는 않는다. 주로 프로그래머의 로컬에 해당 자료형 및 모듈이 없을 경우 사용하거나 동적 로딩에서 많이 쓴다. (이에 대해서는 나중에 공부할 예정)

Class 클래스를 가져오는 방법에는 아래와 같이 세 가지가 있다.

```java
// Object 클래스로부터 상속받은 메소드 사용하는 방법
String s = new String(); // String 클래스로 객체 생성
Class c = s.getClass();

// 컴파일된 상태로 있는 것은 (인스턴스화 없이) 바로 가져올 수 있다
Class c = String.class;

// 동적 로딩 - 이 statement가 수행될 때 인자로 넣은 클래스의 Class 클래스가 로딩됨
Class c = Class.forName("java.lang.String");
```

### 01_getClass()

`getClass()` 메소드는 `Object` 클래스의 메소드로, (이를 상속받은) 모든 클래스에서 호출 가능하다. 하지만 해당 클래스로 객체를 생성한 이후에야 사용 가능하다.

### 02_컴파일 상태에서 .class

객체 생성 없이도 Class 객체로 호출해낼 수 있는 방법이다.

### 03_forName()

**장점** : 유연하다!

1, 2번째는 컴파일될 때 로딩(정적 로딩)이 되는 반면 `forName()` 은 런타임에 로딩(동적 로딩)이 되므로 유연하다는 장점이 있다. JDBC를 예를 들자면, JDBC의 다양한 라이브러리(MsSQL, MySQL 등)를 모두 static하게 링크해서 컴파일하기에는 파일이 너무 커진다. 하지만 라이브러리들을 로컬에 모두 설치해놓고 상황에 따라 필요한 라이브러리만 골라서 불러다가 쓰면 메모리를 효율적으로 사용할 수 있다.

**단점** : 컴파일 타임에 미리 오타 속출 불가능 

인자에 오타가 날 경우 컴파일 타임에 체크할 수 없으므로 해당 문자열에 대한 클래스가 없는 경우 `ClassNotFoundException` 예외가 발생해 런타임에 죽을 수 있다는 단점이 있다.

## reflection 프로그래밍

> 객체를 통해 클래스의 정보를 분석해내는 프로그래밍 기법

클래스 파일의 위치나 이름으로 해당 클래스의 정보를 얻어내고(Class 클래스) 객체를 생성하는, 유연한 프로그래밍을 위한 기법이다. `new` 연산자를 사용하지 않고도 동적으로 객체를 생성할 수도 있게 된다. 앞서 말했듯 로컬에 객체가 이미 있을 경우엔 잘 사용하지 않는다. 반대로 로컬에 객체가 없고 자료형을 알 수 없는 경우에 유용하다.

java.lang.reflect 패키지에 속해 있다.

### +) 동적 로딩

컴파일 시에 데이터타입이 모두 바인딩되어 자료형이 (static loading) 로딩되는 것이 아니라 실행 중에 데이터 타입을 알고 binding되는 방식이다. 실행 시에 로딩되므로 경우에 따라 다른 클래스가 사용될 수 있다. 더 자세한 사항은 잘 정리된 블로그를 발견하여 링크로 남겨두겠다.
