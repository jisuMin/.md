## :bulb: Spirng - Mybatis 연동

- Spirng - Mybatis 연동을 위한 라이브러리 추가 `pom.xml`
- spring-jdbc : spring framework 랑 같은 버전을 선택한다. 

```xml
<!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>4.3.18.RELEASE</version>
</dependency>
```

- mybaits 연동 라이브러리

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis-spring</artifactId>
    <version>1.3.2</version>
</dependency>

```

- spring annotation 인식 패키지 설정 : `spring cofiguration xml`

```xml
<context:component-scan base-package=*"spring.mybtis">
</context:component-scan>
```



## :mag_right: Spring - Mybatis DataSource 설정

```xml
<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
	<property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
	<property name="url" value="jdbc:mysql://127.0.0.1:3306/memberdb"/>
	<property name="username" value="emp2"/>
	<property name="password" value="emp2"/>
</bean>
<!--  mybatis 연동 / sql mapping 파일 위치  -->
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
	<property name="dataSource" ref="dataSource"/>
	<property name="configLocation" value="classpath:spring/mybatis/mybatis-config.xml" />
	<property name="mapperLocations" value="classpath:spring/mybatis/sql-mapping.xml" />
</bean>

<bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
	<constructor-arg ref="sqlSessionFactory"></constructor-arg>
</bean>
```

> spring에서 제공되는 datasource를 사용하기 위해 `xml`  파일에 꼭 필요한 설정들이다.

- 추가로 annotation을 사용(익식)할 패키지 설정

```xml
<context:component-scan base-package="spring.mybatis">
</context:component-scan>
```



## :mag_right: < choose >를 이용한 조건 검색

- < choose > - < when > 조건절을 이용해 각 parameter에 맞는 조회문을 선언한다.
- mybtis sql에서 `like concat`을 이용해 조건 검색을 한다.  

```xml
<select id="searchlist" resultType="memberdto" parameterType="memberdto">
		select * from member where
		<choose>
			<when test="name != null"> name like concat('%',#{name},'%')</when>
			<when test="email != null">email like concat('%',#{email},'%')</when>
			<when test="phone != null">phone like concat('%',#{phone},'%')</when>
			<when test="id != null">id like concat('%',#{id},'%')</when>
		</choose>
		order by id
	</select>
```

> 조회된 결과는 order by를 이용해 id 순으로 정렬한다. 