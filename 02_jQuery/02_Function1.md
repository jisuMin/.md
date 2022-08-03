## :bulb: 함수

`$ (선택자).함수(매개변수, 매개변수)` : 매개변수가 2개면 setter

`$ (선택자).함수(매개변수)` : 매개변수가 1개면 getter



## :mag_right: Setter 용도로 사용한 함수

```html
<script>
$(document).ready(function(){
	$("img:first").attr("src","/html/images/drinks.jpg"); //setter //첫 번째 img 태그에만 적용
	$("img").attr("width","100");
	$("img").attr("height","100");
	$("img:first").attr("alt","쥬스 사진입니다.");
});
</script>

<body>
<img> <!-- 여기에만 적용됨 -->
<img>
</body>
```

- 객체로 만들어 함수 사용

```html
<script>
	$("img:last").attr({ // 마지막 img 태그에만 적용
		src : "/html/images/americano.jpg",
		alt : "커피사진입니다.",
    width : "200",
    height : "200"
	});
	
});

</script>
<body>
<img>
<img> <!-- 여기에만 적용됨 -->
</body>
```



## :mag_right: Getter 용도로 사용한 함수

- 첫 번째 이미지의 url 출력하기

``` html
<script>
alert($('img:first').attr("src")); 
</script>
<body>
<img> <!-- 여기에만 적용됨 -->
<img>
</body>
```

- getter 용도로 쓰여지는 함수는 여러개의 태그를 선택하여도 첫 번째 태그에만 적용된다.

```html
<script>
alert($('img').attr("src")); 
// 모든 img 태그의 src를 가져오는 구문이지만, getter 용도일 경우 첫 번째 태그에만 적용된다.
</script>
<body>
<img> <!-- 첫 번째 태그에만 적용됨 -->
<img>
</body>
```

- 모든 태그에 적용하는 방법 - 1. **반복문 이용**
  - img 태그의 개수만큼 반복하기 위해 개수를 알아본다. :  `$('img').length`

```html
<script>	
for ( var i =0; i < $('img').length; i++){
	alert($('img:eq('+i+')').attr("src"));
}
</script>
```

모든 태그에 적용하는 방법 - 2. **반복문 내장 jQuery 함수 사용**

```html
<script>
$('img').each(function(index) {
		alert($("img:eq("+index+")").attr("src"));
	})
</script>
```



## :mag_right: 속성 제거

- 첫 번째 img 태그의 src 속성 제거
  - 속성 제거 함수 : `removeAttr`

```html
<script>
$('img:first').removeAttr("src");
</script>
```