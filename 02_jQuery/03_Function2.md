## :bulb: 내부 글자 조작 함수

- **종류**

| 메서드 | 설명                            |
| ------ | ------------------------------- |
| html() | 문서 객체 내부의 HTML 태그 조작 |
| text() | 문서 객체 내부의 글자 조작      |



## :mag_right: html() 함수 사용

- id가 contents인 html 태그인 `<input type="text" value="jquery">`를 `<input type= password value='1234'>`로 조작한다.	
- 기존의 것이 없어지고 html() 부분으로 대체 된다.

```html
<script>
$(document).ready(function(){
	
	$('#contents').html("<input type= password value='1234'>");
});
</script>
<body>
<div id="contents">
	<input type="text" value="jquery"><br>
</div>
</body>
```



## :mag_right: text() 함수 사용

- Text() 는 다 문자열로 해석한다

``` html
<script>
$(document).ready(function(){
	
	$('#contents').text("<input type= password value='1234'>");
});
</script>
<body>
<div id="contents">
	<input type="text" value="jquery"><br>
</div>
</body>
```

>  결과 : `<input type= password value='1234'>`



## :mag_right: append() 함수 사용

- 기존의 것을 유지하고, append() 부분을 추가한다.

```html
<script>
$(document).ready(function(){
	
	$('#contents').append("<input type= password value='1234'>");
});
</script>
<body>
<div id="contents">
	<input type="text" value="jquery"><br>
</div>
</body>
```



## :bulb: 클래스 조작 함수

- 클래스 조작 메서드 종류

| 메서드        | 설명             |
| ------------- | ---------------- |
| addClass()    | 클래스 추가 함수 |
| removeClass() | 클래스 제거 함수 |
| toggleClass() | 클래스 전환 함수 |

## :mag_right: addClass()

```html
<script>
$(document).ready(function(){
	$('h1').addClass("a"); // h1 태그에 a 라는 이름의 클래스 추가
  $('h1').addClass("box"); // h1 태그에 box 라는 이름의 클래스 추가
});

</script>
<style>
.a {
	color:red;
	background-color: green;
}

.box{
	width:200px;
	height:200px;
	border: 2px solid navy;
}
</style>
<body>
<h1> 클래스 속성을 제어합니다. </h1> 
<h2> addClass 함수를 공부합니다. </h2>
<h3> removeClass 함수도 공부합니다. </h3>
</body>
```

- h1 태그에 a, box 클래스를 추가하였기 때문에 a,box 클래스에 대한 스타일이 h1에 적용된다.

 

## :mag_right: removeClass()

```html
<script>
$(document).ready(function(){
	$('h1,h3').addClass("a"); // h1과 h3 태그에 a 라는 이름의 클래스 동시에 추가
  $('h1').removeClass("a"); // h1 태그에 a 라는 이름의 클래스 삭제
});

</script>
<style>
.a {
	color:red;
	background-color: green;
}

.box{
	width:200px;
	height:200px;
	border: 2px solid navy;
}
</style>
<body>
<h1> 클래스 속성을 제어합니다. </h1> 
<h2> addClass 함수를 공부합니다. </h2>
<h3> removeClass 함수도 공부합니다. </h3>
</body>
```

- h1과 h3에 a라는 클래스를 추가한 후, h1의 a 클래스를 삭제하여 h1에 a 스타일이 적용되지 않는다.