## :bulb: 시각효과

- 시각 효과 메서드

| 메서드          | 설명                                    |
| --------------- | --------------------------------------- |
| show(속도)      | 문서 객체가 커지며 표시                 |
| hide(속도)      | 문서 객체가 작아지며 사라짐             |
| toggle(속도)    | show() 와 hide() 를 동시에 실행         |
| slideDown(속도) | 문서 객체가 슬리아드 효과와 함께 표시   |
| slideUp(속도)   | 문서 객체가 슬리아드 효과와 함께 사라짐 |
| fadeIn(속도)    | 문서 객체가 선명해지며 표시             |
| fadeOut(속도)   | 문서 객체가 흐려지며 사라짐             |

```html
<script>

$(document).ready(function(){
	$('h1:eq(0)').hide(3000);
	setTimeout(function(){$('h1:eq(0)').show();},2000);
	$('h1:eq(1)').fadeIn(3000); //3초 동안 천천히 보여라
	$('h1:eq(1)').fadeOut(3000);//3초 동안 천천히 사라져라
	$('h1:eq(2)').slideUp(3000);
	$('h1:eq(2)').slideDown('slow');
</script>

<body>
<h1>태그 보이기 / 감추기</h1>
<h1>태그 페이드인 / 패이드 아웃</h1>
<h1>태그 슬라이드 하기 </h1>
<h1>태그 애니메이션</h1>
</body>
```



## :mag_right: 애니메이션 효과

- 사용 방법
  - `$(selector).animator(속성 객체);`
  - `$(selector).animator(속성 객체,시간);`
  - `$(selector).animator(속성 객체,시간, 콜백 함수);`



 ## :mag_right: 프레임 애니메이션

- 타이머 함수 

| 함수                    | 설명                                    |
| ----------------------- | --------------------------------------- |
| setInterval(함수, 시간) | 특정한 시간마다 함수 실행               |
| setTimeout(함수, 시간)  | 특정한 시간 후에 함수 실행              |
| clearInterval(식별번호) | setInterval() 함수로 설정한 타이머 제거 |
| clearTimeout(식별번호)  | setTimeout() 함수로 설정한 타이머 제거  |

- 프레임 애니메이션을 이용해 사람이 달리는 애니메이션을 구현할 수 있다. [예제]()



## :mag_right: 문서 객체 생성과 추가

- jQuery 문서 객체 추가 메서드

| 메서드                | 설명                        |
| --------------------- | --------------------------- |
| $(대상).prepend(객체) | 객체를 대상의 앞부분에 추가 |
| $(대상).append(객체)  | 객체를 대상의 뒷부분에 추가 |
| $(대상).before(객체)  | 객체를 대상의 앞쪽에 추가   |
| $(대상).after(객체)   | 객체를 대상의 뒷쪽에 추가   |

- 생성과 추가 연습해보기

```html
<script>
$(document).ready(function(){
	var cnt =0;
	$("#btnclick").on('click',function(){
		$("#keyout").html(++cnt + " 번 클릭했습니다. ");
		$("#newbuttons").append("<input type=button value ='새로 생성한 버튼"+cnt+"' id = 
                            'btnadd'>");
		
	});
	//새로 생성된 버튼 이벤트 처리 방법 
	$("#newbuttons").on('click',"input:button",function(){
		$("#keyout").html($(this).val());
	});
	$("#btnstop").on('click',function(){
		$("#newbuttons").empty(); // 태그 내부의 것을 지움
		$("#newbuttons").remove(); // 태그까지 제거 
		$("#btnclick").off('click'); // 더 이상 클릭 안됨 
		
	});
});

</script>

<body>
<input type=button value="클릭" id="btnclick">
<input type=button value="중단" id="btnstop">
<div id="newbuttons"></div>
<div id="keyout"></div>
</body>
```



