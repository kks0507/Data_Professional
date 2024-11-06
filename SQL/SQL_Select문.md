# SQL `SELECT` 문 정리

## 테이블 구조와 데이터 예시

### 1. `CLERK` 테이블

직원 정보를 저장하는 테이블로, `STAFF_NM`, `DEP_NM`, `GENDER`, `BIRTH_DT`, `EMP_FLAG` 등의 열을 포함합니다.

| ID  | STAFF_NM | DEP_NM         | GENDER | BIRTH_DT   | EMP_FLAG |
|-----|----------|----------------|--------|------------|----------|
| 135 | 이민성   | 마케팅부       | M      | 1984-02-11 | Y        |
| 142 | 김선영   | 영업지원부     | M      | 1971-12-08 | Y        |
| 121 | 신지원   | 리스크부       | F      | 1978-05-28 | Y        |
| 334 | 고현정   | 전략기획부     | F      | 1965-01-12 | N        |
| 144 | 이기동   | 마케팅분석부   | M      | 1981-03-03 | Y        |
| 703 | 송지희   | 검사부         | F      | 1985-05-14 | Y        |
| 732 | 연승환   | 기업영업지원부 | M      | 1990-01-26 | Y        |
| 911 | 이명준   | 여의도지점     | M      | 1988-06-11 | N        |

#### `CLERK` 테이블 설명
- `ID`: 직원의 고유 식별 번호
- `STAFF_NM`: 직원 이름
- `DEP_NM`: 부서 이름
- `GENDER`: 성별 (M: 남성, F: 여성)
- `BIRTH_DT`: 생년월일
- `EMP_FLAG`: 재직 상태 (Y: 재직, N: 퇴직)

---

### 2. `EMP` 테이블

직원의 직급과 평가 등급을 포함하는 테이블로, `POSITION`과 `GRADE` 등의 열을 포함합니다.

| POSITION | GRADE |
|----------|-------|
| 과장      | 2     |
| 대리      | 1     |
| 대리      | 2     |
| 부장      | 2     |
| 차장      | 3     |

#### `EMP` 테이블 설명
- `POSITION`: 직원의 직급 (예: 대리, 과장, 차장 등)
- `GRADE`: 평가 등급 (숫자가 클수록 높은 등급)

---

### 3. `PERF` 테이블

고객의 방문 및 구매 실적을 저장하는 테이블로, `CUST_ID`, `CUST_NM`, `CUST_BIRTH`, `VISIT_CNT`, `SALES_AMT`, `SALES_CNT` 등의 열을 포함합니다.

| CUST_ID | CUST_NM | CUST_BIRTH | VISIT_CNT | SALES_AMT | SALES_CNT |
|---------|---------|------------|-----------|-----------|-----------|
| 65456   | 모형진   | 1982-01-24 | 123       | 3,700,000 | 24        |
| 54321   | 이상훈   | 1984-05-10 | 23        | 467,200   | 14        |
| 23472   | 이상희   | 1978-02-27 | 117       | 2,237,065 | 22        |
| 27896   | 모연재   | 1982-05-11 | 37        | 123,721   | 2         |
| 35478   | 강주혁   | 1983-09-10 | 86        | 830,000   | 8         |
| 79863   | 이선우   | 1977-07-07 | 103       | 1,789,023 | 7         |

#### `PERF` 테이블 설명
- `CUST_ID`: 고객의 고유 식별 번호
- `CUST_NM`: 고객 이름
- `CUST_BIRTH`: 고객의 생년월일
- `VISIT_CNT`: 방문 횟수
- `SALES_AMT`: 총 구매 금액
- `SALES_CNT`: 구매 상품 수

---

## 1. 기본 `SELECT` 문법

- **기본적으로 특정 열을 조회하기 위해 `SELECT`와 `FROM`을 사용합니다.**
- **예제: 특정 열 조회**
  ```sql
  SELECT ID
  FROM CLERK;


- **예제: 여러 열 조회**
  ```sql
  SELECT ID, STAFF_NM
  FROM CLERK;
  ```
  
- **예제: 모든 열 조회**
  ```sql
  SELECT *
  FROM CLERK;
  ```

---

## 2. `ORDER BY` 정렬 사용법

### 방법 1: 열 이름으로 정렬
- `ORDER BY` 뒤에 열 이름을 명시하여 정렬할 수 있습니다.
- **예제**
  ```sql
  SELECT STAFF_NM, DEP_NM
  FROM CLERK
  ORDER BY STAFF_NM;
  ```

### 방법 2: 열 위치로 정렬
- `ORDER BY` 뒤에 열의 위치(1부터 시작)를 명시하여 정렬할 수 있습니다.
- **예제**
  ```sql
  SELECT STAFF_NM, DEP_NM
  FROM CLERK
  ORDER BY 1;
  ```

### 여러 열 기준으로 정렬하기
- 여러 열을 기준으로 정렬할 때, `ORDER BY` 뒤에 여러 열을 콤마(,)로 구분하여 나열합니다.
- **예제**
  ```sql
  SELECT EMP_FLAG, GENDER, STAFF_NM, DEP_NM
  FROM CLERK
  ORDER BY EMP_FLAG, GENDER;
  ```

### 내림차순 정렬
- 내림차순으로 정렬하고 싶을 때 `DESC`를 사용합니다.
- **예제**
  ```sql
  SELECT BIRTH_DT, STAFF_NM, DEP_NM
  FROM CLERK
  ORDER BY BIRTH_DT DESC;
  ```

---

## 3. `DISTINCT` 사용하여 중복 제거

### 단일 열 중복 제거
- 특정 열에서 중복을 제거할 때 `DISTINCT`를 사용합니다.
- **예제**
  ```sql
  SELECT DISTINCT POSITION
  FROM EMP;
  ```

### 여러 열 중복 제거
- 여러 열에 대해 중복을 제거할 때도 `DISTINCT`를 사용할 수 있습니다.
- **예제**
  ```sql
  SELECT DISTINCT POSITION, GRADE
  FROM EMP;
  ```

---

## 4. COUNT 함수와 DISTINCT를 결합하여 고유 값 개수 세기

### 특정 열의 고유 값 개수 세기
- **예제: 고유한 매니저 수 세기**
  ```sql
  SELECT COUNT(DISTINCT MANAGER_ID) AS CNT
  FROM EMP;
  ```

---

## 5. 실습 예제 정리

### 예제 1: CLERK 테이블에서 이름을 기준으로 오름차순 정렬
- **목표**: CLERK 테이블에서 `STAFF_NM`을 기준으로 오름차순 정렬하여 `STAFF_NM`과 `DEP_NM`을 출력합니다.
- **예제**
  ```sql
  SELECT STAFF_NM, DEP_NM
  FROM CLERK
  ORDER BY STAFF_NM;
  ```

### 예제 2: CLERK 테이블에서 부서명을 기준으로 오름차순 정렬 후, 이름과 부서명을 출력
- **목표**: `DEP_NM`을 기준으로 오름차순 정렬 후, `STAFF_NM`과 `DEP_NM`을 출력합니다.
- **예제**
  ```sql
  SELECT STAFF_NM, DEP_NM
  FROM CLERK
  ORDER BY DEP_NM, STAFF_NM;
  ```

### 예제 3: 부서명, 성별, 이름을 기준으로 정렬하여 재직 여부, 성별, 이름을 출력
- **목표**: `EMP_FLAG`를 내림차순, `GENDER`를 오름차순으로 정렬하여 출력합니다.
- **예제**
  ```sql
  SELECT EMP_FLAG, GENDER, STAFF_NM
  FROM CLERK
  ORDER BY EMP_FLAG DESC, GENDER ASC;
  ```


