## JDBC 설치 및 연결

1. connection.jar 설치 후 이클립스 **class path 설정**

   - classpath에 connectoin.jar가 저장 되어있는 경로 선택

   ![스크린샷 2022-07-18 오전 9.39.00](/Users/minjisu/Desktop/스크린샷 2022-07-18 오전 9.39.00.png)

2. **드라이버 호출**

   ```java
   try {
   		Class.forName("com.mysql.cj.jdbc.Driver");
   		System.out.println("드라이버 호출 완료");
   		}catch (ClassNotFoundException e) {
   			System.out.println("미설치이거나 classpath 미등록");
   		}
   ```

   - 연결 성공 : ``드라이버 호출 완료`` / 미성공 : ``미설치이거나 classpath 미등록``

3. **db 연결**

   ```java
   Connection con = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/empdb","emp","emp");
   		System.out.println("db 연결 성공");
   ```

   - 연결 성공 : ``db 연결 성공``
   
4. **db 연결 해제** : `con.close();`

