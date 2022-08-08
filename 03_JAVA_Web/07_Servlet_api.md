

## :bulb: dispatch를 이용한 포워딩

**클라이언트의 웹 브라우저를 거치지 않고 바로 서버에서 포워딩 진행** 

>  같은 서버 안에 서블릿끼리 같은 작업을 분담하여 진행  (요청 / 응답)



## :mag_right: 바인딩

**브라우저에서 전달 받은 request를 서블릿에서 다른 서블릿으로 전달**

| 메서드                                   | 기능                                                |
| ---------------------------------------- | --------------------------------------------------- |
| setAttribute(String name, Object object) | 자원(데이터)를 각 객체에 바인딩(전달)               |
| getAttribute(String name)                | 각 객체에 바인딩된 자원(데이터)를 name으로 가져온다 |



- `forwardTest1.java`

```java
@WebServlet("/forward1")
public class ForwardTest1 extends HttpServlet {
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String id = request.getParameter("id");
		id = id.toUpperCase();
		request.setAttribute("upperid", id); // 바인딩 
		RequestDispatcher rd = request.getRequestDispatcher("forward2"); // 포워드
		rd.forward(request, response);
		/*response.setContentType("text/html;charset=utf-8");
		PrintWriter o = response.getWriter();
		o.print(id+"회원님 반갑습니다.");*/ //주석처리된 부분을 forwarding 
	}

}

```

- `forwardTest2.java`

```java
@WebServlet("/forward2")
public class ForwardTest2 extends HttpServlet {
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String id = (String)request.getAttribute("upperid"); //바인딩
    //getAttribute로 가져오는 값이 object이기 때문에 형변환 
		response.setContentType("text/html;charset=utf-8");
		PrintWriter o = response.getWriter();
		o.print(id+"회원님 반갑습니다.");
	}

}

```

- 결과 
  - 출력은 `forwardTest2` 에서 했지만 url를 보면 이동을 하지 않았음을 확인할 수 있다.

![스크린샷 2022-08-08 오후 3.23.21](../../../../Library/Application Support/typora-user-images/스크린샷 2022-08-08 오후 3.23.21.png)



> 이떄 응답 역할을 하는 파일 `forwardTest2` 를 먼저 실행할 수 없다. 
>
> > 넘어오는 값이 없기 때문 