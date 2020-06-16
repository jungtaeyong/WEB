# Oracle

세계에서 가장 많이 사용하는 관계형 데이터 베이스. 여러 edition이 있고, express, personal, standard, enterprise 버전이 있고, 뒤로 갈수록 성능과 가격이 높은 버전이다. (express는 무료)

- 기본적인 사용자 생성 구문

```sql
-- 권한을 주는 것도 여러 옵션이 있다.
> GRANT DBA TO egoing;
```

- 테이블 생성

  ```sql
  > CREATE TABLE topic(
  	id NUMBER NOT NULL,
      title VARCHAR2(50) NOT NULL,
      description VARCHAR2(4000),
      created DATE NOT NULL,
      // PK설정
      CONSTRAINT PK_TOPIC PRIMARY KEY(id)
  );
  ```

- Column 삽입

  ```sql
  > INSERT INTO topic(id, title, description, created)
  	VALUES(1, 'ORACLE', 'ORACLE is ....', SYSDATE);	
  -- 작업후 커밋을 해주어야 한다.
  > commit;
  ```

- Offset

  ```sql
  -- 1번째 행을 제외하고 조회한다.
  > SELECT * FROM topic
  	OFFSET 1 ROWS
  ```

- Fetch

  ```sql
  -- 1번째 행을 제외하고 조회한다.
  > SELECT * FROM topic
  	OFFSET 1 ROWS
  	// 1개만 가져온다.
  	FETCH NEXT 1 ROWS ONLY;
  ```

- Sequence 

  시퀀스란 자동으로 순차적으로 증가하는 순번을 반환하는 데이터베이스 객체이다. 보통 PK 값에 중복 값을 방지하기 위해 사용한다. 예를 들어 게시판에 글이 하나 추가될 때마다 글 번호(PK)가 생겨야 한다고 가정해보자. 만약 100번까지 글 번호가 생성되어 있다면 그다음 글이 추가가 되었을 경우 글 번호가 101로 하나의 ROW를 생성해주어야 할 것이다. 이 때, 101이라는 숫자를 얻으려면 기존 글 번호 중 가장 큰 값에 +1을 하는 로직을 어딘가에 넣어야 하는데, 시퀀스를 이용하면 이러한 로직이 필요없이 데이터베이스에 ROW가 추가될 때마다 자동으로 +1을 시켜주어 매우 편리하다.

  ```sql
  --문법
  CREATE SEQUENCE [시퀀스명]
  INCREMENT BY [증감숫자] --증감숫자가 양수면 증가 음수면 감소 디폴트는 1
  START WITH [시작숫자] -- 시작숫자의 디폴트값은 증가일때 MINVALUE 감소일때 MAXVALUE
  NOMINVALUE OR MINVALUE [최솟값] -- NOMINVALUE : 디폴트값 설정, 증가일때 1, 감소일때 -1028 
                                 -- MINVALUE : 최소값 설정, 시작숫자와 작거나 같아야하고 MAXVALUE보다 작아야함
  NOMAXVALUE OR MAXVALUE [최대값] -- NOMAXVALUE : 디폴트값 설정, 증가일때 1027, 감소일때 -1
                                 -- MAXVALUE : 최대값 설정, 시작숫자와 같거나 커야하고 MINVALUE보다 커야함
  CYCLE OR NOCYCLE --CYCLE 설정시 최대값에 도달하면 최소값부터 다시 시작 NOCYCLE 설정시 최대값 생성 시 시퀀스 생성중지
  CACHE OR NOCACHE --CACHE 설정시 메모리에 시퀀스 값을 미리 할당하고 NOCACHE 설정시 시퀀스값을 메로리에 할당하지 않음
  
  --예제
  CREATE SEQUENCE EX_SEQ --시퀀스이름 EX_SEQ
  INCREMENT BY 1 --증감숫자 1
  START WITH 1 --시작숫자 1
  MINVALUE 1 --최소값 1
  MAXVALUE 1000 --최대값 1000
  NOCYCLE --순한하지않음
  CACHE; --메모리에 시퀀스값 미리할당
  
  -- EX_SEQ라는 시퀀스 이고, 1부터 시작해 1씩 증가하며 시작값은 1부터 1000까지 순번을 자동하는 시퀀스이다. Cache를 사용하여 시퀀스 값의 액세스 효율이 Cache를 사용하지 않았을 때보다 증가한다. 위의 쿼리를 조금만 변형하면 2씩 증가하는 시퀀스, 큰 수에서 작은 수로 감소하는 시퀀스도 생성할 수 있다.
  ```

  