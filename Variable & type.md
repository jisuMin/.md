## :bulb: 변수란?

**값을 저장할 수 있는 메모리의 공간** 

- primitive type(기본형 타입) 변수 : 정수(문자), 실수, 논리형( boolean) 데이터 타입이 있다.
- Referenece type(객체형 타입) 변수 : 문자열, 객체
- byte, 8개의 비트로 구성된 데이터양을 나타나는 단위로 -128 ~127의 수를 담고 있다.
- 유니코드, 전 세계의 모든 문자를 컴퓨터에서 일관되게 표현하고 다룰 수 있도록 설계된 산업 표준이며, 유니코드 협회에서 제정한다.
- "="가 있을때는 우항이 먼저 실행 되고 좌항으로 옮겨짐.
- 정수의 사칙연산이 일어나면 자바에서는 무조건 int형으로 인식한다.
- 데이터 타입을 잘못 사용하여 범위를 벗어난 답을 얻어 데이터가 깨질 수 있어 주의를 해야한다.
- 실수의 기본적인 연산은 double이다.
- 정수보다 실수의 데이터값이 더 크다.



## :mag_right: 변수의 선언

**변수 선언은 어떤 타입의 데이터를 저장할 것인지, 이름이 무엇인지를 결정한다. **

``` java
int sum; //정수(int) 값을 저장할 수 있는 sum 변수 선언
double avg; //실수(double) 값을 저장할 수 있는 avg 변수 선언
String name; //문자(String) 값을 저장할 수 있는 name 변수 선언
...
```

**같은 타입의 변수 여러개 선언** - 콤마(,)를 이용해 한꺼번에 선언할 수 있다.

` int x,y,x; `

 **변수 선언과 동시에 초기화**

` int score = 90; `



## :mag_right: 변수 작성 규칙

- 첫번재 끌자는 문자이거나 '$' , '_' 여야 하고 숫자로 시작할 수 없다(필수)
- 영어 대소문자가 구분된다.(필수)
- 첫문자는 영어 소문자로 시작하되, 다른단어가 붙을 경우 첫자를 대문자로 한다(관례) (ex. maxSpeed, firstName)
- 문자 수의 길이 제한은 없다.
- 자바 예약어는 사용 할 수 없다.(for, int public 등...)



## :mag_right: 변수 사용 범위

**변수는 선언된 블록 내에서만 사용 가능하다.**

```java
public class VariableXcopeExample {
	public static void main(String[] args){
    int n1 = 15;
    if (n1 > 10){
      int n2 = n1-10;
    }
    int n3 = n1 + n2; // n2 변수는 if 블록 안에서만 사용 가능 -> 컴파일 에러 
  }
}
```



## :bulb: 데이터 타입과 크기

<table>
  <tr>
   <td><b>종류</b></td><td><b>기본 타입</b></td><td colspan="2"><b>사용 크기</b></td>
  </tr>
   <tr>
    <td rowspan="5">정수</td><td>byte</td><td>1byte</td><td>8bit</td>
  </tr>
  <tr>
    <td>char</td><td>2byte</td><td>16bit</td>
  </tr>
   <tr>
    <td>short</td><td>2byte</td><td>16bit</td>
  </tr>
   <tr>
    <td>int</td><td>4byte</td><td>32bit</td>
  </tr>
   <tr>
    <td>long</td><td>8byte</td><td>64bit</td>
  </tr>
  <tr>
    <td rowspan="2">실수</td><td>float</td><td>4byte</td><td>32bit</td>
  </tr>
   <tr>
    <td>double</td><td>8byte</td><td>64bit</td>
  </tr>
   <tr>
    <td>논리</td><td>boolean</td><td>1byte</td><td>8bit</td>
  </tr>
</table>

- 정수(int) + 실수(double) 일경우 데이터 타입은 **실수형**을 따른다.
- boolean 타입은 true와 false 값만 갖는다.



##  :mag_right:타입 변환 (형 변환)

**데이터 타입을 다른 데이터 타입으로 변환** 

- 자동 타입 변환 : 작은 크기 타입 -> 큰 크기 타입

  ```java
  byte byteValue = 10;
  int intValue = byteValue; // byte가 int보다 작은 타입, 자동 형변환이 일어난다.
  ```

- 강제 타입 변환 : 큰 크기 타입 -> 작은 크기 타입

  ```java
  double doubleValue = 50.5;
  int intValue = doubleValue; // double이 int 보다 큰 타입, 자동 형변환 X, 컴파일 에러
  int intValue = (int)doubleValue; //(변환할 작은 타입) 으로 강제 형변환  
  ```

  > double을 int로 강제 형변환시  소수점 이하 부분은 버려지고, 정수만 저장된다.

  



