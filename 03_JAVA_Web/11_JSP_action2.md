## :bulb: useBean, setProperty, getProperty

| 이름        | 형식                | 설명                                            |
| ----------- | ------------------- | ----------------------------------------------- |
| useBean     | < jsp:useBean >     | 객체를 생성하기 위한 new 연산자를 대신하는 태그 |
| setProperty | < jsp:setProperty > | setter를 대신하는 태그                          |
| getProperty | < jsp:getProperty > | getter를 대신하는 태그                          |



## :mag_right: useBean

- MembetDTO 객체 생성 - class 작성 시 패키지명 꼭 포함시켜주기!

```jsp
<jsp:useBean id="dto" class="dto.MemberDTO"></jsp:useBean> 
```



- scope으로 간단하게 받아오기 - 공유되는 파일의 scope 값은 같아야한다.
  - scopre= requset : forward나 include로 공유하는 파일인 경우 

```jsp
<jsp:useBean id="dto" class="dto.MemberDTO" scope="request"></jsp:useBean>
```

```jsp
<%
if(request.getAttribute("dto") != null){ <%-- forward나 include -->
  MemberDTO dto = (MemberDTO)request.getAttribute("dto");
}else{
  MemberDTO dto = new MemberDTO();
}
%>
```

> 받아오는 값이 있다면 객체를 받아오고, 없다면 새로운 객체를 생성해라 



## :mag_right: setProperty

- 넘겨받는 Parameter 값을 param으로 받기 

```jsp
<jsp:setProperty property="id" name="dto" param="jisu"/>
```

- property 값과 param 값이 같을 경우 생략 가능

```jsp
<jsp:setProperty property="id" name="dto" />
```



## :mag_right: getProperty

- value 안에 getParameter로 값을 가져올 때 "" 앞에 \ 를 붙여줘야 한다. 

```jsp
<jsp:setProperty property="id" name="dto" value="<%=request.getParameter(\"id\") %>"/>
```



## :bulb: 내 정보 수정 useBean으로 생성해보기

