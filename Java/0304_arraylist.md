### 참고
- ArrayList <[https://edu.goorm.io/learn/lecture/41/바로실습-생활코딩-자바-java/lesson/39156/arraylist의-사용법](https://edu.goorm.io/learn/lecture/41/%EB%B0%94%EB%A1%9C%EC%8B%A4%EC%8A%B5-%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9-%EC%9E%90%EB%B0%94-java/lesson/39156/arraylist%EC%9D%98-%EC%82%AC%EC%9A%A9%EB%B2%95)>

# ArrayList

자바 컬렉션 프레임워크 중 List 컬렉션의 구현체다.

컬렉션 프레임워크는 아직 공부하지 않았지만, 찾아본 바에 의하면 객체나 데이터들을 효율적으로 관리(추가, 삭제, 검색, 저장)할 수 있는 자료구조라고 한다. 이 부분은 나중에 다룰 예정이다.

List 클래스의 주요 메소드로는 `boolean add(E e)` , `int size()`  , `E get(int index)` , `E remove(int index)` , `boolean isEmpty()` 등이 있다.

요소의 저장 순서가 유지되며, 인덱스로 요소를 관리한다는 점에서는 배열과 같지만, 크기가 가변적이라는 점에서 큰 차이가 있다. 이런 특징 덕분에 일반 배열 사용 시 자주 마주치게 되는 `java.lang.ArrayIndexOutOfBoundsException` 에러를 피할 수 있다는 장점이 있다.

```java
String[] fruits = new String[2];
fruits[0] = "apple";
fruits[1] = "banana";
fruits[2] = "cherry"; // fruits 배열의 크기 2를 벗어났으므로 오류가 난다

for (int i=0; i<fruits.length(); i++) {
	String str = fruits[i];
	System.out.println(str);
}
```

```java
ArrayList<String> fruits = new ArrayList<String>();
fruits.add("apple");
fruits.add("banana");
fruits.add(0, "cherry"); //추가할 요소의 위치 지정 가능

for (int i=0; i<fruits.size(); i++) {
	String str = fruits.get(i);
	System.out.println(str);
}
```
