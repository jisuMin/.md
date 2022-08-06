## :bulb: 웹 브라우저에서 서블릿으로 데이터 전송하기



## :mag_right: GET/POST 전송 방식

- ```plaintext
  GET
  ```

  전송 방식

  - 서블릿에 데이터를 전송할 때는 데이터가 URL 뒤에 `name=value` 형태로 전송됨
  - 여러 개의 데이터를 전송할 때는 `&` 로 구분해서 전송
  - 보안이 취약
  - 전송할 수 있는 데이터는 최대 255자
  - 기본 전송 방식이고 사용이 쉬움
  - 웹 브라우저에 직접 입력해서 전송할 수도 있음

- ```plaintext
  POST
  ```

   전송방식

  - 서블릿에 데이터를 전송할 떄는 TCP/IP 프로토콜 데이터의 HEAD 영역에 숨겨진 채 전송
  - 보안에 유리
  - 전송 데이터 용량이 무제한
  - 전송 시 서블릿에서는 또다시 가져오는 작업을 행 하므로 처리 속도가 GET 방식보다 느림



## :mag_right: GET 방식 예제

- `<form>` 태그의 `method` 속성을 `get`으로 설정하면 GET 방식으로 데이터를 전송하겠다는 뜻
  - GET이나 POST 를 작성하지 않은 경우 기본은 GET
- 서블릿에선 `doGet()` 메서드를 이용해서 전송된 데이터를 처리

```html
<form action="Calc" method="get">
```

- URL 뒤에 데이터가 붙는 것을 확인![스크린샷 2022-08-06 오후 4.14.58](https://github.com/jisuMin/.md/blob/master/03_JAVA_Web/Images/method_get.png)



## :mag_right: POST 방식 예제

- `<form>` 태그의 `method` 속성을 `get`으로 설정하면 GET 방식으로 데이터를 전송하겠다는 뜻

```html
<form action="Calc" method="post">
```

- URL 뒤에 아무 데이터도 나타나지 않는다.

![스크린샷 2022-08-06 오후 4.17.16](https://github.com/jisuMin/.md/blob/master/03_JAVA_Web/Images/method_post.png)