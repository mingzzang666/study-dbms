## 🐬 MySQL 요약

### ✅ 개요
- 웹사이트 및 다양한 애플리케이션에서 사용되는 **DBMS**  
- **Oracle**은 고가, **MySQL**은 저가형 데이터베이스  
- 문법이 간결하고 사용이 쉬우며, **메모리 사용량이 적음**

---

### ⚙️ 설치
📎 [MySQL 설치 파일](https://drive.google.com/file/d/1OkSYmK7GIrbHa5vFceGaji4H4QWaa8Sn/view?usp=drive_link)  
📎 [DBeaver (IDE) 설치 파일](https://drive.google.com/file/d/1DATzZoOAUJAZOvkTlzJagLcYLFt0-DuU/view?usp=sharing)

---

### 💡 기본 명령어
```sql
-- 로그인
mysql -u root -p
1234

-- 데이터베이스 목록 조회
show databases;

-- 데이터베이스 생성 및 사용
create database [DB명];
use [DB명];

-- 계정 목록 조회
select user, host from user;

-- 계정 생성
create user '계정명'@localhost identified by '비밀번호'; -- 로컬용
create user '계정명'@'%' identified by '비밀번호';       -- 원격용

-- 비밀번호 변경
set password for '계정명'@'%' = '신규비밀번호';

-- 계정 삭제
drop user '계정명'@localhost;
drop user '계정명'@'%';

-- 권한 부여 및 적용
grant all privileges on *.* to '계정명'@'%' with grant option;
flush privileges;
```

---

### 🧱 DBMS 구조 개념
- **DBMS**: 여러 응용 프로그램(고객관리, 주문관리 등)과 데이터를 주고받는 시스템  
- **RDBMS(관계형 DBMS)**: 데이터를 **Table(=Class)** 구조로 관리  

| 용어 | 의미 |
|------|------|
| Column (열, 속성, 필드) | 공통된 값의 주제 |
| Row (행, 튜플, 레코드) | 하나의 정보 단위 |
| Primary Key (PK) | 고유한 값, 중복 및 NULL 불가 |
| Foreign Key (FK) | 다른 테이블의 PK 참조, 중복 가능 |
| Unique Key (UK) | NULL 허용, 중복 불가 |

---

### 🧮 SQL 언어 분류
| 종류 | 이름 | 설명 |
|------|------|------|
| **DDL** | Data Definition Language | 테이블 정의 및 구조 변경 |
| **DML** | Data Manipulation Language | 데이터 조작 (조회, 추가, 수정, 삭제) |
| **DCL** | Data Control Language | 권한 제어 (GRANT, REVOKE) |
| **TCL** | Transaction Control Language | 트랜잭션 제어 (COMMIT, ROLLBACK) |

---

### 📘 주요 자료형
- **정수형**: `tinyint`, `smallint`, `mediumint`, `int`, `bigint`  
- **실수형**: `decimal(m, d)`  
- **날짜형**: `date`, `time`, `datetime`  
- **문자형**: `char(m)` (고정 길이), `varchar(m)` (가변 길이)

---

### 🧰 DDL (데이터 정의어)
```sql
-- 테이블 생성
create table [테이블명] (
  [컬럼명] [자료형] [제약조건],
  ...
);

-- 삭제
drop table [테이블명];

-- 컬럼 추가 / 삭제 / 변경
alter table [테이블명] add [컬럼명] [타입];
alter table [테이블명] drop [컬럼명];
alter table [테이블명] modify [컬럼명] [새타입];
alter table [테이블명] change [기존컬럼] [새컬럼] [타입];

-- 테이블명 변경
alter table [기존명] rename [새이름];

-- 데이터 초기화
truncate table [테이블명];
```

---

### 🔒 무결성 (Integrity)
데이터의 **정확성, 일관성, 유효성**을 유지하는 성질  

| 종류 | 설명 |
|------|------|
| 개체 무결성 | 모든 테이블은 PK를 가져야 함 |
| 참조 무결성 | FK 관계에서 일관성 유지 |
| 도메인 무결성 | 컬럼 타입, NULL 허용 여부 등 제약 조건 유지 |

---

### 🧩 모델링 과정
1. **요구사항 분석** – 관리할 데이터 파악 (회원, 주문, 상품 등)  
2. **개념적 설계** – 주제별 엔티티 구상  
3. **논리적 설계** – PK, FK, 제약조건 정의  
4. **물리적 설계** – 실제 테이블 구조로 변환  
5. **구현** – SQL로 테이블 생성  

---

### 🧠 정규화 (Normalization)
중복을 줄이고 이상현상(Anomaly)을 방지하기 위한 작업  

| 단계 | 해결 문제 | 예시 |
|------|------------|------|
| **1차 정규화** | 반복 컬럼 제거 | 상품명1, 상품명2 → 행으로 분리 |
| **2차 정규화** | 부분 종속 제거 | 복합키 일부에만 종속된 컬럼 분리 |
| **3차 정규화** | 이행 종속 제거 | PK가 아닌 컬럼 간 종속성 제거 |

📌 이상(Anomaly) 현상  
- **삽입 이상**: 불필요한 데이터도 함께 입력해야 함  
- **갱신 이상**: 일부만 수정되어 데이터 불일치 발생  
- **삭제 이상**: 필요 데이터까지 함께 삭제됨  

---

### 💬 DML (데이터 조작어)
```sql
-- 조회
select 컬럼명 from 테이블명 where 조건식;

-- 추가
insert into 테이블명 (컬럼1, 컬럼2, ...) values (값1, 값2, ...);

-- 수정
update 테이블명 set 컬럼1=값1, 컬럼2=값2 where 조건식;

-- 삭제
delete from 테이블명 where 조건식;
```

🧮 **조건식 연산자**
`>, <, >=, <=, =, !=, and, or`

---

### 🔗 JOIN (조인)
여러 테이블의 데이터를 결합하여 결과를 조회하는 문법  

| 종류 | 설명 |
|------|------|
| **INNER JOIN** | 조건에 맞는 데이터만 출력 |
| **OUTER JOIN** | 조건 불일치 데이터도 포함 |
| **등가 조인** | ON 절에 `=` 사용 |
| **비등가 조인** | ON 절에 `>` 또는 `<` 등 사용 |

```sql
select ...
from A inner join B
on A.id = B.id;
```

---

### 🌀 TCL (트랜잭션 제어어)
> 여러 DML 작업을 하나의 서비스 단위로 묶어 처리  

| 명령어 | 설명 |
|---------|------|
| `commit` | 현재 트랜잭션 확정 |
| `rollback` | 마지막 commit 지점으로 복구 |

⚠️ DDL은 트랜잭션이 불가하므로 주의해야 함  

---

### 👁️ VIEW (뷰)
실제 테이블을 바탕으로 만든 **가상 테이블**

| 특징 | 설명 |
|------|------|
| **독립성** | 다른 곳에서 직접 접근 불가 |
| **편리성** | 긴 쿼리문을 짧게 대체 |
| **보안성** | 원본 데이터 노출 방지 |

```sql
-- 생성
create view [뷰이름] as (select ...);

-- 생성 또는 수정
create or replace view [뷰이름] as (select ...);
```
