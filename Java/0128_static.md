### 수강한 강의

패스트캠퍼스 Part2 14강 ~ 16강

참고

- static <[https://m.blog.naver.com/PostView.nhn?blogId=50after&logNo=220870844539&proxyReferer=https:%2F%2Fwww.google.com%2F](https://m.blog.naver.com/PostView.nhn?blogId=50after&logNo=220870844539&proxyReferer=https:%2F%2Fwww.google.com%2F)>
- getter, setter <[https://kephilab.tistory.com/54](https://kephilab.tistory.com/54)>

# static 변수, 메소드

클래스 변수, 정적 변수라고도 함

static 변수는 처음 프로그램이 로드될 때 **데이터 영역(=상수static 영역)**에 생성됨

인스턴스의 생성과 상관 없이 사용할 수 있으므로(공유 메모리) 클래스 이름으로 참조

```java
//아래와 같이 new를 사용하지 않아도 저장 가능
//클래스 이름 Student를 이용해 바로 참조
Student.serialNum = 100; 
```

## getter, setter

외부에서 데이터 읽기 및 수정 시 객체 무결성 깨질 수 있어서 객체 지향 프로그래밍에서는 메소드를 통해 데이터 변경하기를 선호. 즉 데이터는 외부에서 접근 못 하도록 막고(`private`) 메소드는 공개해서(`public`) 외부에서 메소드를 통해 데이터에 접근하도록 함.

- setter: 매개값을 검증하여 유효한 값만 데이터로 저장하게 해줌
- getter: 외부에서 사용 가능한 정도로 데이터 가공 후 전달

+) 필드 타입이 boolean일 경우, getter 메소드명은 get이 아닌 is로 시작하는 것이 관례
