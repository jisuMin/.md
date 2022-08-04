## :bulb: Servlet 세 가지 기능

1. 클라이언트로부터 요청을 받는다.
2. 데이터베이스 연동과 같은 비즈니스 로직을 처리한다.
3. 처리된 결과를 클라이언트에 돌려준다.



## :mag_right: `<form>` 태그 이용해 서블릿에 요청하기

- <form> 태그로 서블릿에 요청하는 과정

```html
<form action="register" >
	사용자명 <input type=text name="name"><br>
	과정명<input type=text name="subject" >
	<input type=submit value="등록">
</form>
```

1. 사용자가 사용자명과 과정명을 입력한 후  “등록”을 클릭
2. `<form>` 태그의 `action` 속성으로 데이터를 전송할 서블릿이나 JSP 지정
3. 지정된 이름인 `register` 서블릿으로 사용자명과 과정명이 전송된다.



## :mag_right: 서블릿에서 클라이언트의 요청을 얻는 방법

- `<form>` 태그로 전송된 데이터를 받아오는 메서드

  - **`String getParameter(String name)`**
    - `name` 의 값을 알고 있을 때 그리고 `name`에 대한 전송된 값을 받아오는 데 사용

  - **`String[] getParameterValues(String name)`**
    - 같은 `name`에 대해 여러 개의 값을 얻을 때 사용

  - **`Enumeration getParameterNames()`**
    - `name` 값을 모를 때 사용
    - 전송된 모든 `name`과 값을 가져옴

## :mag_right: String getParameter(String name) 사용

- `register.html`

```html
<script>
$(document).ready(function(){
	
	});
</script>
</head>
<body>
<form action="register" >
사용자명 <input type=text name="name"><br>
과정명
<select name="subject" multiple="multiple">
	<option>ai</option>
	<option>안드로이드</option>
	<option>스프링</option>
	<option>db</option>
	<option>빅데이터</option>	
	<option>보안</option>
</select>


<input type=submit value="등록">
</form>
</body>
</html>
```

- `RegisterServlet.java`

```java
public class RegisterServlet extends HttpServlet {
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// 사용자 요청 받아오기
		//HttpServletRequest - http요청정보객체 , 
		// <form action="/register">
		// <input type=text name="id" >
		// <input type=submit value="" >
		String name = request.getParameter("name");
		String subject[] = request.getParameterValues("subject");
		if(name == null || name.equals("") ) { 
			name = "입력되지 않은 사용자 "; 
		}
		if(subject == null || subject.length == 0) { 
		   subject[0] = "선택하지 않으셨습니다 "; 
		}
		// 처리 결과- 자바 구현-파일 입출력 , jdbc 
		
		//HttpServletResponse - http응답가능객체
		// 결과 응답= 서버 출력(클라이언트 입력)
		// 브라우저 인코딩 - 서블릿 인코딩
		response.setContentType("text/html;charset=utf-8");
		PrintWriter out = response.getWriter();
		
		System.out.println();
		out.println("<h1> " + name + " 회원님 ");
		//반복문
		for(int i = 0; i < subject.length; i++) {
			out.println( subject[i] + " ");
		}
		out.println(" 과정을 선택하셨습니다 </h1>"); 
	}

}
```

- 결과 

![스크린샷 2022-08-04 오후 11.58.47](https://github.com/jisuMin/.md/blob/master/03_JAVA_Web/Images/register_html.png)

- 등록 버튼 클릭 -> RegisterServlet으로 전송

​	![스크린샷 2022-08-05 오전 12.00.47](https://github.com/jisuMin/.md/blob/master/03_JAVA_Web/Images/register_sv.png)