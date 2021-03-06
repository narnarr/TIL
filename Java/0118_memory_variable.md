### 수강한 강의

패스트캠퍼스 자바 Part2 강의 1~10

+)

참고하기 좋은 블로그 <[https://blog.naver.com/heartflow89/220954420688](https://blog.naver.com/heartflow89/220954420688)>

점프 투 자바 <[https://wikidocs.net/232](https://wikidocs.net/232)>

# 메모리

## 01_Static 영역

- 필드 부분에서 선언된 변수(전역변수)와 정적 멤버변수(`static`이 붙은 자료형, 클래스 변수)들이 저장됨
- 클래스의 인스턴스들이 공통적으로 가지는 데이터를 `static`으로 선언할 경우 하나의 주소를 공유하게 되어 같은 데이터에 대해 매번 메모리를 할당할 필요가 없어지므로 메모리 세이브 가능.
- 하지만 Garbage Collector 관여 X, 프로그램의 시작부터 종료될 때까지 메모리에 남아있음. 그렇기에 전역변수를 무분별하게 많이 사용하면 메모리가 부족해질 수도 있다.
- 모든 객체가 메모리를 공유

## 03_Stack 영역

- 기본 자료형에 해당되는 지역변수의 데이터값이 저장되는 공간
- 해당 메소드가 호출될 때 메모리에 할당되고 종료되면 메모리 해제됨

## 03_Heap 영역

- 주로 객체들이 할당 (인스턴스 생성 시 각 인스턴스에 대한 메모리들은 힙에 저장, 앞에 `static` 없이 그냥 선언할 경우 자동으로 인스턴스 변수가 됨)
- Garbage Collector 관여 O
- 메모리를 공유하지 않음

# 자바의 자료형

## 01_기본형

- 논리형, 문자형(char), 정수형, 실수형
- stack 영역에 값 자체 저장

```java
int primitiveVar = 5;
```

## 02_참조형

- 배열, 클래스(String, Date, Student 등), 인터페이스(Runnable, Enumeration 등), 프로그래머가 직접 생성한 자료형
- 힙 메모리에 저장된 인스턴스(실제 값)를 가리키는 주소(참조 값)를 stack영역에 저장

```java
String referenceVar = new String("Java");
Date today = new Date();

//참조값 예 - 패키지명.클래스명@JVM이 부여한 주소
classpart.Student@6d06d69c
```

# 자바의 변수

## 01_멤버변수(소속변수, 필드)

> 클래스 내부에 소속된 변수로, 대부분의 메소드에서 사용 가능

- 변수 선언 시 초기값 저장하지 않아도 기본값이 디폴트로 저장됨(0, false, null 등)

### 인스턴스변수

> 인스턴스 생성 시 만들어지는 변수. 힙 메모리(동적 메모리)에 따로 저장.

- 각 인스턴스마다 다른 값 가질 수 있음. 인스턴스 생성 필수.

### 클래스변수

> 클래스 로딩 시 만들어지는 변수. 앞에 static 붙음.

- 모든 인스턴스가 같은 값 공유. 인스턴스 생성 없이도 바로 쓸 수 있음.

## 02_지역변수

> 메소드 내부에서 선언되는 변수로, 선언된 메소드 내부에서만 사용

- 변수 선언 시 초기값 저장하지 않고 실행하면 컴파일 오류 발생
- 매개변수

```java
public class Variable {
		int a; //기본형변수, 멤버변수, 인스턴스변수
		static String b; //참조형변수, 멤버변수, 클래스변수
		void mm(int c) { //기본형변수, 지역변수, 매개변수
				int d = c; //기본형변수, 지역변수
		}
		public static void main(String args[]) { //참조형변수, 지역변수, 매개변수
				int e = 0; //기본형변수, 지역변수, 매개변수
				Variable v = new Variable(); //참조형변수, 지역변수
				v.mm(e);
				System.out.printIn(Variable.b); //인스턴스 생성 없이도 사용 가능
		}
}
```

## 주의할 점

보통 메인 메소드는 클래스와 분리하여 새로운 클래스에 따로 만드는데, 학습할 때는 한눈에 보기 편하라고 하나의 클래스에 모두 넣는 경우가 많다. 근데 그럴 경우 메인 메소드도 다른 일반 메소드들처럼 멤버변수를 받는다고 생각하면 안 된다.
