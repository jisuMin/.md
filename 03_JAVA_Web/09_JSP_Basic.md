## :bulb: JSP

서블릿은 자바 코드를 기반으로 문자열을 사용해 HTML과 자바스크립트로 화면 구현,

반대로 **JSP는 HTML, CSS, 자바스크립트를 기반으로 화면 구현** - 재사용성과 유지관리 수월

| 서블릿 자바 문장                 | JSP 자바 문장                |
| -------------------------------- | ---------------------------- |
| src/main/java 폴더 패키지에 저장 | src/main/webapp/*.html, *jsp |



## :mag_right: JSP 구성요소

- HTML 태그, CSS, 자바스크립트 코드
- JSP 기본 태그
- JSP 액션 태그
- 커스텀 태그 





## :mag_right: JSP 페이지 구성요소 

| 태그                      | 형태 (예시)                                                  |
| ------------------------- | ------------------------------------------------------------ |
| 디렉티브 태그             | < jsp:directive >                                            |
| 스크립트 태그             | <% 자바 문장 %>                                              |
| 표현 언어 (쉽고 간결하게) | String type = request.getParameter("type");  ->$(param.type) |
| 내장 객체                 | session.setAttrubute("",객체)                                |
| 액션 태그                 | < jsp:forward page=""/>                                      |
| 커스텀 태그               |                                                              |



## :mag_right: 페이지 디렉티브 태그 

**< %@page >에 들어가는 태그**

| 속성        | 기본값      | 설명                                                         |
| ----------- | ----------- | ------------------------------------------------------------ |
| info        | 없음        | 페이지를 설명해주는 문자열 지정                              |
| language    | "Java"      | JSP 페이지에서 사용할 언어 지정                              |
| contentType | "text/html" | JSP 페이지 출력 형식 지정                                    |
| import      | 없음        | JSP 페이지에서 다른 패키지의 클래스를 임포트                 |
| session     | "true"      | JSP 페이지에서 HTTPSession 객체의 사용 여부                  |
| errorPage   | "false"     | JSP 페이지 처리 도중 예외가 발생할 경우 예외 처리 담당 페이지 지정 |
| isErrorPage | "false"     | 현재 JSP 페이지가 예외 처리 담당 JSP 페이지인지 지정         |



- JSP 사용 예시

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<h1>jsp 파일</h1>
<% String type="servlet"; %>
<h1><%=type %> 파일</h1> <!-- 변수를 출력할 땐 <%= %> 로 출력 -->
</body>
</html>
```