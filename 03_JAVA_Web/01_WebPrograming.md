## :bulb:웹 기반 프로그램

- 클라이언트
  - 사용자의 웹 브라우저를 통해 화면에 해당되는 HTML 문서를 서버에 요청함
  - 자신이 사용하는 클라이언트 프로그램을 직접 설치하는 것이 아니다.
- 서버
  - 요청받은 HTML 문서를 브라우저에 전송하여 해당 기능을 담당하는 화면을 보여줌
- 동작 과정
  1. 브라우저에서 처리할 데이터를 입력받아 서버에 처리를 요청
  2. 서버는 화면에서 입력한 데이터를 전송받아 처리
  3. 계산 결과를 웹 브라우저로 전송하여 결과를 보여준다.
- 사용자가 사용하는 프로그램의 기능이나 화면이 바뀌면 서버에서 모두 처리



## :bulb:웹 프로그래밍과 JSP



## :mag_right: 정적 웹 프로그래밍

- 정적(static) 웹 프로그래밍

  - 웹 서버에 미리 보여줄 HTML 페이지, CSS, 이미지, 자바스크립트 파일을 **저장해 놓고** 브라우저에서 요청할 경우 그대로 전달하는 방식

  - 사용자는 페이지가 변경되지 않고 한 **고정된 웹 페이지**를 보게 됨

  - 구성 요소

    - 웹 서버 : 각 클라이언트에게 서비스를 제공하는 컴퓨터

    - 클라이언트 : 네트워크 서버에 접속한 후 서버로부터 서비스를 제공받는 컴퓨터를 의미

    - HTTP 프로토콜

      - Hyper Text Trasfer Protocol

      - `www` 서비스를 제공하는 통신규약을 의미
      - 웹 서버와 클라이언트는 이 프로토콜을 통해 정보를 주고 받는다.

    - HTML

      - Hyper Text Markup Language: `www` 서비스를 제공하기 위한 표준 언어

    - 자바스크립트 : HTML 웹 페이지의 여러가지 동적인 기능을 제공하는 스크립트 언어

    - CSS(Style Sheet) : HTML 문서에서 서체나 책상, 정렬 등 세부적인 HTML 페이지의 디자인에 관련된 여러가지 기능을 제공

  - 특징

    - 사용자에게 화면 디자인 같은 **고정된 정보만 제공**
    - 정보 수정 시 **관리자가 직접 HTML 소스를 수정**하여 사용자에게 정보를 제공



## :mag_right: 동적 웹 프로그래밍

- CGI

  - Common Gate Interface
  - 공용 게이트웨이 인터페이스
  - 초기 웹 프로그램에서 사용하는 방식
  - 프로세스 방식으로 실행
  - 같은 기능을 수행하더라도 각 경우에 대해 처음부터 메모리에 기능(프록세스)을 로드(load)하여 수행해야함
  - 서버의 부하가 심함
  - 동작 방식
    1. 클라이언트1 정보를 요청
    2. 서버는 프로세스를 메모리에 생성
    3. 데이터베이스와 연동하여 로직 수행 후 클라이언트에게 정보 반환
    4. 클라이언트2 동일한 정보를 요청
    5. 클라이언트1과 **같은 정보를 요청하더라도 서버는 메모리에 또 프로세스를 생성**해서 정보 반환
  - CGI 의 문제점을 보완하여 나온 것
    - JSP, ASP, PHP 등의 동적 웹 프로그래밍 기술

- **JSP**

  - 스레드(thread) 방식
  - 동작 방식
    1. 클라이언트1 정보를 요청
    2. 서버는 기능을 메모리에 로드한 후 정보를 얻어와서 클라이언트에 반환
    3. 클라이언트2가 동일한 정보를 요청
    4. 기존의 기능이 메모리에 존재하므로 **따로 로드하지 않고 기능 수행**
  - 특징
    - 프로세스 방식이 아닌 **스레드 방식으로 실행**
    - 클라이언트의 요구를 처리하는 기능은 **최초 한번만 메모리에 로드** 된다.
    - 클라이언트가 동일한 기능을 요구하면 기존에 사용한 기능을 **재사용**한다.

  

## :mag_right: 웹 어플리케이션

- 기존의 정적인 웹 어플리케이션의 기능을 그대로 사용하면서 서블릿,  JSP,  JAVA 등을 추가하여 **동적인 서비스를 제공**하는 프로그램

- 기본 구조

  - 웹 컨테이너에서 실행하는 웹 어플리케이션의 기본 디렉토리 구조

  

  > **컨테이너**
  >
  > - Java 서블릿과 상호작용하는 WAS의 구성요소
  > - WAS 내부에서 개발자 대신 서블릿을 관리

  

  | 구성요소 | 기능                                                         |
  | -------- | ------------------------------------------------------------ |
  | webShop  | - 웹 어플리케이션의 root 디렉터리                                                                                                              - 다른 웹 어플리케이션 이름과 중복을 허용하지 않음                                                                             -  JST, HTML 파일이 저장됨 |
  | WEB-INF  | - 웹 어플리케이션에 관한 정보가 저장되는 곳                                                                                     - - 외부에서 접근할 수 없음 |
  | classes  | - 웹 어플리케이션이 수행하는 서블릿과 다른 일반 클래스들이 위치하는 곳 |
  | lib      | - 웹 어플리케이션에서 사용되는 여러 가지 라이브러리 압축 파일(`jar` 파일)이 저장되는 곳                   - DB 연동 드라이버나 프레임워크 기능 관련 `jar` 파일이 여기에 저장됨                                                -  `lib` 디렉터리의 `jar` 는 클래스패스가 자동으로 설정됨 |
  | web.xml  | - 배치 지시자(deployment descriptor)로서 일종의 환경 설정 파일                                                     - 웹 어플리케이션에 대한 여러가지 설정을 할 때 사용 |



## :mag_right: 컨텍스트

- `server.xml` 에 등록하는 웹 어플리케이션

- 톰캣 입장에서 인식하는 한 개의 웹 어플리케이션

- 컨테이너 실행 시 하나의 컨텍스트가 생성

- 컨텍스트 이름은 웹 어플리케이션 이름과 같게 만드는 것이 일반적

- 주요 특징

  - 웹 어플리케이션당 하나의 컨텍스트가 등록된다.
  - 웹 어플리케이션 이름과 같을 수도 있고 다를 수도 있다.
  - 컨텍스트 이름은 중복되면 안된다.
  - 웹 어플리케이션의 의미를 가장 잘 나타낼 수 있는 명사형으로 지정

  - 대소문자를 구분

  - `server.xml`에 등록

- **server.xml에 컨텍스트 등록 ** 

```plaintext
<Context path ="/컨텍스트 이름"   
		docBase="실제 웹 어플리케이션의 WEB-INF 디렉터리 위치"          
		reloadable="true 또는 false" />
```

- **<Context>** 태그 구성 요소 기능

  ```plaintext
  path
  ```

  - 웹 어플리케이션의 컨텍스트 이름
  - 웹 어플리케이션 이름과 다를 수도 있다.
  - 웹 브라우저에서 실제 웹 어플리케이션을 요청하는 이름

  ```plaintext
  docBase
  ```

  - 컨텍스트에 대한 실제 웹 어플리케이션이 위치한 경로
  - `WEB-INF` 상위 폴더까지의 경로를 나타낸다. _ `reloadable`
  - 실행 중 소스 코드가 수정될 경우 바로 생신할지를 설정한다.
  - `false` 로 설정하면 톰캣을 다시 실행해야 추가한 소스 코드의 기능이 반영된다.

  ```plaintext
  reloadable
  ```

  - 실행 중 소스코드가 수정될 경우 바로 갱신할지 결정 
  - `false`로 설정하면 톰캣을 다시 실행해야 추가한 소스 코드의 기능이 반영된다.



## :mag_right: 톰캣 컨테이너에서의 웹 어플리케이션 동작 과정

1. 웹 브라우저에서 컨텍스트 이름으로 요청한다.
2. 요청을 받은 톰캣 컨테이너는 요청한 컨텍스트 이름이 `server.xml`에 있는지 확인한다.
3. 해당 컨텍스트 이름이 있으면 컨텍스트 이름에 대한 실제 웹 애플리케이션이 있는 경로로 가서 요청한 화면을 클라이언트 웹 브라우저로 전송한다.
4. 웹 브라우저는 전송된 화면을 브라우저에 나타낸다.

 **등록되어 있지 않은 컨텍스트 이름으로 요청하면 `404` 오류가 발생한다.**



# :mag_right: 배치

- 웹 어플리케이션을 실제로 서비스 하는 것
- 개발을 마친 후 프로젝트를 `war` 파일로 압축 후 FTP 를 이용해 리눅스나 유닉스 같은 운영서버에 업로드
- 텔넷(telnet)을 통해 `bin` 폴더의 `Tomcat.exe`를 다시 실행하면 톰캣 실행 시 `war` 파일의 압축이 해제됨과 동시에 자동으로 등록되어 웹 애플리케이션이 실행된다.