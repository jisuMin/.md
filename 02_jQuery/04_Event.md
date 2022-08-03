##  :bulb:click 이벤트

- 클릭했을 때의 동작을 설정한다.

```html
<script>
$(document).ready(function(){
	//h1태그이면서 아이디가 first 인 것 
	$('h1#first').click(function(){
    $('h1#first').css("width","300"); // 클릭 영역 설정 
		$("div#last").html( $('h1#first').html() ); //h1 태그 내부에 있는 값을 읽어와 div에 삽입 
	});
});

</script>

<body>
<h1 id="first"> 클릭해보세요. </h1>
<div id="last"></div>
</body>
```

h1 태그를 (클릭해보세요.)를 클릭하면 div의 클릭해보세요.가 나타난다.



## :mag_right: 이벤트 연결 메서드 사용

- 이벤트 연결과 제거 메서드

| 메서드 | 설명        |
| ------ | ----------- |
| on()   | 이벤트 연결 |
| off()  | 이벤트 제거 |

- **이벤트 연결** - on 메서드 사용 

```html
<script>
$(document).ready(function(){
	$('h1#first').on('click',function(){
		$('h1#first').css("width","300");
		$("div#last").html( $('h1#first').html() );
	});
});

</script>

<body>
<h1 id="first"> 클릭해보세요. </h1>
<div id="last"></div>
</body>
```

- **이벤트 제거** - off 메서드 사용

```html
<script>
$(document).ready(function(){
	$('h1#first').on('click',function(){
		$('h1#first').css("width","300");
		$("div#last").append( $('h1#first').html() ); //append를 사용해 '클릭하세요' 무한 출력
	});
	
	$('input:button').on('click',function(){
			$('h1#first').off('click');	// 무한 출력되는 '클릭하세요' 종료 
		});
	
});

</script>
</head>
<body>
<h1 id="first"> 클릭해보세요. </h1>
<input type="button" value="이벤트 멈춤">
<div id="last"></div>
```



## :mag_right: 복합 이벤트 연결

- 이벤트들을 객채로 선언하여 복합 연결이 가능하게 한다.

```html
<script>
	$('div#box').on(
		{
			click : function(){
				$(this).css("background-color","red");
			},
			mouseenter : function(){
				$(this).css("background-color","green");
			},
			mouseleave : function(){
				$(this).css("background-color","blue");
			}
		}
	);
});

</script>
<body>
<div id = "box"></div>
</body>
```

