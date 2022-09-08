##  :bulb: 게시판 만들기

- 게시물 리스트 보기 (로그인x)
  - 게시물 검색
  - 게시물 리스트 (1페이지당 3개씩 )
  - 테이블 태그 - 번호, 제목(링크걸기), 작성자, 조회수 
  - 제목 링크 클릭 - 상세 게시물 출력  - 수정/삭제 버튼 
  - 수정, 삭제 - > 게시글 암호 매칭 
- 글쓰러 가기 (로그인 o)
  - 로그인 안하면 "로그인하세요." alert 
  - 글쓰기 폼 - 작성자 로그인 id를 default value값으로 저장
  - 제목, 내용 입력
  - 글 번호 = db 테이블에서 자동 증가 
- 로그인하기
  - `HttpSession`으로 로그인 유지 
- 로그아웃하기 
  - `removeSession`

## :mag_right: 게시판 테이블 구성

- member  테이블
  - 아이디 - id varchar(30) PK : id는 중복될 수 없음
  - 비밀번호 - password int
  - 이름 - name  varchar(30)
  - 폰 번호 - phone char(13)
  - 이메일 - email varchar(30)
  - 회원가입일 - regdate datetime now()



- board 테이블 - 게시물 저장 테이블
  - 게시물 번호 - seq int auto increment primary key : 숫자는 자동 증가, 중복될 수 없음
  - 제목 - title archer(100) not null 
  - 내용 - contents varchar(4000)
  - 작성자 - writer varchar(30) : member 테이블의 id 컬럼 존재값만 사용 가능하게 foreign 제약 조건 추가하기
  - 암호 - pw int
  - 조회수 - viewcount int
  - 작성시간 - wtime datetime now()

- 작성 쿼리

  - member

  ```mysql
  create table board 
  (id int primary key,
  password int,
  name varchar(30),
  phone char(13),
  email varchar(30),
  regdate datetime);
  ```

  - board

  ```sql
  create table board 
  (seq int primary key auto_increment,
  title varchar(100) not null,
  contents varchar(4000),
  writer varchar(30),
  pw int,
  viewcount int,
  wtime datetime);
  ```

  		- board table writer에 제약조건 추가

  ```mysql
  alter table board add constraint board_writer_fk foreign key(writer) 
  references member(id) on delete cascade on update cascade;
  ```

  > cascade => 참조하는 부모가 삭제되거나 수정되면 자식도 같이 삭제, 변경
  >
  > > member 테이블의 id를 참조, member 테이블의 id가 삭제 , 수정되면 board의 writer도 함께 삭제, 수정된다.



1. `servlet - context.xml`에 사용할 패키지 추가 

```xml
<context:component-scan base-package="board.spring.mybatis"/>
```

2. `web.xml`에 datasource 설정 xml 지정 

```xml
<context-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>
		/WEB-INF/spring/root-context.xml
		classpath:board/spring/mybatis/spring-mybatis.xml
		</param-value>
</context-param>
```

3. `web.xml`에 지정한 참조할 `spring-mybatis.xml`에 datasource 설정

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.3.xsd">


<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
	<property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
	<property name="url" value="jdbc:mysql://127.0.0.1:3306/memberdb"/>
	<property name="username" value="emp2"/>
	<property name="password" value="emp2"/>
</bean>

<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
	<property name="dataSource" ref="dataSource"/>
	<property name="configLocation" value="classpath:board/spring/mybatis/mybatis-config.xml" />
	<property name="mapperLocations" value="classpath:board/spring/mybatis/*-mapping.xml" />
</bean>

<bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
	<constructor-arg ref="sqlSessionFactory"></constructor-arg>
</bean>
```

> sql문이 작성되는 mapping 파일은 여러 개가 될 수 있다. 
>
> > 그래서 mapping 파일을 지정하는 태그는 s를 붙여 복수를 나타낸다. = `<mapeerLocations`
> >
> > > 패키지에 포함된 모든 mapping 파일을 참조할 시 *로 모든 파일을 표현한다.