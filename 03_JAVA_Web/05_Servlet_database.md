## :bulb: Servlet에서 요청받아 처리

- LoginDBServlet.java

```java
@WebServlet("/LoginDB")
public class LoginDBServlet extends HttpServlet {
	Connection conn =null;
	private int connectionDB(String id, String userpassword) {
		int condition = 0;
		try {
		Class.forName("com.mysql.cj.jdbc.Driver");
		conn = DriverManager.getConnection
		("jdbc:mysql://127.0.0.1:3306/memberdb", "emp2", "emp2");
		String sql = "select id, password from member where id=?";
		PreparedStatement pt = conn.prepareStatement(sql);
		pt.setString(1, id);
		ResultSet rs = pt.executeQuery();
		// sql 실행결과가 여러 개의 레코드이거나, 1개가 검색되도 -> 첫 번째 검색된 것만 출력 
		// sql 실행결과 0개 
		
		String dbid = null, dbpassword= null;
		if(rs.next()) { // rs.next()가 true인 경우 = id가 존재하는 경우 
			condition = 1; // id 존재 , password 불일치 
			dbid = rs.getString("id");
			dbpassword = rs.getString("password");
			// id 존재, password 일치 
			if(dbpassword.equals(userpassword)) {
				condition =2 ;
			}
		}else {
			condition = 3; // id 존재하지 않음 
		}
		}catch (Exception e){
			e.printStackTrace();
		}finally {
			try {
				conn.close();
			}catch(SQLException e) {}
		}
		return condition;
	}
	
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String id = request.getParameter("id");
		String pw = request.getParameter("pw");
		String role = request.getParameter("role");
		String output="";
		int condition = connectionDB(id,pw);
		
		if(condition == 2) {
	
		if(role.equals("admin")) {
			output = id + " 계정의 관리자 <br>";
			output+="<ul><li>모든 사용자 정보 조회</li>";
			output+="<li>블랙리스트 관리</li>";
			output+="<li>상품관리</li></ul>";
		}else if(role.equals("user")){
			output = id + " 계정의 사용자 ";
			output+="<ol><li>내 정보 조회</li>";
			output+="<li>로그아웃</li>";
			output+="<li>게시판 보기</li></ol>";
		}
		}// condition 2 end
		else if(condition == 1) {
			output="<h3>암호가 다릅니다.</h3>";
			output+="<a href='logindb.html'>다시 로그인 하러가기</a>";
		}// condition 1 end
		else {
			output="<h3>회원 정보가 없습니다.</h3>";
			output+= "<a href='insertmemberdb.html'>회원가입 하러가기</a>";
		}// condition 3 end
		response.setContentType("text/html;charset=utf-8");
		PrintWriter o = response.getWriter();
		o.print(output);
	}

}

```

- logindb.html

```html
<script>
$(document).ready(function(){
	$("form").on('submit',function(){		
	
		if( $("input:text").val() == "adm" ||
			$("input:text").val() == "administor" ||
			$("input:text").val() == "administrator") {
			$("input:hidden").val("admin");
		}else{
			$("input:hidden").val("user");
		}
		
	});
});

</script>

<body>
<form action="LoginDB">
아이디 <input type="text" name="id">
비밀번호 <input type="password" name="pw">
<input type="submit" value="로그인">
<input type="hidden" name="role">
</form>
</body>

```

- MemberDTO

```java
package dto;
// JDBC -- MYBATIS
public class MemberDTO {
	String id; //varchar(30)
	int password;
	String name; //varchar(30)
	String phone; //char(13)
	String email;// varchar(30)
	String regdate; // datetime
	
	public String getId() {
		return id;
	}
	public void setId(String id) {
		this.id = id;
	}
	public int getPassword() {
		return password;
	}
	public void setPassword(int password) {
		this.password = password;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getPhone() {
		return phone;
	}
	public void setPhone(String phone) {
		this.phone = phone;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public String getRegdate() {
		return regdate;
	}
	public void setRegdate(String regdate) {
		this.regdate = regdate;
	}
```

- MemberDAO

```java
public class MemberDAO {
	//Member 테이블 CRUD
	public int selectMember(String id, String userpassword) {
		Connection conn =null;
		int condition = 0;
		try {
		Class.forName("com.mysql.cj.jdbc.Driver");
		conn = DriverManager.getConnection
		("jdbc:mysql://127.0.0.1:3306/memberdb", "emp2", "emp2");
		String sql = "select id, password from member where id=?";
		PreparedStatement pt = conn.prepareStatement(sql);
		pt.setString(1, id);
		ResultSet rs = pt.executeQuery();
		// sql 실행결과가 여러 개의 레코드이거나, 1개가 검색되도 -> 첫 번째 검색된 것만 출력 
		// sql 실행결과 0개 
		
		String dbid = null, dbpassword= null;
		if(rs.next()) { // rs.next()가 true인 경우 = id가 존재하는 경우 
			condition = 1; // id 존재 , password 불일치 
			dbid = rs.getString("id");
			dbpassword = rs.getString("password");
			// id 존재, password 일치 
			if(dbpassword.equals(userpassword)) {
				condition =2 ;
			}
		}else {
			condition = 3; // id 존재하지 않음 
		}
		}catch (Exception e){
			e.printStackTrace();
		}finally {
			try {
				conn.close();
			}catch(SQLException e) {}
		}
		return condition;
	}

	public int insertMember(MemberDTO dto) {
		Connection conn =null;
		int condition = 0; //insert한 행의 갯수 
		
		try {
		Class.forName("com.mysql.cj.jdbc.Driver");
		conn = DriverManager.getConnection
		("jdbc:mysql://127.0.0.1:3306/memberdb", "emp2", "emp2");
		String sql = "insert into member values(?,?,?,?,?,now())";	
		PreparedStatement pt = conn.prepareStatement(sql);		
		pt.setString(1,dto.getId());
		pt.setInt(2,dto.getPassword());
		pt.setString(3,dto.getName());
		pt.setString(4,dto.getPhone());
		pt.setString(5,dto.getEmail());
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
```

- 실행결과

1. 없는 아이디인 경우 회원가입을 먼저 진행

2. 로그인한 실행 결과를 보기 위해  `adm,11` 과 `Servlet_id1,11`로 회원가입

3. DB에 저장되었는지 확인

   ![스크린샷 2022-08-08 오후 4.24.22](../../../../Library/Application Support/typora-user-images/스크린샷 2022-08-08 오후 4.24.22.png)

4.  결과 확인

- `id = adm, password = 11`를 입력 : **관리자로 로그인한 경우**

![스크린샷 2022-08-08 오후 4.22.13](../../../../Library/Application Support/typora-user-images/스크린샷 2022-08-08 오후 4.22.13.png)

- `id = Servlet_id1, password = 11`를 입력 : **사용자로 로그인한 경우**

![스크린샷 2022-08-08 오후 4.22.46](../../../../Library/Application Support/typora-user-images/스크린샷 2022-08-08 오후 4.22.46.png)

