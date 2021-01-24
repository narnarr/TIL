# 개발환경 세팅하기

1. JDK 설치 완료
2. Eclipse, Spring 설치 완료
3. Tomcat 설치 완료
4. 서버 연결(Hello World 페이지 확인) 완료
5. MariaDB, MySQL workbench 설치 완료
6. movie 테이블 생성 및 레코드 생성 완료
7. 연동 실패
-  `root-context.xml`에서 `Mybatis log` 부분에서 에러남
```xml
 <!-- <mybatis-spring:scan base-package="com.devfun.dao" /> -->
    <context:component-scan
        base-package="com.devfun.dao"></context:component-scan>
    <context:component-scan
        base-package="com.devfun.service"></context:component-scan>
```
위의 부분을 아래 코드의 어디에 삽입해야 할 지 모르겠음. (`<beans>` 안에 넣어도, 밖에 넣어도 다 에러남ㅠㅠ)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans https://www.springframework.org/schema/beans/spring-beans.xsd">

	<!-- Root Context: defines shared resources visible to all other web components -->
	<bean id="dataSource"
		class="org.springframework.jdbc.datasource.DriverManagerDataSource">
		<property name="driverClassName"
			value="net.sf.log4jdbc.sql.jdbcapi.DriverSpy"></property>
		<property name="url"
			value="jdbc:log4jdbc:mariadb://127.0.0.1:3306/theater" />
		<property name="username" value="root" />
		<property name="password" value="qorskf421" />
	</bean>

	<bean id="sqlSessionFactory"
		class="org.mybatis.spring.SqlSessionFactoryBean">
		<property name="dataSource" ref="dataSource"></property>
		<property name="configLocation"
			value="classpath:/mybatis/mybatis-config.xml"></property>
		<property name="mapperLocations"
			value="classpath*:/mybatis/sql/*.xml"></property>
	</bean>

	<bean id="sqlSession"
		class="org.mybatis.spring.SqlSessionTemplate">
		<constructor-arg name="sqlSessionFactory"
			ref="sqlSessionFactory"></constructor-arg>
	</bean>
</beans>
```
- `com.devfun.vo/MovieVo.java` 파일을 작성하는 법이 블로그에 적혀있지 않아서 이를 참조하는 다른 파일들에서 모두 에러 표시가 남
