## :bulb: Servlet 이란?

:grey_exclamation: 서버 쪽에서 실행되면서 클라이언트의 요청에 따라 동적으로 서비스를 제공하는 **자바 클래스**

:grey_exclamation: 자바로 작성되어 있으므로 자바의 일반적인 특징을 모두 가진다.

:grey_exclamation:  일반 자바 프로그램과 다르게 **독자적으로 실행되지 못하고** 톰캣과 같은 JSP/Servlet 컨테이너에서 실행된다.

:grey_exclamation: Servlet 동작 과정

		1. 사용자 정의 서블릿 클래스 생성
		1. 서블릿 생명주기 메서드 구현
		1. 서블릿 매핑 작업
		1. 웹 브라우저에서 서블릿 매핑 이름으로 요청하기



## :mag_right: 1. Servlet 클래스 생성 

![스크린샷 2022-08-04 오후 4.02.22](https://github.com/jisuMin/.md/blob/master/03_JAVA_Web/Create%20Servlet.png)



## :mag_right: 2. 생명주기 메서드 구현

- 서블릿 실행 단계마다 호출되어 기능을 수행하는 콜백 메서드 : ex) `doGet()`
- 서블릿도 자바 클래스이므로 실행하면 초기화 가정 그리고 메모리에 인스턴스를 생성하여 서비스를 수행한 후 다시 소멸하는 과정을 거침
- 이 단계를 거칠 때 마다 서블릿 클래스의 메서드가 호출되어 초기화, 데이터베이스 연동, 마무리 작업을 수행

```java
package Servelt;
public class ServletFile extends HttpServlet {
	
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.getWriter().println("<h1>title</h1>");
	}

}
```

- 메서드 종류

  - ```plaintext
    init()
    ```

    - 서블릿 요청 시 맨 처음 한 번만 호출됨 - 생략 가능 
    - 서블릿 생성 시 초기화 작업을 주로 수행
    - 실행 초기에 서블릿 기능 수행과 관련된 기능을 설정하는 용도로 많이 사용됨

  - `doGet()`
    - 서블릿 요청 시 매번 호출됨 , 필수 구현 
    - 실제로 클라이언트가 요청하는 작업을 수행함
    - 요청 할 때 마다 실행해야 할 작업 구현 

  - ```plaintext
    destroy()
    ```

    - 서블릿이 기능을 수행하고 메모리에서 소멸될 때 호출 - 생략 가능 
    - 서블릿의 마무리 작업을 주로 수행
    - 서블릿이 메모리에서 소멸될 때 여러 종료 작업을 수행

    

## :mag_right: 3. Servlet 매핑 작업

**서블릿 클래스 이름에 대응되는 새 주소로 변경하여 보안을 높이는 것**

- **Servlet 클래스 생성 시 작업**

![스크린샷 2022-08-04 오후 4.02.55](../../../../Library/Application Support/typora-user-images/스크린샷 2022-08-04 오후 4.02.55.png)

- **`web.xml`에 작업**

```java
<servlet>
 	<servlet-name>SF</servlet-name>
  <servlet-class>ServletFile</servlet-class>  	
</servlet>
  
<servlet-mapping>
  <servlet-name>SF</servlet-name>
  <url-pattern>/ServletFile</url-pattern>
</servlet-mapping>
```

- **애너테이션을 이용한 매핑** : `@WebServlet`
  - 이 애너테이션이 적용되는 클래스는 반드시 `HttpServlet` 클래스를 상속받아야한다.
  - 매핑 이름이 이미 사용된 다른 매핑 이름과 중복되지 않아야 한다. 

```java
package Servelt;

@WebServlet("/SF")
public class ServletFile extends HttpServlet {
	...
}
```