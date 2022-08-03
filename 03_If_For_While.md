## :bulb: 조건문

### :mag_right: if 문

조건의 결과에 따라 블록 실행 여부가 결정된다. 중괄호 {} 블록은 여러개의 실행문을 하나로 묵기 위해 작성되는데, 실행 해야할 문장이 하나 밖에 없다면 생략 할 수도 있다. (버그 발생의 원인이 되기도 하고, 가독성을 위해 추천하지는 않는다.)

```java
int jamsu = 90;

if(jamsu >= 90) {
	System.out.prinln("점수가 90 이상이네요");
    	System.out.println("A등급입니다");
}
```

### :mag_right: if-else 문

- if 문의 조건식이 true이면 if문의 블록이 실행되고, 조건이 false라면 else 블록이 실행된다.
- 조건식의 결과에 따라 두 블록 중 한 블록의 내용만 실행되고 전체 if 문을 벗어나게 되는 것이다.
- 단순 else에는 조건이 붙지 않는다 (조건을 걸 수 없다)

```java
int jamsu = 90;

if(jamsu >= 90) {
	System.out.prinln("점수가 90 이상이네요");
    	System.out.println("A등급입니다");
} else {
	System.out.println("점수가 90 미만이네요");
    	System.out.println("B등급입니다");
}
```



### :mag_right: if-else if-else 문

조건이 여러개인 if 문도 있다. else if 문의 갯수는 제한없으며, 여러개의 조건식 중 true 가 되는 블록만 실행하고 전체 if 문을 벗어난다. 모든 조건식이 false 일 경우 else 블록을 실행 한뒤 if 문을 빠져나온다.

```java
int jamsu = 90;

if(jamsu >= 90) {
	System.out.prinln("점수가 90 이상이네요");
    	System.out.println("A등급입니다");
} else if(jamsu >=85){
	System.out.println("점수가 90 미만이네요");
    	System.out.println("B등급입니다");
} else if(jamsu < 85) {
	System.out.println("점수가 85 미만이네요");
    	System.out.println("C등급입니다");
} else {
	System.out.println("아까워요");
}
```



### :mag_right: 중첩 if 문

- if문의 블록 내부에는 또 다른 if문을 사용할 수 있다.
- 중첩의 단계는 제한이 없기 때문에 흐름을 잘 판단해 작성하면 된다.
- 사실 if문 뿐만 아니라 for, while, switch, do-while문은 교차해서 중첩이 가능하다.

```java
int jamsu = 90;

if(jamsu >= 90) {
	System.out.println("점수가 90 이상이네요");
	if(jamsu >= 95) {
    	System.out.println("A등급입니다");
	} else {
		System.out.println("A-등급입니다");
	}
} else{
	System.out.println("A는 아니네요");
```



### :mag_right: switch 문

- 조건 제어문이다.
- 변수가 어떤 값을 갖느냐에 따라 실행문이 선택된다.

```java
int num = (int)(Math.random()*6) + 1;
// 1~6까지의 숫자 중 랜덤으로 숫자 튀어나옴
		
switch(num) {
	case 1:
		System.out.println("1번");
		break;
        	//break = 더 이상 다른 case 실행하지 말고 종료
	case 2:
		System.out.println("2번");
		break;
	case 3:
		System.out.println("3번");
		break;
	case 4:
		System.out.println("4번");
		break;
	case 5:
		System.out.println("5번");
		break;
	default:
		System.out.println("6번");
		break;
}
```

## :bulb: 반복문

**어떤 작업(코드들)이 반복적으로 실행되도록 할 때 사용**

### :mag_right: for 문

- 똑같은 실행문을 반복적으로 실행해야 할 경우, 코드를 간결하게 만들어준다.
- 코드가 간결하면 개발시간을 줄일 수 있고, 오류가 날 확률도 줄어든다.

```java
for(int i=0; i<10; i++)
//초기화; 조건식; 증감식;
```

1부터 100까지 합을 출력하는 식을 작성해보자

```java
int sum = 0;
for(int i=1; i<=100; i++){
	sum += i;
}
System.out.println("합 : " + sum);
```

### :mag_right: while문

- for 문이 정해진 횟수만큼 반복한다면, while문은 조건식이 true일 경우 계속해 반복한다.

```java
int i = 1;

while (true){
//무한반복한다
	System.out.println(i);
    	i++;
}
```

- 1부터 100까지 합을 출력하는 식을 while문으로도 작성해보자

```java
int sum = 0;

while(i <= 100) {
	sum += i;
    	i++;
}

System.out.println("합 : " + sum)
```

### :mag_right: do-while 문

- while 문과 비슷하다.
- while : 시작부터 조건식을 검사하여 블록 내부를 실행할 것인지 결정한다면
  do-while : 블록을 일단 실행 시키고 결과에 따라 계속 반복할지 결정한다.

```java
Scanner sc = new Scanner(System.in);
String inputString;

do {
	System.out.print(">");
    	inputString = sc.next();
        System.out.println(inputString);
}while( ! inputString.equals("q");

//while 뒤에는 실행 블록이 아니라 세미콜론 (;)
```

### :mag_right: break 문

실행 중지. 조건을 만족한 뒤 더 이상 반복하지 않아도 될 때 사용한다.

```java
//switch-case 문 예제에서 쓰였던 break 예시

switch(num) {
	case 1:
		System.out.println("1번");
		break;
        	//break = 더 이상 다른 case 실행하지 말고 종료
	case 2:
		System.out.println("2번");
		break;
        .
        .
        .
}
```

### :mag_right: continue 문

break가 조건 만족시 반복을 중지시킨다면 continue는 조건 만족시 그대로 지나가라는 뜻이다. 이후의 문장을 실행하지 않고 다음 반복으로 넘어가는 것.

```java
for(int i=0; i<=10; i++) {
	if(i % 2 == 0) { //만약 홀수인경우
		continue;
     }
  System.out.println(i);
  //print 문 출력 안함
}
```

