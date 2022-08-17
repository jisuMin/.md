## :bulb: aspectj weaver 라이브러리 추가

- 프로젝트`pom.xml` 의 `<dependencies></dependencies>` 사이에  [MVN](https://mvnrepository.com)에서 찾은 maven을 추가한다.

> 소스만 추가해도 라이브러리가 자동으로 다운로드 되는 것을 확인할 수 있다. 

```xml
<!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.9.1</version>
    <scope>runtime</scope>
</dependency>

```

- 다운로드 확인

`Maven Dependencies` 항목에 추가된 것을 확인할 수 있다.  ![스크린샷 2022-08-17 오후 1.35.04](../../../../Library/Application Support/typora-user-images/스크린샷 2022-08-17 오후 1.35.04.png)



- 핵심관심 구현 클래스 객체 생성 `aop1.xml`