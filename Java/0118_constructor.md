# 생성자 Constructor

- new 연산자를 통해서 인스턴스 생성할 때 호출이 되고 제일 먼저 실행되는 일종의 메소드(!= 메소드)
- 인스턴스 변수(필드값 등)를 초기화하는 코드가 구현됨

    ```java
    public class Student {
    		//필드 선언
    		public int studentID;
    		public String studentName;
    		public String address;

    		//생성자
    		public Student(int id, String name) {
    				//매가값을 이용한 필드 초기화
    				studentID = id;
    				studentName = name;
    		}

    		public void printInfo() {
    				System.out.println(
    		}
    }
    ```

- 반환값이 없음, 상속되지 않음
- 생성자는 클래스 이름과 동일

### 기본 생성자 default constructor

- 하나의 클래스에는 반드시 하나 이상의 생성자 존재해야 함
- 프로그래머가 생성자를 구현하지 않으면 컴파일러가 자동으로 생성자 생성
- 기본 생성자는 매개변수가 없고, 구현부가 없음

    ```java
    //기본생성자
    public Student() {
    		super(); //부모클래스의 생성자 호출
    }
    ```

같은 이름의 생성자의 매개변수를 다르게 지정한 것이 여러개 있을 경우를 생성자 오버로딩이라고 한다.

## 생성자와 메소드의 차이

- 생성자는 반드시 클래스명과 동일하게 정의 (메소드는 자유롭게 정의 가능)
- 생성자 앞에는 접근 제어자(public, private 등)만 올 수 있다 (메소드는 static과 같은 수식어 작성 가능)
- 반환값이 없으므로 void나 자료형을 작성할 수 없다 (메소드는 반드시 있어야 한다)
- 상속이 되지 않는다 (메소드는 상속 가능)
