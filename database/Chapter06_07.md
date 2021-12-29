### **Chapter06**

1. 관계 데이터 연산 : 관계 데이터 모델의 연산

   1. 관계 대수(절차 언어) : 원하는 결과를 얻기 위해 데이터의 처리 과정(how)을 순서대로 기술
   2. 관계 해석 (비절차 언어) : 원하는 결과를 얻기 위해 처리를 원하는 데이터가 무엇(what)인지만 기술
   3. 질의 : 데이터에 대한 처리 요구

2. 관계 대수 : 원하는 결과를 얻기 위해 릴레이션을 처리하는 과정을 순서대로 기술하는 언어 => 연산자들의 집합

   1. 일반 집합 연산자

      - 제약조건
        - 두 릴레이션의 차수(속성 개수)가 같음
        - 2개의 릴레이션에서 서로 대응되는 속성의 도메인이 같음, 도메인이 같으면 속성의 이름은 달라도 됨

      1. 합집합
         - 릴레이션 R에 속하거나 릴레이션 S에 속하는 모든 튜플의 결과
         - 합집합 연산 후 릴레이션의 차수는 릴레이션 R과 S의 차수와 동일함
         - 릴레이션의 기본 특징에 따라 중복 튜플이 존재하지 않기 때문에 카디널리티(튜플의 전체 개수)는 릴레이션 R과 S의 튜플 개수를 더한 것과 같거나 적음
      2. 교집합
         - R과 S에 공통으로 속하는 튜플
         - 교집합 연산 후 릴레이션의 차수는 릴레이션 R과 S의 차수와 동일함
         - 카디널리티는 릴레이션 R과 S의 카디널리티와 같거나 적음
      3. 차집합
         - R-S는 R에는 존재하지만 S에는 존재하지 않는 튜플들의 결과
         - 차집합 연산 후 릴레이션의 차수는 릴레이션 R과 S의 차수와 동일함
         - 카디널리티는 릴레이션 R이나 S의 카디널리티와 같거나 적음
      4. 카티션 프로덕트 - 제약조건과 상관없이 연산 가능
         - R에 속한 각 튜플과 S에 속한 각 튜플을 모두 연결하여 만들어진 새로운 튜플의 결과
         - 카티션 프로덕트 연산 후 릴레이션의 차수는 릴레이션 R과 S의 차수를 더한 것과 같음
         - 카디널리티는 릴레이션 R과 S의 차수를 곱한 것과 같음

   2. 순수 관계 연산자 : 릴레이션의 구조와 특성 이용

      1. 셀렉트(수평적 연산자)
         - 하나의 릴레이션을 대상으로 조건을 만족하는 튜플만 선택
      2. 프로젝트(수직적 연산자)
         - 주어진 속성들의 값으로만 구성된 튜플 선택
      3. 조인
         - 공통 속성을 이용해 두 릴레이션의 튜플을 연결
      4. 디비전
         - R÷S는 S의 모든 튜플과 관련 있는 R의 튜플의 결과, R이 S의 모든 속성을 포함하고 있어야함

### Chapter07

1. SQL : 관계 데이터베이스를 위한 표준 질의어

   1. 데이터 정의어(DDL) : 테이블을 생성하고 변경, 제거하는 기능 제공
   2. 데이터 조작어(DML) : 테이블에 새 데이터를 삽입하거나, 저장된 데이터를 수정, 삭제, 검색하는 기능 제공
   3. 데이터 제어어(DCL) : 보안을 위해 데이터에 대한 접근 및 사용 권한을 사용자별로 부여하거나 취소하는 기능 제공 - 데이터베이스 관리자가 주로 사용

2. 데이터 정의

   1. CREATE TABLE : 테이블 생성

      ```sql
      CREATE TABLE 테이블 이름(
      		속성 이름 데이터 타입 [NOT NULL] [DEFAULT 기본 값],
      		[PRIMARY KEY(속성 리스트)],
      		[UNIQUE (속성 리스트)],
      		[FOREIGN KEY(속성 리스트) REFERENCES 테이블 이름(속성 리스트)] [ON DELETE 옵셥] [ON UPDATE 옵션],
      		[CONSTRAINT 이름] [CHECK(조건)]
      );
      ```

      1. 키의 정의
         1. PRIMARY KEY : 모든 테이블에서 기본키는 반드시 하나만 지정할 수 있고, 여러 개의 속성으로 구성 가능
         2. UNIQUE : 대체키로 지정된 속성의 값은 중복되면 안되고 유일성을 가져야하지만 NULL값 가능하며 여러 개 지정 가능
         3. FOREIGN KEY REFERENCES - 참조 무결성 제약조건 유지
         4. CHECK : 데이터 무결성 제약조건

   2. ALTER TABLE : 테이블 변경

      1. 새로운 속성 추가

         ```sql
         ALTER TABLE 테이블 이름
         	ADD 속성 이름 데이터 타입 [NOT NULL] [DEFAULT 기본 값];
         ```

      2. 기존 속성 삭제

         ```sql
         ALTER TABLE 테이블 이름
         	DROP COLUMN 속성 이름;
         ```

      3. 새로운 제약조건 추가

         ```sql
         ALTER TABLE 테이블 이름
         	ADD CONSTRAINT 제약조건 이름 제약조건 내용;
         ```

      4. 기존 제약조건 삭제

         ```sql
         ALTER TABLE 테이블 이름
         	DROP CONSTRAINT 제약조건 이름;
         ```

   c. DROP TABLE : 테이블 삭제

   - 참조하는 테이블이 있다면 참조하는 외래키 제약조건을 먼저 삭제해야함

     ```sql
     DROP TABLE 테이블 이름;
     ```

3. 데이터 조작

   1. SELECT : 데이터 검색

      ```sql
      SELECT [ALL|DISTINCT] 속성 리스트
      FROM 테이블 리스트
      [WHERE 조건]
      [GROUP BY 속성 리스트 [HAVING 조건]]
      [ORDER BY 속성 리스트 [ASC|DESC]];
      ```

      [집계 함수](https://www.notion.so/80cdfbb8b0604fa694e32865711f7208)

   - 집계 함수는 널 값을 제외하고 계산
   - WHERE 절에서 사용 불가, SELECT, HAVING 절에서 사용 가능
   - 그룹별로 검색 시 집계 함수나 GROUP BY 절에 있는 속성 외의 속성은 SELECT 절에서 사용 불가

   b. INSERT : 데이터 삽입

   ```sql
   INSERT 
   INTO 테이블 이름[(속성 리스트)]
   VALUES (속성값 리스트);
   ```

   c. UPDATE : 데이터 수정

   ```sql
   UPDATE 테이블 이름
   SET 속성 이름1 = 값1, 속성 이름2 = 값2 ,,
   [WHERE 조건];
   ```

   e. DELETE : 데이터 삭제

   ```sql
   DELETE
   FROM 테이블 이름
   [WHERE 조건];
   ```

4. 뷰 : 다른 테이블을 기반으로 만들어진 가상 테이블, 데이터 저장 X

   ```sql
   // 뷰 생성
   CREATE VIEW 뷰 이름[(속성 리스트)]
   AS SELECT 문
   [WITH CHECK OPTION];
   
   // 뷰 삭제
   DROP VIEW 뷰 이름
   ```

   - 뷰에 대한 삽입, 수정, 삭제 연산은 기본 테이블의 내용을 자동으로 변경
   - 검색 연산은 모든 뷰에 수행 가능 / 삽입, 수정, 삭제 연산은 허용되지 않는 뷰 존재