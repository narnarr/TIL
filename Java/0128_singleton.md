### 참고
- 싱글톤 <[https://elfinlas.github.io/2019/09/23/java-singleton/](https://elfinlas.github.io/2019/09/23/java-singleton/)>

# singleton 패턴

> 생성자가 여러 차례 호출되더라도 하나의 인스턴스만 존재하고 그 이후에 호출된 생성자는 최초의 인스턴스를 리턴하는 소프트웨어 디자인 패턴

ex) 하나의 프린터기를 여러 명의 사원이 공유할 때, 하나의 날짜에 대한 여러 시간대를 호출할 때

`static`으로 최초 한 번만 메모리를 할당하고

`private`을 사용하여 메인 메소드에서 함부로 객체 생성을 하지 못하게 한다.

`public static get()` 메소드를 통해 외부에서 유일한 객체를 참조할 수 있게 해준다.

```java
public class ExampleClass {
    //Instance
    private static ExampleClass instance = new ExampleClass();

    //private construct
    private ExampleClass() {}

    public static ExampleClass getInstance() {
        return instance;
    }
}
```
