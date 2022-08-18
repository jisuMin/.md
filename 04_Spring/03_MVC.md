패키지 명이 a.b.test이면 실행시 url =localhost:8080/test/...

web project settings -> context root를 바꿔주면 됨

or

server.xml의 path 변경 (docBase=project name)

```xml
<Context docBase="second" path="/mvc" reloadable="true" source="org.eclipse.jst.jee.server:second"/>
```



post로 넘길 때 DispatcherServlet 한글 깨짐 설정

doPost 서블릿 : request.setCharacterEncoding("utf-8")

모든 controller에 적용하는 방법 = web.xml에 추가 

resurce에 들어간건 빼고 나머지 js,dispatcherServlet등  웹 요청이 되면 모든 url에 encoding 필터 적용 = utf-8로 변경

