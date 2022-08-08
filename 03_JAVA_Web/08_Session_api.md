## :bulb:세션을 이용한 웹 페이지 연동

**웹 페이지들 사이의 공유 정보를 서버의 메모리에 저장해 놓고 사용** : 브라우저를 닫으면 저장 정보가 사라진다.

> 쿠키 : 클라이언트에 저장 



## :mag_right: 세션 API

- 서블릿에서 세션을 이용하려면 HttpSession 클래스객체를 생성해서 사용

  - `getSession();` 메서드를 호출해서 생성 

  - ```java
    HttpSession session = request.getSession();
    // 브라우저에서 최초 요청인 경우 -해당 클라이언트의 세션 객체 생성(저장 정보x), 클라이언트에게 세션id 부여
    ```

- session 확인 : sessionid 공유(같은 브라우저에서 실행)

  - `AServlet`  

```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		
		HttpSession session = request.getSession();
		String sessionid = (String)session.getAttribute("sessionid");
		
		response.setContentType("text/html;charset=utf-8");
		PrintWriter out = response.getWriter();
		out.print("<h1> AServlet에서 사용 "+sessionid + "</h1>");
	}

}
```

![스크린샷 2022-08-08 오후 5.19.58](../../../../Library/Application Support/typora-user-images/스크린샷 2022-08-08 오후 5.19.58.png)

- 브라우저가 닫기 전 30분 동안 액션 없으면 정보 삭제 : `servers/../web.xml`

```java
  <session-config>
        <session-timeout>30</session-timeout> //30분동안 동작 없을 경우, 시간 수정 가능
   </session-config>
```

- 세션 연결 시간 Servlet에서 초 단위로 설정 - 유효시간 설정 

```java
session.setMaxInactiveInterval(5); // 세션의 유효시간을 5초로 설정 
```



## :mag_right: 세션 삭제 

- 세션 Attribute 별 삭제 : **세션 연결을 삭제하는 것이 아닌, 정보를 삭제**

``` java
session.setAttribute("name","spring");
session.setAttribute("cart","computer");

session.removeAttribute("cart") // 세션 id가 cart인 것만 삭제, named은 세션에 남아있음
```

- 세션 무효화 (소멸) 

```java
session.invalidate();
```