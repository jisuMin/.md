## :bulb: AOP (Aspect oriented programing) = 관심지향

**메서드 안의 주기능과 보조 기능을 분리한 후 선택적으로 메서드에 적용하는 개념** 

- 클래스가 여러개, 메소드도 여러개일 때 공통되는 내용이 있다면 공통되는 내용을 따로 클래스를 만들어 처리하는 방식

- 공통되는 내용을 **공통관심**이라 하며 보조 기능을 하는 내용을 **핵심관심**이라고 한다.
  -  aspect 클래스 = 공통관심 = 횡단관심
  - Target 클래스 = 핵심관심 = 종단관심



## :mag_right: aspectj weaver 라이브러리 추가

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

```xml
<aop:config>
	<aop:pointcut expression="execution(public * *.*.login(..))" id="pc"/>
	<aop:aspect id="aopaspect" ref="common"> <!-- common을 공통관심으로 사용 -->
		<aop:before method="a" pointcut-ref="pc"/>
		<aop:after method="b" pointcut-ref="pc"/>
	</aop:aspect> 
</aop:config>
```

- pointcut = target 클래스에 aspect 를 적용하는 대상과 시점 지정 
  - *(modifier* 리턴타입 패키지명*.*클래스명*.*메소드명*(..)*
    - \* : 모든 패키지, 클래스, 메소드 ...
    -  (..) : 모든 매개변수
    -  .. : 하위패키지 포함