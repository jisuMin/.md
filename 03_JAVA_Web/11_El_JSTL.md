## :bulb: 표현언어 = Expression Language = EL



## :bulb: JSP 표준 태그 라이브러리 = JSTL

**커스텀 태그**(자주 사용하는 자바 코드를 대체하는 태그) 중 **가장 많이 사용되는 태그를 표준화하여 라이브러리로 제공**

- http://mvnrepository.com 에 접속해 사용할 JSTL jar 파일 다운받기 

![스크린샷 2022-08-12 오전 11.19.49](../../../../Desktop/스크린샷 2022-08-12 오전 11.19.49.png)



- 사용할 project -> webapp/WEB-INF/lib 폴더에 jar파일 추가

![스크린샷 2022-08-12 오전 11.25.31](../../../../Library/Application Support/typora-user-images/스크린샷 2022-08-12 오전 11.25.31.png)



## :mag_right: Core 태그 라이브러리 사용하기

- jsp 페이지 상단에 디렉티브 태그 추가하기

```jsp
<%@ taglib prefix ="c" uri="http://java.sun.com/jsp/jstl/core" %>
```



#### 1. `<c:set>` 태그 이용해보기 : JSP 페이지에서 변수를 지정하는 기능 

- 출력해보기! : el를 이용하여 출력 

```jsp
<c:set var="id" value="jstl"/>
<h1>${id}</h1>
```

> `<% String id = "jstl"; %>` 과 같은 의미 
>
> > **c태그를 사용하는 이유 => el로 바로 출력이 가능하다.**

- 다른 속성(jsp)의 값을 value 값으로 지정해 el로 출력하기 

```jsp
<% String id2 = "jsp"; %>
<c:set var="id2" value="<%=id2 %>"/>
<h1>${id2 }</h1>
```

> jsp 출력

- el 태그를 value로 사용해보기

```jsp
<c:set var="pw" value="100"/>
<%-- jsp에서는 정수도 ""안에 선언, pw가 숫자만 있으면 알아서 정수로 취급  --%>

<c:set var="result" value="${pw+200 }"/>

<h1>${result }</h1>
```

> 300 출력 

- out 태그를 사용하여 출력하는 방법 

```jsp
<c:set var="i" value="100"/>
<c:out var="i"/>
```

> 출력 100
>
> > out을 이용해 출력할 수 있지만 더 간단하게 출력할 수 있는 el를 더 많이 사용함



**이처럼 JSP, JAVA, el 등 여러가지 언어를 이용해 변수 선언 시 원활한 출력을 위해 < c:set > 태그를 이용한다. **



#### 2. `<c:remove>` 태그 이용해보기 : c 태그로 만들어진 변수값 삭제 

```jsp
<c:set var="id2" value="<%=id2 %>"/>
<h1>${id2 }</h1>

<c:remove var="id2"/>
```

> remove 태그엔 value 속성을 주지 않아도 됨. set 태그로 만들어진 메모리에 저장된 변수값을 삭제함





#### 3. `c:if` 조건문 태그 

- **id2 변수가 존재한다면( 비어있지 않으면 )  **id2 값 출력 = 200

```jsp
<c:set var="id2" value="200"/>
<c:if test="${!empty id2 }">
	<h1>${id2}</h1>
</c:if>
```

- 자바 문장 삽입 가능 : **10이 5보다 크면 **10>5 출력

```jsp
<c:if test="<%= 10>5 %>">
	<h1>10>5</h1>
</c:if>
```

- `c:if`에는 else가 없어 조건을 하나씩 명시 해줘야함. :이름과 나이를 전달받아 구분

```jsp
<c:if test="${!empty param.name || !empty param.age}">
	<c:if test="${param.age >=20 }"> <h1>${param.name }님 성인인증 되었습니다.</h1></c:if>
	<c:if test="${param.age >=17 && param.age<=19 }"> <h1>${param.name }님 고등학생입니다.</h1></c:if>
	<c:if test="${param.age >=1 && param.age<=16 }"> <h1>${param.name }님 중학생 이하 입니다.</h1></c:if>
	<c:if test="${param.age <=0 }"> <h1>잘못된 나이입니다.</h1></c:if>
</c:if>
```



#### 4. `< c:choose >` swtich 기능의 태그

- **switch-case 처럼 < c:choose >엔 < c:when >이 필요하다**
- 위에 나이를 구분하는 < c:if > 예제를 < c:choose>로 구현해보기

```jsp
<c:set var="pname" value="${param.name }"/>
<c:set var="page" value="${param.age}"/>
<c:if test="${empty pname || empty page}">
<c:choose>
	<c:when test="${page >=20 }"><h1 style="color:blue">${pname }님 성인인증 되었습니다.</h1></c:when>
	<c:when test="${page >=17 && page<=19 }"><h1 style="color:green">${pname }님 고등학생입니다.</h1></c:when>
	<c:when test="${page >=1 && page<=16 }"><h1 style="color:black">${pname }님 중학생 이하입니다.</h1></c:when>
	<c:otherwise><h1 style="color:red">잘못된 나이입니다.</h1></c:otherwise>
</c:choose>
</c:if>
```

> param.name과 param.age를 계속 사용해야 하기 때문에 편리성을 위해 set태그를 이용해 변수로 지정했다.
>
> > name과 age값이 있을 때만 choose문을 실행한다.
> >
> > > switch에서 **default기능을 하는 otherwise**를 사용해 나머지의 값을 처리해준다.
> > >
> > > > 각 case를 when으로 처리한다.





#### 5. `<c:forEach>` 반목문 태그

```jsp
<c:forEach var="변수이름" items="반복할객체이름" var="출력할때 사용할 변수 이름">
	실행문
</c:forEach>
```

- 배열(array) 출력 해보기 - `items` 사용

```jsp
<%
String array[] = {"red","black","white","green","blue"};
%>
<c:set var="colors" value="<%=array %>"/>

<c:forEach items="${colors }" var="onecolor" varStatus="vs">
	<h1>${vs.index} : ${onecolor }</h1>
</c:forEach>
```

 **items = "객체이름" : 객체 갯수만큼 반복** 

> varStatus = 반복상태 속성 ( .index / .count 키워드 )

- begin, end, step 등 상태 속성들도 존재. 생략 가능

```jsp
<c:forEach var="i" begin="2" end="10" step="2">
	<h1>${i }</h1>
</c:forEach>
```

