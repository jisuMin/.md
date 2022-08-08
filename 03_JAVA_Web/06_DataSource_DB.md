## :bulb: DataSource 이용해 데이터베이스 연동하기

- jdbc 문제점

  - db 연결 소요 시간과 메모리 정리 시간이 소요

  - sql 전송마다 반복 작업이 많다.

  - 예외처리 반복 

> **커넥션풀(Connectionpool) 방법을 사용하여 해결** : `tomcat` 제공 라이브러리 
>
> > 데이터베이스와 연결시킨 상태를 유지 



## :mag_right: 톰캣의 DataSource 설정 및 사용 방법

- 톰캣 커넥션 Pool 설정 과정
  1. JDBC 드라이버를 `/WEB-INF/lib` 폴더에 설치
  2. 커넥션 풀 기능 관련 `jar` 파일을 `/WEB-INF/lib` 폴더에 설치
  3. `CATALINA_HOME/context.xml`에 커넥션풀 생성 시 연결할 데이터베이스 정보를 JNDI로 설정
  4. DAO 클래스에서 DB 연동시 미리 설정한 JNDI라는 이름으로 DB 연결해서 작업



- Context.xml 내용 추가

```java
<Context>
<Resource name ="jdbc/mydb" 
    auth="Container" 
    type="javax.sql.DataSource"
    driverClassName="com.mysql.jdbc.Driver"
    url="jdbc:mysql://127.0.0.1:3306/memberdb"
    username="emp2"
    password="emp2"
    maxActive ="5" maxIdle="3" maxWait="-1"
    />
</Context>
```

- doGet() 작성 

```java
public class ConnectionServlet extends HttpServlet {
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		try {
            // 1. context.xml 파일 정의 내용을 읽어올 준비 
            Context initContext = new InitialContext();
            // 2. <Resource 태그 설정 정보 읽어오기 
            Context envContext = (Context)initContext.lookup("java:/comp/env"); 
            // 3. Resource가 여러개일때 jdbc/mydb 설정 태그만 읽어오기 - connectionpool 클래스 객체 생성 
            DataSource ds = (DataSource)envContext.lookup("jdbc/mydb");
            long start = System.currentTimeMillis();
            for(int i = 1; i<=1000;i++) {
              Connection conn = ds.getConnection(); //미리 생성된 connection 빌려옴 
              System.out.println(i+"> mysql 연결 성공"); //브라우저에 출력 x, 서버 콘솔에 출력됨 
              conn.close();//connection 반납 
     }catch(Exception e) {
				e.printStackTrace();
			}
		}

```

- DataSource를 이용한 MemberDAO 작성 
  - 이전에 [05_Servlet_database]()에서 작성한 DAO와 다름을 확인 

```java

	public ArrayList<MemberDTO> selectAllMember()  {
		Connection conn =null;
		ArrayList<MemberDTO> memberlist = new ArrayList<MemberDTO>();
		try {
			Context initContext = new InitialContext();
			Context envContext = (Context)initContext.lookup("java:/comp/env"); 			
			DataSource ds = (DataSource)envContext.lookup("jdbc/mydb");
			conn= ds.getConnection();
			
			String sql = "select * from member";
			PreparedStatement pt = conn.prepareStatement(sql);
			ResultSet rs = pt.executeQuery();
			
			while(rs.next()) {
				MemberDTO dto = new MemberDTO();
				dto.setId(rs.getString("id"));
				//dto.setPassword(rs.getInt("password"));
				dto.setName(rs.getString("name"));
				dto.setPhone(rs.getString("phone"));
				dto.setEmail(rs.getString("email"));
				dto.setRegdate(rs.getString("regdate"));
				memberlist.add(dto);
			}
			}catch (Exception e){
				e.printStackTrace();
			}finally {
				try {
					conn.close();
				}catch(SQLException e) {}
			}
			return memberlist;
	}//selectAllmember

	public int deleteMember(String id, String pw) {
		Connection conn =null;
		int condition = 0; //delete한 행의 갯수 
		
		try {
			Context initContext = new InitialContext();
			Context envContext = (Context)initContext.lookup("java:/comp/env"); 			
			DataSource ds = (DataSource)envContext.lookup("jdbc/mydb");
			conn= ds.getConnection();
		
			String sql = "delete from member where id=? and password=?";	
			PreparedStatement pt = conn.prepareStatement(sql);		
			pt.setString(1,id);
			pt.setInt(2,Integer.parseInt(pw));
		
			condition = pt.executeUpdate();
			}catch (Exception e){
				e.printStackTrace();
			}finally {
				try {
					conn.close();
				}catch(SQLException e) {}
			}
			return condition;
		}


}

```