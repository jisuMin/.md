1. db 연결
2. Sql 전송
3. sql 결과검색

==> 반복

4. 할 일이 없으면 db 연결 해제



jdbc 단점

- 코드 반복이 심함

  - connection, 예외처리 등 사용객체 해제 빈번 

- 자바 언어와 sql 언어는 다른데 1개 파일에 공존함

  - ```java
    String sql = "select * from member"; 
    		PreparedStatement pt = conn.prepareStatement(sql);
    		ResultSet rs = pt.executeQuery();

- 테이블 결과는 무조건 ResultSet -> 객체 코드 수동 구현 -> 개발자 몫