## :heavy_exclamation_mark: Semi_Project

> 3일만에 주제 선정, 기획, 역할 분담, 실제 기능 구현, 팀원들꺼 병합, ppt 만들어서 발표까지 해야하는 .. ㅎ
>
> > 처음엔 상품관리를 생각했고, 당근마켓을 모티브하여 프로젝트를 진행하기로했다. 
> >
> > 하루에 8시간 수업을 들으면서 정할게 많아져 머리아팠다...ㅠ



**상품관리** ex) 당근마켓

- 역할분담 

1. 글쓰기(상품등록) - 정찬식
2. 마이페이지 - 글 수정  - 김정수 
3. 검색, 메인페이지 - 권도연  
4. **게시물 상세보기, 댓글, 글 삭제 - 민지수** 
5. 회원가입, 끌어올리기 - 김미애



- 테이블 구성

  - member

  ```sql
  CREATE TABLE member (
    id varchar(30) NOT NULL,
    email varchar(45) NOT NULL,
    address varchar(45) NOT NULL,
    nickname varchar(45) NOT NULL,
    password int NOT NULL,
    PRIMARY KEY (`id`,`nickname`)
  );
  ```

  - product

  ```sql
  CREATE TABLE product (
    product_seq int NOT NULL AUTO_INCREMENT,
    product_name varchar(30) NOT NULL,
    product_title varchar(45) NOT NULL,
    product_category varchar(45) NOT NULL,
    product_price int NOT NULL,
    product_time datetime NOT NULL,
    product_image varchar(45) ,
    product_info varchar(500),
    PRIMARY KEY (product_seq)
  );
  ```
  
  - comment
  
  ```sql
  CREATE TABLE comment (
    commentnum INT NOT NULL AUTO_INCREMENT,
    productnum INT NULL,
    writer VARCHAR(45) NULL,
    content VARCHAR(45) NOT NULL,
    ctime DATETIME NULL,
    PRIMARY KEY (commentnum));



## :mag_right: 메뉴, 화면 구성

- Main 메뉴

  - 로그인

    - db에 id 존재 체크 
    - password 동일 체크
    - 로그인 창 구현

    > 로그인 성공 : 메인메뉴의 로그인 버튼 -> 로그아웃 버튼으로 바뀌게 

  - 글쓰기
    - 로그인시에만 글 작성 가능하게
    - 아이디 없으면 -> 회원가입
    - 글 작성(등록) 하면 메인화면으로 이동
    
  - 글검색
    - like '%' 로 검색
    - 카테고리 선택 가능하게

- 게시물 상세 페이지

  - 등록된 게시물 클릭 : 상세 페이지 보여주기
  - 댓글 작성 기능 - 게시물 번호를 가져와 해당 번호로 댓글 테이블에 저장
  - 글수정 / 삭제
    - 회원 아이디가 다를 시 수정/삭제 불가능

- 마이페이지

  - 내가 쓴 글 목록 list
  - 끌어올리기 - db의 time을 끌어올리기 버튼 클릭 시간으로 update 
  - 회원탈퇴 버튼 -> db 정보 삭제 



