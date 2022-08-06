## :bulb: 참조 타입 (Reference Type)



- 자바의 데이터 타입은 원시타입(Primitive Type)과 참조타입(Reference Type)이 있다.

| 원시 타입(primitive type) | 미리 정해놓은 크기, stack 실제값 저장 구조, heap 영역 사용 x |
| ------------------------- | ------------------------------------------------------------ |
| 정수 타입                 | byte                                                         |
|                           | char                                                         |
|                           | short                                                        |
|                           | int                                                          |
|                           | long                                                         |
| 실수 타입                 | float                                                        |
|                           | double                                                       |
| 논리 타입                 | boolean                                                      |

---



| 참조 타입(reference type) | 크기를 정할 수 없는 데이터 표현, stack 주소값 저장 구조, heap 참조영역이 실제값 |
| ------------------------- | ------------------------------------------------------------ |
| 배열 타입                 |                                                              |
| 열거 타입                 |                                                              |
| 클래스                    |                                                              |
| 인터페이스                |                                                              |



- 원시 타입으로 선언된 변수와 참조 타입으로 선언된 변수의 차이점 
  - 원시 타입인 byte, char, short, int , long, float, double, boolean을 이용해 선언한 변수에는 실제 값이 저장됨.
  -  참조 타입인 배열, 열거, 클래스, 인터페이스을 이용해 선언한 변수는 메모리의 번지(주소)를 값으로 갖는다. 

```java
//[기본 타입 변수]
int n = 25;

//[참조 타입 변수]
String s = "abc";
```

| 스택 영역                     | 힙 영역          |
| ----------------------------- | ---------------- |
| n : 25 /  s : 주소값 (ex.100) | 100 주소 : "abc" |

>  기본 타입 변수인 n은 직접 값을 저장하고 있지만, 참조 타입 변수인 s는 각각 문자열 리터럴인 “abc"의 주소값을 가리킴
>
> > 자바는 c와 달리 reference type인 경우 포인터가 따로 필요가 없음



## :mag_right: 참조 변수의 ==,!= 연산

기본 타입 변수의 ==, != 연산은 변수의 값이 같은지, 아닌지를 조사하지만
**참조 타입 변수들 간의 ==, != 연산은 동일한 객체를 참조하는지, 다른 객체를 참조하는 지 알아볼 때 사용된다.**
즉 참조타입 변수의 값이 힙 영역의 객체 주소이므로 결국 **주소값**을 비교하는 것이다.

- String의 값을 비교할 땐 `equals()`를 사용한다. 

```JAVA
String a = "JAVA";
String b = "java";
if(b.equals(a)){
  Sysout.system.println("같다.");
}else{
  Sysout.system.println("다름 : 대소문자 구분");
}
```

> **자바는 대소문자를 구분해 값을 비교하기 때문에 두 개의 비교 값은 다르다고 나온다. **



- 대소문자를 구분하지 않고 비교하는 메소드 : `eqaulsIgnoreCase()`

```java
String a = "JAVA";
String b = "java";
if(b.equals(a)){
  Sysout.system.println("같다. : 대소문자 구분 x");
}else{
  Sysout.system.println("다름 : 대소문자 구분");
}
```

> **대소문자 구분을 하지 않기 때문에 결과 값은 같다고 나온다.**



## :mag_right: null 과 NullPointerException

- 참조 타입 변수는 힙 영역의 객체를 참조하지 않는다는 뜻으로 null값을 가질 수 있다.
  -  null 값도 초기값으로 사용할 수 있기 때문에 null로 초기화된 변수는 스택 영역에 생성된다.(다만 힙 영역의 객체를 참조하지 않는다.)

| 스택 영역 | 값   |
| --------- | ---- |
| String a  | null |

- NullPointerException : 참조 타입 변수 a의 값이 null인데, a로 객체 관련해서 메소드를 호출하거나 값을 할당하면 발생하는 예외(Error)

  ```java
  public class NullPointerEx {
    public static void main(String[] args) {
          try {
              int[] Array = null;
              Array[0] = 10;// 참조변수인 배열 intArray가 null값인데, 객체 intArray[0]에 10을 할당하려하므로 NullPointerException 발생.
          }
          catch (NullPointerException e){
              e.printStackTrace();
          }
    }
  }
  ```



## :mag_right: 배열 타입

- 배열에 다른 타입의 값을 저장하려고 하면 타입 불일치 컴파일 오류가 발생한다. => 같은 타입만 저장 가능
- 배열의 길이가 한번 생성되었으면 길이를 늘리거나 줄일 수 없다. => 정적 배열(Static array)



- 초기화와 동시에 배열 생성 

```java
int[] a ={1,2,3};
// 지역 변수 a는 스택에 생성됨. a[0], a[1], a[2]는 객체로써 힙 영역에 생성되고 값이 각각 1,2,3 으로 할당됨.
// 배열 a는 첫번째 요소 a[0]의 시작 주소를 가리킴
```

- 배열 생성 후 초기화 : `new`

```java
int[] a;
a = new int[]{1,2,3}; // new 연산자를 사용하여 초기화 가능.
```

>  `a = {1,2,3}` 으로 초기화 Error 발생

- 메소드의 매개값이 배열일 경우

```java
int add(int[] scores){ ...}  //함수 add 의 매개변수인 배열 scores
int result = add(new int[] {95,85,90}) // 정상작동
```

> new 연산자로 배열 생성



- 배열 길이 : `.length`

```java
int[] arr = {1,2,3};
int le = arr.length; // le는 3 
```

>  “java 클래스”로 프로그램을 실행하면 JVM은 길이가 0인 String배열을 먼저 생성하고 main() 메소드를 호출할 때 매개값으로 전달한다.

```
public class Args {
    public static void main(String[] args) {
        int num1 = Integer.parseInt(args[0]);
        int num2 = Integer.parseInt(args[1]);

        int result = num1+num2;
        System.out.println("result: " + result);
    }
}
```



- 다차원 배열

```
int[][] scores = new int[2][3];
```

- 배열 복사
  1. `for문` 이용

```java
public class Copy {
    public static void main(String[] args) {
        int[] oldArray = {1,2,3,4};
        int[] newArray = new int[8];

        for(int i=0; i < newArray.length; i++){
            if(i<4)
              newArray[i] = oldArray[i];
            else
                newArray[i] = i+1;
            System.out.print(newArray[i] + " ");
        }

    }
}
```

​		2. `System.arraycopy()` 이용

```java
System.arraycopy(Object oldarr, int oldIn, Object newarr, int nnewIn, int length);

public class Copy {
    public static void main(String[] args) {
        int[] oldArray = {1,2,3,4};
        int[] newArray = new int[8];

        System.arraycopy(oldArray,0,newArray,0,oldArray.length);
        for(int i=0; i<newArray.length; i++)
            System.out.print(newArray[i] +" ");  // 1 2 3 4 0 0 0 0 
        System.out.println();
        }

}
```



## :mag_right: 열거 타입

- 열거타입을 선언

  ```java
  public enum Week {
    MONDAY, 
    TUESDAY, 
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY,
    SUNDAY
  }
  ```

- 열거 객체가 가지고 있는 문자열을 리턴한다.

```java
 Week today = Week.SUNDAY;
 String name = today.name(); // SUNDAY 값 리턴되서 name 변수에 저장.
```