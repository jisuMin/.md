

## :bulb: jQuery 란?

**무료로 사용 가능한 오픈 소스 라이브러리**



## :mag_right: 사용 목적

1. 쉬운 문서 객체 모델과 관련한 처리 구현
2. 쉽고 일관적인 이벤트 처리
3. 쉬운 시각적 효과 구현
4. 쉬운 Ajax 응용 프로그램 개발



![스크린샷 2022-08-03 오전 9.55.03](../../Library/Application Support/typora-user-images/스크린샷 2022-08-03 오전 9.55.03.png)



**Pattern에 아래 내용을 수정(추가)하여 파일을 새로 생성했을 때 자동완성이 가능하도록 한다.**

``` javascript
<script src="js/jquery-3.6.0.min.js"></script>
<script>
$$(document).ready(function(){

});
```



## :mag_right: 사용 방법 (jQuery 문법)

$ (**선택자**) .메서드(**매개변수, 매개변수**)

- **id가 a**인 것의 배경색상을 빨간색으로 설정

```html
<script>
$(document).ready(function(){
	$("#a").css("background-color","red");
});
</script>
```

- **tag가 h1**인 것들을 모두 색상을 파란색으로 설정

```html
<script>
$(document).ready(function(){
	$("h1").css("color", "blue");
});
</script>
```

- **h1 태그 중 처음, 마지막** 만 색상 빨간색으로 설정

```html
<script>
$(document).ready(function(){
	$("h1:first").css("color", "blue"); // h1 태그 중 첫 번째 
  $("h1:last").css("color", "blue"); // h1 태그 중 마지막 
});
</script>
```

- **클래스 이름이 red**인 것의 색상을 빨간색으로 설정 

```html
<script>
$(document).ready(function(){
	$(".red").css("color", "red");
});
</script>
```

- 두 가지 tag, **h1과 td 태그** 색상을 노란색으로 설정

```html
<script>
$(document).ready(function(){
	$("h1,td").css("color", "yellow");
});
</script>
```

- **input 태그, 타입은 text** 인 것의 색상을 빨간색으로 설정

```html
<script>
$(document).ready(function(){
	$("input:text").css("color", "yellow");
});
</script>
```

 ... 등 여러가지 표현을 사용할 수 있다.

- 태그 범위 - 조건해당 

```html
<script>
$("input[type^=te]").css("color", "yellow"); // te 라는 문자로 시작
$("input[type$=l]").css("color", "yellow"); // ㅣ이라는 문자로 종료 
$("input[type*=e]").css("color", "yellow"); // e 라는 문자 포함
</script>
```

- 위치 - 조건 해당

```html
<script>
$("tr:eq(3) td").css("color", "red"); // 3번째 줄만 빨간색 
$("tr:gt(3) td").css("color", "blue"); // 3번째 줄보다 큰 범위 모두 파란색
$("tr:lt(3) td").css("color", "green"); // 3번째 줄보다 작은 범위 모두 초록색 
</script>
```