# 개발 DB 객체 계약

확인일: 2026-11-09. 환경: 개발 SQL Server, 기본 연결 DB `smartwork`. `sqlcmd -S … -C`로 `sys.objects`, `sys.parameters`, `sys.columns`, `sys.sql_expression_dependencies`, `OBJECT_DEFINITION`만 조회했다. 업무 프로시저와 쓰기 SQL은 실행하지 않았다.

직접 호출 객체 342개와 하위 참조를 포함한 831개 객체의 메타데이터를 확인했다. 아래 입력·출력 계약은 개발 DB 정의 기준이며 다른 환경 적용이나 실행 결과를 보장하지 않는다.

RETURN은 sys.parameters의 OUT과 다르다. Mapper의 `mode=OUT` 및 RETURN 바인딩을 함께 확인한다. T-SQL 파라미터 기본값은 `has_default_value`만으로 단정하지 않고 정의의 선언부에서 추출했다. 실제 결과 컬럼은 해당 Mapper의 명시 매핑을 기록했다.

동적 SQL에서는 정적으로 드러난 객체와 하위 호출을 추적했다. 런타임에 조합되는 DB·테이블명, 날짜별 테이블, 외부 서버, CLR 함수의 내부 구현은 메타데이터만으로 전부 확정할 수 없어 해당 항목에 표시했다.

<a id="db001"></a>
## MIGRATION_ETCASP.dbo.MIGRATION_MAPPING_COMPANY

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `COM_NO` | `int` | 불가 | 아니오 |
| `COM_REGNO` | `varchar(10)` | 불가 | 아니오 |
| `COM_NAME` | `varchar(70)` | 불가 | 아니오 |
| `ACCESS_ROUTE` | `varchar(50)` | 불가 | 아니오 |
| `M_FLAG` | `varchar(50)` | 불가 | 아니오 |
| `USE_YN` | `varchar(1)` | 불가 | 아니오 |
| `CDATE` | `datetime` | 불가 | 아니오 |
| `UDATE` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2018-08-29T10:41:50.723 |
| 읽기·참조 객체 | `migration_etcasp.dbo.migration_mapping_company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findRevealBusinessNumber](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankCompanyMapper.kt#L45) — 바인딩: `comNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findSensitiveValue](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankMemberMapper.kt#L82) — 바인딩: `memNo`, `memNo`, `memNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db002"></a>
## MIGRATION_ETCASP.dbo.MIGRATION_MAPPING_MEMBER

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `MIG_ID` | `varchar(50)` | 불가 | 아니오 |
| `SB_ID` | `varchar(12)` | 불가 | 아니오 |
| `MEM_NO` | `int` | 불가 | 아니오 |
| `MEM_EMAIL` | `varchar(70)` | 불가 | 아니오 |
| `ACCESS_ROUTE` | `varchar(50)` | 불가 | 아니오 |
| `M_FLAG` | `varchar(50)` | 불가 | 아니오 |
| `USE_YN` | `varchar(1)` | 불가 | 아니오 |
| `CDATE` | `datetime` | 불가 | 아니오 |
| `UDATE` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2016-10-20T15:36:20.600 |
| 읽기·참조 객체 | `migration_etcasp.dbo.migration_mapping_member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getTransferMap](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L351) — 바인딩: `comNo`. 결과 매핑: `MEM_NO` → `memNo`, `TRANSFER_GUBUN` → `transferGubun`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db003"></a>
## OFFICE.dbo.BUSINESS

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `BNS_ID` | `int` | 불가 | 예 |
| `BNS_SITE` | `varchar(100)` | 허용 | 아니오 |
| `BNS_LEADER` | `int` | 허용 | 아니오 |
| `BNS_CATEGORY` | `char(2)` | 허용 | 아니오 |
| `BNS_GRADE` | `char(1)` | 허용 | 아니오 |
| `SALE_RANK` | `int` | 허용 | 아니오 |
| `CONTACT_POINT` | `varchar(20)` | 허용 | 아니오 |
| `CONTACT_HP` | `varchar(20)` | 허용 | 아니오 |
| `CONTACT_EMAIL` | `varchar(200)` | 허용 | 아니오 |
| `AR_CUSTOMER` | `int` | 허용 | 아니오 |
| `AP_CUSTOMER` | `int` | 허용 | 아니오 |
| `SW_NO` | `int` | 허용 | 아니오 |
| `AR_USE_DATE` | `varchar(10)` | 허용 | 아니오 |
| `AP_USE_DATE` | `varchar(10)` | 허용 | 아니오 |
| `ENTRY_DATE` | `varchar(10)` | 허용 | 아니오 |
| `INF_TYPE` | `varchar(10)` | 허용 | 아니오 |
| `REG_DATE` | `datetime` | 허용 | 아니오 |
| `MOD_DATE` | `datetime` | 허용 | 아니오 |
| `BNS_CATEGORY_DTL` | `char(4)` | 허용 | 아니오 |
| `CONEXPDATE` | `varchar(10)` | 허용 | 아니오 |
| `STRATEGY` | `varchar(50)` | 허용 | 아니오 |
| `STRATEGY_DTL` | `varchar(50)` | 허용 | 아니오 |
| `RECEIVE_DATE` | `varchar(50)` | 허용 | 아니오 |
| `GROUP_NAME` | `varchar(20)` | 허용 | 아니오 |
| `STRATEGY_NEW` | `varchar(50)` | 허용 | 아니오 |
| `PM` | `int` | 허용 | 아니오 |
| `COM_REGNO` | `varchar(10)` | 허용 | 아니오 |
| `BNS_PRODUCT` | `varchar(2)` | 허용 | 아니오 |
| `BNS_DIVISION` | `char(1)` | 허용 | 아니오 |
| `BNS_SALES_STATUS` | `char(1)` | 허용 | 아니오 |
| `BNS_INTEGRATION_STATUS` | `char(1)` | 허용 | 아니오 |
| `BNS_SALES_GRADE` | `char(1)` | 허용 | 아니오 |
| `BNS_INTEGRATION_COMPLETED_DATE` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-05-07T17:28:41.240 |
| 읽기·참조 객체 | `office.dbo.business` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findSalesRepNames](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/CertificateRegistrationMapper.kt#L68) — 바인딩: `sbKey`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [selectHubCompanies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptCodeMapper.kt#L93) — 바인딩: `bnsName,jdbcType=VARCHAR`. 결과 매핑: `bns_id` → `bnsId`, `bns_site` → `bnsName`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db004"></a>
## Office.dbo.CTI_RequestMessage

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `IDX` | `int` | 불가 | 예 |
| `TRANSFER_ID` | `varchar(50)` | 불가 | 아니오 |
| `ERR_IDX` | `int` | 허용 | 아니오 |
| `PROCESS_ID` | `varchar(30)` | 허용 | 아니오 |
| `CUser` | `varchar(10)` | 허용 | 아니오 |
| `CDate` | `datetime` | 허용 | 아니오 |
| `IN_OUT` | `varchar(1)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2014-11-12T20:29:23.073 |
| 읽기·참조 객체 | `office.dbo.cti_requestmessage` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectSentMessages](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptCtiMapper.kt#L34) — 바인딩: `errorId`. 결과 매핑: `IDX` → `id`, `TRANSFER_ID` → `transferId`, `CUser` → `sentBy`, `CDate` → `sentAt`.
- [selectTransferId](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptCtiMapper.kt#L42) — 바인딩: `errorId`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db005"></a>
## Office.dbo.dept

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `DEPT_NO` | `int` | 불가 | 예 |
| `PT_NO` | `int` | 허용 | 아니오 |
| `DEPT_NAME` | `varchar(200)` | 허용 | 아니오 |
| `CREATE_DATE` | `datetime` | 허용 | 아니오 |
| `DEL_YN` | `char(1)` | 허용 | 아니오 |
| `DEL_DATE` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2017-08-22T16:55:56.443 |
| 읽기·참조 객체 | `office.dbo.dept` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectSawonOptions](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptCodeMapper.kt#L131) — 바인딩: . 결과 매핑: `sw_no` → `swNo`, `sname` → `sname`, `dept_name` → `deptName`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db006"></a>
## Office.dbo.dept_detail

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `DETAIL_NO` | `int` | 불가 | 예 |
| `SW_NO` | `int` | 허용 | 아니오 |
| `DEPT_NO` | `int` | 허용 | 아니오 |
| `CREATE_DATE` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2014-11-12T20:18:24.787 |
| 읽기·참조 객체 | `office.dbo.dept_detail` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectSawonOptions](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptCodeMapper.kt#L131) — 바인딩: . 결과 매핑: `sw_no` → `swNo`, `sname` → `sname`, `dept_name` → `deptName`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db007"></a>
## OFFICE.dbo.MNG_HUB

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `HUB_ID` | `int` | 불가 | 예 |
| `BNS_ID` | `int` | 허용 | 아니오 |
| `BRANCH_COM_COUNT` | `int` | 허용 | 아니오 |
| `AR_MNGR_NAME` | `varchar(20)` | 허용 | 아니오 |
| `AR_MNGR_TEL` | `varchar(20)` | 허용 | 아니오 |
| `AR_MNGR_HP` | `varchar(20)` | 허용 | 아니오 |
| `AR_MNGR_EMAIL` | `varchar(200)` | 허용 | 아니오 |
| `AP_MNGR_NAME` | `varchar(20)` | 허용 | 아니오 |
| `AP_MNGR_TEL` | `varchar(20)` | 허용 | 아니오 |
| `AP_MNGR_HP` | `varchar(20)` | 허용 | 아니오 |
| `AP_MNGR_EMAIL` | `varchar(200)` | 허용 | 아니오 |
| `SW_NO` | `int` | 허용 | 아니오 |
| `CREATE_DATE` | `datetime` | 허용 | 아니오 |
| `UPDATE_DATE` | `datetime` | 허용 | 아니오 |
| `FLAG` | `char(1)` | 허용 | 아니오 |
| `NETWORK_MNGR_NAME` | `varchar(20)` | 허용 | 아니오 |
| `NETWORK_MNGR_TEL` | `varchar(20)` | 허용 | 아니오 |
| `NETWORK_MNGR_HP` | `varchar(20)` | 허용 | 아니오 |
| `NETWORK_MNGR_EMAIL` | `varchar(200)` | 허용 | 아니오 |
| `TECH_MNGR_NAME` | `varchar(20)` | 허용 | 아니오 |
| `TECH_MNGR_TEL` | `varchar(20)` | 허용 | 아니오 |
| `TECH_MNGR_HP` | `varchar(20)` | 허용 | 아니오 |
| `TECH_MNGR_EMAIL` | `varchar(200)` | 허용 | 아니오 |
| `VIEW_DTI_YN` | `char(1)` | 허용 | 아니오 |
| `VIEW_DCT_YN` | `char(1)` | 허용 | 아니오 |
| `SYSTEM_ID` | `int` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2017-08-22T16:55:56.740 |
| 읽기·참조 객체 | `office.dbo.mng_hub` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findSalesRepNames](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/CertificateRegistrationMapper.kt#L68) — 바인딩: `sbKey`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [selectCompanies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptCodeMapper.kt#L71) — 바인딩: `schText,jdbcType=VARCHAR`, `schText,jdbcType=VARCHAR`, `schText,jdbcType=VARCHAR`, `schText,jdbcType=VARCHAR`. 결과 매핑: `com_regno` → `comRegno`, `com_name` → `comName`, `mem_realname` → `memRealname`, `mem_tel` → `memTel`, `routing_type` → `routingType`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db008"></a>
## Office.dbo.MNG_HUB_DETAIL

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `DETAIL_ID` | `int` | 불가 | 예 |
| `HUB_ID` | `int` | 허용 | 아니오 |
| `COM_REGNO` | `varchar(12)` | 허용 | 아니오 |
| `SW_NO` | `int` | 허용 | 아니오 |
| `CREATE_DATE` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2024-12-11T17:40:31.190 |
| 읽기·참조 객체 | `office.dbo.mng_hub_detail` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectCompanies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptCodeMapper.kt#L71) — 바인딩: `schText,jdbcType=VARCHAR`, `schText,jdbcType=VARCHAR`, `schText,jdbcType=VARCHAR`, `schText,jdbcType=VARCHAR`. 결과 매핑: `com_regno` → `comRegno`, `com_name` → `comName`, `mem_realname` → `memRealname`, `mem_tel` → `memTel`, `routing_type` → `routingType`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db009"></a>
## OFFICE.dbo.SAWON

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `SW_NO` | `int` | 불가 | 예 |
| `SID` | `varchar(15)` | 허용 | 아니오 |
| `PW` | `varchar(100)` | 허용 | 아니오 |
| `SNAME` | `varchar(20)` | 허용 | 아니오 |
| `CLASS` | `varchar(4)` | 허용 | 아니오 |
| `JOB` | `varchar(4)` | 허용 | 아니오 |
| `SW_EMAIL` | `varchar(200)` | 허용 | 아니오 |
| `HP` | `varchar(20)` | 허용 | 아니오 |
| `BIRTHDAY_TYPE` | `char(1)` | 허용 | 아니오 |
| `BIRTHDAY` | `varchar(8)` | 허용 | 아니오 |
| `ADMIN_TYPE` | `char(1)` | 허용 | 아니오 |
| `SUPER_RIGHT` | `char(1)` | 허용 | 아니오 |
| `JOIN_DATE` | `datetime` | 허용 | 아니오 |
| `LEAVE_DATE` | `datetime` | 허용 | 아니오 |
| `LEAVE_YN` | `char(1)` | 허용 | 아니오 |
| `CREATE_DATE` | `datetime` | 허용 | 아니오 |
| `pw_change_date` | `datetime` | 허용 | 아니오 |
| `sha256_YN` | `char(1)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2019-04-25T16:26:37.953 |
| 읽기·참조 객체 | `office.dbo.sawon` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findSalesRepNames](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/CertificateRegistrationMapper.kt#L68) — 바인딩: `sbKey`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findRevealAccountNumber](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/bulkaccountdeposit/repository/BulkAccountDepositMapper.kt#L40) — 바인딩: `idx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findActive](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/depositdeduction/repository/DepositDeductionMapper.kt#L40) — 바인딩: `channel`, `depositIdx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [selectSawonOptions](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptCodeMapper.kt#L131) — 바인딩: . 결과 매핑: `sw_no` → `swNo`, `sname` → `sname`, `dept_name` → `deptName`.
- [selectUserId](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptCtiMapper.kt#L45) — 바인딩: `swNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db010"></a>
## OFFICE.dbo.upApp_Account_Payment_View

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:07.607 |
| 읽기·참조 객체 | `office.dbo.sawon`, `smartbill3.dbo.account_bulk`, `smartbill3.dbo.account_bulk_app`, `smartbill3.dbo.common_code`, `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getDetailInfo](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/bulkaccountdeposit/repository/BulkAccountDepositMapper.kt#L77) — 바인딩: `idx`. 결과 매핑: `IDX` → `idx`, `PAYMENT_DATE` → `paymentDate`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `CODE_DETAIL_NM` → `codeDetailNm`, `BANK_CODE` → `bankCode`, `BANK_REGNO` → `bankRegno`, `AMOUT_PAYABLE` → `amountPayable`, `STATUS` → `status`, `COMPLETION_DATE` → `completionDate`, `DESCRIPTION` → `description`, `COM_NO` → `comNo`, `SNAME` → `sName`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT JOIN [SMARTBILL3].[dbo].[ACCOUNT_BULK] K ON P.[BANK_REGNO] = K.[BANK_REGNO]
LEFT JOIN [office].[dbo].[SAWON] N ON P.[SW_NO] = N.[SW_NO]
LEFT JOIN [SMARTBILL3].[DBO].[COMPANY] Y ON K.COM_NO = Y.COM_NO
LEFT JOIN [SMARTBILL3].[DBO].[COMMON_CODE] E ON P.[BANK_CODE] = E.[CODE] AND [CODE_TYPE] = 'BULK'
WHERE P.[IDX] = @IDX
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db011"></a>
## OFFICE.dbo.upApp_BusinessSawonList

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-10-12T09:52:27.963 |
| 읽기·참조 객체 | `office.dbo.dept_detail`, `office.dbo.dept_manager`, `office.dbo.sawon` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findSalesReps](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/CertificateRegistrationMapper.kt#L55) — 바인딩: . 결과 매핑: `sw_no` → `swNo`, `sname` → `sname`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
join sawon sa on dm.sw_no = sa.sw_no
where dept_no in (46, 47)
join sawon sa on dd.sw_no = sa.sw_no
where dept_no in (46, 47)
order by sname
select * from dept_manager where dept_no in (46, 47)
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db012"></a>
## Office.dbo.upCafe_Lst_MemCfrm_File

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@cafe_id` | `varchar(15)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:09.120 |
| 읽기·참조 객체 | `smartbill3.dbo.tax_memcfrm`, `smartbill3.dbo.tax_memcfrm_detail` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getUploadList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/registrationinquiry/repository/RegistrationInquiryMapper.kt#L44) — 바인딩: `cafeId`. 결과 매핑: `memcfrm_date` → `memcfrmDate`, `memcfrm_file` → `memcfrmFile`, `memcfrm_memname` → `memcfrmMemname`, `mem_count` → `memCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Select @com_count = count(memcfrm_com_regno) from smartbill3.dbo.tax_memcfrm_detail where cafe_id = @cafe_id
Where cafe_id = @cafe_id
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db013"></a>
## Office.dbo.upCafe_Sav_Memcfrm02

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@cafe_id` | `varchar(15)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@com_regno` | `varchar(13)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@com_name` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@mem_email` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@mem_hp` | `varchar(14)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:09.057 |
| 읽기·참조 객체 | `smartbill3.dbo.tax_memcfrm_detail` |
| 쓰기 대상 | `smartbill3.dbo.tax_memcfrm_detail` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `0`; `1` |

### Mapper 입출력 매핑

- [saveCompanyDetail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/registrationinquiry/repository/RegistrationInquiryMapper.kt#L130) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `cafeId`, `businessNumber`, `companyName`, `email`, `phone`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db014"></a>
## Office.dbo.upCafe_Sav_MemcfrmFile

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@cafe_id` | `varchar(15)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@mem_name` | `varchar(24)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@bulk_file` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:09.093 |
| 읽기·참조 객체 | `smartbill3.dbo.tax_memcfrm`, `smartbill3.dbo.tax_memcfrm_detail` |
| 쓰기 대상 | `smartbill3.dbo.tax_memcfrm`, `smartbill3.dbo.tax_memcfrm_detail` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `0`; `1` |

### Mapper 입출력 매핑

- [saveFileMetadata](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/registrationinquiry/repository/RegistrationInquiryMapper.kt#L121) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `cafeId`, `uploaderName`, `filename`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
begin tran
delete from smartbill3.dbo.tax_memcfrm where cafe_id = @cafe_id
delete from smartbill3.dbo.tax_memcfrm_detail where cafe_id=@cafe_id
rollback
Commit
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db015"></a>
## Office.dbo.upCOM_HubName

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:05.637 |
| 읽기·참조 객체 | `office.dbo.business`, `office.dbo.mng_hub`, `office.dbo.mng_hub_detail`, `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getHubNameList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L568) — 바인딩: `comNo`. 결과 매핑: `BNS_SITE` → `bnsSite`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE A.BNS_ID = B.BNS_ID
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db016"></a>
## Office.dbo.upCTI_SaveRequestMessage

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@TRANSFER_ID` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PROCESS_ID` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CUser` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@InOut` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:09.387 |
| 읽기·참조 객체 | `office.dbo.cti_requestmessage` |
| 쓰기 대상 | `office.dbo.cti_requestmessage` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [saveSentMessage](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptCtiMapper.kt#L84) — 바인딩: `transferId`, `userId`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Begin Tran
rollback
Commit
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db017"></a>
## Office.dbo.upGW_CntErrCode

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@today` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:08.187 |
| 읽기·참조 객체 | `office.dbo.error_managemennt` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectTodayCount](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptMapper.kt#L170) — 바인딩: `today`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
where convert(varchar(10), err_date, 120) = @today
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db018"></a>
## Office.dbo.upGW_CompanyINFO

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2023-06-02T10:13:00.720 |
| 읽기·참조 객체 | `migration_etcasp.dbo.migration_mapping_company`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getCompanyInfoList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L210) — 바인딩: `comNo`. 결과 매핑: `COM_NO` → `comNo`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `COM_PRESIDENT` → `comPresident`, `COM_ZIPCODE` → `comZipcode`, `COM_ADDRESS` → `comAddress`, `COM_STATUS` → `comStatus`, `COM_SEAL` → `comSeal`, `CERT_DN` → `certDn`, `COM_ENTRY_DATE` → `comEntryDate`, `COM_MODIFY_DATE` → `comModifyDate`, `MEM_NO` → `memNo`, `MEM_NAME` → `memName`, `MEM_REGNO` → `memRegno`, `MEM_ID` → `memId`, `MEM_TYPE` → `memType`, `MEM_TEL` → `memTel`, `MEM_EMAIL` → `memEmail`, `MEM_STATUS` → `memStatus`, `MEM_ENTRY_DATE` → `memEntryDate`, `MEM_HP` → `memHp`, `COM_BIZSTATUS` → `comBizstatus`, `COM_BIZCLASS` → `comBizclass`, `BIZ_CTG` → `bizCtg`, `BIZ_CTG_DETAIL` → `bizCtgDetail`, `MEM_REALNAME` → `memRealname`, `MEM_MODIFY_DATE` → `memModifyDate`, `MEM_DEL_YN` → `memDelYn`, `M_FLAG` → `mFlag`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
INNER JOIN SMARTBILL3..MEMBER M WITH(NOLOCK) ON C.COM_NO=M.COM_NO
LEFT JOIN MIGRATION_ETCASP..MIGRATION_MAPPING_COMPANY MIG WITH(NOLOCK) ON C.COM_NO = MIG.COM_NO
WHERE C.COM_NO = @COM_NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db019"></a>
## Office.dbo.upGW_DeptInfo

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:08.697 |
| 읽기·참조 객체 | `office.dbo.dept` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectDepts](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/source/repository/SourceManagementCodeMapper.kt#L36) — 바인딩: . 결과 매핑: `DEPT_NO` → `deptNo`, `DEPT_NAME` → `deptName`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE DEL_YN='N'
ORDER BY DEPT_NAME ASC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db020"></a>
## Office.dbo.upGW_ErrREqTeamGroupList

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:09.503 |
| 읽기·참조 객체 | `office.dbo.dept`, `office.dbo.function_code` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectTeams](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptCodeMapper.kt#L106) — 바인딩: . 결과 매핑: `dept_no` → `deptNo`, `dept_name` → `deptName`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
join function_code b on a.dept_no = b.code and b.cate01 = 'ERROR_REQ_TEAM'
order by  dept_name
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db021"></a>
## office.dbo.upGW_Lst_SumDailyDCT01

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@yymm` | `varchar(7)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:08.453 |
| 읽기·참조 객체 | `smartbill3.dbo.mng_daily_dct_sum` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectDailyElectronicContractUsage](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/dailyelectroniccontractusage/repository/DailyElectronicContractUsageMapper.kt#L33) — 바인딩: `yymm, mode=IN, jdbcType=VARCHAR`. 결과 매핑: `use_date` → `useDate`, `ar_com_count` → `arComCount`, `ar_dct_count` → `arDctCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
where  convert(varchar(7),use_date,120)=@yymm
order by use_date
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db022"></a>
## office.dbo.upGW_Lst_SumDailyDTI01

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@YYMM` | `varchar(7)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:09.117 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti.dbo.dti_header_giro_cub`, `sb_dti.dbo.dti_header_giro_cub_2nd_2020`, `sb_dti.dbo.dti_header_giro_cub_2nd_2021`, `sb_dti.dbo.dti_header_giro_cub_2nd_2022`, `sb_dti.dbo.dti_header_giro_cub_2nd_2023`, `sb_dti.dbo.dti_header_giro_cub_part`, `smartbill3.dbo.mng_daily_sum` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectDailyTaxInvoiceUsage](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/dailytaxinvoiceusage/repository/DailyTaxInvoiceUsageMapper.kt#L38) — 바인딩: `yymm, mode=IN, jdbcType=VARCHAR`. 결과 매핑: `USE_DATE` → `useDate`, `AR_COM_COUNT` → `arComCount`, `AR_DTI_COUNT` → `arDtiCount`, `AR_COM_G_COUNT` → `arComGCount`, `AR_DTI_G_COUNT` → `arDtiGCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @TODATE = (SELECT TOP 1
SET @IN_YYMM = (SELECT TOP 1
SET @FROM_TODATE = @TODATE + ' 00:00:00'
SET @TO_TODATE = @TODATE + ' 23:59:59'
WHERE
WHERE
WHERE
WHERE
GROUP  BY
WHERE
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_giro_cub`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db023"></a>
## Office.dbo.upGW_LstDTIMismatch

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:09.003 |
| 읽기·참조 객체 | `office.dbo.dti_mismatch_alarm`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectDtiMismatchAlarms](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptCodeMapper.kt#L149) — 바인딩: . 결과 매핑: `IDX` → `idx`, `ETC_PCS_NO` → `etcPcsNo`, `ISSUE_ID` → `issueId`, `SUP_COM_NAME` → `supComName`, `CDATE` → `cdate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE
ORDER  BY
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_header_cub`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db024"></a>
## Office.dbo.upGW_MemAdminInfo1

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@com_no` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:09.150 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getCorporateAdmin](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L683) — 바인딩: `comNo`. 결과 매핑: `MEM_NO` → `memNo`, `MEM_ID` → `memId`, `MEM_NAME` → `memName`, `MEM_REALNAME` → `memRealname`, `MEM_TEL` → `memTel`, `MEM_HP` → `memHp`, `MEM_EMAIL` → `memEmail`, `MEM_DEL_YN` → `memDelYn`, `MEM_ENTRY_DATE` → `memEntryDate`, `MEM_MODIFY_DATE` → `memModifyDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Join smartbill3..member m on m.com_no = c.com_no
Where c.com_no = @com_no and mem_type = 'F'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db025"></a>
## Office.dbo.upGW_MemAdminInfo2

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@service_type` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@com_no` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:09.170 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.dept_manager`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getEContractAdminList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L721) — 바인딩: `serviceType`, `comNo`. 결과 매핑: `MEM_NO` → `memNo`, `MEM_ID` → `memId`, `MEM_NAME` → `memName`, `MEM_REALNAME` → `memRealname`, `MEM_TEL` → `memTel`, `MEM_HP` → `memHp`, `MEM_EMAIL` → `memEmail`, `MEM_DEL_YN` → `memDelYn`, `MEM_ENTRY_DATE` → `memEntryDate`, `MEM_MODIFY_DATE` → `memModifyDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Left outer join smartbill3..company c on dm.com_no = c.com_no
Left outer join smartbill3..member m on dm.mem_no = m.mem_no and m.mem_del_yn = 'N'
Where  dm.service_type = @service_type and dm.com_no = @com_no
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db026"></a>
## Office.dbo.upGW_MemAdminInfo3

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@com_no` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:09.230 |
| 읽기·참조 객체 | `smartbill3.dbo.member`, `smartbill3.dbo.tax_admin` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getTaxCafeAdmin](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L741) — 바인딩: `comNo`. 결과 매핑: `MEM_NO` → `memNo`, `MEM_ID` → `memId`, `MEM_NAME` → `memName`, `MEM_REALNAME` → `memRealname`, `MEM_TEL` → `memTel`, `MEM_HP` → `memHp`, `MEM_EMAIL` → `memEmail`, `MEM_DEL_YN` → `memDelYn`, `MEM_ENTRY_DATE` → `memEntryDate`, `MEM_MODIFY_DATE` → `memModifyDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Join smartbill3..member me on ca.mem_no = me.mem_no
Where me.com_no = @com_no  and mem_rgt='F'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db027"></a>
## Office.dbo.upGW_MemAdminInfo4

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@comId` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:08.967 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.dept_manager`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getReceivableAdminList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L758) — 바인딩: `comId`. 결과 매핑: `MEM_NO` → `memNo`, `MEM_ID` → `memId`, `MEM_NAME` → `memName`, `MEM_REALNAME` → `memRealname`, `MEM_TEL` → `memTel`, `MEM_HP` → `memHp`, `MEM_EMAIL` → `memEmail`, `MEM_DEL_YN` → `memDelYn`, `MEM_ENTRY_DATE` → `memEntryDate`, `MEM_MODIFY_DATE` → `memModifyDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Left outer join smartbill3..company c on dm.com_no = c.com_no
Left outer join smartbill3..member m on dm.mem_no = m.mem_no and m.mem_del_yn = 'N'
Where  dm.service_type = 'drc' and dm.com_no = @comId
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db028"></a>
## Office.dbo.upGW_ModError

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@err_idx` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_status` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@req_team` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_bns_name` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_bns_id` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@routing_type` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_code` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_type` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@svc_type` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_detail_code` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@error_etc` | `varchar(500)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:05.330 |
| 읽기·참조 객체 | `office.dbo.error_managemennt` |
| 쓰기 대상 | `office.dbo.error_managemennt` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [updateErrorReceipt](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptMapper.kt#L199) — 바인딩: `errIdx`, `errStatus`, `reqTeam`, `errBnsName`, `errBnsId`, `routingType`, `errCode`, `errType`, `svcType`, `errDetailCode`, `errorEtc`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
where err_idx = @err_idx
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db029"></a>
## Office.dbo.upGW_ModErrorEndDate

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@err_idx` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:07.330 |
| 읽기·참조 객체 | `office.dbo.error_managemennt` |
| 쓰기 대상 | `office.dbo.error_managemennt` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [updateEndDate](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptMapper.kt#L208) — 바인딩: `errIdx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
where err_idx = @err_idx
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db030"></a>
## Office.dbo.upGW_OrganSupport_Regist

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@SERVICE_NAME` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_REGNO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@UNIQUE_KEY` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@STATUS` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DEFAULT_URL` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MENU_CALLER` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ENCRYPTION_VALUE` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SYSTEM_CODE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@AUTH_OPTION` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2020-04-16T10:06:06.113 |
| 읽기·참조 객체 | `sb_common.dbo.sso_info`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | `sb_common.dbo.sso_info` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [registerSso](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L1097) — 바인딩: `serviceName`, `comRegno`, `uniqueKey`, `status`, `defaultUrl`, `menuCaller`, `encryptionValue`, `systemCode`, `authOption`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SELECT * FROM [SB_COMMON].[dbo].[SSO_INFO] WITH(NOLOCK) WHERE COM_REGNO = @COM_REGNO
SET @MOD = 'UPDATE'
SET @MOD = 'INSERT'
SET @ADMIN_NO = 3
SELECT @SERVICEID = MAX(SERVICE_ID) FROM [SB_COMMON].[dbo].[SSO_INFO] WITH(NOLOCK) WHERE SERVICE_ID < 999
SELECT @SERVICEID = MAX(SERVICE_ID) FROM [SB_COMMON].[dbo].[SSO_INFO] WITH(NOLOCK) WHERE SERVICE_ID > 999
FROM   [SmartBill3].[dbo].[COMPANY] C WITH(NOLOCK) INNER JOIN
WHERE  com_del_yn <> 'Y' AND
SET @ADMIN_NO = 1
WHERE
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db031"></a>
## Office.dbo.upGW_OrganSupport_Select

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_REGNO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2020-04-16T10:06:06.570 |
| 읽기·참조 객체 | `sb_common.dbo.sso_info` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getSsoConfigList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L780) — 바인딩: `comRegno`. 결과 매핑: `COM_REGNO` → `comRegno`, `UNIQUE_KEY` → `uniqueKey`, `DEFAULT_URL` → `defaultUrl`, `MENU_CALLER` → `menuCaller`, `ENCRYPTION_VALUE` → `encryptionValue`, `SYSTEM_CODE` → `systemCode`, `AUTH_OPTION` → `authOption`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE COM_REGNO = @COM_REGNO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db032"></a>
## Office.dbo.upGW_SaveError

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@err_num` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@write_sw_no` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@sw_no` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_com_regno` | `varchar(13)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_com_name` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_com_admin` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_com_phone` | `varchar(15)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_title` | `varchar(256)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_content` | `text` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_file` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_type` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@routing_type` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_code` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_status` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@req_team` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@sms_chk` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@call_no` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:05.367 |
| 읽기·참조 객체 | `office.dbo.error_managemennt` |
| 쓰기 대상 | `office.dbo.error_managemennt` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [insertErrorReceipt](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptMapper.kt#L185) — 바인딩: `errNum`, `writeSwNo`, `swNo`, `errComRegno`, `errComName`, `errComAdmin`, `errComPhone`, `errTitle`, `errContent, jdbcType=LONGVARCHAR`, `errFile`, `errType`, `routingType`, `errCode`, `errStatus`, `reqTeam`, `smsChk`, `callNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db033"></a>
## Office.dbo.upGW_SaveErrorDetail

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@err_idx` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@sw_no` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@deal_time_h` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@deal_content` | `text` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@deal_status` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@deal_team` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@str_file` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:07.110 |
| 읽기·참조 객체 | `office.dbo.error_deal` |
| 쓰기 대상 | `office.dbo.error_deal` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [insertDeal](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptDealMapper.kt#L66) — 바인딩: `errIdx`, `swNo`, `dealTimeH, jdbcType=VARCHAR`, `dealContent, jdbcType=LONGVARCHAR`, `dealStatus`, `dealTeam`, `strFile`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db034"></a>
## Office.dbo.UPGW_SaveSrcMng

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@MODE` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TITLE` | `varchar(500)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DEPT_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DEV_SW_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DEMO_REG_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PRD_REG_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REG_STATUS` | `varchar(5)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CONTENTS` | `text` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REG_MEM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TYPE1` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@APPROVAL_NO` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SVC_CATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@APPRO_BILL_NO` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SVC_CATE_DETAIL` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2024-04-08T15:39:32.643 |
| 읽기·참조 객체 | `office.dbo.mng_src` |
| 쓰기 대상 | `office.dbo.mng_src` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `@ERROR`; `@ERROR` |

### Mapper 입출력 매핑

- [saveSrcMng](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/source/repository/SourceManagementMapper.kt#L123) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `mode`, `idx`, `title`, `deptNo`, `devSwNo`, `demoRegDate`, `prdRegDate`, `regStatus`, `contents, jdbcType=LONGVARCHAR`, `regMemNo`, `type1`, `approvalNo`, `svcCate`, `approBillNo`, `svcCateDetail`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @ERROR = 0
WHERE IDX = @IDX
DELETE FROM MNG_SRC WHERE IDX = @IDX
UPDATE MNG_SRC SET REG_STATUS = @REG_STATUS, UDATE = GETDATE() WHERE IDX = @IDX
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db035"></a>
## OFFICE.dbo.upGW_SawonInfo

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@sw_no` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:05.610 |
| 읽기·참조 객체 | `office.dbo.sawon` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findSawonInfo](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcCompanyLinkMapper.kt#L100) — 바인딩: `swNo`. 결과 매핑: `SNAME` → `sname`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE SW_NO=@sw_no
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db036"></a>
## Office.dbo.upGW_SawonList

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DEPT_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:04.620 |
| 읽기·참조 객체 | `office.dbo.dept_detail`, `office.dbo.sawon` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectSawonByDept](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/source/repository/SourceManagementCodeMapper.kt#L49) — 바인딩: `deptNo`. 결과 매핑: `SW_NO` → `swNo`, `SNAME` → `sname`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
JOIN SAWON SA ON DD.SW_NO = SA.SW_NO
WHERE LEAVE_YN ='N'
ORDER BY SA.SNAME ASC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db037"></a>
## office.dbo.upGW_Sch_SumMonthDCT01

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@from_yymm` | `varchar(7)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@to_yymm` | `varchar(7)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:08.460 |
| 읽기·참조 객체 | `smartbill3.dbo.mng_monthly_dct_sum` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectDctMonthly](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/monthlyusage/repository/MonthlyUsageMapper.kt#L66) — 바인딩: `fromYymm, mode=IN, jdbcType=VARCHAR`, `toYymm,   mode=IN, jdbcType=VARCHAR`. 결과 매핑: `use_yymm` → `useYymm`, `ar_com_count` → `arComCount`, `ar_dct_count` → `arDctCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
where use_yymm between @from_yymm and @to_yymm
order by use_yymm
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db038"></a>
## office.dbo.upGW_Sch_SumMonthDTI01

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@from_yymm` | `varchar(7)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@to_yymm` | `varchar(7)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:06.050 |
| 읽기·참조 객체 | `smartbill3.dbo.mng_monthly_sum` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectDtiMonthly](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/monthlyusage/repository/MonthlyUsageMapper.kt#L47) — 바인딩: `fromYymm, mode=IN, jdbcType=VARCHAR`, `toYymm,   mode=IN, jdbcType=VARCHAR`. 결과 매핑: `use_yymm` → `useYymm`, `ar_com_count` → `arComCount`, `ar_dti_count` → `arDtiCount`, `mem_count` → `memCount`, `ar_com_g_count` → `arComGCount`, `ar_dti_g_count` → `arDtiGCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
where use_yymm between @from_yymm and @to_yymm
order by use_yymm
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db039"></a>
## office.dbo.upGW_SELECT_DTI_DAILY_DATA

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@FROM_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2025-02-19T15:57:06.877 |
| 읽기·참조 객체 | 정적으로 확정한 테이블 없음 |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectDailyTaxInvoiceAggregate](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/dailytaxinvoiceaggregate/repository/DailyTaxInvoiceAggregateMapper.kt#L39) — 바인딩: `yearMonth, mode=IN, jdbcType=VARCHAR`. 결과 매핑: `DTI_ISSUEDATE` → `issueDate`, `TOTAL_COUNT` → `totalCount`, `WEB_COUNT` → `webCount`, `LINK_COUNT` → `linkCount`, `TOTAL_COUNT_COM` → `totalCountCom`, `WEB_COUNT_COM` → `webCountCom`, `LINK_COUNT_COM` → `linkCountCom`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @FROM_DATE = @FROM_DATE + '-01'
SET @TO_DATE = DATEADD(DAY, -1, DATEADD(MONTH, 1, CONVERT(DATE, @FROM_DATE)))
SET @PARAM = N'@FROM_DATE VARCHAR(10), @TO_DATE VARCHAR(10)'
SET @STRSQL = N'
WHERE
ORDER BY DTI_ISSUEDATE ASC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db040"></a>
## Office.dbo.upGw_SelectSrcMng

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2024-04-08T16:30:00.777 |
| 읽기·참조 객체 | `office.dbo.dept`, `office.dbo.mng_src`, `office.dbo.sawon` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectDetail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/source/repository/SourceManagementMapper.kt#L105) — 바인딩: `idx`. 결과 매핑: `IDX` → `idx`, `TITLE` → `title`, `DEPT_NO` → `deptNo`, `DEPT_NAME` → `deptName`, `DEV_SW_NO` → `devSwNo`, `SNAME` → `sname`, `DEMO_REG_DATE` → `demoRegDate`, `PRD_REG_DATE` → `prdRegDate`, `REG_STATUS` → `regStatus`, `CONTENTS` → `contents`, `REG_MEM_NO` → `regMemNo`, `REG_MEM_NAME` → `regMemName`, `TYPE1` → `type1`, `APPROVAL_NO` → `approvalNo`, `SVC_CATE` → `svcCate`, `APPRO_BILL_NO` → `approBillNo`, `SVC_CATE_DETAIL` → `svcCateDetail`, `CDATE` → `cdate`, `UDATE` → `udate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
JOIN DEPT DT ON MR.DEPT_NO = DT.DEPT_NO
JOIN SAWON SA ON MR.DEV_SW_NO = SA.SW_NO
WHERE IDX = @IDX
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db041"></a>
## Office.dbo.UPGW_SERVERCERTIYN

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:08.830 |
| 읽기·참조 객체 | `sb_dti.dbo.company_dticonfig` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getServerCertificateYn](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L766) — 바인딩: `comNo`. 결과 매핑: `SERVER_CERTI_YN` → `serverCertiYn`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE COM_NO = @COM_NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db042"></a>
## Office.dbo.UPGW_SRCLIST

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@REG_TYPE` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REG_FROM_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REG_TO_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DEV_TYPE` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DEV_KEYWORD` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REG_STATUS` | `varchar(5)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DEPT_NO` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2010-04-06T19:05:54.317 |
| 읽기·참조 객체 | `office.dbo.dept`, `office.dbo.mng_src`, `office.dbo.sawon` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/source/repository/SourceManagementMapper.kt#L55) — 바인딩: `regType`, `regFromDate`, `regToDate`, `devType`, `devKeyword`, `regStatus`, `deptNo`. 결과 매핑: `IDX` → `idx`, `TITLE` → `title`, `DEPT_NAME` → `deptName`, `SNAME` → `sname`, `DEMO_REG_DATE` → `demoRegDate`, `PRD_REG_DATE` → `prdRegDate`, `REG_STATUS` → `regStatus`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SQL = '
JOIN DEPT DT ON MR.DEPT_NO = DT.DEPT_NO
JOIN SAWON SA ON MR.DEV_SW_NO = SA.SW_NO WHERE 1=1 '
SET @REG_TO_DATE = CONVERT(VARCHAR(10),DATEADD(D,1,@REG_TO_DATE),120)
SET @SQL = @SQL + ' AND DEMO_REG_DATE BETWEEN ''' + @REG_FROM_DATE + ''' AND ''' + @REG_TO_DATE + ''' '
SET @SQL = @SQL + ' AND PRD_REG_DATE BETWEEN ''' + @REG_FROM_DATE + ''' AND ''' + @REG_TO_DATE + ''' '
SET @SQL = @SQL + ' AND TITLE LIKE ''%'+@DEV_KEYWORD+ '%'' '
SET @SQL = @SQL + ' AND REG_STATUS IN ('+@REG_STATUS+') '
SET @SQL = @SQL + ' AND MR.DEPT_NO = '+ @DEPT_NO
SET @SQL = @SQL +' ORDER BY IDX DESC '
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db043"></a>
## Office.dbo.UPGW_SRCLISTCOUNT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@REG_TYPE` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REG_FROM_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REG_TO_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DEV_TYPE` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DEV_KEYWORD` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REG_STATUS` | `varchar(5)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DEPT_NO` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2010-04-06T17:48:48.100 |
| 읽기·참조 객체 | `office.dbo.dept`, `office.dbo.mng_src`, `office.dbo.sawon` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectListCount](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/source/repository/SourceManagementMapper.kt#L71) — 바인딩: `regType`, `regFromDate`, `regToDate`, `devType`, `devKeyword`, `regStatus`, `deptNo`. 결과 매핑: `CNT` → `cnt`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SQL = '
JOIN DEPT DT ON MR.DEPT_NO = DT.DEPT_NO
JOIN SAWON SA ON MR.DEV_SW_NO = SA.SW_NO WHERE 1=1 '
SET @REG_TO_DATE = CONVERT(VARCHAR(10),DATEADD(D,1,@REG_TO_DATE),120)
SET @SQL = @SQL + ' AND DEMO_REG_DATE BETWEEN ''' + @REG_FROM_DATE + ''' AND ''' + @REG_TO_DATE + ''' '
SET @SQL = @SQL + ' AND PRD_REG_DATE BETWEEN ''' + @REG_FROM_DATE + ''' AND ''' + @REG_TO_DATE + ''' '
SET @SQL = @SQL + ' AND TITLE LIKE ''%'+@DEV_KEYWORD+ '%'' '
SET @SQL = @SQL + ' AND REG_STATUS IN ('+@REG_STATUS+') '
SET @SQL = @SQL + ' AND MR.DEPT_NO = '+ @DEPT_NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db044"></a>
## Office.dbo.upGW_ViewErrorDetail

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@err_idx` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:07.330 |
| 읽기·참조 객체 | `office.dbo.dept`, `office.dbo.error_deal`, `office.dbo.sawon` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectDeals](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptDealMapper.kt#L38) — 바인딩: `errIdx`. 결과 매핑: `err_dtl_idx` → `errDtlIdx`, `sname` → `sname`, `deal_time_h` → `dealTimeH`, `deal_content` → `dealContent`, `deal_status` → `dealStatus`, `deal_date` → `dealDate`, `dept_name` → `deptName`, `str_file` → `strFile`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
join sawon s on e.sw_no = s.sw_no
left outer join dept d on e.deal_team = d.dept_no
where err_idx = @err_idx
order by deal_date
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db045"></a>
## Office.dbo.upGW_ViewErrorHistory

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@err_num` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:05.680 |
| 읽기·참조 객체 | `office.dbo.error_managemennt` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectRelatedErrors](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptMapper.kt#L161) — 바인딩: `regno`. 결과 매핑: `ERR_IDx` → `errIdx`, `ERR_NUM` → `errNum`, `ERR_COM_ADMIN` → `errComAdmin`, `ERR_COM_PHONE` → `errComPhone`, `ERR_TITLE` → `errTitle`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
where ERR_COM_REGNO = @err_num
order by ERR_IDx DESC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db046"></a>
## Office.dbo.upGW_ViewErrorReply

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@err_idx` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:07.343 |
| 읽기·참조 객체 | `office.dbo.error_reply`, `office.dbo.sawon` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectReplies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptDealMapper.kt#L53) — 바인딩: `errIdx`. 결과 매핑: `reply_content` → `replyContent`, `sname` → `sname`, `reply_file` → `replyFile`, `reg_date` → `regDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
join sawon s on s.sw_no = y.reply_swno
where err_idx = @err_idx
order by reg_date
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db047"></a>
## Office.dbo.upHub_HubList03

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2017-12-05T11:32:49.133 |
| 읽기·참조 객체 | `office.dbo.business`, `office.dbo.mng_hub` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findHubCompanies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcHubErrorMapper.kt#L59) — 바인딩: . 결과 매핑: `hub_id` → `hubId`, `bns_site` → `bnsSite`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
select distinct hub_id, bns_site from business a join mng_hub b on a.bns_id = b.bns_id order by bns_site asc
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db048"></a>
## Office.dbo.upMem_LstSettle

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@service_type` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@com_no` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:06.217 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.settlement` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getBillingPlan](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L560) — 바인딩: `serviceType`, `comNo`. 결과 매핑: `BILL_TYPE` → `billType`, `COM_ENTRY_DATE` → `comEntryDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Join smartbill3..company c on sm.com_no = c.com_no
Where  sm.com_no = @com_no and  service_type = @service_type
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db049"></a>
## office.dbo.upNT_CnttNoticeReply

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@noti_id` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:06.590 |
| 읽기·참조 객체 | `office.dbo.notice_reply` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [countReplies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/spfBoard/repository/AdminSpfBoardReplyMapper.kt#L45) — 바인딩: `notiId`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
where noti_id = @noti_id
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db050"></a>
## office.dbo.upNT_DelNotice

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@note_id` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:08.920 |
| 읽기·참조 객체 | `office.dbo.notice`, `office.dbo.notice_reply` |
| 쓰기 대상 | `office.dbo.notice`, `office.dbo.notice_reply` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [deleteBoard](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/spfBoard/repository/AdminSpfBoardMapper.kt#L87) — 바인딩: `noteId`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Delete from notice  Where noti_id = @note_id
Delete from notice_reply  Where noti_id = @note_id
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db051"></a>
## office.dbo.upNT_DelNotiReply

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@reply_id` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:06.287 |
| 읽기·참조 객체 | `office.dbo.notice_reply` |
| 쓰기 대상 | `office.dbo.notice_reply` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [deleteReply](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/spfBoard/repository/AdminSpfBoardReplyMapper.kt#L53) — 바인딩: `replyId`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
where reply_id = @reply_id
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db052"></a>
## office.dbo.upNT_LstNotice

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@sch_Code` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@sch_Text` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@noti_id` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@strDiv` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2007-08-24T19:33:36.200 |
| 읽기·참조 객체 | `office.dbo.notice`, `office.dbo.sawon` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchBoards](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/spfBoard/repository/AdminSpfBoardMapper.kt#L51) — 바인딩: `schCode`, `schText`, `notiId`, `strDiv`. 결과 매핑: `noti_id` → `notiId`, `noti_type` → `notiType`, `title` → `title`, `content` → `content`, `att_file` → `attFile`, `hit` → `hit`, `reg_Date` → `regDate`, `sname` → `sname`, `sw_no` → `swNo`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
set @strSql = ' set nocount on
join sawon s
where noti_type = ''' + @strDiv + ''''
set @strSql = @strSql + 'and noti_id = '''+cast(@noti_id as varchar)+''''
set @strSql = @strSql + ' and (title like ''%'+@sch_Text+'%''  or content like ''%'+@sch_Text+'%'')'
set @strSql = @strSql + ' and sname like ''%'+@sch_Text+'%'''
set @strSql = @strSql + ' order by noti_id desc set nocount off '
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db053"></a>
## office.dbo.upnt_LstNotiReply

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@noti_id` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:06.467 |
| 읽기·참조 객체 | `office.dbo.notice_reply`, `office.dbo.sawon` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [listReplies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/spfBoard/repository/AdminSpfBoardReplyMapper.kt#L40) — 바인딩: `notiId`. 결과 매핑: `noti_id` → `notiId`, `sw_no` → `swNo`, `reg_date` → `regDate`, `content` → `content`, `sname` → `sname`, `reply_id` → `replyId`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
join sawon s on nr.sw_no = s.sw_no
where noti_id = @noti_id
order by reg_date desc
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db054"></a>
## office.dbo.upNT_ModNotice

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@note_id` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@title` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@content` | `text` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@att_file` | `varchar(1000)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:09 |
| 읽기·참조 객체 | `office.dbo.notice` |
| 쓰기 대상 | `office.dbo.notice` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [modBoard](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/spfBoard/repository/AdminSpfBoardMapper.kt#L79) — 바인딩: `noteId`, `title`, `content`, `attFile`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Where noti_id = @note_id
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db055"></a>
## office.dbo.upNT_SavNotice

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@noti_type` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@title` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@content` | `text` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@att_file` | `varchar(1000)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@hit` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@sw_no` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:07.777 |
| 읽기·참조 객체 | `office.dbo.notice` |
| 쓰기 대상 | `office.dbo.notice` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [saveBoard](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/spfBoard/repository/AdminSpfBoardMapper.kt#L71) — 바인딩: `notiType`, `title`, `content`, `attFile`, `hit`, `swNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db056"></a>
## office.dbo.upNT_SavNotiReply

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@noti_id` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@sw_no` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@content` | `varchar(1000)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:06.333 |
| 읽기·참조 객체 | `office.dbo.notice_reply` |
| 쓰기 대상 | `office.dbo.notice_reply` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [saveReply](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/spfBoard/repository/AdminSpfBoardReplyMapper.kt#L49) — 바인딩: `notiId`, `swNo`, `content`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db057"></a>
## office.dbo.upNT_UpHitNotice

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@noti_id` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:07.973 |
| 읽기·참조 객체 | `office.dbo.notice` |
| 쓰기 대상 | `office.dbo.notice` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [incrementHit](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/spfBoard/repository/AdminSpfBoardMapper.kt#L58) — 바인딩: `notiId`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
where noti_id = @noti_id
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db058"></a>
## OFFICE.dbo.upPJT_BNSHubList_mnghub

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@BNS_PRODUCT` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2017-01-02T14:49:24.850 |
| 읽기·참조 객체 | `office.dbo.business`, `office.dbo.function_code`, `office.dbo.mng_hub` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findHubCompanies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcCompanyLinkMapper.kt#L91) — 바인딩: `productCode`. 결과 매핑: `hub_id` → `hubId`, `bns_site` → `bnsSite`, `BNS_PRODUCT` → `bnsProduct`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
where a.bns_id = b.bns_id
order by bns_site asc
where a.bns_id = b.bns_id
order by bns_site asc
```

하위 프로시저·함수·뷰: `office.dbo.hubproduct`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db059"></a>
## OFFICE.dbo.upPJT_MNGHubList

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-12-09T15:10:27.490 |
| 읽기·참조 객체 | `office.dbo.business`, `office.dbo.function_code`, `office.dbo.mng_hub` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findHubVendors](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/AuthKeyMapper.kt#L106) — 바인딩: . 결과 매핑: `HUB_ID` → `hubId`, `BNS_SITE` → `bnsSite`, `BNS_PRODUCT` → `bnsProduct`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
select B.BNS_SITE, H.HUB_ID,ISNULL([OFFICE].[dbo].HUBPRODUCT(B.BNS_PRODUCT),'') AS BNS_PRODUCT    from office..mng_hub H with(nolock) join (SELECT * FROM office..business With(nolock) WHERE BNS_PRODUCT = '03') B  on H.BNS_ID = B.BNS_ID
where bns_grade in('F','G','H')
order by bns_site asc
```

하위 프로시저·함수·뷰: `office.dbo.hubproduct`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db060"></a>
## Office.dbo.upSCM_Join_FileDtlCnt

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@cafe_id` | `varchar(15)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2021-10-06T15:36:03.243 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.company_exception`, `smartbill3.dbo.tax_memcfrm`, `smartbill3.dbo.tax_memcfrm_detail`, `smartbill3.dbo.v_dummy_company_exception` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getSummary](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/registrationinquiry/repository/RegistrationInquiryMapper.kt#L59) — 바인딩: `cafeId`. 결과 매핑: `memcfrm_date` → `memcfrmDate`, `memcfrm_file` → `memcfrmFile`, `total_cnt` → `totalCnt`, `mem_cnt` → `memCnt`, `non_cnt` → `nonCnt`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Select @total_Cnt = count(memcfrm_detail_no) From smartbill3.dbo.tax_memcfrm_detail where cafe_id = @cafe_id
Join (select com.* from  smartbill3.dbo.company com WITH (NOLOCK)
LEFT OUTER JOIN SMARTBILL3..[V_DUMMY_COMPANY_EXCEPTION]  E WITH (NOLOCK)
ON com.COM_NO = E.COM_NO     where   E.COM_NO IS NULL  ) c   on t.memcfrm_com_regno = c.com_regno
Where t.cafe_id = @cafe_id and com_del_yn= 'N'  and  memcfrm_email <> '[이메일 생략]'
Where cafe_id = @cafe_id
```

하위 프로시저·함수·뷰: `smartbill3.dbo.v_dummy_company_exception`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db061"></a>
## OFFICE.dbo.upSM_mailSend_Insert

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@TITLE` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CONTENT` | `text` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CUSER` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT` | `int` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:04.333 |
| 읽기·참조 객체 | `office.dbo.servicemail_send` |
| 쓰기 대상 | `office.dbo.servicemail_send` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [insertMailSend](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/servicenoticemail/repository/EmailVendorMapper.kt#L125) — 바인딩: `title`, `content`, `cuser`, `result, mode=OUT, jdbcType=INTEGER`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @RESULT = '2'
set @RESULT = @@identity
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db062"></a>
## OFFICE.dbo.upSM_mailSendList

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DIV` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:04.793 |
| 읽기·참조 객체 | `office.dbo.servicemail` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [listRecipients](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/integration/hubservice/servicenoticemail/repository/EmailVendorMapper.kt#L114) — 바인딩: `div`. 결과 매핑: `NO` → `no`, `COM_REGNO` → `comRegno`, `EMAIL` → `email`, `NAME` → `name`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db063"></a>
## SB_BILL.dbo.BILL_COMMON_CODE

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `IDX` | `int` | 불가 | 예 |
| `CODE_TYPE` | `varchar(20)` | 불가 | 아니오 |
| `SUB_TYPE` | `varchar(20)` | 불가 | 아니오 |
| `CODE` | `varchar(30)` | 불가 | 아니오 |
| `SORT_NO` | `int` | 불가 | 아니오 |
| `CODE_DETAIL` | `varchar(100)` | 허용 | 아니오 |
| `REMARK` | `varchar(max)` | 허용 | 아니오 |
| `USE_YN` | `varchar(1)` | 불가 | 아니오 |
| `CDATE` | `datetime` | 불가 | 아니오 |
| `UDATE` | `datetime` | 허용 | 아니오 |
| `SW_NO` | `int` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2017-04-11T18:15:07.597 |
| 읽기·참조 객체 | `sb_bill.dbo.bill_common_code` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchEb22Detail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L281) — 바인딩: `idx`. 결과 매핑: `IDX` → `idx`, `DETAIL_WDATE` → `detailWdate`, `EA22FILE_NAME` → `ea22FileName`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `BANK_CODE` → `bankCode`, `BANK_ACCNO` → `bankAccNo`, `BANK_REGNO` → `bankRegno`, `INV_AMT` → `invAmt`, `RSLT_CODE` → `rsltCode`, `ERR_CODE` → `errCode`, `COM_NO` → `comNo`, `CODE_DETAIL_NM` → `codeDetailNm`, `BANK_NAME` → `bankName`.
- [searchEb14Detail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) — 바인딩: `idx`, `resultCode`, `resultCode`. 결과 매핑: `IDX` → `idx`, `DETAIL_WDATE` → `detailWriteDate`, `EA14_IDX` → `ea14Idx`, `PAYER_NO` → `payerNo`, `FILE_APPDATE` → `fileAppDate`, `BANK_CODE` → `bankCode`, `BANK_ACCNO` → `bankAccNo`, `BANK_REGNO` → `bankRegNo`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegNo`, `RSLT_CODE` → `resultCode`, `ERR_CODE` → `errorCode`, `CODE_DETAIL_NM` → `errorMessage`, `MEM_EMAIL` → `memberEmail`, `COM_NO` → `comNo`, `MEM_NO` → `memNo`, `MEM_NAME` → `memName`, `BANK_NAME` → `bankName`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db064"></a>
## SB_BILL.dbo.PAYMENT

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `IDX` | `int` | 불가 | 예 |
| `OrderID` | `varchar(64)` | 허용 | 아니오 |
| `ChargeMonth` | `varchar(6)` | 허용 | 아니오 |
| `ComNo` | `int` | 허용 | 아니오 |
| `MemNo` | `int` | 허용 | 아니오 |
| `PaymentAmount` | `money` | 허용 | 아니오 |
| `PaymentDate` | `datetime` | 허용 | 아니오 |
| `PaymentDivision` | `varchar(10)` | 허용 | 아니오 |
| `DtiIdx` | `int` | 허용 | 아니오 |
| `REMARK` | `varchar(300)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-11-02T10:02:41.460 |
| 읽기·참조 객체 | `sb_bill.dbo.payment` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findPayerName](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/status/repository/PaymentStatusInfoMapper.kt#L102) — 바인딩: `idx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [clearPaymentAmount](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/status/repository/PaymentStatusInfoMapper.kt#L162) — 바인딩: `idx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db065"></a>
## SB_BILL.dbo.UPMEM_ACCETC_CANCEL

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MEM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ORDER_ID` | `varchar(64)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PREPAYNO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT` | `varchar(5)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-03-09T16:30:12.290 |
| 읽기·참조 객체 | `sb_bill.dbo.close`, `sb_bill.dbo.invoice`, `sb_bill.dbo.payment`, `sb_bill.dbo.payment_his`, `sb_bill.dbo.service_prepay_monthly_remain`, `sb_bill.dbo.service_prepay_monthly_remain_card_cancle_history`, `smartbill3.dbo.accinfo_cancel`, `smartbill3.dbo.accinfo_history`, `smartbill3.dbo.company`, `smartbill3.dbo.company_history`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 쓰기 대상 | `sb_bill.dbo.invoice`, `sb_bill.dbo.payment`, `sb_bill.dbo.payment_his`, `sb_bill.dbo.service_prepay_monthly_remain`, `sb_bill.dbo.service_prepay_monthly_remain_card_cancle_history`, `smartbill3.dbo.accinfo_cancel`, `smartbill3.dbo.accinfo_history`, `smartbill3.dbo.company`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `'99999'`; `@RESULT` |

### Mapper 입출력 매핑

- [cancelDepositCardHp](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/status/repository/PaymentStatusInfoMapper.kt#L148) — 바인딩: `comNo`, `memNo`, `orderId`, `prepayNo`, `result, mode=OUT, jdbcType=VARCHAR`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [cancelDeposit](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DepositProcessMapper.kt#L127) — 바인딩: `comNo`, `memNo`, `orderId`, `prepayNo`, `result, mode=OUT, jdbcType=VARCHAR`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
BEGIN  TRAN
SET @STRINVYYMM =  CONVERT(VARCHAR(6),GETDATE(),112)
SET @STRPREYYMM =  CONVERT(VARCHAR(6),DATEADD(M,-1,GETDATE()),112)
SET @RESULT ='30000'
WHERE  ORDER_ID = @ORDER_ID
SET @COM_NO = @STRCOMNO
WHERE COM_NO = @STRCOMNO AND PREPAY_NO = @PREPAYNO
SET @RESULT = '99998'
WHERE COM_NO = @STRCOMNO
ORDER BY PREPAY_NO DESC
SET @RESULT = '99997'
WHERE COM_NO = @STRCOMNO AND PREPAY_NO = @PREPAYNO
ORDER BY PREPAY_NO DESC
WHERE COM_NO = @STRCOMNO AND PREPAY_NO <> @PREPAYNO
ORDER BY PREPAY_NO DESC
SET @SUMCARRYOVER_AMT = @STRCARRYOVERAMT -  @C_USE_AMT
SET @SUMCARRYOVER_AMT = 0
WHERE PREPAY_NO = @PREPAYNO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db066"></a>
## SB_BILL.dbo.UPMEM_ACCETC_TRANSFER_CANCEL

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MEM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PREPAYNO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ORDER_ID` | `varchar(64)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT` | `varchar(5)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-12-11T18:11:33.693 |
| 읽기·참조 객체 | `sb_bill.dbo.cardbilling_transfer_result`, `sb_bill.dbo.payment`, `smartbill3.dbo.accinfo_cancel`, `smartbill3.dbo.company`, `smartbill3.dbo.company_history` |
| 쓰기 대상 | `sb_bill.dbo.cardbilling_transfer_result`, `sb_bill.dbo.payment`, `smartbill3.dbo.accinfo_cancel`, `smartbill3.dbo.company` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `'99999'`; `@RESULT` |

### Mapper 입출력 매핑

- [cancelDepositCardTransfer](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/status/repository/PaymentStatusInfoMapper.kt#L158) — 바인딩: `comNo`, `memNo`, `prepayNo`, `orderId`, `result, mode=OUT, jdbcType=VARCHAR`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
BEGIN  TRAN
SET @STRINVYYMM =  CONVERT(VARCHAR(6),GETDATE(),112)
SET @STRPREYYMM =  CONVERT(VARCHAR(6),DATEADD(M,-1,GETDATE()),112)
SET @RESULT ='30000'
WHERE  IDX = CONVERT(INT,@ORDER_ID)
SET @COM_NO = @STRCOMNO
WHERE IDX = @ORDER_ID AND ComNo = @STRCOMNO
WHERE IDX = @PREPAYNO AND ComNo = @STRCOMNO
SELECT TOP 1  @LASTCOM_STATUS = COM_STATUS FROM SMARTBILL3.DBO.COMPANY_HISTORY WITH (NOLOCK) WHERE COM_NO = @STRCOMNO  ORDER BY COM_HISTORY_DATE DESC
WHERE COM_NO = @STRCOMNO
SET @RESULT ='29999'
ROLLBACK
COMMIT
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db067"></a>
## SB_BILL.dbo.UspBill_BalanceCheckList_SELECT_TOP

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SEARCH_CODE` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SEARCH_TEXT` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-09-19T14:54:59.983 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.service_prepay` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchDepositBalanceList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DepositBalanceMapper.kt#L45) — 바인딩: `page`, `top`, `searchCode`, `searchText`. 결과 매핑: `TOT_COUNT` → `totCount`, `PREPAY_NO` → `prepayNo`, `COM_NO` → `comNo`, `PREPAY_DATE` → `prepayDate`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `COM_DEL_YN` → `comDelYn`, `PREPAY_AMT` → `prepayAmt`, `CARRYOVER_AMT` → `carryoverAmt`, `USE_AMT` → `useAmt`, `BALANCE_AMT` → `balanceAmt`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

하위 프로시저·함수·뷰: `sb_bill.dbo.uspbill_balancechecklist_select_top_nosearch`, `sb_bill.dbo.uspbill_balancechecklist_select_top_search`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db068"></a>
## Sb_Bill.dbo.UspBill_BalanceDepositAmountInfo_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.347 |
| 읽기·참조 객체 | `smartbill3.dbo.service_prepay` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getAvailableAmount](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DepositProcessMapper.kt#L86) — 바인딩: `prepayNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE PREPAY_NO = @IDX
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db069"></a>
## SB_BILL.dbo.UspBill_BalanceDepositProcessInfo_INSERT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@IDX` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CHARGE_MONTH` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@AMOUNT` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@STATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REMARK` | `varchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SW_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT` | `varchar(1)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2017-09-27T16:42:36.757 |
| 읽기·참조 객체 | `sb_bill.dbo.invoice`, `sb_bill.dbo.payment`, `sb_bill.dbo.payment_his`, `smartbill3.dbo.company`, `smartbill3.dbo.company_history`, `smartbill3.dbo.member`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 쓰기 대상 | `sb_bill.dbo.invoice`, `sb_bill.dbo.payment`, `sb_bill.dbo.payment_his`, `smartbill3.dbo.company`, `smartbill3.dbo.company_history`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [processDepositPayment](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DepositProcessMapper.kt#L96) — 바인딩: `idx`, `comNo`, `chargeMonth`, `amount`, `state`, `remark`, `swNo`, `result, mode=OUT, jdbcType=VARCHAR`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE PREPAY_NO = @IDX;
SET @RESULT = '1';
WHERE COM_NO = @COM_NO
SET @CURRENT_CHARGE_MONTH = CONVERT(VARCHAR(6), GETDATE(), 112);
SET @RESULT = '0';
BEGIN TRAN;
WHERE PREPAY_NO = @IDX;
IF NOT EXISTS ( SELECT * FROM SB_BILL..INVOICE WHERE COMNO = @COM_NO AND CHARGEMONTH != @CHARGE_MONTH)
WHERE
WHERE
WHERE
WHERE
WHERE ORDERID = @IDX
ORDER BY IDX DESC;
COMMIT TRAN;
SET @RESULT = '2';
ROLLBACK TRAN;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db070"></a>
## SB_BILL.dbo.UspBill_BalanceDetailInfo_SELECT_WITH_USEAGE_HIS

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2021-02-24T14:20:51.547 |
| 읽기·참조 객체 | `office.dbo.sawon`, `sb_bill.dbo.payment`, `sb_dti.dbo.dti_sign_cub`, `sb_dti.dbo.dti_sign_cub_2023_07`, `sb_dti.dbo.dti_sign_cub_part`, `sb_dti.dbo.dti_sign_cub_prev_buffer`, `smartbill3.dbo.company`, `smartbill3.dbo.member`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getDepositDetailHistoryAll](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DepositDetailMapper.kt#L79) — 바인딩: `page`, `top`, `comNo`. 결과 매핑: `TOT_COUNT` → `totCount`, `CHANNEL` → `channel`, `MEM_NAME` → `manager`, `STATEMENT` → `statement`, `STATEMENTAMOUNT` → `amount`, `PRINCIPAL_AMT` → `principalAmt`, `CARRYOVER_AMT` → `carryoverAmt`, `CDATE` → `registrationDate`, `COM_REGNO` → `comRegno`, `PAY_METHOD` → `payMethod`, `PREPAY_NO` → `prepayNo`, `ORDER_ID` → `orderId`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SNUM = 1 + ((@PAGE * @TOP) - @TOP)
SET @ENUM = (@PAGE * @TOP)
SET @STRSQL = N'
WHERE
INNER JOIN COM C WITH(NOLOCK) ON C.COM_NO = M.COM_NO
*, ROW_NUMBER() OVER(ORDER BY CDATE DESC) AS RNUM, COUNT(1) OVER() [Total]
JOIN SMARTBILL3..SERVICE_PREPAY_HIS B WITH(NOLOCK) ON A.PREPAY_NO = B.IDX
LEFT JOIN OFFICE..SAWON M WITH(NOLOCK) ON B.SWNO = M.SW_NO
LEFT JOIN MEM MB WITH(NOLOCK) ON B.MEMNO = MB.MEM_NO
LEFT JOIN SB_BILL..PAYMENT D WITH(NOLOCK) ON B.CHANNELIDX = D.IDX AND D.COMNO = A.COM_NO
INNER JOIN COM C WITH(NOLOCK) ON  A.COM_NO = C.COM_NO
JOIN SB_DTI..DTI_SIGN_CUB C WITH(NOLOCK) ON SP.PREPAY_NO = C.PREPAY_NO
JOIN MEM MB WITH(NOLOCK) ON SP.PREPAY_MEM_NO = MB.MEM_NO AND SP.COM_NO = MB.COM_NO
WHERE
JOIN SMARTBILL3..DCT_CON_INFO DC WITH(NOLOCK) ON DU.DCT_NO = DC.DCT_NO AND DC.COM_NO = DU.COM_NO
JOIN MEM M WITH(NOLOCK) ON M.MEM_NO = DC.MEM_NO AND DU.COM_NO = M.COM_NO
WHERE
WHERE RNUM BETWEEN @SNUM AND @ENUM
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_sign_cub`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db071"></a>
## SB_BILL.dbo.UspBill_BalanceDetailInfo_SELECT_WITHOUT_USEAGE_HIS

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2021-02-24T14:20:44.790 |
| 읽기·참조 객체 | `office.dbo.sawon`, `sb_bill.dbo.payment`, `smartbill3.dbo.company`, `smartbill3.dbo.member`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getDepositDetailHistoryWithoutUsage](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DepositDetailMapper.kt#L103) — 바인딩: `page`, `top`, `comNo`. 결과 매핑: `TOT_COUNT` → `totCount`, `CHANNEL` → `channel`, `MEM_NAME` → `manager`, `STATEMENT` → `statement`, `STATEMENTAMOUNT` → `amount`, `PRINCIPAL_AMT` → `principalAmt`, `CARRYOVER_AMT` → `carryoverAmt`, `CDATE` → `registrationDate`, `COM_REGNO` → `comRegno`, `PAY_METHOD` → `payMethod`, `PREPAY_NO` → `prepayNo`, `ORDER_ID` → `orderId`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SNUM = 1 + ((@PAGE * @TOP) - @TOP)
SET @ENUM = (@PAGE * @TOP)
SET @STRSQL = '
*, ROW_NUMBER() OVER(ORDER BY CDATE DESC) AS RNUM, COUNT(1) OVER() [Total]
WHERE COM_NO = ' + CONVERT(VARCHAR,@COM_NO) + '
JOIN SMARTBILL3..SERVICE_PREPAY_HIS B WITH(NOLOCK) ON A.PREPAY_NO = B.IDX
LEFT JOIN OFFICE..SAWON M WITH(NOLOCK) ON B.SWNO = M.SW_NO
LEFT JOIN SMARTBILL3..MEMBER C WITH(NOLOCK) ON B.MEMNO = C.MEM_NO
LEFT JOIN
JOIN SMARTBILL3..COMPANY CP WITH(NOLOCK) ON PM.COMNO = CP.COM_NO
WHERE CP.COM_NO = ' + CONVERT(VARCHAR,@COM_NO) + '
WHERE CHANNEL != ''DTISERVICE'' AND CHANNEL != ''DCTSERVICE'' AND CHANNEL != ''CSSSERVICE'' AND CHANNEL != ''SBISERVICE''
WHERE
ORDER BY CDATE DESC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db072"></a>
## SB_BILL.dbo.UspBill_BalanceInfo_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PREPAY_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.510 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.service_prepay` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getDepositDetailInfo](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DepositDetailMapper.kt#L36) — 바인딩: `prepayNo`. 결과 매핑: `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `BALANCE_AMT` → `availableAmt`, `PREPAY_DATE` → `lastChargeDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT JOIN SMARTBILL3..COMPANY B
WHERE A.PREPAY_NO = @PREPAY_NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db073"></a>
## SB_BILL.dbo.UspBill_BalanceTopInfo_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PREPAY_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT` | `varchar(1)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.337 |
| 읽기·참조 객체 | `smartbill3.dbo.service_prepay` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [checkLatestDeposit](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DepositDetailMapper.kt#L126) — 바인딩: `prepayNo`, `result, mode=OUT, jdbcType=VARCHAR`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SELECT @COM_NO = COM_NO FROM SMARTBILL3..SERVICE_PREPAY WHERE PREPAY_NO = @PREPAY_NO
SELECT TOP 1 @TOP_PREPAY_NO = PREPAY_NO FROM SMARTBILL3..SERVICE_PREPAY WHERE COM_NO = @COM_NO ORDER BY PREPAY_NO DESC
SET @RESULT = '0'
SET @RESULT = '1'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db074"></a>
## Sb_Bill.dbo.UspBill_BulkAccountDepositAmountInfo_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.563 |
| 읽기·참조 객체 | `smartbill3.dbo.account_bulk_app`, `smartbill3.dbo.account_bulk_app_his_new` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getAvailableAmount](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/bulkaccountdeposit/repository/BulkAccountDepositMapper.kt#L84) — 바인딩: `idx`. 결과 매핑: `BALANCEAMT` → `balanceAmt`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT JOIN SMARTBILL3..ACCOUNT_BULK_APP_HIS_NEW B
WHERE A.IDX = @IDX
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db075"></a>
## SB_BILL.dbo.UspBill_HeadOfficeDepositProcessChargeAmount_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CHARGE_MONTH` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.960 |
| 읽기·참조 객체 | `sb_bill.dbo.invoice`, `sb_bill.dbo.payment`, `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getChargeAmount](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DepositProcessMapper.kt#L81) — 바인딩: `comNo`, `chargeMonth`. 결과 매핑: `INV_AMOUNT` → `chargeAmount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
INNER JOIN SMARTBILL3..COMPANY B ON A.COMNO = B.COM_NO
LEFT JOIN (SELECT SUM(PAYMENTAMOUNT) AS PAYMENTAMOUNT, COMNO, CHARGEMONTH  FROM SB_BILL..PAYMENT
WHERE COMNO = @COM_NO AND CHARGEMONTH = @CHARGE_MONTH GROUP BY COMNO, CHARGEMONTH) C
WHERE A.COMNO = @COM_NO AND A.CHARGEMONTH = @CHARGE_MONTH
GROUP BY A.CHARGEMONTH, A.COMNO
ORDER BY CHARGEMONTH DESC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db076"></a>
## SB_BILL.dbo.UspBill_LapseDepositSaveCloverProcess

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@AMOUNT` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SW_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CLOVER_COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CLOVER_CNT` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REMARK` | `varchar(300)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT` | `varchar(5)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2021-02-24T15:09:35.680 |
| 읽기·참조 객체 | `sb_common.dbo.free_service`, `sb_common.dbo.free_service_his`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 쓰기 대상 | `sb_common.dbo.free_service`, `sb_common.dbo.free_service_his`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `END`; `END CATCH`; `END` |

### Mapper 입출력 매핑

- [processLapseWithClover](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DepositProcessMapper.kt#L117) — 바인딩: `idx`, `amount`, `swNo`, `cloverComNo`, `cloverCnt`, `remark`, `result, mode=OUT, jdbcType=VARCHAR`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @RESULT = '9'
WHERE PREPAY_NO = @IDX
SET @RESULT = '1'
BEGIN TRAN
WHERE PREPAY_NO = @IDX
WHERE PREPAY_NO = @IDX
SET @RESULT = '0'
COMMIT TRAN
ROLLBACK TRAN
SET @RESULT = '9'
SET @RESULT = '8'
```

하위 프로시저·함수·뷰: `sb_bill.dbo.uspbill_eventsingleinfo_insert`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db077"></a>
## SB_BILL.dbo.UspBill_PaymentBalanceDepositProcessInfo_INSERT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@AMOUNT` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REMARK` | `varchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SW_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT` | `varchar(1)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2024-03-11T11:16:35.757 |
| 읽기·참조 객체 | `sb_bill.dbo.invoice`, `sb_bill.dbo.payment`, `sb_bill.dbo.payment_his`, `smartbill3.dbo.member`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 쓰기 대상 | `sb_bill.dbo.invoice`, `sb_bill.dbo.payment`, `sb_bill.dbo.payment_his`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `END`; `END CATCH` |

### Mapper 입출력 매핑

- [processDepositPrepaid](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/status/repository/PaymentStatusInfoMapper.kt#L138) — 바인딩: `idx`, `comNo`, `amount`, `remark`, `swNo`, `result, mode=OUT, jdbcType=VARCHAR`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SELECT @BALANCE_AMT = PAYMENTAMOUNT ,@CHARGEMONTH = CHARGEMONTH , @PaymentDivision  = PaymentDivision  FROM SB_BILL..PAYMENT  with (nolock)  WHERE IDX = @IDX
SET @RESULT = '1'
SELECT @MEM_NO = MEM_NO FROM SMARTBILL3..MEMBER with (nolock) WHERE COM_NO = @COM_NO AND MEM_TYPE = 'F'
SET @RESULT = '0'
BEGIN TRAN
IF EXISTS(SELECT * FROM SMARTBILL3..SERVICE_PREPAY WHERE COM_NO = @COM_NO)
SELECT TOP 1 @CARRYOVER_AMT = (ISNULL(PRINCIPAL_AMT,0) - ISNULL(USE_AMT,0)) FROM SMARTBILL3..SERVICE_PREPAY WHERE COM_NO = @COM_NO ORDER BY PREPAY_NO DESC
SET @CARRYOVER_AMT = 0
SET @CHANNEL_IDX = @@IDENTITY
SET  @TODAY_CHARGEMONTH = CONVERT(varchar(7), getdate(),112)
WHERE comno = @COM_NO and ChargeMonth = @TODAY_CHARGEMONTH and Division='UNPAY'
COMMIT TRAN
SET @RESULT = '2'
ROLLBACK TRAN
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db078"></a>
## SB_BILL.dbo.UspBill_PayMentDetail_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.930 |
| 읽기·참조 객체 | `sb_bill.dbo.invoice`, `sb_bill.dbo.payment`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getPaymentDetail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/status/repository/PaymentStatusInfoMapper.kt#L68) — 바인딩: `idx`. 결과 매핑: `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `MEM_NAME` → `memName`, `MEM_REALNAME` → `memRealname`, `PAYMENTDATE` → `paymentDate`, `PAYMENTAMOUNT` → `paymentAmount`, `CHARGEMONTH` → `chargeMonth`, `INV_AMOUNT` → `invAmount`, `PAYMENTDIVISION` → `paymentDivision`, `ETC_PCS_NO` → `etcPcsNo`, `ORDERID` → `orderId`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT JOIN SB_BILL..INVOICE B WITH(NOLOCK)
WHERE
GROUP  BY
JOIN SMARTBILL3..COMPANY B
LEFT JOIN SMARTBILL3..MEMBER C
LEFT JOIN SB_DTI..DTI_HEADER_CUB D WITH(NOLOCK)
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_header_cub`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db079"></a>
## sb_bill.dbo.UspBill_Refund_Create_Dti

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REFUND_AMOUNT` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ERR_CODE` | `int` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.423 |
| 읽기·참조 객체 | `sb_dti.dbo.bizplace`, `sb_dti.dbo.bizplace_member`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti.dbo.dti_header_detail`, `sb_dti.dbo.dti_header_detail_2023_07`, `sb_dti.dbo.dti_header_detail_part`, `sb_dti.dbo.dti_header_detail_prev_buffer`, `sb_dti.dbo.dti_issue_id`, `sb_dti.dbo.dti_item`, `sb_dti.dbo.dti_item_2023_07`, `sb_dti.dbo.dti_item_part`, `sb_dti.dbo.dti_item_prev_buffer`, `sb_dti.dbo.dti_paymethod`, `sb_dti.dbo.dti_paymethod_2023_07`, `sb_dti.dbo.dti_paymethod_part`, `sb_dti.dbo.dti_paymethod_prev_buffer`, `sb_dti.dbo.dti_sequence01`, `sb_dti.dbo.dti_sequence02`, `sb_dti.dbo.dti_status_his`, `sb_dti.dbo.dti_status_his_2023_07`, `sb_dti.dbo.dti_status_his_part`, `sb_dti.dbo.dti_status_his_prev_buffer`, `sb_dti.dbo.service_admin`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_detail`, `sb_dti.dbo.dti_item`, `sb_dti.dbo.dti_paymethod`, `sb_dti.dbo.dti_sequence01`, `sb_dti.dbo.dti_sequence02`, `sb_dti.dbo.dti_status_his` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [createRefundInvoiceAmend](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/refund/repository/RefundDetailMapper.kt#L101) — 바인딩: `comNo`, `refundAmount`, `errCode, mode=OUT, jdbcType=INTEGER`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @DTIYYMMDD = CONVERT(VARCHAR(10), GETDATE(), 120)
SET @SUM_CHARGE_AMOUNT = FLOOR(@REFUND_AMOUNT / 10) * 10 * -1
SET @BLANK_COUNT = 11 - LEN(@SUM_CHARGE_AMOUNT)
SET @SUP_AMOUNT = @SUM_CHARGE_AMOUNT / 1.1
SET @TAX_AMOUNT = @SUM_CHARGE_AMOUNT - @SUP_AMOUNT
JOIN SB_DTI..SERVICE_ADMIN SA
JOIN SMARTBILL3..MEMBER M1
WHERE
WHERE
JOIN SMARTBILL3..MEMBER M2
WHERE
LEFT OUTER JOIN SB_DTI..BIZPLACE_MEMBER BM
LEFT OUTER JOIN SB_DTI..BIZPLACE BL
WHERE
SET @BYR_SBID = @BYR_ID
BEGIN TRAN
SET @ITEMYYMMDD = REPLACE(@DTIYYMMDD, '-', '')
COMMIT;
```

하위 프로시저·함수·뷰: `master.dbo.clr_enc_char_ins_tc`, `master.dbo.clr_enc_index_tc`, `master.dbo.enc_char_ins_tc`, `master.dbo.enc_index_char_sel_tc`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_detail`, `sb_dti.dbo.dti_item`, `sb_dti.dbo.dti_paymethod`, `sb_dti.dbo.dti_status_his`, `sb_dti.dbo.upsave_dti_header`, `sb_dti.dbo.upsave_dti_item`, `sb_dti.dbo.upselect_dti_issue_id`, `sb_dti.dbo.upselect_dti_number`, `smartbill3.dbo.fnfilldigit`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db080"></a>
## Sb_Bill.dbo.UspBill_RefundCheck_ComRegNo

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_REGNO` | `varchar(16)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.347 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.member`, `smartbill3.dbo.service_prepay` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getCompanyInfo](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/refund/repository/RefundRegistrationMapper.kt#L32) — 바인딩: `comRegno`. 결과 매핑: `COM_NAME` → `comName`, `mem_realname` → `memRealname`, `mem_tel` → `memTel`, `PRINCIPAL_AMT` → `principalAmt`, `USE_AMT` → `useAmt`, `PREPAY_NO` → `prepayNo`, `COM_NO` → `comNo`, `MEM_NO` → `memNo`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET  @COM_REGNO = REPLACE(@COM_REGNO, '-', '')
SELECT @COM_NO = COM_NO FROM SMARTBILL3..COMPANY WITH (NOLOCK) WHERE COM_REGNO = @COM_REGNO and com_del_yn = 'N'
left outer join (select * from smartbill3..member with(nolock) where mem_type ='F') b on a.com_no = b.com_no
where a.com_no = @COM_NO
LEFT OUTER JOIN
WHERE  COM_NO = @COM_NO ORDER BY PREPAY_NO DESC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db081"></a>
## Sb_Bill.dbo.UspBill_RefundCheckList_SELECT_TOP

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROM_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TO_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SEARCH_CODE` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SEARCH_TEXT` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REFUND_STATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@GROUP_NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.550 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.service_refund` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchRefundList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/refund/repository/RefundMapper.kt#L36) — 바인딩: `page`, `top`, `fromDate`, `toDate`, `searchCode`, `searchText`, `refundState`, `groupNo`. 결과 매핑: `TOT_COUNT` → `totCount`, `REFUND_NO` → `refundNo`, `REFUND_DATE` → `refundDate`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `COM_DEL_YN` → `comDelYn`, `REFUND_AMT` → `refundAmt`, `ACC_DATE` → `accDate`, `REFUND_STATE` → `refundState`, `RESULT_DATE` → `resultDate`, `REFUND_NAME` → `refundName`, `REFUND_TEL` → `refundTel`, `ACCNAME` → `accName`, `ACCNO` → `accNo`, `PRINCIPAL_AMT` → `principalAmt`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @GROUP_YN ='N'
SET @GROUP_YN = 'Y'
SET @TOP2 = @TOT_COUNT - (@PAGE - 1) * @TOP
SET @TOP2 = @TOP
SET @STRSQL = '
LEFT JOIN SMARTBILL3..COMPANY B
WHERE 1=1 '
SET @STRSQL = @STRSQL + 'AND REFUND_DATE BETWEEN @FROM_DATE AND @TO_DATE + '' 23:59:59'' '
SET @STRSQL = @STRSQL + 'AND REFUND_DATE >= @FROM_DATE '
SET @STRSQL = @STRSQL + 'AND REFUND_DATE <= @TO_DATE '
SET @STRSQL = @STRSQL + 'AND B.COM_NAME LIKE @SEARCH_TEXT+''%'' '
SET @STRSQL = @STRSQL + 'AND B.COM_REGNO = @SEARCH_TEXT '
SET @STRSQL = @STRSQL + 'AND CHARINDEX(A.REFUND_STATE, '''+@REFUND_STATE+''')>0 '
SET @STRSQL = @STRSQL + 'AND PREPAY_NO = @GROUP_NO '
SET @STRSQL = @STRSQL + 'AND GROUP_NO = @GROUP_NO '
SET @STRSQL = @STRSQL + 'ORDER BY A.REFUND_NO DESC
ORDER BY REFUND_NO ASC
LEFT JOIN SMARTBILL3..COMPANY B
```

하위 프로시저·함수·뷰: `sb_bill.dbo.uspbill_refundchecklistcount_select`, `sb_bill.dbo.uspbill_refundchecklistcount_select_1`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db082"></a>
## Sb_Bill.dbo.UspBill_RefundDetail_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PREPAY_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REFUND_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.140 |
| 읽기·참조 객체 | `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getRefundActualDetail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/refund/repository/RefundDetailMapper.kt#L75) — 바인딩: `comNo`, `prepayNo`, `refundDate`. 결과 매핑: `PREPAY_DATE` → `prepayDate`, `PREPAY_AMT` → `prepayAmt`, `PRINCIPAL_AMT` → `principalAmt`, `SUBTRACTION` → `subtraction`, `CHARGE` → `charge`, `REFUND` → `refund`, `COMMISSION` → `commission`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
from SMARTBILL3..SERVICE_PREPAY a WITH (NOLOCK) join SMARTBILL3..SERVICE_PREPAY_his b WITH (NOLOCK) on a.prepay_no = b.idx
WHERE A.COM_NO = @COM_NO AND IDX = @PREPAY_NO and channel in ('REFUND', 'COMMI')
) A GROUP BY  idx
LEFT OUTER JOIN
JOIN(SELECT COM_NO, SUM(USE_AMT) AS USE_AMT FROM SMARTBILL3..SERVICE_PREPAY WITH (NOLOCK)
WHERE COM_NO = @COM_NO
GROUP BY COM_NO) B
WHERE A.COM_NO = @COM_NO AND PREPAY_DATE BETWEEN DATEADD(DAY,-90,@REFUND_DATE) AND  DATEADD(DAY,1,@REFUND_DATE)
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db083"></a>
## Sb_Bill.dbo.UspBill_refundInfo_INSERT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PREPAY_NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PRINCIPAL_AMT` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REFUND_AMT` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REFUND_NAME` | `varchar(35)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REFUND_TEL` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MEM_NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BANK_NAME` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BANK_NO` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SW_ID` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REFUND_IDX` | `int` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.370 |
| 읽기·참조 객체 | `smartbill3.dbo.service_refund`, `smartbill3.dbo.service_refund_his` |
| 쓰기 대상 | `smartbill3.dbo.service_refund`, `smartbill3.dbo.service_refund_his` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `END`; `END CATCH` |

### Mapper 입출력 매핑

- [insertRefundInfo](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/refund/repository/RefundRegistrationMapper.kt#L36) — 바인딩: `prepayNo`, `principalAmt`, `refundAmt`, `refundName`, `refundTel`, `memNo`, `comNo`, `bankName`, `bankNo`, `swId`, `refundIdx, mode=OUT, jdbcType=INTEGER`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SELECT @REFUND_CNT =  COUNT(*) FROM SMARTBILL3.DBO.SERVICE_REFUND WITH(NOLOCK) WHERE REFUND_STATE IN('01','02') AND COM_NO = @COM_NO
SET @REFUND_IDX = '1'
BEGIN TRAN
SET @REFUND_IDX = @@IDENTITY
COMMIT TRAN
ROLLBACK TRAN
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db084"></a>
## Sb_Bill.dbo.UspBill_RefundInfo_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@REFUND_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.247 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his`, `smartbill3.dbo.service_refund` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getRefundBasicInfo](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/refund/repository/RefundDetailMapper.kt#L39) — 바인딩: `refundNo`. 결과 매핑: `REFUND_DATE` → `refundDate`, `REFUND_STATE` → `refundState`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `REFUND_NAME` → `refundName`, `REFUND_TEL` → `refundTel`, `ACCNAME` → `accName`, `ACCNO` → `accNo`, `REFUND_AMT` → `refundAmt`, `COM_NO` → `comNo`, `PREPAY_NO` → `prepayNo`, `GROUP_NO` → `groupNo`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SELECT @COM_NO = COM_NO, @REFUNDDATE = CONVERT(char(10),REFUND_DATE,120), @GROUP_NO = GROUP_NO, @PREPAY_NO = PREPAY_NO FROM SMARTBILL3..SERVICE_REFUND WITH (NOLOCK) WHERE REFUND_NO = @REFUND_NO
JOIN SMARTBILL3..COMPANY B  WITH (NOLOCK)
WHERE REFUND_NO = @REFUND_NO
JOIN(SELECT COM_NO, SUM(USE_AMT) AS USE_AMT, isnull(SUM(REFUND_AMT), 0) AS REFUND_AMT, isnull(SUM(REFUND_COMMISSION_AMT), 0) AS REFUND_COMMISSION_AMT FROM SMARTBILL3..SERVICE_PREPAY WITH (NOLOCK)
WHERE COM_NO = @COM_NO
GROUP BY COM_NO) B
LEFT OUTER JOIN(SELECT IDX, STATEMENTAMOUNT FROM SMARTBILL3..SERVICE_PREPAY_HIS WHERE CHANNEL = 'REFUND') C ON A.PREPAY_NO = C.IDX
WHERE A.COM_NO = @COM_NO AND PREPAY_DATE BETWEEN DATEADD(DAY,-90,@REFUNDDATE) AND  DATEADD(DAY,1,@REFUNDDATE)
FROM SMARTBILL3..SERVICE_PREPAY A WITH (NOLOCK) WHERE COM_NO = @COM_NO ORDER BY PREPAY_NO DESC
JOIN(SELECT COM_NO, SUM(USE_AMT) AS USE_AMT, isnull(SUM(REFUND_AMT), 0) AS REFUND_AMT, isnull(SUM(REFUND_COMMISSION_AMT), 0) AS REFUND_COMMISSION_AMT FROM SMARTBILL3..SERVICE_PREPAY WITH (NOLOCK)
WHERE COM_NO = @COM_NO
GROUP BY COM_NO) B
LEFT OUTER JOIN(SELECT IDX, STATEMENTAMOUNT FROM SMARTBILL3..SERVICE_PREPAY_HIS WHERE CHANNEL = 'REFUND') C ON A.PREPAY_NO = C.IDX
LEFT OUTER JOIN  (select idx,  sum(statementAmount) as one_use_amt from SMARTBILL3..SERVICE_PREPAY_his with(nolock) where channel = 'dtiservice' group by idx) D ON A.PREPAY_NO = D.IDX
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db085"></a>
## Sb_Bill.dbo.UspBill_RefundInfo_UPDATE

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@REFUND_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REQUEST_AMT` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ACC_NO` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ACC_NAME` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SW_ID` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT` | `varchar(1)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.490 |
| 읽기·참조 객체 | `smartbill3.dbo.service_refund`, `smartbill3.dbo.service_refund_his` |
| 쓰기 대상 | `smartbill3.dbo.service_refund`, `smartbill3.dbo.service_refund_his` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [updateRefundInfo](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/refund/repository/RefundRegistrationMapper.kt#L40) — 바인딩: `refundNo`, `requestAmt`, `accNo`, `accName`, `swId`, `result, mode=OUT, jdbcType=NVARCHAR`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @RESULT = '0'
BEGIN TRAN
WHERE REFUND_NO = @REFUND_NO
COMMIT TRAN
ROLLBACK TRAN
SET @RESULT = '2'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db086"></a>
## Sb_Bill.dbo.UspBill_RefundStateInfo_UPDATE

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@REFUND_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REFUND_STATE` | `varchar(2)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CONTENT` | `varchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SW_ID` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CHARGE` | `money` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PREPAY_ARRAY` | `varchar(500)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT` | `varchar(1)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.453 |
| 읽기·참조 객체 | `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his`, `smartbill3.dbo.service_refund`, `smartbill3.dbo.service_refund_his` |
| 쓰기 대상 | `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his`, `smartbill3.dbo.service_refund`, `smartbill3.dbo.service_refund_his` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `END`; `END`; `END` |

### Mapper 입출력 매핑

- [changeRefundState](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/refund/repository/RefundDetailMapper.kt#L93) — 바인딩: `refundNo`, `refundState`, `content`, `swId`, `charge`, `prepayArray`, `result, mode=OUT, jdbcType=NVARCHAR`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @RESULT = '0'
WHERE REFUND_NO = @REFUND_NO
WHERE REFUND_NO = @REFUND_NO
WHERE REFUND_NO = @REFUND_NO
WHERE group_no = @GROUP_NO and refund_state != '03' order by prepay_no asc
SET @RESULT = '3'
FROM SMARTBILL3..SERVICE_PREPAY WHERE COM_NO = @COM_NO ORDER BY PREPAY_NO DESC
SET @RESULT = '1'
BEGIN TRAN
WHERE COM_NO = @COM_NO ORDER BY PREPAY_NO DESC
WHERE REFUND_NO = @REFUND_NO
WHERE PREPAY_NO = @PREPAY_NO2
SELECT @MEM_NO = MEM_NO FROM SMARTBILL3..SERVICE_REFUND_HIS WHERE REFUND_NO = @REFUND_NO AND REFUND_STATE = '01'
SET @PREPAY_ARRAY = SUBSTRING( @PREPAY_ARRAY, CHARINDEX(',', @PREPAY_ARRAY) + 1, LEN(@PREPAY_ARRAY) )
COMMIT TRAN
WHERE REFUND_NO = @REFUND_NO
WHERE group_no = @GROUP_NO and refund_state = '03' order by prepay_no asc
SET @RESULT = '4'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db087"></a>
## Sb_Bill.dbo.UspBill_SearchCompanyRegno_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COMREGNO` | `varchar(13)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2020-06-15T10:43:54.483 |
| 읽기·참조 객체 | `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getComNoByRegno](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DepositProcessMapper.kt#L31) — 바인딩: `comRegno`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE		COM_REGNO = @COMREGNO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db088"></a>
## SB_BILL.dbo.UspBill_UnPaidClearCompanyInfo_INSERT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROM_MONTH` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TO_MONTH` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REASON` | `varchar(500)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@USE_YN` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SW_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT` | `varchar(1)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.063 |
| 읽기·참조 객체 | `sb_bill.dbo.unpaid_charge_clear`, `sb_bill.dbo.unpaid_charge_clear_his` |
| 쓰기 대상 | `sb_bill.dbo.unpaid_charge_clear`, `sb_bill.dbo.unpaid_charge_clear_his` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `END` |

### Mapper 입출력 매핑

- [save](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/unpaidexception/repository/UnpaidExceptionMapper.kt#L62) — 바인딩: `comNo`, `fromMonth`, `toMonth`, `reason`, `useYn`, `swNo`, `result, mode=OUT, jdbcType=VARCHAR`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @RESULT = '0'
SET @FROM_MONTH = REPLACE(@FROM_MONTH,'-','')
SET @TO_MONTH   = REPLACE(@TO_MONTH,'-','')
IF EXISTS(SELECT COMNO FROM SB_BILL..UNPAID_CHARGE_CLEAR WHERE COMNO = @COM_NO)
SET @RESULT = '1'
SET @RESULT = '2'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db089"></a>
## SB_BILL.dbo.UspBill_UnPaidCompanyClearInfo_DELETE

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SW_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT` | `varchar(1)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.080 |
| 읽기·참조 객체 | `sb_bill.dbo.unpaid_charge_clear`, `sb_bill.dbo.unpaid_charge_clear_his` |
| 쓰기 대상 | `sb_bill.dbo.unpaid_charge_clear`, `sb_bill.dbo.unpaid_charge_clear_his` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `END CATCH` |

### Mapper 입출력 매핑

- [delete](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/unpaidexception/repository/UnpaidExceptionMapper.kt#L70) — 바인딩: `comNo`, `swNo`, `result, mode=OUT, jdbcType=VARCHAR`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @RESULT = '0'
FROM UNPAID_CHARGE_CLEAR WHERE COMNO = @COM_NO
WHERE COMNO = @COM_NO
SET @RESULT = '2'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db090"></a>
## SB_BILL.dbo.UspBill_UnPaidCompanyClearInfo_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.123 |
| 읽기·참조 객체 | `office.dbo.sawon`, `sb_bill.dbo.unpaid_charge_clear`, `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getDetail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/unpaidexception/repository/UnpaidExceptionMapper.kt#L49) — 바인딩: `comNo`. 결과 매핑: `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `FROMMONTH` → `fromMonth`, `TOMONTH` → `toMonth`, `REASON` → `reason`, `USEYN` → `useYn`, `SNAME` → `sname`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
JOIN SMARTBILL3..COMPANY B
JOIN OFFICE..SAWON C
WHERE A.COMNO = @COM_NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db091"></a>
## SB_BILL.dbo.UspBill_UnPaidCompanyClearInfo_UPDATE

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROM_MONTH` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TO_MONTH` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REASON` | `varchar(500)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@USE_YN` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SW_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT` | `varchar(1)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:26.113 |
| 읽기·참조 객체 | `sb_bill.dbo.unpaid_charge_clear`, `sb_bill.dbo.unpaid_charge_clear_his` |
| 쓰기 대상 | `sb_bill.dbo.unpaid_charge_clear`, `sb_bill.dbo.unpaid_charge_clear_his` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `END CATCH` |

### Mapper 입출력 매핑

- [update](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/unpaidexception/repository/UnpaidExceptionMapper.kt#L66) — 바인딩: `comNo`, `fromMonth`, `toMonth`, `reason`, `useYn`, `swNo`, `result, mode=OUT, jdbcType=VARCHAR`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @RESULT = '0'
SET @FROM_MONTH = REPLACE(@FROM_MONTH,'-','')
SET @TO_MONTH   = REPLACE(@TO_MONTH,'-','')
WHERE COMNO = @COM_NO
SET @RESULT = '2'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db092"></a>
## SB_BILL_LINKED.dbo.CRM_API_LOG

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `IDX` | `bigint` | 불가 | 예 |
| `CORRELATION_ID` | `char(36)` | 불가 | 아니오 |
| `SYSTEMNAME` | `varchar(50)` | 불가 | 아니오 |
| `SERVERIP` | `varchar(15)` | 허용 | 아니오 |
| `ACTION_NAME` | `varchar(100)` | 허용 | 아니오 |
| `API_URL` | `varchar(2000)` | 허용 | 아니오 |
| `REQUEST_BODY` | `nvarchar(max)` | 허용 | 아니오 |
| `RESPONSE_BODY` | `nvarchar(max)` | 허용 | 아니오 |
| `RESULT_STATUS` | `varchar(10)` | 불가 | 아니오 |
| `FAIL_TYPE` | `varchar(20)` | 허용 | 아니오 |
| `ERROR_MSG` | `nvarchar(1000)` | 허용 | 아니오 |
| `ELAPSED_MS` | `int` | 허용 | 아니오 |
| `RETRY_TARGET_YN` | `char(1)` | 불가 | 아니오 |
| `RETRY_COUNT` | `tinyint` | 불가 | 아니오 |
| `RETRY_IDX` | `bigint` | 허용 | 아니오 |
| `CDATE` | `datetime` | 불가 | 아니오 |
| `UDATE` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-06-05T14:20:06.850 |
| 읽기·참조 객체 | `sb_bill_linked.dbo.crm_api_log` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [insert](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/CrmApiLogMapper.kt#L25) — 바인딩: `correlationId`, `systemName`, `actionName`, `apiUrl`, `requestBody`, `responseBody`, `resultStatus`, `failType`, `errorMsg`, `elapsedMs, jdbcType=INTEGER`, `retryTargetYn`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db093"></a>
## SB_BILL_LINKED.dbo.CRM_T_CR_OS_IV

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `CR_CD` | `varchar(20)` | 불가 | 아니오 |
| `SERVICE_CD` | `varchar(20)` | 불가 | 아니오 |
| `SEQ` | `smallint` | 불가 | 아니오 |
| `IV_DT` | `varchar(20)` | 허용 | 아니오 |
| `AMT` | `decimal(20,5)` | 불가 | 아니오 |
| `VAT` | `decimal(20,5)` | 불가 | 아니오 |
| `TOTAL_AMT` | `decimal(20,5)` | 불가 | 아니오 |
| `IV_SEND_TP` | `varchar(20)` | 불가 | 아니오 |
| `IV_STAT_TP` | `varchar(20)` | 불가 | 아니오 |
| `TX_CD` | `varchar(20)` | 허용 | 아니오 |
| `TX_DUE_DT` | `varchar(8)` | 허용 | 아니오 |
| `TX_TOTAL_AMT` | `decimal(20,5)` | 불가 | 아니오 |
| `ITEM_TX_NM` | `nvarchar(1000)` | 허용 | 아니오 |
| `TX_CAT_TP` | `varchar(10)` | 불가 | 아니오 |
| `RS_PRC_SDT` | `varchar(8)` | 허용 | 아니오 |
| `RS_PRC_EDT` | `varchar(8)` | 허용 | 아니오 |
| `PAY_PRC_TP` | `varchar(10)` | 불가 | 아니오 |
| `MEMO` | `nvarchar(max)` | 허용 | 아니오 |
| `SORT_NO` | `smallint` | 불가 | 아니오 |
| `USE_YN` | `bit` | 불가 | 아니오 |
| `IDX` | `bigint` | 불가 | 아니오 |
| `INS_USER_CD` | `varchar(20)` | 허용 | 아니오 |
| `INS_DT` | `datetime` | 불가 | 아니오 |
| `UPD_USER_CD` | `varchar(20)` | 허용 | 아니오 |
| `UPD_DT` | `datetime` | 불가 | 아니오 |
| `COM_NO` | `varchar(20)` | 허용 | 아니오 |
| `CUST_NM` | `varchar(200)` | 허용 | 아니오 |
| `REG_NO` | `varchar(20)` | 허용 | 아니오 |
| `SERVICE_NM` | `varchar(400)` | 허용 | 아니오 |
| `CreateDate` | `datetime` | 불가 | 아니오 |
| `ModifyDate` | `datetime` | 불가 | 아니오 |
| `BOC_SERVICE_IDX` | `int` | 허용 | 아니오 |
| `PayMentAmount` | `money` | 허용 | 아니오 |
| `PayMentDate` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-05-15T14:17:07.633 |
| 읽기·참조 객체 | `sb_bill_linked.dbo.crm_t_cr_os_iv` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findUnpaidChargeMonths](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L145) — 바인딩: . 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findUnpaidChargesByMonth](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L181) — 바인딩: `chargeMonth`, `offset`, `pageSize`. 결과 매핑: `TOT_COUNT` → `totCount`, `COM_NO` → `comNo`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `CHARGE_MONTH` → `chargeMonth`, `BILLING_AMOUNT` → `billingAmount`, `CR_CD` → `crCd`, `SERVICE_CD` → `serviceCd`, `SEQ` → `seq`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db094"></a>
## SB_COMMON.dbo.DOCUBILL_SBJOIN_HIS

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `IDX` | `int` | 불가 | 예 |
| `D_ComRegNo` | `varchar(13)` | 불가 | 아니오 |
| `D_ComName` | `varchar(400)` | 허용 | 아니오 |
| `D_ComPresident` | `varchar(200)` | 허용 | 아니오 |
| `D_ComBizStatus` | `varchar(200)` | 허용 | 아니오 |
| `D_ComBizClass` | `varchar(200)` | 허용 | 아니오 |
| `D_ZipCode` | `varchar(6)` | 허용 | 아니오 |
| `D_ComAddress` | `varchar(600)` | 허용 | 아니오 |
| `D_MemName` | `varchar(200)` | 허용 | 아니오 |
| `D_MemTel` | `varchar(40)` | 허용 | 아니오 |
| `D_MemHP` | `varchar(40)` | 허용 | 아니오 |
| `D_MemFax` | `varchar(40)` | 허용 | 아니오 |
| `D_MemEmail` | `varchar(200)` | 허용 | 아니오 |
| `D_MasterYN` | `char(1)` | 허용 | 아니오 |
| `U_MasterYN` | `char(1)` | 허용 | 아니오 |
| `E_COMYN` | `char(1)` | 허용 | 아니오 |
| `E_MEMYN` | `char(1)` | 허용 | 아니오 |
| `CDATE` | `datetime` | 허용 | 아니오 |
| `ComNo` | `int` | 허용 | 아니오 |
| `MemNo` | `int` | 허용 | 아니오 |
| `Old_MasterMemNo` | `int` | 허용 | 아니오 |
| `Old_MasterFlag` | `char(1)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2018-01-29T10:53:20.313 |
| 읽기·참조 객체 | `sb_common.dbo.docubill_sbjoin_his` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getTransferMap](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L351) — 바인딩: `comNo`. 결과 매핑: `MEM_NO` → `memNo`, `TRANSFER_GUBUN` → `transferGubun`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db095"></a>
## SB_COMMON.dbo.MIGRATION_SBJOIN_HIS

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `IDX` | `int` | 불가 | 예 |
| `M_ComRegNo` | `varchar(13)` | 불가 | 아니오 |
| `M_ComName` | `varchar(400)` | 허용 | 아니오 |
| `M_ComPresident` | `varchar(200)` | 허용 | 아니오 |
| `M_ComBizStatus` | `varchar(200)` | 허용 | 아니오 |
| `M_ComBizClass` | `varchar(200)` | 허용 | 아니오 |
| `M_ZipCode` | `varchar(6)` | 허용 | 아니오 |
| `M_ComAddress` | `varchar(600)` | 허용 | 아니오 |
| `M_MemName` | `varchar(200)` | 허용 | 아니오 |
| `M_MemTel` | `varchar(40)` | 허용 | 아니오 |
| `M_MemHP` | `varchar(40)` | 허용 | 아니오 |
| `M_MemFax` | `varchar(40)` | 허용 | 아니오 |
| `M_MemEmail` | `varchar(200)` | 허용 | 아니오 |
| `M_MasterYN` | `char(1)` | 허용 | 아니오 |
| `E_COMYN` | `char(1)` | 허용 | 아니오 |
| `E_MEMYN` | `char(1)` | 허용 | 아니오 |
| `CDATE` | `datetime` | 허용 | 아니오 |
| `ComNo` | `int` | 허용 | 아니오 |
| `MemNo` | `int` | 허용 | 아니오 |
| `Old_MasterMemNo` | `int` | 허용 | 아니오 |
| `Old_MasterFlag` | `char(1)` | 허용 | 아니오 |
| `Migration_Flag` | `varchar(50)` | 허용 | 아니오 |
| `oldId` | `varchar(12)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2018-01-29T09:53:59.110 |
| 읽기·참조 객체 | `sb_common.dbo.migration_sbjoin_his` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getTransferMap](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L351) — 바인딩: `comNo`. 결과 매핑: `MEM_NO` → `memNo`, `TRANSFER_GUBUN` → `transferGubun`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db096"></a>
## SB_COMMON.dbo.upSBAdm_CanCelReason

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DTI_IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:49.813 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_header`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti.dbo.dti_status_his`, `sb_dti.dbo.dti_status_his_2023_07`, `sb_dti.dbo.dti_status_his_part`, `sb_dti.dbo.dti_status_his_prev_buffer` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getCancelReason](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/transactionstatement/repository/TransactionStatementMapper.kt#L249) — 바인딩: `dtiIdx`. 결과 매핑: `DTI_STATUS` → `dtiStatus`, `MEM_NAME` → `memName`, `REASON` → `reason`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE DTI_IDX = @DTI_IDX
WHERE DTI_IDX =@DTI_IDX
ORDER BY CDATE DESC
WHERE DTI_IDX = @DTI_IDX
ORDER BY CDATE DESC
WHERE DTI_IDX = @DTI_IDX
ORDER BY CDATE DESC
WHERE DTI_IDX = @DTI_IDX
ORDER BY CDATE DESC
```

하위 프로시저·함수·뷰: `master.dbo.clr_dec_char_sel_tc`, `master.dbo.dec_char_sel_tc`, `sb_dti.dbo.dti_header`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_status_his`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db097"></a>
## SB_COMMON.dbo.upSBAdm_DTT_ITEM

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DTT_IDX` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTT_WDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:50.647 |
| 읽기·참조 객체 | `sb_dti.dbo.dtt_item`, `sb_dti.dbo.dtt_item_2020_01`, `sb_dti.dbo.dtt_item_2021_01`, `sb_dti.dbo.dtt_item_2022_01`, `sb_dti.dbo.dtt_item_2023_01`, `sb_dti.dbo.dtt_item_bf`, `sb_dti.dbo.dtt_item_part` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getItems](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/transactionstatement/repository/TransactionStatementMapper.kt#L232) — 바인딩: `dttIdx`, `dttWday`. 결과 매핑: `ITEM_IDX` → `itemIdx`, `ITEM_MD` → `itemMd`, `ITEM_CODE` → `itemCode`, `ITEM_NAME` → `itemName`, `ITEM_SIZE` → `itemSize`, `ITEM_QNT` → `itemQnt`, `UNIT_PRICE` → `unitPrice`, `SUP_AMT` → `supAmt`, `TAX_AMT` → `taxAmt`, `ITEM_REMARK` → `itemRemark`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE DTT_WDAY = @DTT_WDAY AND DTT_IDX = @DTT_IDX
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dtt_item`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db098"></a>
## SB_COMMON.dbo.upSBAdm_DTT_PAYMETHOD

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTT_WDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SERVICE` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2021-02-15T11:32:59.023 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_paymethod`, `sb_dti.dbo.dti_paymethod_2023_07`, `sb_dti.dbo.dti_paymethod_part`, `sb_dti.dbo.dti_paymethod_prev_buffer`, `sb_dti.dbo.dtt_paymethod`, `sb_dti.dbo.dtt_paymethod_2020_01`, `sb_dti.dbo.dtt_paymethod_2021_01`, `sb_dti.dbo.dtt_paymethod_2022_01`, `sb_dti.dbo.dtt_paymethod_2023_01`, `sb_dti.dbo.dtt_paymethod_bf`, `sb_dti.dbo.dtt_paymethod_part` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getPayMethod](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/transactionstatement/repository/TransactionStatementMapper.kt#L208) — 바인딩: `idx`, `dttWday`, `service`. 결과 매핑: `MNYCASH` → `mnyCash`, `MNYCHECK` → `mnyCheck`, `MNYBILL` → `mnyBill`, `MNYCREDIT` → `mnyCredit`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE
WHERE
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_paymethod`, `sb_dti.dbo.dtt_paymethod`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db099"></a>
## SB_COMMON.dbo.upSBAdm_DttSingle_QryEmailLog

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@ETC_PCS_NO` | `varchar(35)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2020-09-16T15:18:10.357 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_email_send_his`, `sb_dti.dbo.dtt_header_cub`, `sb_dti.dbo.dtt_header_cub_2020_01`, `sb_dti.dbo.dtt_header_cub_2021_01`, `sb_dti.dbo.dtt_header_cub_2022_01`, `sb_dti.dbo.dtt_header_cub_2023_01`, `sb_dti.dbo.dtt_header_cub_bf`, `sb_dti.dbo.dtt_header_cub_part`, `sb_dti_log.dbo.dti_email_his`, `sb_dti_log.dbo.dti_email_send_his`, `sb_dti_log.dbo.dti_email_send_his_old`, `sb_dti_log.dbo.dti_email_send_his_part` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getStandaloneEmailHistory](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/transactionstatement/repository/TransactionStatementMapper.kt#L61) — 바인딩: `referenceNumber`. 결과 매핑: `ACTION` → `action`, `EMAIL` → `email`, `CDATE` → `cdate`, `SUCCESS_YN` → `successYn`, `SMTP_MSG` → `smtpMsg`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
JOIN SB_DTI_LOG..DTI_EMAIL_HIS EH WITH(NOLOCK) ON H.DTT_IDX = EH.DTI_IDX AND H.DTT_WDAY = EH.DTI_WDAY
JOIN SB_DTI..DTI_EMAIL_SEND_HIS SH WITH(NOLOCK) ON EH.SB_IDX = SH.SB_IDX
WHERE 1 = 1
JOIN SB_DTI_LOG..DTI_EMAIL_HIS EH WITH(NOLOCK) ON H.DTT_IDX = EH.DTI_IDX AND H.DTT_WDAY = EH.DTI_WDAY
JOIN SB_DTI_LOG..DTI_EMAIL_SEND_HIS SH WITH(NOLOCK) ON EH.SB_IDX = SH.SB_IDX
WHERE 1 = 1
ORDER  BY X.CDATE ASC
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dtt_header_cub`, `sb_dti_log.dbo.dti_email_send_his`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db100"></a>
## SB_COMMON.dbo.upSBAdm_Lst_MEMCOUPON_HIS

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_REGNO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COUPON_KIND` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@QUARTER` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2023-01-13T17:16:51.600 |
| 읽기·참조 객체 | `sb_common.dbo.coupon_kind_info`, `sb_common.dbo.coupon_manage_his`, `sb_common.dbo.coupon_manage_info`, `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchHistories](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/coupon/repository/AdminCouponHistoryMapper.kt#L48) — 바인딩: `page`, `top`, `comRegno`, `couponKind`, `quarter`. 결과 매핑: `RN` → `rn`, `CDATE` → `cdate`, `COUPON_NO` → `couponNo`, `USE_STATE` → `useState`, `TODATE` → `todate`, `FROMDATE` → `fromdate`, `TITLE` → `title`, `CONTENTS` → `contents`, `STATE_DESC` → `stateDesc`, `COUPON_TYPE` → `couponType`, `TOTALCOUNT` → `totalCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SQL = N'
MH.IDX AS IDX, ROW_NUMBER() OVER(ORDER BY MH.CDATE DESC) AS RN,  COUNT(*) OVER() AS TOTALCOUNT
JOIN SB_COMMON..COUPON_MANAGE_INFO AS MI WITH(NOLOCK) ON MI.COUPON_NO = MH.COUPON_NO
JOIN SB_COMMON..COUPON_KIND_INFO AS KI WITH(NOLOCK) ON MI.COUPONKIND_NO = KI.COUPONKIND_NO
JOIN SmartBill3..COMPANY AS C WITH(NOLOCK) ON C.com_no = MI.COM_NO
WHERE 1 = 1
SET @SQL = @SQL + ' C.com_regno = ''' + @COM_REGNO + ''''
SET @SQL = @SQL + ' AND KI.COUPON_TYPE = ' + '''' + @COUPON_KIND + ''''
SET @SQL = @SQL + 'AND MI.QUARTER = ' + '''' + @QUARTER + ''''
SET @SQL = @SQL + N'        )
JOIN SB_COMMON..COUPON_MANAGE_INFO AS MI WITH(NOLOCK) ON MI.COUPON_NO = MH.COUPON_NO
JOIN SB_COMMON..COUPON_KIND_INFO AS KI WITH(NOLOCK) ON MI.COUPONKIND_NO = KI.COUPONKIND_NO
JOIN SmartBill3..COMPANY AS C WITH(NOLOCK) ON C.com_no = MI.COM_NO
INNER JOIN ALLPAGES AS V WITH(NOLOCK) ON V.IDX = MH.IDX
WHERE RN BETWEEN @START_ROWNO AND @END_ROWNO
ORDER BY RN ASC'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db101"></a>
## SB_COMMON.dbo.upSBAdm_LstDeptMng

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DIVISION` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DEPT_NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:50.670 |
| 읽기·참조 객체 | `sb_dti.dbo.dept_admin`, `sb_dti.dbo.dept_member`, `sb_dti.dbo.service_admin`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getTaxInvoiceAdmin](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L700) — 바인딩: `division`, `comNo`, `deptNo`. 결과 매핑: `MEM_NO` → `memNo`, `MEM_ID` → `memId`, `MEM_NAME` → `memName`, `MEM_REALNAME` → `memRealname`, `MEM_TEL` → `memTel`, `MEM_HP` → `memHp`, `MEM_EMAIL` → `memEmail`, `MEM_DEL_YN` → `memDelYn`, `MEM_ENTRY_DATE` → `memEntryDate`, `MEM_MODIFY_DATE` → `memModifyDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
JOIN SMARTBILL3..MEMBER M ON SA.MEM_NO = M.MEM_NO
WHERE SA.COM_NO = @COM_NO
JOIN SMARTBILL3..MEMBER M ON DA.MEM_NO = M.MEM_NO
WHERE DA.COM_NO = @COM_NO AND MEM_DEL_YN = 'N'
JOIN SMARTBILL3..MEMBER M ON DA.MEM_NO = M.MEM_NO
WHERE DA.DEPT_NO = @DEPT_NO AND MEM_DEL_YN = 'N'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db102"></a>
## SB_COMMON.dbo.upSBAdm_LstDTI04

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DTI_WDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:50.017 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti_log.dbo.dti_customer_pwd`, `sb_dti_log.dbo.v_dti_customer_pwd` |
| 쓰기 대상 | `sb_dti_log.dbo.dti_customer_pwd` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [ensureGuestPassword](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/taxinvoice/repository/BonabankTaxInvoiceMapper.kt#L231) — 바인딩: `dtiWday`, `dtiIdx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [ensureGuestPassword](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L467) — 바인딩: `dtiWday`, `dtiIdx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SELECT @BYR_TYPE = BYR_TYPE FROM SB_DTI..DTI_HEADER_CUB WITH(NOLOCK) WHERE DTI_WDAY = @DTI_WDAY AND DTI_IDX = @DTI_IDX
SET @CLASS = '3'
SET @CLASS = '1'
IF NOT EXISTS (SELECT 1 FROM SB_DTI_LOG..V_DTI_CUSTOMER_PWD WHERE DTI_IDX = @DTI_IDX AND CLASS = @CLASS)
WHERE DTI_IDX = @DTI_IDX AND CLASS = @CLASS
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_header_cub`, `sb_dti_log.dbo.v_dti_customer_pwd`, `smartbill3.dbo.fnranbyemail`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db103"></a>
## SB_COMMON.dbo.upSBAdm_LstDTI04_DW

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DTI_WDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:50.437 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_header_cub_2020_01`, `sb_dti.dbo.dti_header_cub_2020_02`, `sb_dti.dbo.dti_header_cub_2020_03`, `sb_dti.dbo.dti_header_cub_2020_04`, `sb_dti.dbo.dti_header_cub_2020_05`, `sb_dti.dbo.dti_header_cub_2020_06`, `sb_dti.dbo.dti_header_cub_2020_07`, `sb_dti.dbo.dti_header_cub_2020_08`, `sb_dti.dbo.dti_header_cub_2020_09`, `sb_dti.dbo.dti_header_cub_2020_10`, `sb_dti.dbo.dti_header_cub_2020_11`, `sb_dti.dbo.dti_header_cub_2020_12`, `sb_dti.dbo.dti_header_cub_2021_01`, `sb_dti.dbo.dti_header_cub_2021_02`, `sb_dti.dbo.dti_header_cub_2021_03`, `sb_dti.dbo.dti_header_cub_2021_04`, `sb_dti.dbo.dti_header_cub_2021_05`, `sb_dti.dbo.dti_header_cub_2021_06`, `sb_dti.dbo.dti_header_cub_2021_07`, `sb_dti.dbo.dti_header_cub_2021_08`, `sb_dti.dbo.dti_header_cub_2021_09`, `sb_dti.dbo.dti_header_cub_2021_10`, `sb_dti.dbo.dti_header_cub_2021_11`, `sb_dti.dbo.dti_header_cub_2021_12`, `sb_dti.dbo.dti_header_cub_2022_01`, `sb_dti.dbo.dti_header_cub_2022_02`, `sb_dti.dbo.dti_header_cub_2022_03`, `sb_dti.dbo.dti_header_cub_2022_04`, `sb_dti.dbo.dti_header_cub_2022_05`, `sb_dti.dbo.dti_header_cub_2022_06`, `sb_dti.dbo.dti_header_cub_2022_07`, `sb_dti.dbo.dti_header_cub_2022_08`, `sb_dti.dbo.dti_header_cub_2022_09`, `sb_dti.dbo.dti_header_cub_2022_10`, `sb_dti.dbo.dti_header_cub_2022_11`, `sb_dti.dbo.dti_header_cub_2022_12`, `sb_dti.dbo.dti_header_cub_2023_01`, `sb_dti.dbo.dti_header_cub_2023_02`, `sb_dti.dbo.dti_header_cub_2023_03`, `sb_dti.dbo.dti_header_cub_2023_04`, `sb_dti.dbo.dti_header_cub_2023_05`, `sb_dti.dbo.dti_header_cub_2023_06`, `sb_dti_dw.dbo.dti_header_cub`, `sb_dti_log.dbo.dti_customer_pwd`, `sb_dti_log.dbo.v_dti_customer_pwd` |
| 쓰기 대상 | `sb_dti_log.dbo.dti_customer_pwd` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [ensureGuestPassword](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L356) — 바인딩: `dtiWday`, `dtiIdx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SELECT @BYR_TYPE = BYR_TYPE FROM SB_DTI_DW..DTI_HEADER_CUB WITH(NOLOCK) WHERE DTI_WDAY = @DTI_WDAY AND DTI_IDX = @DTI_IDX
SET @CLASS = '3'
SET @CLASS = '1'
IF NOT EXISTS (SELECT 1 FROM SB_DTI_LOG..V_DTI_CUSTOMER_PWD WHERE DTI_IDX = @DTI_IDX AND CLASS = @CLASS)
WHERE DTI_IDX = @DTI_IDX AND CLASS = @CLASS
```

하위 프로시저·함수·뷰: `sb_dti_dw.dbo.dti_header_cub`, `sb_dti_log.dbo.v_dti_customer_pwd`, `smartbill3.dbo.fnranbyemail`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db104"></a>
## SB_COMMON.dbo.upSBAdm_LstDTIFail_Bona

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FMDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TODATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-10-28T16:10:12.853 |
| 읽기·참조 객체 | `migration_etcasp.dbo.migration_mapping_company`, `sb_common.dbo.free_service`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti.dbo.dti_header_detail`, `sb_dti.dbo.dti_header_detail_2023_07`, `sb_dti.dbo.dti_header_detail_part`, `sb_dti.dbo.dti_header_detail_prev_buffer`, `sb_dti.dbo.dti_sign_cub`, `sb_dti.dbo.dti_sign_cub_2023_07`, `sb_dti.dbo.dti_sign_cub_part`, `sb_dti.dbo.dti_sign_cub_prev_buffer` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchNtsFailures](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/ntsfailure/repository/BonabankNtsFailureMapper.kt#L51) — 바인딩: `page`, `top`, `fromDate`, `toDate`. 결과 매핑: `DTI_WDAY` → `dtiWday`, `DTI_ISSUEDATE` → `dtiIssueDate`, `ISSUE_ID` → `issueId`, `SUP_COM_REGNO` → `supComRegno`, `SUP_COM_NAME` → `supComName`, `BYR_COM_REGNO` → `byrComRegno`, `BYR_COM_NAME` → `byrComName`, `SUP_AMT` → `supAmt`, `DTI_TYPE` → `dtiType`, `NTS_RESULT_CODE` → `ntsResultCode`, `TOT_COUNT` → `totCount`, `NTS_SEND_DATE` → `ntsSendDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @TOP2 = @TOT_COUNT - ( @PAGE - 1 ) * @TOP
SET @TOP2 = @TOP
SET @SQL = '
INNER JOIN SB_DTI..DTI_HEADER_DETAIL DD WITH(NOLOCK)
LEFT OUTER JOIN SB_DTI..DTI_SIGN_CUB DS WITH(NOLOCK)
LEFT OUTER JOIN SB_COMMON..FREE_SERVICE B WITH(NOLOCK)
INNER JOIN (SELECT COM_REGNO FROM MIGRATION_ETCASP..MIGRATION_MAPPING_COMPANY WITH(NOLOCK) WHERE M_FLAG=''ETAXBILL'' AND USE_YN=''Y'')MC ON DM.SUP_COM_REGNO = MC.COM_REGNO
WHERE DS.BILL_TYPE = ''90'' AND DM.NTS_SEND_STATUS = ''3''
SET @SQL = @SQL + N'
ORDER BY DTI_IDX DESC
ORDER BY DTI_IDX ASC
SB_DTI..DTI_HEADER_CUB DM WITH(NOLOCK) JOIN SB_DTI..DTI_HEADER_DETAIL DD WITH(NOLOCK) ON DM.DTI_WDAY = DD.DTI_WDAY AND DM.DTI_IDX = DD.DTI_IDX
LEFT OUTER JOIN SB_DTI..DTI_SIGN_CUB DS WITH(NOLOCK) ON DD.DTI_WDAY = DS.DTI_WDAY AND DD.DTI_IDX = DS.DTI_IDX
LEFT OUTER JOIN SB_COMMON..FREE_SERVICE FS ON DS.FREE_NO = FS.IDX
INNER JOIN (SELECT COM_REGNO FROM MIGRATION_ETCASP..MIGRATION_MAPPING_COMPANY WITH(NOLOCK) WHERE M_FLAG=''ETAXBILL'' AND USE_YN=''Y'')MC ON DM.SUP_COM_REGNO = MC.COM_REGNO
INNER JOIN LASTPAGES AS V
ORDER BY DM.DTI_IDX DESC'
```

하위 프로시저·함수·뷰: `sb_common.dbo.upsbadm_lstdtifail_bona_count`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_detail`, `sb_dti.dbo.dti_sign_cub`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db105"></a>
## SB_COMMON.dbo.upSBAdm_LstDTIFail_Bona_excel

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@FMDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TODATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-10-28T16:10:51.840 |
| 읽기·참조 객체 | `migration_etcasp.dbo.migration_mapping_company`, `sb_common.dbo.free_service`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti.dbo.dti_header_detail`, `sb_dti.dbo.dti_header_detail_2023_07`, `sb_dti.dbo.dti_header_detail_part`, `sb_dti.dbo.dti_header_detail_prev_buffer`, `sb_dti.dbo.dti_sign_cub`, `sb_dti.dbo.dti_sign_cub_2023_07`, `sb_dti.dbo.dti_sign_cub_part`, `sb_dti.dbo.dti_sign_cub_prev_buffer` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [fetchForExport](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/ntsfailure/repository/BonabankNtsFailureMapper.kt#L73) — 바인딩: `fromDate`, `toDate`. 결과 매핑: `DTI_WDAY` → `dtiWday`, `DTI_ISSUEDATE` → `dtiIssueDate`, `ISSUE_ID` → `issueId`, `SUP_COM_REGNO` → `supComRegno`, `SUP_COM_NAME` → `supComName`, `BYR_COM_REGNO` → `byrComRegno`, `BYR_COM_NAME` → `byrComName`, `SUP_AMT` → `supAmt`, `DTI_TYPE` → `dtiType`, `NTS_RESULT_CODE` → `ntsResultCode`, `NTS_SEND_DATE` → `ntsSendDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SQL = '
SB_DTI..DTI_HEADER_CUB DM WITH(NOLOCK) JOIN SB_DTI..DTI_HEADER_DETAIL DD WITH(NOLOCK) ON DM.DTI_WDAY = DD.DTI_WDAY AND DM.DTI_IDX = DD.DTI_IDX
LEFT OUTER JOIN SB_DTI..DTI_SIGN_CUB DS WITH(NOLOCK) ON DD.DTI_WDAY = DS.DTI_WDAY AND DD.DTI_IDX = DS.DTI_IDX
LEFT OUTER JOIN SB_COMMON..FREE_SERVICE FS ON DS.FREE_NO = FS.IDX
INNER JOIN (SELECT COM_REGNO FROM MIGRATION_ETCASP..MIGRATION_MAPPING_COMPANY WITH(NOLOCK) WHERE M_FLAG=''ETAXBILL'' AND USE_YN=''Y'')MC ON DM.SUP_COM_REGNO = MC.COM_REGNO
WHERE DS.BILL_TYPE = ''90'' AND DM.NTS_SEND_STATUS = ''3''
ORDER BY DM.DTI_IDX DESC'
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_detail`, `sb_dti.dbo.dti_sign_cub`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db106"></a>
## SB_COMMON.dbo.upSBAdm_NtsSendCompany_Bona

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ROWS` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@STAT_MONTH` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_TYPE` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_REGNO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DATE_TYPE` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-10-13T15:10:41.033 |
| 읽기·참조 객체 | `migration_etcasp.dbo.migration_mapping_company`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti.dbo.dti_sign_cub`, `sb_dti.dbo.dti_sign_cub_2023_07`, `sb_dti.dbo.dti_sign_cub_part`, `sb_dti.dbo.dti_sign_cub_prev_buffer`, `sb_dti.dbo.service_admin`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchCompanyChange](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/taxstatistics/repository/BonabankTaxStatisticsMapper.kt#L181) — 바인딩: `pageNo`, `rows`, `statMonth`, `dtiType`, `comRegno`. 결과 매핑: `COM_NAME` → `comName`, `SUP_COM_REGNO` → `supComRegno`, `PRECNT` → `preCnt`, `PREAMT` → `preAmt`, `CNT` → `cnt`, `AMT` → `amt`, `aa` → `amtDiff`, `bb` → `cntDiff`, `MEM_REALNAME` → `memRealname`, `MEM_TEL` → `memTel`, `RCOUNT` → `rCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @DATE_TYPE = 'W'
SET @SPAGE = ((@PAGE_NO - 1) * @ROWS) + 1
SET @EPAGE = @SPAGE - 1 + @ROWS
INNER JOIN SMARTBILL3..COMPANY C WITH(NOLOCK) ON C.COM_REGNO = MC.COM_REGNO
INNER JOIN SMARTBILL3..MEMBER M WITH(NOLOCK) ON M.COM_NO = C.COM_NO
WHERE MC.M_FLAG = 'ETAXBILL' AND MC.USE_YN = 'Y'
INNER JOIN #MEM MM ON MM.MEM_NO = DM.SUP_IDX
WHERE DM.DTI_ISSUEDATE >= @PREV_FROM_DATE
SET @SQL = '
INNER JOIN SB_DTI..DTI_HEADER_CUB DH WITH(NOLOCK)
INNER JOIN SB_DTI..DTI_SIGN_CUB DS WITH(NOLOCK)
INNER JOIN #KEY K
WHERE
GROUP BY
ROW_NUMBER() OVER(ORDER BY SUP_COM_REGNO ASC) AS RN,
GROUP BY
INNER JOIN SB_DTI.DBO.SERVICE_ADMIN AS B WITH(NOLOCK)
LEFT JOIN SMARTBILL3..COMPANY C WITH(NOLOCK)
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_sign_cub`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db107"></a>
## SB_COMMON.dbo.upSBAdm_NtsSendCompany_Bona_excel

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@STAT_MONTH` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_TYPE` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_REGNO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DATE_TYPE` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-10-13T15:11:19.127 |
| 읽기·참조 객체 | `migration_etcasp.dbo.migration_mapping_company`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti.dbo.dti_sign_cub`, `sb_dti.dbo.dti_sign_cub_2023_07`, `sb_dti.dbo.dti_sign_cub_part`, `sb_dti.dbo.dti_sign_cub_prev_buffer`, `sb_dti.dbo.service_admin`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [fetchCompanyChangeForExport](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/taxstatistics/repository/BonabankTaxStatisticsMapper.kt#L202) — 바인딩: `statMonth`, `dtiType`, `comRegno`. 결과 매핑: `COM_NAME` → `comName`, `SUP_COM_REGNO` → `supComRegno`, `PRECNT` → `preCnt`, `PREAMT` → `preAmt`, `CNT` → `cnt`, `AMT` → `amt`, `aa` → `amtDiff`, `bb` → `cntDiff`, `MEM_REALNAME` → `memRealname`, `MEM_TEL` → `memTel`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @DATE_TYPE = 'W'
INNER JOIN SMARTBILL3..COMPANY C WITH(NOLOCK) ON C.COM_REGNO = MC.COM_REGNO
INNER JOIN SMARTBILL3..MEMBER M WITH(NOLOCK) ON M.COM_NO = C.COM_NO
WHERE MC.M_FLAG = 'ETAXBILL' AND MC.USE_YN = 'Y'
INNER JOIN #MEM MM ON MM.MEM_NO = DM.SUP_IDX
WHERE DM.DTI_ISSUEDATE >= @PREV_FROM_DATE
SET @SQL = '
INNER JOIN SB_DTI..DTI_HEADER_CUB DH WITH(NOLOCK)
INNER JOIN SB_DTI..DTI_SIGN_CUB DS WITH(NOLOCK)
INNER JOIN #KEY K
WHERE
GROUP BY
GROUP BY
INNER JOIN SB_DTI.DBO.SERVICE_ADMIN AS B WITH(NOLOCK)
LEFT JOIN SMARTBILL3..COMPANY C WITH(NOLOCK)
LEFT JOIN MANAGER M
ORDER BY
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_sign_cub`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db108"></a>
## SB_COMMON.dbo.upSBAdm_QryEmailLog

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@ETC_PCS_NO` | `varchar(35)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:50.313 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_email_send_his`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti_log.dbo.dti_email_his`, `sb_dti_log.dbo.dti_email_send_his`, `sb_dti_log.dbo.dti_email_send_his_old`, `sb_dti_log.dbo.dti_email_send_his_part` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getEmailHistory](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L336) — 바인딩: `etcPcsNo`. 결과 매핑: `ACTION` → `action`, `EMAIL` → `email`, `CDATE` → `cdate`, `SUCCESS_YN` → `successYn`, `SMTP_MSG` → `smtpMsg`.
- [findEmailLog](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/taxinvoice/repository/BonabankTaxInvoiceMapper.kt#L160) — 바인딩: `etcPcsNo`. 결과 매핑: `ACTION` → `action`, `EMAIL` → `email`, `CDATE` → `cDate`, `SUCCESS_YN` → `successYn`, `SMTP_MSG` → `smtpMsg`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE
WHERE
ORDER  BY
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_header_cub`, `sb_dti_log.dbo.dti_email_send_his`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db109"></a>
## SB_COMMON.dbo.upSBAdm_QryEmailLog_DW

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@ETC_PCS_NO` | `varchar(35)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:50.473 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_email_send_his`, `sb_dti.dbo.dti_header_cub_2020_01`, `sb_dti.dbo.dti_header_cub_2020_02`, `sb_dti.dbo.dti_header_cub_2020_03`, `sb_dti.dbo.dti_header_cub_2020_04`, `sb_dti.dbo.dti_header_cub_2020_05`, `sb_dti.dbo.dti_header_cub_2020_06`, `sb_dti.dbo.dti_header_cub_2020_07`, `sb_dti.dbo.dti_header_cub_2020_08`, `sb_dti.dbo.dti_header_cub_2020_09`, `sb_dti.dbo.dti_header_cub_2020_10`, `sb_dti.dbo.dti_header_cub_2020_11`, `sb_dti.dbo.dti_header_cub_2020_12`, `sb_dti.dbo.dti_header_cub_2021_01`, `sb_dti.dbo.dti_header_cub_2021_02`, `sb_dti.dbo.dti_header_cub_2021_03`, `sb_dti.dbo.dti_header_cub_2021_04`, `sb_dti.dbo.dti_header_cub_2021_05`, `sb_dti.dbo.dti_header_cub_2021_06`, `sb_dti.dbo.dti_header_cub_2021_07`, `sb_dti.dbo.dti_header_cub_2021_08`, `sb_dti.dbo.dti_header_cub_2021_09`, `sb_dti.dbo.dti_header_cub_2021_10`, `sb_dti.dbo.dti_header_cub_2021_11`, `sb_dti.dbo.dti_header_cub_2021_12`, `sb_dti.dbo.dti_header_cub_2022_01`, `sb_dti.dbo.dti_header_cub_2022_02`, `sb_dti.dbo.dti_header_cub_2022_03`, `sb_dti.dbo.dti_header_cub_2022_04`, `sb_dti.dbo.dti_header_cub_2022_05`, `sb_dti.dbo.dti_header_cub_2022_06`, `sb_dti.dbo.dti_header_cub_2022_07`, `sb_dti.dbo.dti_header_cub_2022_08`, `sb_dti.dbo.dti_header_cub_2022_09`, `sb_dti.dbo.dti_header_cub_2022_10`, `sb_dti.dbo.dti_header_cub_2022_11`, `sb_dti.dbo.dti_header_cub_2022_12`, `sb_dti.dbo.dti_header_cub_2023_01`, `sb_dti.dbo.dti_header_cub_2023_02`, `sb_dti.dbo.dti_header_cub_2023_03`, `sb_dti.dbo.dti_header_cub_2023_04`, `sb_dti.dbo.dti_header_cub_2023_05`, `sb_dti.dbo.dti_header_cub_2023_06`, `sb_dti_dw.dbo.dti_header_cub`, `sb_dti_log.dbo.dti_email_his`, `sb_dti_log.dbo.dti_email_send_his`, `sb_dti_log.dbo.dti_email_send_his_old`, `sb_dti_log.dbo.dti_email_send_his_part` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getEmailHistory](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L262) — 바인딩: `etcPcsNo`. 결과 매핑: `ACTION` → `action`, `EMAIL` → `email`, `CDATE` → `cdate`, `SUCCESS_YN` → `successYn`, `SMTP_MSG` → `smtpMsg`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE
WHERE
ORDER  BY
```

하위 프로시저·함수·뷰: `sb_dti_dw.dbo.dti_header_cub`, `sb_dti_log.dbo.dti_email_send_his`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db110"></a>
## SB_COMMON.dbo.upSBAdm_QryMemID

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DTI_WDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2025-05-19T13:15:20.287 |
| 읽기·참조 객체 | `sb_common.dbo.neobill_oapi_log_b2b`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti.dbo.dti_header_detail`, `sb_dti.dbo.dti_header_detail_2020_01`, `sb_dti.dbo.dti_header_detail_2020_02`, `sb_dti.dbo.dti_header_detail_2020_03`, `sb_dti.dbo.dti_header_detail_2020_04`, `sb_dti.dbo.dti_header_detail_2020_05`, `sb_dti.dbo.dti_header_detail_2020_06`, `sb_dti.dbo.dti_header_detail_2020_07`, `sb_dti.dbo.dti_header_detail_2020_08`, `sb_dti.dbo.dti_header_detail_2020_09`, `sb_dti.dbo.dti_header_detail_2020_10`, `sb_dti.dbo.dti_header_detail_2020_11`, `sb_dti.dbo.dti_header_detail_2020_12`, `sb_dti.dbo.dti_header_detail_2021_01`, `sb_dti.dbo.dti_header_detail_2021_02`, `sb_dti.dbo.dti_header_detail_2021_03`, `sb_dti.dbo.dti_header_detail_2021_04`, `sb_dti.dbo.dti_header_detail_2021_05`, `sb_dti.dbo.dti_header_detail_2021_06`, `sb_dti.dbo.dti_header_detail_2021_07`, `sb_dti.dbo.dti_header_detail_2021_08`, `sb_dti.dbo.dti_header_detail_2021_09`, `sb_dti.dbo.dti_header_detail_2021_10`, `sb_dti.dbo.dti_header_detail_2021_11`, `sb_dti.dbo.dti_header_detail_2021_12`, `sb_dti.dbo.dti_header_detail_2022_01`, `sb_dti.dbo.dti_header_detail_2022_02`, `sb_dti.dbo.dti_header_detail_2022_03`, `sb_dti.dbo.dti_header_detail_2022_04`, `sb_dti.dbo.dti_header_detail_2022_05`, `sb_dti.dbo.dti_header_detail_2022_06`, `sb_dti.dbo.dti_header_detail_2022_07`, `sb_dti.dbo.dti_header_detail_2022_08`, `sb_dti.dbo.dti_header_detail_2022_09`, `sb_dti.dbo.dti_header_detail_2022_10`, `sb_dti.dbo.dti_header_detail_2022_11`, `sb_dti.dbo.dti_header_detail_2022_12`, `sb_dti.dbo.dti_header_detail_2023_01`, `sb_dti.dbo.dti_header_detail_2023_02`, `sb_dti.dbo.dti_header_detail_2023_03`, `sb_dti.dbo.dti_header_detail_2023_04`, `sb_dti.dbo.dti_header_detail_2023_05`, `sb_dti.dbo.dti_header_detail_2023_06`, `sb_dti.dbo.dti_header_detail_2023_07`, `sb_dti.dbo.dti_header_detail_global`, `sb_dti.dbo.dti_header_detail_part`, `sb_dti.dbo.dti_header_detail_prev_buffer`, `sb_dti.dbo.service_admin`, `sb_dti_dw.dbo.dti_header_detail`, `smartbill3.dbo.company`, `smartbill3.dbo.company_exception`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getMemberInfo](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L321) — 바인딩: `dtiWday`, `dtiIdx`. 결과 매핑: `SUP_ID` → `supId`, `BYR_ID` → `byrId`, `DELAY_YN` → `delayYn`, `DTI_STATUS` → `dtiStatus`, `REQ_RCV_IDX` → `reqRcvIdx`, `DTI_ADM_NO` → `dtiAdmNo`, `SUP_NOMEM_YN` → `supNomemYn`, `SUP_SENDMAIL_YN` → `supSendmailYn`, `ISSUE_PATH` → `issuePath`.
- [findMemberInfo](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/taxinvoice/repository/BonabankTaxInvoiceMapper.kt#L143) — 바인딩: `wday`, `dtiIdx`. 결과 매핑: `SUP_ID` → `supId`, `BYR_ID` → `byrId`, `DELAY_YN` → `delayYn`, `DTI_STATUS` → `dtiStatus`, `REQ_RCV_IDX` → `reqRcvIdx`, `DTI_ADM_NO` → `dtiAdmNo`, `SUP_NOMEM_YN` → `supNomemYn`, `SUP_SENDMAIL_YN` → `supSendmailYn`, `ISSUE_PATH` → `issuePath`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SUP_SENDMAIL_YN = 'N'
WHERE
WHERE
WHERE
SET @BYR_ID = '비회원'
JOIN SMARTBILL3..MEMBER B WITH(NOLOCK)
JOIN SB_DTI..SERVICE_ADMIN C WITH(NOLOCK)
WHERE
JOIN SMARTBILL3..COMPANY COM WITH (NOLOCK) ON EX.COM_NO = COM.COM_NO
WHERE EX.EXCEPT_CODE = 'BRK_GUESTSUP' AND EX.USE_YN ='Y'
SET @SUP_SENDMAIL_YN = 'Y'
INNER JOIN SB_DTI..DTI_HEADER_DETAIL_GLOBAL DD WITH(NOLOCK)
LEFT OUTER JOIN SB_COMMON..NEOBILL_OAPI_LOG_B2B B2B WITH(NOLOCK) ON DM.DTI_WDAY = B2B.DTI_WDAY AND DM.DTI_IDX = B2B.DTI_IDX
WHERE DM.DTI_WDAY = @DTI_WDAY
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_detail`, `sb_dti.dbo.dti_header_detail_global`, `sb_dti_dw.dbo.dti_header_detail`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db111"></a>
## SB_COMMON.dbo.upSBAdm_QryMemID_DW

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DTI_WDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:50.463 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_header_cub_2020_01`, `sb_dti.dbo.dti_header_cub_2020_02`, `sb_dti.dbo.dti_header_cub_2020_03`, `sb_dti.dbo.dti_header_cub_2020_04`, `sb_dti.dbo.dti_header_cub_2020_05`, `sb_dti.dbo.dti_header_cub_2020_06`, `sb_dti.dbo.dti_header_cub_2020_07`, `sb_dti.dbo.dti_header_cub_2020_08`, `sb_dti.dbo.dti_header_cub_2020_09`, `sb_dti.dbo.dti_header_cub_2020_10`, `sb_dti.dbo.dti_header_cub_2020_11`, `sb_dti.dbo.dti_header_cub_2020_12`, `sb_dti.dbo.dti_header_cub_2021_01`, `sb_dti.dbo.dti_header_cub_2021_02`, `sb_dti.dbo.dti_header_cub_2021_03`, `sb_dti.dbo.dti_header_cub_2021_04`, `sb_dti.dbo.dti_header_cub_2021_05`, `sb_dti.dbo.dti_header_cub_2021_06`, `sb_dti.dbo.dti_header_cub_2021_07`, `sb_dti.dbo.dti_header_cub_2021_08`, `sb_dti.dbo.dti_header_cub_2021_09`, `sb_dti.dbo.dti_header_cub_2021_10`, `sb_dti.dbo.dti_header_cub_2021_11`, `sb_dti.dbo.dti_header_cub_2021_12`, `sb_dti.dbo.dti_header_cub_2022_01`, `sb_dti.dbo.dti_header_cub_2022_02`, `sb_dti.dbo.dti_header_cub_2022_03`, `sb_dti.dbo.dti_header_cub_2022_04`, `sb_dti.dbo.dti_header_cub_2022_05`, `sb_dti.dbo.dti_header_cub_2022_06`, `sb_dti.dbo.dti_header_cub_2022_07`, `sb_dti.dbo.dti_header_cub_2022_08`, `sb_dti.dbo.dti_header_cub_2022_09`, `sb_dti.dbo.dti_header_cub_2022_10`, `sb_dti.dbo.dti_header_cub_2022_11`, `sb_dti.dbo.dti_header_cub_2022_12`, `sb_dti.dbo.dti_header_cub_2023_01`, `sb_dti.dbo.dti_header_cub_2023_02`, `sb_dti.dbo.dti_header_cub_2023_03`, `sb_dti.dbo.dti_header_cub_2023_04`, `sb_dti.dbo.dti_header_cub_2023_05`, `sb_dti.dbo.dti_header_cub_2023_06`, `sb_dti.dbo.service_admin`, `sb_dti_dw.dbo.dti_header_cub`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getMemberInfo](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L247) — 바인딩: `dtiWday`, `dtiIdx`. 결과 매핑: `SUP_ID` → `supId`, `BYR_ID` → `byrId`, `DELAY_YN` → `delayYn`, `DTI_STATUS` → `dtiStatus`, `REQ_RCV_IDX` → `reqRcvIdx`, `DTI_ADM_NO` → `dtiAdmNo`, `SUP_NOMEM_YN` → `supNomemYn`, `SUP_SENDMAIL_YN` → `supSendmailYn`, `ISSUE_PATH` → `issuePath`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE
WHERE
WHERE
SET @BYR_ID = '비회원'
JOIN SMARTBILL3..MEMBER B WITH(NOLOCK)
JOIN SB_DTI..SERVICE_ADMIN C WITH(NOLOCK)
WHERE
```

하위 프로시저·함수·뷰: `sb_dti_dw.dbo.dti_header_cub`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db112"></a>
## SB_COMMON.dbo.upSBAdm_RefundBillList

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_REGNO` | `varchar(16)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REFUNDDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:50.357 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchRefundAvailableAmount](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/refund/repository/RefundAmountMapper.kt#L35) — 바인딩: `comRegno`, `refundDate`. 결과 매핑: `PREPAY_NO` → `prepayNo`, `PREPAY_DATE` → `prepayDate`, `PREPAY_AMT` → `prepayAmt`, `PRINCIPAL_AMT` → `principalAmt`, `REFUND_DATE` → `refundDate`, `SUBTRACTION` → `subtraction`, `CHARGE` → `charge`, `USE_AMT` → `useAmt`, `REFUND_YN` → `refundYn`, `REFUND_AMT` → `refundAmt`, `REFUND_COMMISSION_AMT` → `refundCommissionAmt`, `one_refund_amt` → `oneRefundAmt`, `one_refund_commission_amt` → `oneRefundCommissionAmt`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET  @COM_REGNO = REPLACE(@COM_REGNO, '-', '')
WHERE COM_REGNO = @COM_REGNO AND COM_DEL_YN = 'N'
JOIN(SELECT COM_NO, SUM(USE_AMT) AS USE_AMT, isnull(SUM(REFUND_AMT), 0) AS REFUND_AMT, isnull(SUM(REFUND_COMMISSION_AMT), 0) AS REFUND_COMMISSION_AMT FROM SMARTBILL3..SERVICE_PREPAY WITH (NOLOCK)
WHERE COM_NO = @COMNO
GROUP BY COM_NO) B
LEFT OUTER JOIN(SELECT IDX, isnull(STATEMENTAMOUNT, 0) as STATEMENTAMOUNT FROM SMARTBILL3..SERVICE_PREPAY_HIS WHERE CHANNEL = 'REFUND') C ON A.PREPAY_NO = C.IDX
LEFT OUTER JOIN  (select idx,  sum(statementAmount) as one_use_amt from SMARTBILL3..SERVICE_PREPAY_his with(nolock) where channel = 'dtiservice' group by idx) D ON A.PREPAY_NO = D.IDX
WHERE A.COM_NO = @COMNO AND PREPAY_DATE BETWEEN DATEADD(DAY,-90,@REFUNDDATE) AND  DATEADD(DAY,1,@REFUNDDATE)
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db113"></a>
## SB_COMMON.dbo.upSBAdm_Sav_Qna

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DIV` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@QNA_TYPE` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@NUM` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@QNA_WRITER` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@QNA_TITLE` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@QNA_CONTENTS` | `text` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MEM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-09-12T10:41:13.830 |
| 읽기·참조 객체 | `office.dbo.msg_queue`, `smartbill3.dbo.arreo_sms_sb`, `smartbill3.dbo.member`, `smartbill3.dbo.qna` |
| 쓰기 대상 | `office.dbo.msg_queue`, `smartbill3.dbo.arreo_sms_sb`, `smartbill3.dbo.qna` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `0`; `1` |

### Mapper 입출력 매핑

- [saveQna](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/qna/repository/AdminQnaMapper.kt#L156) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `gubun`, `qnaType`, `num`, `qnaWriter`, `qnaTitle`, `qnaContents`, `memNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SND_COM_NO = 0
SET @RCV_COM_NO = 0
Begin Tran
set @intMaxRef = 1
set @intMaxRef = @intMaxRef + 1
WHERE QNA_NO = @NUM
set @strRStep = @strSStep + 1
where qna_ref = @strRef and qna_ansnum = @strAnsnum
where qna_ref = @strRef and qna_step <= @strSStep and qna_ansnum > @strAnsnum
where qna_ref = @strRef and qna_ansnum >= @intMinAnsnum
where qna_ref = @strRef
set @strAnsnum = @intMaxAnsnum + 1
SELECT @RCV_COM_NO = COM_NO FROM SMARTBILL3..MEMBER WHERE MEM_NO = @RCV_MEM_NO
SELECT @SND_COM_NO = COM_NO FROM SMARTBILL3..MEMBER WHERE MEM_NO = @MEM_NO
SET @IDENTITY = @@IDENTITY
WHERE QNA_NO = @NUM
where qna_no = @num
set @strQnaWriterSe = 'u'
```

하위 프로시저·함수·뷰: `smartbill3.dbo.upsave_managementsms`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db114"></a>
## SB_COMMON.dbo.upSBAdm_Save_MEMCOUPON_Update

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COUPON_NO` | `varchar(25)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@USE_STATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@STATE_DESC` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REASON` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BIZ_CUSER` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT_CODE` | `int` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2023-01-13T17:17:14.363 |
| 읽기·참조 객체 | `sb_common.dbo.coupon_kind_info`, `sb_common.dbo.coupon_manage_his`, `sb_common.dbo.coupon_manage_info`, `smartbill3.dbo.company` |
| 쓰기 대상 | `sb_common.dbo.coupon_manage_his`, `sb_common.dbo.coupon_manage_info` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `END CATCH` |

### Mapper 입출력 매핑

- [updateCouponState](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/coupon/repository/AdminCouponMapper.kt#L95) — 바인딩: `couponNo`, `useState`, `stateDesc`, `reason`, `bizCuser`, `resultCode, mode=OUT, jdbcType=INTEGER`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
BEGIN TRAN
JOIN COUPON_KIND_INFO AS KI WITH(NOLOCK) ON MI.COUPONKIND_NO = KI.COUPONKIND_NO
JOIN SmartBill3..COMPANY AS C WITH(NOLOCK) ON C.com_no = MI.COM_NO
WHERE MI.COUPON_NO = @COUPON_NO
SET @ROWCOUNT_MH = @@ROWCOUNT
SET USE_STATE = @USE_STATE, UDATE = GETDATE() WHERE COUPON_NO = @COUPON_NO
SET @ROWCOUNT_MI = @@ROWCOUNT
SET @RESULT_CODE = '30000'
SET @RESULT_CODE = '99999'
ROLLBACK TRAN
COMMIT TRAN
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db115"></a>
## SB_COMMON.dbo.upSBAdm_StatsDTI_Bona

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@FROMDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TODATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_TYPE` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_REGNO` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DATE_TYPE` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-10-13T15:08:57.583 |
| 읽기·참조 객체 | `migration_etcasp.dbo.migration_mapping_company`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti.dbo.dti_sign_cub`, `sb_dti.dbo.dti_sign_cub_2023_07`, `sb_dti.dbo.dti_sign_cub_part`, `sb_dti.dbo.dti_sign_cub_prev_buffer`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [fetchSummary](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/taxstatistics/repository/BonabankTaxStatisticsMapper.kt#L114) — 바인딩: `fromDate`, `toDate`, `dtiType`, `comRegno`. 결과 매핑: `TotalT` → `totalT`, `BsumT` → `bsumT`, `RsumT` → `rsumT`, `FsumT` → `fsumT`, `R1sumT` → `r1sumT`, `TotalAmtT` → `totalAmtT`, `TotalF` → `totalF`, `BsumF` → `bsumF`, `RsumF` → `rsumF`, `FsumF` → `fsumF`, `R1sumF` → `r1sumF`, `TotalAmtF` → `totalAmtF`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
INNER JOIN SMARTBILL3..COMPANY C WITH(NOLOCK) ON C.COM_REGNO = MC.COM_REGNO
INNER JOIN SMARTBILL3..MEMBER M WITH(NOLOCK) ON M.COM_NO = C.COM_NO
WHERE MC.M_FLAG = 'ETAXBILL' AND MC.USE_YN = 'Y'
INNER JOIN #MEM MM ON MM.MEM_NO = DM.SUP_IDX
WHERE DM.DTI_ISSUEDATE >= CAST(@FROMDATE AS DATETIME)
SET @SQL = '
INNER JOIN MIGRATION_ETCASP..MIGRATION_MAPPING_COMPANY MC WITH(NOLOCK)
INNER JOIN SB_DTI..DTI_SIGN_CUB DS WITH(NOLOCK)
N'		INNER JOIN #KEY K
WHERE
group by DTI_TYPE, NTS_SEND_STATUS
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_sign_cub`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db116"></a>
## SB_COMMON.dbo.upSBAdm_StatsDTICompany_Bona

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROMDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TODATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_TYPE` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_REGNO` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DATE_TYPE` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-10-13T15:09:30.780 |
| 읽기·참조 객체 | `migration_etcasp.dbo.migration_mapping_company`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti.dbo.dti_sign_cub`, `sb_dti.dbo.dti_sign_cub_2023_07`, `sb_dti.dbo.dti_sign_cub_part`, `sb_dti.dbo.dti_sign_cub_prev_buffer`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchCompanies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/taxstatistics/repository/BonabankTaxStatisticsMapper.kt#L134) — 바인딩: `page`, `top`, `fromDate`, `toDate`, `dtiType`, `comRegno`. 결과 매핑: `COM_NAME` → `comName`, `SUP_COM_REGNO` → `supComRegno`, `COM_BSUM` → `comBsum`, `COM_RSUM` → `comRsum`, `COM_FSUM` → `comFsum`, `COM_R1SUM` → `comR1sum`, `COM_TOTAL` → `comTotal`, `COM_TOTALAMT` → `comTotalAmt`, `TOT_COUNT` → `totCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @START_ROW = ((@PAGE-1) * @TOP)+1
SET @END_ROW = CAST(@START_ROW AS INT) + CAST(@TOP AS INT) - 1;
INNER JOIN SMARTBILL3..COMPANY C WITH(NOLOCK) ON C.COM_REGNO = MC.COM_REGNO
INNER JOIN SMARTBILL3..MEMBER M WITH(NOLOCK) ON M.COM_NO = C.COM_NO
WHERE MC.M_FLAG = 'ETAXBILL' AND MC.USE_YN = 'Y'
INNER JOIN #MEM MM ON MM.MEM_NO = DM.SUP_IDX
WHERE DM.DTI_ISSUEDATE >= CAST(@FROMDATE AS DATETIME)
SET @SQL = '
, ROW_NUMBER() OVER (ORDER BY SUP_COM_REGNO DESC) AS ROWRANK
INNER JOIN SB_DTI..DTI_SIGN_CUB DS WITH(NOLOCK)
INNER JOIN (SELECT COM_REGNO FROM MIGRATION_ETCASP..MIGRATION_MAPPING_COMPANY WITH(NOLOCK) WHERE M_FLAG=''ETAXBILL'' AND USE_YN=''Y'')MC ON DM.SUP_COM_REGNO = MC.COM_REGNO
'			INNER JOIN #KEY K
WHERE
GROUP BY SUP_COM_REGNO, NTS_SEND_STATUS
A GROUP BY SUP_COM_REGNO
INNER JOIN SMARTBILL3..COMPANY C WITH(NOLOCK) ON O.SUP_COM_REGNO = C.COM_REGNO AND C.COM_DEL_YN = ''N''
WHERE RowRank BETWEEN ''' + CONVERT(VARCHAR, @START_ROW) +''' AND ''' + CONVERT(VARCHAR, @END_ROW) + '''
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_sign_cub`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db117"></a>
## SB_COMMON.dbo.upSBAdm_StatsDTICompany_Bona_excel

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@FROMDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TODATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_TYPE` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_REGNO` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DATE_TYPE` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-10-13T15:09:58.193 |
| 읽기·참조 객체 | `migration_etcasp.dbo.migration_mapping_company`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti.dbo.dti_sign_cub`, `sb_dti.dbo.dti_sign_cub_2023_07`, `sb_dti.dbo.dti_sign_cub_part`, `sb_dti.dbo.dti_sign_cub_prev_buffer`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [fetchCompaniesForExport](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/taxstatistics/repository/BonabankTaxStatisticsMapper.kt#L153) — 바인딩: `fromDate`, `toDate`, `dtiType`, `comRegno`. 결과 매핑: `com_name` → `comName`, `sup_com_regno` → `supComRegno`, `com_Bsum` → `comBsum`, `com_Rsum` → `comRsum`, `com_Fsum` → `comFsum`, `com_R1sum` → `comR1sum`, `com_Total` → `comTotal`, `com_TotalAmt` → `comTotalAmt`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
INNER JOIN SMARTBILL3..COMPANY C WITH(NOLOCK) ON C.COM_REGNO = MC.COM_REGNO
INNER JOIN SMARTBILL3..MEMBER M WITH(NOLOCK) ON M.COM_NO = C.COM_NO
WHERE MC.M_FLAG = 'ETAXBILL' AND MC.USE_YN = 'Y'
INNER JOIN #MEM MM ON MM.MEM_NO = DM.SUP_IDX
WHERE DM.DTI_ISSUEDATE >= CAST(@FROMDATE AS DATETIME)
SET @SQL = '
INNER JOIN SB_DTI..DTI_SIGN_CUB DS WITH(NOLOCK)
INNER JOIN (SELECT COM_REGNO FROM MIGRATION_ETCASP..MIGRATION_MAPPING_COMPANY WITH(NOLOCK) WHERE M_FLAG=''ETAXBILL'' AND USE_YN=''Y'')MC ON DM.SUP_COM_REGNO = MC.COM_REGNO
N'			INNER JOIN #KEY K
WHERE
group by sup_com_regno, NTS_SEND_STATUS
) a group by sup_com_regno
left join smartbill3..COMPANY C with(nolock) on D.sup_com_regno = C.com_regno and C.com_del_yn = ''N''
ORDER BY sup_com_regno DESC '
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_sign_cub`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db118"></a>
## SB_COMMON.dbo.upSup_HitFaq

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@FAQ_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ERR_CODE` | `varchar(10)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISSUCCESS` | `bit` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:50.827 |
| 읽기·참조 객체 | `smartbill3.dbo.faq` |
| 쓰기 대상 | `smartbill3.dbo.faq` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [incrementHit](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/faq/repository/AdminFaqMapper.kt#L129) — 바인딩: `faqNo`, `errCode, mode=OUT, jdbcType=NVARCHAR`, `isSuccess, mode=OUT, jdbcType=BIT`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @ERR_CODE = '30000'
SET @ISSUCCESS = 1
WHERE FAQ_NO = @FAQ_NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db119"></a>
## SB_COMMON.dbo.upSup_HitNotice

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@NOTICE_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ERR_CODE` | `varchar(10)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISSUCCESS` | `bit` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:50.830 |
| 읽기·참조 객체 | `smartbill3.dbo.notice` |
| 쓰기 대상 | `smartbill3.dbo.notice` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [incrementHit](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/notice/repository/BonabankNoticeMapper.kt#L98) — 바인딩: `noticeNo`, `errCode, mode=OUT, jdbcType=NVARCHAR`, `isSuccess, mode=OUT, jdbcType=BIT`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [incrementHit](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/notice/repository/AdminNoticeMapper.kt#L112) — 바인딩: `noticeNo`, `errCode, mode=OUT, jdbcType=NVARCHAR`, `isSuccess, mode=OUT, jdbcType=BIT`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @ERR_CODE = '30000'
SET @ISSUCCESS = 1
WHERE NOTICE_NO = @NOTICE_NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db120"></a>
## SB_COMMON.dbo.upSup_HitPds

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PDS_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ERR_CODE` | `varchar(10)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISSUCCESS` | `bit` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:37:50.833 |
| 읽기·참조 객체 | `smartbill3.dbo.pds` |
| 쓰기 대상 | `smartbill3.dbo.pds` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [incrementHit](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/pds/repository/AdminPdsMapper.kt#L125) — 바인딩: `pdsNo`, `errCode, mode=OUT, jdbcType=NVARCHAR`, `isSuccess, mode=OUT, jdbcType=BIT`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @ERR_CODE = '30000'
SET @ISSUCCESS = 1
WHERE PDS_NO = @PDS_NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db121"></a>
## SB_Customize.dbo.upSEC_CodeInfo

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_REGNO` | `varchar(13)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CODE` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CODE_TYPE` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:41:50.163 |
| 읽기·참조 객체 | `sb_customize.dbo.sec_code` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findCode](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/SamsungSystemCodeMapper.kt#L20) — 바인딩: `companyRegistrationNumber`, `code`, `codeType`. 결과 매핑: `CODE` → `code`, `CODE_DESC` → `codeDesc`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
IF EXISTS (    SELECT *  FROM SB_CUSTOMIZE..SEC_CODE WITH (NOLOCK) WHERE COM_REGNO = @COM_REGNO AND CODE_TYPE = @CODE_TYPE  AND CODE = @CODE  )
WHERE COM_REGNO = @COM_REGNO AND CODE_TYPE = @CODE_TYPE  AND CODE = @CODE
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db122"></a>
## SB_DRC.dbo.PrDrc_AdminDrcCompany

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DRC_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ComType` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-01-05T17:30:09.263 |
| 읽기·참조 객체 | `sb_drc.dbo.drc_company`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findMemberCompany](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/CreditorBalanceCertificateMapper.kt#L116) — 바인딩: `drcNo`, `comType`. 결과 매핑: `DRC_no` → `drcNo`, `Com_no` → `comNo`, `Com_Type` → `comType`, `Mem_No` → `memNo`, `com_regno` → `comRegno`, `com_name` → `comName`, `com_president` → `comPresident`, `Com_Address` → `comAddress`, `mem_name` → `memName`, `mem_tel` → `memTel`, `mem_email` → `memEmail`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
JOIN smartbill3.dbo.company com WITH(NOLOCK) on drccom.com_no=com.com_no
JOIN smartbill3.dbo.member mem WITH(NOLOCK)  on drccom.com_no=mem.com_no and drccom.mem_no=mem.mem_no
WHERE
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db123"></a>
## SB_DRC.dbo.PrDrc_AdminDrcCompany_NM

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DRC_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ComType` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2019-03-06T15:51:52.660 |
| 읽기·참조 객체 | `sb_drc.dbo.drc_company_nm` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findNonMemberCompany](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/CreditorBalanceCertificateMapper.kt#L133) — 바인딩: `drcNo`, `comType`. 결과 매핑: `DRC_no` → `drcNo`, `Com_no` → `comNo`, `Com_Type` → `comType`, `Mem_No` → `memNo`, `com_regno` → `comRegno`, `com_name` → `comName`, `com_president` → `comPresident`, `Com_Address` → `comAddress`, `mem_name` → `memName`, `mem_tel` → `memTel`, `mem_email` → `memEmail`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db124"></a>
## SB_DRC.dbo.PrDrc_AdminDrcFile

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DRC_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-01-05T17:30:21.807 |
| 읽기·참조 객체 | `sb_drc.dbo.drc_file` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findFiles](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/CreditorBalanceCertificateMapper.kt#L148) — 바인딩: `drcNo`. 결과 매핑: `DRC_No` → `drcNo`, `File_No` → `fileNo`, `File_Type` → `fileType`, `File_Status` → `fileStatus`, `File_Name` → `fileName`, `File_path` → `filePath`, `File_Size` → `fileSize`, `IF_File_Seq` → `ifFileSeq`, `Reg_Date` → `regDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db125"></a>
## SB_DRC.dbo.PrDrc_AdminMain

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DRC_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-01-05T17:30:29.310 |
| 읽기·참조 객체 | `sb_drc.dbo.drc_main` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findMain](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/CreditorBalanceCertificateMapper.kt#L99) — 바인딩: `drcNo`. 결과 매핑: `DRC_No` → `drcNo`, `Basic_Date` → `basicDate`, `Currency_Unit` → `currencyUnit`, `Receivable_Balance` → `receivableBalance`, `Creditor_Remark` → `creditorRemark`, `Debtor_Remark` → `debtorRemark`, `Purchase_Amount` → `purchaseAmount`, `Payment_Cash` → `paymentCash`, `Payment_PostdatedCheck` → `paymentPostdatedCheck`, `Before_Receivables_Balance` → `beforeReceivablesBalance`, `Confirm_Balance` → `confirmBalance`, `DTI_Date` → `dtiDate`, `IF_Conversation_Id` → `ifConversationId`, `Reg_Date` → `regDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db126"></a>
## SB_DRC.dbo.PrDrc_DrcUserRight_Q

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@Mem_No` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-01-05T17:34:46.137 |
| 읽기·참조 객체 | `sb_drc.dbo.drc_member_right`, `sb_drc.dbo.drc_right` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findMemberRights](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcRightMapper.kt#L84) — 바인딩: `memNo`. 결과 매핑: `Service_Id` → `serviceId`, `Right_Code` → `rightCode`, `Right_name` → `rightName`, `Use_Yn` → `useYn`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE Mem_No = @Mem_No
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db127"></a>
## SB_DRC.dbo.upAdmSB_Lst_DRC_MoniteringLst

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@StartDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@EndDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SearchType` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SearchText` | `varchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Com_Type` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Status_Code` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ConvId` | `varchar(35)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TransferStatus` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2023-07-20T11:24:40.307 |
| 읽기·참조 객체 | `sb_drc.dbo.drc_company`, `sb_drc.dbo.drc_company_link`, `sb_drc.dbo.drc_main`, `sb_drc.dbo.drc_status`, `sb_drc.dbo.drc_use`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchTransfersMember](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/ReceivableBalanceTransferMapper.kt#L48) — 바인딩: `startDate`, `endDate`, `searchType`, `searchText`, `comType`, `statusCode`, `convId`, `transferStatus`. 결과 매핑: `DRC_No` → `drcNo`, `IF_CONVERSATION_ID` → `conversationId`, `Basic_Date` → `basicDate`, `Receivable_Balance` → `receivableBalance`, `Creditor_com_regno` → `creditorComRegno`, `Creditor_com_name` → `creditorComName`, `Creditor_mem_name` → `creditorMemName`, `Creditor_com_no` → `creditorComNo`, `Debetor_com_regno` → `debetorComRegno`, `Debetor_com_name` → `debetorComName`, `Debetor_mem_name` → `debetorMemName`, `Debetor_com_no` → `debetorComNo`, `Status_Code` → `statusCode`, `Transfer_Status` → `transferStatus`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SQL = N'
LEFT JOIN SB_DRC.dbo.DRC_Status stat WITH(NOLOCK) ON main.DRC_No = stat.DRC_No
JOIN (select * from SB_DRC.dbo.DRC_Company WITH(NOLOCK) where COM_TYPE=''C'') drcComC on main.DRC_No = drcComC.DRC_No
LEFT JOIN SmartBill3.dbo.COMPANY comC WITH(NOLOCK) on drcComC.com_no = comC.com_no
LEFT JOIN SmartBill3.dbo.MEMBER memC WITH(NOLOCK) on drcComC.mem_no = memC.mem_no
LEFT JOIN SB_DRC.dbo.DRC_COMPANY_LINK comLink WITH(NOLOCK) on comLink.com_no=comC.com_no
LEFT JOIN SB_DRC.dbo.DRC_USE duC WITH(NOLOCK) on duC.drc_no = main.DRC_No and comC.com_no = duC.com_no
JOIN (select * from SB_DRC.dbo.DRC_Company WITH(NOLOCK) where COM_TYPE=''D'') drcComD on main.DRC_No = drcComD.DRC_No
LEFT JOIN SmartBill3.dbo.COMPANY comD WITH(NOLOCK) on drcComD.com_no = comD.com_no
LEFT JOIN SmartBill3.dbo.MEMBER memD WITH(NOLOCK) on drcComD.mem_no = memD.mem_no
LEFT JOIN SB_DRC.dbo.DRC_USE duD WITH(NOLOCK) on duD.drc_no = main.DRC_No and comD.com_no = duD.com_no
where comLink.Active_YN=''Y''
SET @SQL = @SQL + ' AND left(convert(varchar, main.Basic_Date, 120), 10) BETWEEN '''+@StartDate+''' AND '''+@EndDate+''''
SET @SQL = @SQL + ' AND  (comC.com_regno='''+@SearchText+''' OR comD.com_regno= ''' +    @SearchText + ''') '
SET @SearchText = '%' + @SearchText + '%'
SET @SQL = @SQL + ' AND  (comC.com_name LIKE '''+@SearchText+''' OR comD.com_name LIKE ''' + @SearchText + ''') '
SET @SQL = @SQL + ' AND  IF_Conversation_Id= '''+@ConvId+''' '
SET @SQL = @SQL + ' AND stat.Status_Code IN ( ' +  @Status_Code + ' )'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db128"></a>
## SB_DRC.dbo.upAdmSB_Lst_DRC_MoniteringLst_NM

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@StartDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@EndDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SearchType` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SearchText` | `varchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Com_Type` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Status_Code` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ConvId` | `varchar(35)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TransferStatus` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2023-07-20T11:24:47.557 |
| 읽기·참조 객체 | `sb_drc.dbo.drc_company_link`, `sb_drc.dbo.drc_company_nm`, `sb_drc.dbo.drc_main`, `sb_drc.dbo.drc_status_nm`, `sb_drc.dbo.drc_use`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchTransfersNonMember](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/ReceivableBalanceTransferMapper.kt#L74) — 바인딩: `startDate`, `endDate`, `searchType`, `searchText`, `comType`, `statusCode`, `convId`, `transferStatus`. 결과 매핑: `DRC_No` → `drcNo`, `IF_CONVERSATION_ID` → `conversationId`, `Basic_Date` → `basicDate`, `Receivable_Balance` → `receivableBalance`, `Creditor_com_regno` → `creditorComRegno`, `Creditor_com_name` → `creditorComName`, `Creditor_mem_name` → `creditorMemName`, `Creditor_com_no` → `creditorComNo`, `Debetor_com_regno` → `debetorComRegno`, `Debetor_com_name` → `debetorComName`, `Debetor_mem_name` → `debetorMemName`, `Debetor_com_no` → `debetorComNo`, `Status_Code` → `statusCode`, `Transfer_Status` → `transferStatus`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SQL = N'
LEFT JOIN SB_DRC.dbo.DRC_Status_NM stat WITH(NOLOCK) ON main.DRC_No = stat.DRC_No
JOIN (select * from SB_DRC.dbo.DRC_Company_NM WITH(NOLOCK) where COM_TYPE=''C'') drcComC on main.DRC_No = drcComC.DRC_No
LEFT JOIN SmartBill3.dbo.COMPANY comC WITH(NOLOCK) on drcComC.com_no = comC.com_no
LEFT JOIN SmartBill3.dbo.MEMBER memC WITH(NOLOCK) on drcComC.mem_no = memC.mem_no
LEFT JOIN SB_DRC.dbo.DRC_COMPANY_LINK comLink WITH(NOLOCK) on comLink.com_no=comC.com_no
LEFT JOIN SB_DRC.dbo.DRC_USE duC WITH(NOLOCK) on duC.drc_no = main.DRC_No and comC.com_no = duC.com_no
JOIN (select * from SB_DRC.dbo.DRC_Company_NM WITH(NOLOCK) where COM_TYPE=''D'') drcComD on main.DRC_No = drcComD.DRC_No
where comLink.Active_YN=''Y''
SET @SQL = @SQL + ' AND left(convert(varchar, main.Basic_Date, 120), 10) BETWEEN '''+@StartDate+''' AND '''+@EndDate+''''
SET @SQL = @SQL + ' AND  (comC.com_regno='''+@SearchText+''' OR drcComD.com_regno= ''' +    @SearchText + ''') '
SET @SearchText = '%' + @SearchText + '%'
SET @SQL = @SQL + ' AND  (comC.com_name LIKE '''+@SearchText+''' OR drcComD.com_name LIKE ''' + @SearchText + ''') '
SET @SQL = @SQL + ' AND  IF_Conversation_Id= '''+@ConvId+''' '
SET @SQL = @SQL + ' AND stat.Status_Code IN ( ' +  @Status_Code + ' )'
SET @SQL = @SQL + ' AND stat.Transfer_Status IN ( ' +  @TransferStatus + ' )'
SET @SQL = @SQL + ' ORDER BY Basic_Date DESC'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db129"></a>
## SB_DRC.dbo.upDRC_Routing_Error_Reg

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@ERROR_YN` | `varchar(5)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ERROR_REG_SIG` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PORT` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ROUTINGURL` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SW_NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SB_USE_CODE` | `varchar(5)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROM_DATETIME` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TO_DATETIME` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ERROR_MSG` | `varchar(1000)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-01-22T15:25:19.720 |
| 읽기·참조 객체 | `sb_drc.dbo.drc_company_link`, `sb_drc.dbo.drc_routing_error_reg`, `sb_drc.dbo.drc_routing_error_reg_his` |
| 쓰기 대상 | `sb_drc.dbo.drc_routing_error_reg`, `sb_drc.dbo.drc_routing_error_reg_his` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [saveHubError](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcHubErrorMapper.kt#L109) — 바인딩: `errorYn`, `errorRegSig`, `port`, `routingUrl`, `swNo`, `sbUseCode`, `fromDatetime`, `toDatetime`, `errorMsg`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SELECT GETDATE(), ROUTINGURL, @ERROR_YN, ERROR_REG_DATE, ERROR_MSG, @SW_NO, @FROM_DATETIME, @TO_DATETIME, @SB_USE_CODE, PORT FROM SB_DRC..DRC_ROUTING_ERROR_REG WHERE ROUTINGURL = @ROUTINGURL
WHERE ROUTINGURL = @ROUTINGURL
SELECT GETDATE(), ROUTINGURL, @ERROR_YN, ERROR_REG_DATE, ERROR_MSG, @SW_NO, @FROM_DATETIME, @TO_DATETIME, SB_USE_CODE, PORT FROM SB_DRC..DRC_ROUTING_ERROR_REG WHERE ROUTINGURL = @ROUTINGURL AND PORT = @PORT
WHERE ROUTINGURL = @ROUTINGURL and PORT = @PORT
WHERE ROUTINGURL = @ROUTINGURL
SELECT PORT AS PORT_TMP FROM SB_DRC..DRC_COMPANY_LINK WHERE ROUTINGURL = @ROUTINGURL AND ACTIVE_YN = 'Y'  GROUP BY PORT
WHERE ROUTINGURL = @ROUTINGURL AND PORT = @PORT
SELECT GETDATE(), ROUTINGURL, 'N', GETDATE(), ERROR_MSG, @SW_NO, @FROM_DATETIME, @TO_DATETIME, @SB_USE_CODE, PORT FROM SB_DRC..DRC_ROUTING_ERROR_REG WHERE ROUTINGURL = @ROUTINGURL
WHERE ROUTINGURL = @ROUTINGURL
WHERE ROUTINGURL = @ROUTINGURL AND PORT = @PORT
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db130"></a>
## SB_DRC.dbo.upDRC_Routing_Error_Reg_history

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@ROUTINGURL` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-01-22T15:07:29.103 |
| 읽기·참조 객체 | `office.dbo.sawon`, `sb_drc.dbo.drc_routing_error_reg_his` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findHistories](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcHubErrorMapper.kt#L101) — 바인딩: `routingUrl`. 결과 매핑: `HIS_DATETIME` → `hisDatetime`, `ERROR_YN` → `errorYn`, `FROM_DATETIME` → `fromDatetime`, `TO_DATETIME` → `toDatetime`, `SB_USE_CODE` → `sbUseCode`, `PORT` → `port`, `SNAME` → `sname`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
JOIN OFFICE..SAWON B WITH(NOLOCK) ON A.SW_NO = B.SW_NO
WHERE
ORDER BY HIS_DATETIME DESC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db131"></a>
## SB_DRC.dbo.upGw_DRC_HubError_Reg_NEW

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@HUB_ID` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-01-22T14:53:38.640 |
| 읽기·참조 객체 | `office.dbo.business`, `office.dbo.mng_hub`, `office.dbo.mng_hub_etc_detail`, `office.dbo.sawon`, `sb_drc.dbo.drc_company_link`, `sb_drc.dbo.drc_routing_error_reg`, `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchHubErrors](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcHubErrorMapper.kt#L49) — 바인딩: `hubId`. 결과 매핑: `bns_id` → `bnsId`, `bns_site` → `bnsSite`, `routing_type` → `routingType`, `routingurl` → `routingUrl`, `cnt` → `cnt`, `error_YN` → `errorYn`, `error_Msg` → `errorMsg`, `regdate` → `regdate`, `SW_NO` → `swNo`, `SNAME` → `sname`, `PORT` → `port`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
set @qry = '
JOIN SMARTBILL3..COMPANY C ON MCC.COM_NO = C.COM_NO
JOIN OFFICE..MNG_HUB_ETC_DETAIL MHD ON C.COM_REGNO = MHD.COM_REGNO
JOIN OFFICE..MNG_HUB MH ON MHD.HUB_ID = MH.HUB_ID
JOIN OFFICE..BUSINESS B ON MH.BNS_ID = B.BNS_ID
WHERE MCC.Active_YN = ''Y'' AND MHD.[SERVICE] = ''DRC'' AND ROUTINGURL <> ''http://'' AND ROUTINGURL <> ''''
GROUP BY B.BNS_ID, B.BNS_SITE, MCC.SYSTEM_ID, MCC.ROUTINGURL
LEFT OUTER JOIN SB_DRC..DRC_ROUTING_ERROR_REG B ON A.ROUTINGURL = B.ROUTINGURL
LEFT OUTER JOIN office..sawon sa ON B.sw_no=sa.SW_NO '
set @qry = @qry + ' where bns_id in ( select bns_id from office..mng_hub where hub_id = ' + cast(@hub_id as varchar(10)) + ') '
set @qry = @qry + 'order by error_YN desc, bns_site asc '
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db132"></a>
## SB_DRC.dbo.upStm_LstDRCCompanyLinkInfo

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@Com_No` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2019-03-12T13:45:06.680 |
| 읽기·참조 객체 | `sb_drc.dbo.drc_company_link` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findCompanyLinkDetail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcCompanyLinkMapper.kt#L70) — 바인딩: `comNo`. 결과 매핑: `COMPANY_LINK_OUT_IDX` → `companyLinkOutIdx`, `Com_No` → `comNo`, `Service_Type` → `serviceType`, `System_ID` → `systemId`, `Start_RoutingDate` → `startRoutingDate`, `End_RoutingDate` → `endRoutingDate`, `RoutingURL` → `routingUrl`, `Port` → `port`, `Active_YN` → `activeYn`, `SAPClientCode` → `sapClientCode`, `SAPCompanyCode` → `sapCompanyCode`, `SAPSystemId` → `sapSystemId`, `Biz_CUser` → `bizCUser`, `CDate` → `cDate`, `Biz_UUser` → `bizUUser`, `UDate` → `uDate`, `Trouble_Yn` → `troubleYn`, `Trouble_Msg` → `troubleMsg`, `Trouble_RegDate` → `troubleRegDate`, `Trouble_RegUser` → `troubleRegUser`, `Hub_Id` → `hubId`, `NM_YN` → `nmYn`, `OUT_YN` → `outYn`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE  Com_No = @Com_No
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db133"></a>
## SB_DRC.dbo.upStm_SavDRCCompanyLink

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@Com_No` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@System_ID` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Start_RoutingDate` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@End_RoutingDate` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RoutingURL` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Port` | `varchar(5)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Active_YN` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SAPClientCode` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SAPCompanyCode` | `varchar(4)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SAPSystemId` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Biz_UUser` | `varchar(12)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Hub_Id` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Trouble_Yn` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Trouble_Msg` | `varchar(1000)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@NM_YN` | `varchar(4)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@OUT_YN` | `varchar(4)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2021-06-15T17:37:18.183 |
| 읽기·참조 객체 | `office.dbo.mng_company_except`, `office.dbo.mng_hub_etc_detail`, `sb_drc.dbo.drc_company_link`, `smartbill3.dbo.company` |
| 쓰기 대상 | `office.dbo.mng_company_except`, `office.dbo.mng_hub_etc_detail`, `sb_drc.dbo.drc_company_link` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [saveCompanyLink](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcCompanyLinkMapper.kt#L80) — 바인딩: `comNo`, `systemId`, `startRoutingDate`, `endRoutingDate`, `routingUrl`, `port`, `activeYn`, `sapClientCode`, `sapCompanyCode`, `sapSystemId`, `bizUUser`, `hubId`, `troubleYn`, `troubleMsg`, `nmYn`, `outYn`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SERVICE = 'DRC'
SET @bns_product = '16'
SELECT  @REG_NO = COM_REGNO FROM SMARTBILL3..COMPANY WITH (NOLOCK)  WHERE COM_NO = @COM_NO
IF NOT EXISTS(SELECT * FROM SB_DRC.dbo.DRC_COMPANY_LINK WHERE Com_No=@Com_No)
WHERE  Com_No = @Com_No
IF NOT EXISTS(SELECT * FROM [office].[dbo].[MNG_HUB_ETC_DETAIL] WHERE [COM_REGNO] =@REG_NO AND [SERVICE] = @SERVICE  AND bns_product = @bns_product )
WHERE  [COM_REGNO] =@REG_NO AND [SERVICE] = @SERVICE AND bns_product = @bns_product
WHERE  [COM_REGNO] =@REG_NO AND [SERVICE] = @SERVICE AND bns_product = @bns_product
SELECT @COM_REGNO = COM_REGNO FROM SMARTBILL3..COMPANY WITH(NOLOCK) WHERE COM_NO = @COM_NO
IF EXISTS ( SELECT COM_REGNO FROM office..MNG_COMPANY_EXCEPT WITH(NOLOCK) WHERE COM_REGNO = @COM_REGNO AND EXCEPT_CODE='PAY_AUTO_DTI')
WHERE
IF EXISTS ( SELECT COM_REGNO FROM office..MNG_COMPANY_EXCEPT WITH(NOLOCK) WHERE COM_REGNO = @COM_REGNO AND EXCEPT_CODE='PAY_AUTO_DCT')
WHERE
IF EXISTS ( SELECT COM_REGNO FROM office..MNG_COMPANY_EXCEPT WITH(NOLOCK) WHERE COM_REGNO = @COM_REGNO AND EXCEPT_CODE='PAY_AUTO_DRC')
WHERE
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db134"></a>
## SB_DTI.dbo.ATTACH_FILE_INFO

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `ETC_PCS_NO` | `char(35)` | 불가 | 아니오 |
| `FILE_IDX` | `int` | 불가 | 아니오 |
| `PATH` | `varchar(200)` | 불가 | 아니오 |
| `SIZE` | `int` | 불가 | 아니오 |
| `STATE` | `char(1)` | 불가 | 아니오 |
| `CUSER` | `varchar(12)` | 불가 | 아니오 |
| `CDATE` | `datetime` | 불가 | 아니오 |
| `UUSER` | `varchar(12)` | 허용 | 아니오 |
| `UDATE` | `datetime` | 허용 | 아니오 |
| `ERROR_CODE` | `varchar(5)` | 허용 | 아니오 |
| `ERROR_MESSAGE` | `varchar(100)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2018-03-02T18:11:05.577 |
| 읽기·참조 객체 | `sb_dti.dbo.attach_file_info` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getAttachFileHistory](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L356) — 바인딩: `etcPcsNo`. 결과 매핑: `FILE_IDX` → `fileIdx`, `PATH` → `path`, `SIZE` → `size`, `STATE` → `state`, `CDATE` → `cdate`, `UDATE` → `udate`.
- [getAttachFileHistory](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L288) — 바인딩: `etcPcsNo`. 결과 매핑: `FILE_IDX` → `fileIdx`, `PATH` → `path`, `SIZE` → `size`, `STATE` → `state`, `CDATE` → `cdate`, `UDATE` → `udate`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db135"></a>
## SB_DTI.dbo.COMPANY_DTICONFIG

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `COM_NO` | `int` | 불가 | 아니오 |
| `BIZPLACE_CODE` | `varchar(35)` | 불가 | 아니오 |
| `RECEIVE_NONMEM` | `char(1)` | 허용 | 아니오 |
| `ISSUE_YN` | `char(1)` | 허용 | 아니오 |
| `TOTALTABLE_YN` | `char(1)` | 허용 | 아니오 |
| `RCV_YN` | `char(1)` | 허용 | 아니오 |
| `REQUEST_YN` | `char(1)` | 허용 | 아니오 |
| `ALLDTI_YN` | `char(1)` | 허용 | 아니오 |
| `BDTI_SUP_RCV_YN` | `char(1)` | 허용 | 아니오 |
| `NTS_SEND_YN` | `char(1)` | 허용 | 아니오 |
| `ISSUE_CMT_YN` | `char(1)` | 허용 | 아니오 |
| `RISSUE_CMT_YN` | `char(1)` | 허용 | 아니오 |
| `PISSUE_CMT_YN` | `char(1)` | 허용 | 아니오 |
| `DTI_SMS` | `varchar(1)` | 허용 | 아니오 |
| `DTI_MSG` | `varchar(80)` | 허용 | 아니오 |
| `RDTI_SMS` | `varchar(1)` | 허용 | 아니오 |
| `RDTI_MSG` | `varchar(80)` | 허용 | 아니오 |
| `BDTI_SMS` | `char(1)` | 허용 | 아니오 |
| `BDTI_MSG` | `varchar(80)` | 허용 | 아니오 |
| `CLIENT_SHARE_YN` | `char(1)` | 허용 | 아니오 |
| `CUser` | `varchar(12)` | 불가 | 아니오 |
| `CDate` | `datetime` | 불가 | 아니오 |
| `UUser` | `varchar(12)` | 불가 | 아니오 |
| `UDate` | `datetime` | 불가 | 아니오 |
| `NO_EMAIL_BANNER_YN` | `char(1)` | 허용 | 아니오 |
| `SERVER_CERTI_YN` | `char(1)` | 허용 | 아니오 |
| `BILL36524_YN` | `char(1)` | 불가 | 아니오 |
| `CSV_YN` | `char(1)` | 불가 | 아니오 |
| `GIRO_YN` | `char(1)` | 불가 | 아니오 |
| `DELAY_ISSUE_YN` | `char(1)` | 불가 | 아니오 |
| `TAXFREE_ISSUE_YN` | `char(1)` | 불가 | 아니오 |
| `ISSUE_NO` | `varchar(8)` | 허용 | 아니오 |
| `LINK_ENCRYPTION` | `char(1)` | 허용 | 아니오 |
| `TEMP_ISSUE_YN` | `char(1)` | 불가 | 아니오 |
| `DELAY_NTS_YN` | `char(1)` | 불가 | 아니오 |
| `MEMBER_CHK_YN` | `char(1)` | 허용 | 아니오 |
| `DTI_PREVIEWNOTI_YN` | `char(1)` | 허용 | 아니오 |
| `RDTI_RESENDMAIL_YN` | `char(1)` | 허용 | 아니오 |
| `RDTI_RESENDMAIL_CHECKCYCLE` | `char(1)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2018-03-02T19:04:09.480 |
| 읽기·참조 객체 | `sb_dti.dbo.company_dticonfig` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [updateDtiConfigField](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankCompanyMapper.kt#L229) — 바인딩: `value`, `comNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [getTaxInvoiceConfig](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L888) — 바인딩: `comNo`. 결과 매핑: `COM_NO` → `comNo`, `BIZPLACE_CODE` → `bizplaceCode`, `RECEIVE_NONMEM` → `receiveNonmem`, `NTS_SEND_YN` → `ntsSendYn`, `SERVER_CERTI_YN` → `serverCertiYn`, `BILL36524_YN` → `bill36524Yn`, `CSV_YN` → `csvYn`, `GIRO_YN` → `giroYn`, `DELAY_ISSUE_YN` → `delayIssueYn`, `TAXFREE_ISSUE_YN` → `taxfreeIssueYn`, `ISSUE_NO` → `issueNo`, `LINK_ENCRYPTION` → `linkEncryption`, `TEMP_ISSUE_YN` → `tempIssueYn`, `DELAY_NTS_YN` → `delayNtsYn`, `MEMBER_CHK_YN` → `memberChkYn`, `DTI_PREVIEWNOTI_YN` → `dtiPreviewnotiYn`, `RDTI_RESENDMAIL_YN` → `rdtiResendmailYn`, `CDate` → `cDate`, `UDate` → `uDate`.
- [updateTaxInvoiceConfigField](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L896) — 바인딩: `value`, `comNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db136"></a>
## SB_DTI.dbo.COMPANY_LINK_OUT

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `COMPANY_LINK_OUT_IDX` | `int` | 불가 | 예 |
| `Com_No` | `int` | 불가 | 아니오 |
| `ServiceType` | `varchar(3)` | 허용 | 아니오 |
| `ProcessID` | `varchar(3)` | 허용 | 아니오 |
| `SystemID` | `varchar(10)` | 허용 | 아니오 |
| `SubSystemID` | `varchar(10)` | 허용 | 아니오 |
| `StartDtiDate` | `datetime` | 불가 | 아니오 |
| `EndDtiDate` | `datetime` | 불가 | 아니오 |
| `StartRoutingDate` | `datetime` | 불가 | 아니오 |
| `EndRoutingDate` | `datetime` | 불가 | 아니오 |
| `RoutingURL` | `varchar(100)` | 허용 | 아니오 |
| `Port` | `varchar(5)` | 허용 | 아니오 |
| `Active_YN` | `varchar(1)` | 불가 | 아니오 |
| `SAPClientCode` | `varchar(3)` | 허용 | 아니오 |
| `SAPCompanyCode` | `varchar(4)` | 허용 | 아니오 |
| `SystemAlias` | `varchar(35)` | 허용 | 아니오 |
| `STATUS_RECOVERY_YN` | `varchar(1)` | 불가 | 아니오 |
| `Biz_CUser` | `varchar(12)` | 불가 | 아니오 |
| `CDate` | `datetime` | 불가 | 아니오 |
| `Biz_UUser` | `varchar(12)` | 불가 | 아니오 |
| `UDate` | `datetime` | 불가 | 아니오 |
| `Version` | `varchar(3)` | 허용 | 아니오 |
| `LinkSystemID` | `varchar(3)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2023-06-07T10:28:40.293 |
| 읽기·참조 객체 | `sb_dti.dbo.company_link_out` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectCompanies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptCodeMapper.kt#L71) — 바인딩: `schText,jdbcType=VARCHAR`, `schText,jdbcType=VARCHAR`, `schText,jdbcType=VARCHAR`, `schText,jdbcType=VARCHAR`. 결과 매핑: `com_regno` → `comRegno`, `com_name` → `comName`, `mem_realname` → `memRealname`, `mem_tel` → `memTel`, `routing_type` → `routingType`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db137"></a>
## SB_DTI.dbo.COMPANY_MNG_INFO

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `Com_No` | `int` | 불가 | 아니오 |
| `BIZPLACE_YN` | `varchar(1)` | 불가 | 아니오 |
| `BIZPLACE_START_DTIWDAY` | `varchar(10)` | 허용 | 아니오 |
| `BIZPLACE_START_DATE` | `varchar(10)` | 불가 | 아니오 |
| `VirtualID_YN` | `varchar(1)` | 불가 | 아니오 |
| `AR_PERSON_MASTER_USE_YN` | `varchar(1)` | 불가 | 아니오 |
| `AP_PERSON_MASTER_USE_YN` | `varchar(1)` | 불가 | 아니오 |
| `AR_COM_MASTER_USE_YN` | `varchar(1)` | 불가 | 아니오 |
| `AP_COM_MASTER_USE_YN` | `varchar(1)` | 불가 | 아니오 |
| `BRK_SUPLINK_YN` | `varchar(1)` | 불가 | 아니오 |
| `EMAIL_LINK_YN` | `varchar(1)` | 불가 | 아니오 |
| `CUser` | `varchar(12)` | 불가 | 아니오 |
| `CDate` | `datetime` | 불가 | 아니오 |
| `UUser` | `varchar(12)` | 불가 | 아니오 |
| `UDate` | `datetime` | 불가 | 아니오 |
| `CLOSEBUSINESS_SMS` | `varchar(1)` | 불가 | 아니오 |
| `MULTI_LINK_YN` | `char(1)` | 허용 | 아니오 |
| `PROXY_MG_YN` | `char(1)` | 허용 | 아니오 |
| `BRANCH_MG_YN` | `char(1)` | 허용 | 아니오 |
| `BULKMEMBER_MG_YN` | `char(1)` | 허용 | 아니오 |
| `FCHGSTATUS_USE_YN` | `char(1)` | 허용 | 아니오 |
| `BRK_BYRMYCOM_YN` | `varchar(1)` | 허용 | 아니오 |
| `REVERSE_SUPPLIER_CRITERIA` | `varchar(10)` | 허용 | 아니오 |
| `REVERSE_RECIPIENT_CRITERIA` | `varchar(10)` | 허용 | 아니오 |
| `REVERSE_RECIPIENT_CONTACT_CRITERIA` | `varchar(10)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-06-01T17:12:36.807 |
| 읽기·참조 객체 | `sb_dti.dbo.company_mng_info` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getUnitTaxationFromMngInfo](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L394) — 바인딩: `comNo`. 결과 매핑: `BIZPLACE_YN` → `bizplaceYn`, `BIZPLACE_START_DTIWDAY` → `taxInvoiceStartDate`, `BIZPLACE_START_DATE` → `unitTaxationStartDate`, `BRK_SUPLINK_YN` → `brkSuplinkYn`, `BULKMEMBER_MG_YN` → `bulkmemberMgYn`, `EMAIL_LINK_YN` → `emailLinkYn`, `PROXY_MG_YN` → `proxyMgYn`, `BRANCH_MG_YN` → `branchMgYn`, `VirtualID_YN` → `virtualIdYn`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db138"></a>
## SB_DTI.dbo.COMPANY_QUIT_STATUS

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `COM_REGNO` | `varchar(10)` | 불가 | 아니오 |
| `TAX_TYPE` | `varchar(2)` | 허용 | 아니오 |
| `NTS_APPLY_DATE` | `varchar(10)` | 허용 | 아니오 |
| `SEARCH_DATE` | `varchar(10)` | 허용 | 아니오 |
| `QUIT_DATE` | `varchar(10)` | 허용 | 아니오 |
| `TAX_TYPE_CHANGE_DATE` | `varchar(10)` | 허용 | 아니오 |
| `ERROR_MSG` | `varchar(200)` | 허용 | 아니오 |
| `COM_REGNO#` | `varchar(52)` | 허용 | 아니오 |
| `REG_USER` | `int` | 허용 | 아니오 |
| `REG_DATE` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-04-23T15:02:56.097 |
| 읽기·참조 객체 | `sb_dti.dbo.company_quit_status` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getComquitStatus](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L417) — 바인딩: `comRegno`. 결과 매핑: `TAX_TYPE` → `taxType`, `ERROR_MSG` → `errorMsg`.
- [findQuitStatus](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankCompanyMapper.kt#L218) — 바인딩: `comRegno`. 결과 매핑: `TAX_TYPE` → `taxType`, `NTS_APPLY_DATE` → `ntsApplyDate`, `SEARCH_DATE` → `searchDate`.
- [getQuitStatusDates](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L281) — 바인딩: `comRegno`. 결과 매핑: `TAX_TYPE` → `taxType`, `NTS_APPLY_DATE` → `ntsDataDate`, `SEARCH_DATE` → `smartbillDataDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db139"></a>
## SB_DTI.dbo.DTI_HEADER_CUB

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `DTI_WDAY` | `varchar(10)` | 불가 | 아니오 |
| `DTI_IDX` | `int` | 불가 | 아니오 |
| `DIRECTION` | `char(1)` | 허용 | 아니오 |
| `UPLOAD_IDX` | `int` | 허용 | 아니오 |
| `DTI_ISSUEDATE` | `datetime` | 허용 | 아니오 |
| `DTI_APPROVEDATE` | `datetime` | 허용 | 아니오 |
| `DTI_TYPE` | `char(1)` | 허용 | 아니오 |
| `TAXINVOICE_TYPE` | `varchar(3)` | 허용 | 아니오 |
| `TAX_DEMAND` | `varchar(2)` | 허용 | 아니오 |
| `VOLUME_NO` | `varchar(35)` | 허용 | 아니오 |
| `ISSUE_NO` | `varchar(35)` | 허용 | 아니오 |
| `SEQ_NO` | `varchar(48)` | 허용 | 아니오 |
| `REMARK` | `varchar(300)` | 허용 | 아니오 |
| `TOT_AMT` | `money` | 불가 | 아니오 |
| `SUP_AMT` | `money` | 허용 | 아니오 |
| `TAX_AMT` | `money` | 허용 | 아니오 |
| `SUP_IDX` | `int` | 허용 | 아니오 |
| `SUP_COM_NAME` | `varchar(400)` | 허용 | 아니오 |
| `SUP_COM_REGNO` | `varchar(10)` | 허용 | 아니오 |
| `SUP_ID` | `varchar(12)` | 허용 | 아니오 |
| `BYR_IDX` | `int` | 허용 | 아니오 |
| `BYR_COM_NAME` | `varchar(400)` | 허용 | 아니오 |
| `BYR_COM_REGNO` | `varchar(32)` | 허용 | 아니오 |
| `BYR_TYPE` | `char(1)` | 허용 | 아니오 |
| `BYR_ID` | `varchar(12)` | 허용 | 아니오 |
| `BRK_IDX` | `int` | 허용 | 아니오 |
| `BRK_COM_NAME` | `varchar(400)` | 허용 | 아니오 |
| `BRK_COM_REGNO` | `varchar(13)` | 허용 | 아니오 |
| `BRK_ID` | `varchar(12)` | 허용 | 아니오 |
| `BRK_DTI_YN` | `char(1)` | 허용 | 아니오 |
| `ETC_PCS_NO` | `varchar(35)` | 허용 | 아니오 |
| `DTT_LINK_TYPE` | `varchar(3)` | 허용 | 아니오 |
| `REQ_RCV_IDX` | `int` | 허용 | 아니오 |
| `DTI_STATUS` | `varchar(2)` | 불가 | 아니오 |
| `SUP_PRINT_CNT` | `int` | 허용 | 아니오 |
| `BYR_PRINT_CNT` | `int` | 허용 | 아니오 |
| `BRK_PRINT_CNT` | `int` | 허용 | 아니오 |
| `SUP_VIEW_CNT` | `int` | 허용 | 아니오 |
| `BYR_VIEW_CNT` | `int` | 허용 | 아니오 |
| `BRK_VIEW_CNT` | `int` | 허용 | 아니오 |
| `SUP_DEL_IDX` | `int` | 허용 | 아니오 |
| `BYR_DEL_IDX` | `int` | 허용 | 아니오 |
| `BRK_DEL_IDX` | `int` | 허용 | 아니오 |
| `SUP_BIZPLACE_CODE` | `varchar(35)` | 허용 | 아니오 |
| `BYR_BIZPLACE_CODE` | `varchar(35)` | 허용 | 아니오 |
| `BRK_BIZPLACE_CODE` | `varchar(35)` | 허용 | 아니오 |
| `CUSER` | `varchar(12)` | 불가 | 아니오 |
| `CDATE` | `datetime` | 불가 | 아니오 |
| `UUSER` | `varchar(12)` | 불가 | 아니오 |
| `UDATE` | `datetime` | 불가 | 아니오 |
| `UPLOAD_DTI_IDX` | `int` | 허용 | 아니오 |
| `VERSION` | `varchar(3)` | 허용 | 아니오 |
| `AMEND_CODE` | `varchar(2)` | 허용 | 아니오 |
| `REMARK2` | `varchar(300)` | 허용 | 아니오 |
| `REMARK3` | `varchar(300)` | 허용 | 아니오 |
| `EXCHANED_DOC_ID` | `varchar(24)` | 허용 | 아니오 |
| `ISSUE_ID` | `varchar(24)` | 허용 | 아니오 |
| `TYPECODE` | `char(4)` | 허용 | 아니오 |
| `NTS_SEND_STATUS` | `numeric(2,0)` | 허용 | 아니오 |
| `NTS_RESULT_CODE` | `varchar(6)` | 허용 | 아니오 |
| `NTS_SEND_DATE` | `datetime` | 허용 | 아니오 |
| `DELAY_ISSUE` | `char(1)` | 허용 | 아니오 |
| `NTS_INSTANCE_TYPE` | `char(1)` | 허용 | 아니오 |
| `ORI_ISSUE_ID` | `varchar(24)` | 허용 | 아니오 |
| `ISENCRYPTED` | `varchar(1)` | 허용 | 아니오 |
| `BYR_COM_REGNO#` | `varchar(52)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | VIEW / 2026-05-07T19:13:10.530 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getBrokeredFlag](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/taxinvoice/repository/BonabankTaxInvoiceMapper.kt#L220) — 바인딩: `dtiWday`, `dtiIdx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [getBrokeredFlag](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L459) — 바인딩: `dtiWday`, `dtiIdx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [getDtiWday](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L453) — 바인딩: `dtiIdx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findLinkedStatement](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L500) — 바인딩: `dtiIdx`, `dtiWday`. 결과 매핑: `DTT_IDX` → `dttIdx`, `DTT_WDAY` → `dttWday`.
- [getNtsResultCode](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L427) — 바인딩: `dtiIdx`, `dtiWday`. 결과 매핑: `NTS_RESULT_CODE` → `ntsResultCode`, `EXCHANED_DOC_ID` → `exchangedDocId`.
- [findKeyByReference](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L477) — 바인딩: `referenceNumber`. 결과 매핑: `DTI_IDX` → `dtiIdx`, `DTI_WDAY` → `dtiWday`.
- [getDetailHeader](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/transactionstatement/repository/TransactionStatementMapper.kt#L179) — 바인딩: `dttIdx`, `dttWday`. 결과 매핑: `DTT_IDX` → `dttIdx`, `DTT_WDAY` → `dttWday`, `DTI_IDX` → `dtiIdx`, `DIRECTION` → `direction`, `ETC_PCS_NO` → `etcPcsNo`, `DTT_NO` → `dttNo`, `BLANK_COUNT` → `blankCount`, `DTT_TYPE` → `dttType`, `TAX_DEMAND` → `taxDemand`, `VOLUME_NO` → `volumeNo`, `ISSUE_NO` → `issueNo`, `SEQ_NO` → `seqNo`, `REMARK` → `remark`, `REMARK2` → `remark2`, `INP_TYPE` → `inpType`, `TOT_AMT` → `totAmt`, `SUP_AMT` → `supAmt`, `TAX_AMT` → `taxAmt`, `SUP_IDX` → `supIdx`, `SUP_ID` → `supId`, `SUP_COM_NAME` → `supComName`, `SUP_COM_REGNO` → `supComRegno`, `SUP_BIZPLACE_CODE` → `supBizplaceCode`, `SUP_PARTY` → `supParty`, `SUP_BIZTYPE` → `supBiztype`, `SUP_BIZCLASS` → `supBizclass`, `SUP_ADDRESS` → `supAddress`, `SUP_MEM_NAME` → `supMemName`, `SUP_MEM_TEL` → `supMemTel`, `SUP_EMAIL` → `supEmail`, `BYR_ID` → `byrId`, `BYR_TYPE` → `byrType`, `BYR_COM_NAME` → `byrComName`, `BYR_COM_REGNO` → `byrComRegno`, `BYR_BIZPLACE_CODE` → `byrBizplaceCode`, `BYR_PARTY` → `byrParty`, `BYR_BIZTYPE` → `byrBiztype`, `BYR_BIZCLASS` → `byrBizclass`, `BYR_ADDRESS` → `byrAddress`, `BYR_MEM_NAME` → `byrMemName`, `BYR_MEM_TEL` → `byrMemTel`, `BYR_EMAIL` → `byrEmail`, `REQ_RCV_IDX` → `reqRcvIdx`, `ETC_NO1` → `etcNo1`, `ETC_NO2` → `etcNo2`, `ETC_NO3` → `etcNo3`, `ETC_NO4` → `etcNo4`, `DTI_STATUS` → `dtiStatus`.
- [findAccessibleLinkedStatement](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L524) — 바인딩: `dttIdx`, `dttWday`. 결과 매핑: `DTT_IDX` → `dttIdx`, `DTT_WDAY` → `dttWday`.
- [findAttachmentReference](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L362) — 바인딩: `dtiIdx`, `dtiWday`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [fetchHeaderContext](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/taxinvoice/repository/BonabankTaxInvoiceMapper.kt#L96) — 바인딩: `wday`, `dtiIdx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db140"></a>
## SB_DTI.dbo.DTI_SIGN

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `DTI_WDAY` | `varchar(10)` | 불가 | 아니오 |
| `DTI_IDX` | `int` | 불가 | 아니오 |
| `PREPAY_NO` | `int` | 허용 | 아니오 |
| `BILL_TYPE` | `varchar(2)` | 허용 | 아니오 |
| `USE_AMT` | `money` | 허용 | 아니오 |
| `EVENT_NO` | `int` | 허용 | 아니오 |
| `DTI_XML` | `varchar(max)` | 허용 | 아니오 |
| `DTI_XMLFILE` | `varchar(128)` | 허용 | 아니오 |
| `IS_DB_OR_FILE` | `varchar(1)` | 불가 | 아니오 |
| `CUSER` | `varchar(12)` | 불가 | 아니오 |
| `CDATE` | `datetime` | 불가 | 아니오 |
| `RANDOM_VALUE` | `varchar(50)` | 허용 | 아니오 |
| `PROXY_NO` | `int` | 불가 | 아니오 |
| `FREE_NO` | `int` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | VIEW / 2016-09-02T21:44:36.383 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_sign`, `sb_dti.dbo.dti_sign_cub`, `sb_dti.dbo.dti_sign_cub_2023_07`, `sb_dti.dbo.dti_sign_cub_part`, `sb_dti.dbo.dti_sign_cub_prev_buffer`, `sb_dti.dbo.dti_sign_xml`, `sb_dti.dbo.dti_sign_xml_2023_07`, `sb_dti.dbo.dti_sign_xml_part`, `sb_dti.dbo.dti_sign_xml_prev_buffer` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getDtiXml](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L573) — 바인딩: `dtiIdx`, `dtiWday`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [getDtiSignedXml](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L582) — 바인딩: `dtiIdx`, `dtiWday`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT JOIN SB_DTI..DTI_SIGN_XML B
```

하위 프로시저·함수·뷰: `master.dbo.clr_dec_lob_sel`, `master.dbo.dec_lob_sel`, `sb_dti.dbo.dti_sign_cub`, `sb_dti.dbo.dti_sign_xml`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db141"></a>
## SB_DTI.dbo.DTT_HEADER_CUB

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `DTT_WDAY` | `varchar(10)` | 불가 | 아니오 |
| `DTT_IDX` | `int` | 불가 | 아니오 |
| `DTI_IDX` | `int` | 불가 | 아니오 |
| `DIRECTION` | `char(1)` | 허용 | 아니오 |
| `UPLOAD_IDX` | `int` | 허용 | 아니오 |
| `DTT_ISSUEDATE` | `datetime` | 허용 | 아니오 |
| `DTT_APPROVEDATE` | `datetime` | 허용 | 아니오 |
| `DTT_TYPE` | `char(1)` | 허용 | 아니오 |
| `TAXINVOICE_TYPE` | `varchar(3)` | 허용 | 아니오 |
| `TAX_DEMAND` | `varchar(2)` | 허용 | 아니오 |
| `VOLUME_NO` | `varchar(35)` | 허용 | 아니오 |
| `ISSUE_NO` | `varchar(35)` | 허용 | 아니오 |
| `SEQ_NO` | `varchar(48)` | 허용 | 아니오 |
| `REMARK` | `varchar(300)` | 허용 | 아니오 |
| `TOT_AMT` | `money` | 불가 | 아니오 |
| `SUP_AMT` | `money` | 허용 | 아니오 |
| `TAX_AMT` | `money` | 허용 | 아니오 |
| `SUP_IDX` | `int` | 허용 | 아니오 |
| `SUP_COM_NAME` | `varchar(400)` | 허용 | 아니오 |
| `SUP_COM_REGNO` | `varchar(10)` | 허용 | 아니오 |
| `SUP_ID` | `varchar(12)` | 허용 | 아니오 |
| `BYR_IDX` | `int` | 허용 | 아니오 |
| `BYR_COM_NAME` | `varchar(400)` | 허용 | 아니오 |
| `BYR_COM_REGNO` | `varchar(32)` | 허용 | 아니오 |
| `BYR_TYPE` | `char(1)` | 허용 | 아니오 |
| `BYR_ID` | `varchar(12)` | 허용 | 아니오 |
| `BRK_IDX` | `int` | 허용 | 아니오 |
| `BRK_COM_NAME` | `varchar(400)` | 허용 | 아니오 |
| `BRK_COM_REGNO` | `varchar(13)` | 허용 | 아니오 |
| `BRK_ID` | `varchar(12)` | 허용 | 아니오 |
| `BRK_DTT_YN` | `char(1)` | 허용 | 아니오 |
| `ETC_PCS_NO` | `varchar(35)` | 허용 | 아니오 |
| `REQ_RCV_IDX` | `int` | 허용 | 아니오 |
| `DTT_STATUS` | `varchar(2)` | 불가 | 아니오 |
| `SUP_PRINT_CNT` | `int` | 허용 | 아니오 |
| `BYR_PRINT_CNT` | `int` | 허용 | 아니오 |
| `BRK_PRINT_CNT` | `int` | 허용 | 아니오 |
| `SUP_VIEW_CNT` | `int` | 허용 | 아니오 |
| `BYR_VIEW_CNT` | `int` | 허용 | 아니오 |
| `BRK_VIEW_CNT` | `int` | 허용 | 아니오 |
| `SUP_DEL_IDX` | `int` | 허용 | 아니오 |
| `BYR_DEL_IDX` | `int` | 허용 | 아니오 |
| `BRK_DEL_IDX` | `int` | 허용 | 아니오 |
| `SUP_BIZPLACE_CODE` | `varchar(35)` | 허용 | 아니오 |
| `BYR_BIZPLACE_CODE` | `varchar(35)` | 허용 | 아니오 |
| `BRK_BIZPLACE_CODE` | `varchar(35)` | 허용 | 아니오 |
| `CUSER` | `varchar(12)` | 불가 | 아니오 |
| `CDATE` | `datetime` | 불가 | 아니오 |
| `UUSER` | `varchar(12)` | 불가 | 아니오 |
| `UDATE` | `datetime` | 불가 | 아니오 |
| `UPLOAD_DTT_IDX` | `int` | 허용 | 아니오 |
| `VERSION` | `varchar(3)` | 허용 | 아니오 |
| `AMEND_CODE` | `varchar(2)` | 허용 | 아니오 |
| `REMARK2` | `varchar(300)` | 허용 | 아니오 |
| `REMARK3` | `varchar(300)` | 허용 | 아니오 |
| `EXCHANED_DOC_ID` | `varchar(24)` | 허용 | 아니오 |
| `ISSUE_ID` | `varchar(24)` | 허용 | 아니오 |
| `TYPECODE` | `char(4)` | 허용 | 아니오 |
| `BYR_COM_REGNO#` | `varchar(52)` | 허용 | 아니오 |
| `ISENCRYPTED` | `varchar(1)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | VIEW / 2024-11-19T19:39:04.900 |
| 읽기·참조 객체 | `sb_dti.dbo.dtt_header_cub`, `sb_dti.dbo.dtt_header_cub_2020_01`, `sb_dti.dbo.dtt_header_cub_2021_01`, `sb_dti.dbo.dtt_header_cub_2022_01`, `sb_dti.dbo.dtt_header_cub_2023_01`, `sb_dti.dbo.dtt_header_cub_bf`, `sb_dti.dbo.dtt_header_cub_part` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findLinkedStatement](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L500) — 바인딩: `dtiIdx`, `dtiWday`. 결과 매핑: `DTT_IDX` → `dttIdx`, `DTT_WDAY` → `dttWday`.
- [getIssueId](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/transactionstatement/repository/TransactionStatementMapper.kt#L191) — 바인딩: `dttIdx`, `dttWday`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findAccessibleLinkedStatement](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L524) — 바인딩: `dttIdx`, `dttWday`. 결과 매핑: `DTT_IDX` → `dttIdx`, `DTT_WDAY` → `dttWday`.
- [findAccessibleStandaloneStatement](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L545) — 바인딩: `dttIdx`, `dttWday`. 결과 매핑: `DTT_IDX` → `dttIdx`, `DTT_WDAY` → `dttWday`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db142"></a>
## SB_DTI.dbo.DTT_HEADER_DETAIL

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `DTT_WDAY` | `varchar(10)` | 불가 | 아니오 |
| `DTT_IDX` | `int` | 불가 | 아니오 |
| `DTT_NO` | `varchar(12)` | 허용 | 아니오 |
| `BLANK_COUNT` | `int` | 허용 | 아니오 |
| `INP_TYPE` | `char(1)` | 허용 | 아니오 |
| `SUP_PARTY` | `varchar(200)` | 허용 | 아니오 |
| `SUP_BIZTYPE` | `varchar(200)` | 허용 | 아니오 |
| `SUP_BIZCLASS` | `varchar(200)` | 허용 | 아니오 |
| `SUP_ADDRESS` | `varchar(600)` | 허용 | 아니오 |
| `SUP_EMAIL` | `varchar(200)` | 허용 | 아니오 |
| `SUP_DEPT` | `varchar(200)` | 허용 | 아니오 |
| `SUP_MEM_NAME` | `varchar(200)` | 허용 | 아니오 |
| `SUP_MEM_TEL` | `varchar(40)` | 허용 | 아니오 |
| `BYR_PARTY` | `varchar(200)` | 허용 | 아니오 |
| `BYR_BIZTYPE` | `varchar(200)` | 허용 | 아니오 |
| `BYR_BIZCLASS` | `varchar(200)` | 허용 | 아니오 |
| `BYR_ADDRESS` | `varchar(600)` | 허용 | 아니오 |
| `BYR_EMAIL` | `varchar(200)` | 허용 | 아니오 |
| `BYR_DEPT` | `varchar(200)` | 허용 | 아니오 |
| `BYR_MEM_NAME` | `varchar(200)` | 허용 | 아니오 |
| `BYR_MEM_TEL` | `varchar(40)` | 허용 | 아니오 |
| `BRK_PARTY` | `varchar(200)` | 허용 | 아니오 |
| `BRK_BIZTYPE` | `varchar(200)` | 허용 | 아니오 |
| `BRK_BIZCLASS` | `varchar(200)` | 허용 | 아니오 |
| `BRK_ADDRESS` | `varchar(600)` | 허용 | 아니오 |
| `BRK_EMAIL` | `varchar(200)` | 허용 | 아니오 |
| `BRK_DEPT` | `varchar(200)` | 허용 | 아니오 |
| `BRK_MEM_NAME` | `varchar(200)` | 허용 | 아니오 |
| `BRK_MEM_TEL` | `varchar(40)` | 허용 | 아니오 |
| `SYS_CD` | `varchar(35)` | 허용 | 아니오 |
| `SUP_SID` | `varchar(35)` | 허용 | 아니오 |
| `BYR_SID` | `varchar(35)` | 허용 | 아니오 |
| `REFINFO1` | `varchar(35)` | 허용 | 아니오 |
| `REFINFO2` | `varchar(35)` | 허용 | 아니오 |
| `SUP_RCV_EMAIL` | `varchar(200)` | 허용 | 아니오 |
| `BYR_RCV_EMAIL` | `varchar(200)` | 허용 | 아니오 |
| `BRK_RCV_EMAIL` | `varchar(200)` | 허용 | 아니오 |
| `SUP_SMS_SEND_YN` | `varchar(1)` | 허용 | 아니오 |
| `BYR_SMS_SEND_YN` | `varchar(1)` | 허용 | 아니오 |
| `BRK_SMS_SEND_YN` | `varchar(1)` | 허용 | 아니오 |
| `ATTACHEDFILE_FULLPATH` | `varchar(285)` | 허용 | 아니오 |
| `ATTACHEDFILE_SIZE` | `int` | 허용 | 아니오 |
| `CREATE_LINK_IDX` | `int` | 허용 | 아니오 |
| `SUP_SBID` | `varchar(35)` | 허용 | 아니오 |
| `BYR_SBID` | `varchar(35)` | 허용 | 아니오 |
| `BRK_SBID` | `varchar(35)` | 허용 | 아니오 |
| `SUP_BIZPLACE_NAME` | `varchar(400)` | 허용 | 아니오 |
| `BYR_BIZPLACE_NAME` | `varchar(400)` | 허용 | 아니오 |
| `BRK_BIZPLACE_NAME` | `varchar(400)` | 허용 | 아니오 |
| `ETC_NO1` | `varchar(50)` | 허용 | 아니오 |
| `ETC_NO2` | `varchar(50)` | 허용 | 아니오 |
| `ETC_NO3` | `varchar(50)` | 허용 | 아니오 |
| `ETC_NO4` | `varchar(50)` | 허용 | 아니오 |
| `CUSER` | `varchar(12)` | 불가 | 아니오 |
| `CDATE` | `datetime` | 불가 | 아니오 |
| `UUSER` | `varchar(12)` | 불가 | 아니오 |
| `UDATE` | `datetime` | 불가 | 아니오 |
| `BYR_DEPT2` | `varchar(200)` | 허용 | 아니오 |
| `BYR_MEM_NAME2` | `varchar(200)` | 허용 | 아니오 |
| `BYR_MEM_TEL2` | `varchar(20)` | 허용 | 아니오 |
| `BYR_EMAIL2` | `varchar(200)` | 허용 | 아니오 |
| `IMPORTDOC_ID` | `varchar(15)` | 허용 | 아니오 |
| `IMPORTDOC_STARTDATE` | `varchar(8)` | 허용 | 아니오 |
| `IMPORTDOC_ENDDATE` | `varchar(8)` | 허용 | 아니오 |
| `IMPORTDOC_ITEMQTY` | `int` | 허용 | 아니오 |
| `FAX_SEND_YN` | `varchar(1)` | 허용 | 아니오 |
| `BYR_FAX_NO` | `varchar(20)` | 허용 | 아니오 |
| `SUP_ATT01` | `varchar(200)` | 허용 | 아니오 |
| `SUP_ATT02` | `varchar(200)` | 허용 | 아니오 |
| `SUP_ATT03` | `varchar(200)` | 허용 | 아니오 |
| `SUP_ATT04` | `varchar(200)` | 허용 | 아니오 |
| `SUP_ATT05` | `varchar(200)` | 허용 | 아니오 |
| `SUP_ATT06` | `varchar(200)` | 허용 | 아니오 |
| `SUP_ATT07` | `varchar(200)` | 허용 | 아니오 |
| `SUP_ATT08` | `varchar(200)` | 허용 | 아니오 |
| `SUP_ATT09` | `varchar(200)` | 허용 | 아니오 |
| `SUP_ATT10` | `varchar(200)` | 허용 | 아니오 |
| `SUP_ATT11` | `varchar(200)` | 허용 | 아니오 |
| `BYR_ATT01` | `varchar(200)` | 허용 | 아니오 |
| `BYR_ATT02` | `varchar(200)` | 허용 | 아니오 |
| `BYR_ATT03` | `varchar(200)` | 허용 | 아니오 |
| `BYR_ATT04` | `varchar(200)` | 허용 | 아니오 |
| `BYR_ATT05` | `varchar(200)` | 허용 | 아니오 |
| `BYR_ATT06` | `varchar(200)` | 허용 | 아니오 |
| `BYR_ATT07` | `varchar(200)` | 허용 | 아니오 |
| `BYR_ATT08` | `varchar(200)` | 허용 | 아니오 |
| `BYR_ATT09` | `varchar(200)` | 허용 | 아니오 |
| `BYR_ATT10` | `varchar(200)` | 허용 | 아니오 |
| `BYR_ATT11` | `varchar(200)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | VIEW / 2024-11-19T19:38:59.490 |
| 읽기·참조 객체 | `sb_dti.dbo.dtt_header_detail`, `sb_dti.dbo.dtt_header_detail_2020_01`, `sb_dti.dbo.dtt_header_detail_2021_01`, `sb_dti.dbo.dtt_header_detail_2022_01`, `sb_dti.dbo.dtt_header_detail_2023_01`, `sb_dti.dbo.dtt_header_detail_bf`, `sb_dti.dbo.dtt_header_detail_part` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getStandaloneStatementManagers](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L169) — 바인딩: `row.dtiWday`, `row.dtiIdx`. 결과 매핑: `DTT_IDX` → `dttIdx`, `DTT_WDAY` → `dttWday`, `SUP_MEM_NAME` → `supplierManager`, `BYR_MEM_NAME` → `buyerManager`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db143"></a>
## SB_DTI.dbo.NTS_TRANSMIT_METHOD

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `COM_NO` | `int` | 불가 | 아니오 |
| `TRANSMIT_METHOD` | `char(1)` | 불가 | 아니오 |
| `TRANSMIT_DAY` | `int` | 불가 | 아니오 |
| `ISSUE_STATUS_YN` | `char(1)` | 불가 | 아니오 |
| `AUTO_TRANSMIT_YN` | `char(1)` | 불가 | 아니오 |
| `MEM_NO` | `int` | 불가 | 아니오 |
| `CDATE` | `datetime` | 허용 | 아니오 |
| `UDATE` | `datetime` | 허용 | 아니오 |
| `REMARK` | `varchar(300)` | 허용 | 아니오 |
| `TRANSMIT_METHOD_NEW` | `char(1)` | 허용 | 아니오 |
| `ADMIN_YN` | `char(1)` | 불가 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2018-03-02T21:10:46.567 |
| 읽기·참조 객체 | `sb_dti.dbo.nts_transmit_method` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getNtsTransmitMethod](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L539) — 바인딩: `comNo`. 결과 매핑: `TRANSMIT_METHOD_NEW` → `transmitMethodNew`, `TRANSMIT_METHOD` → `transmitMethod`, `AUTO_TRANSMIT_YN` → `autoTransmitYn`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db144"></a>
## SB_DTI.dbo.SERVICE_ADMIN

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `com_no` | `int` | 불가 | 아니오 |
| `mem_no` | `int` | 불가 | 아니오 |
| `CUSER` | `varchar(12)` | 허용 | 아니오 |
| `CDATE` | `datetime` | 불가 | 아니오 |
| `UUSER` | `varchar(12)` | 허용 | 아니오 |
| `UDATE` | `datetime` | 불가 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2018-03-02T20:05:57.430 |
| 읽기·참조 객체 | `sb_dti.dbo.service_admin` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findAdministratorSensitiveValue](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L165) — 바인딩: `comNo`, `comNo`, `comNo`, `comNo`, `comNo`, `memNo`. 결과 매핑: `DUPLICATE_ROLE_COUNT` → `duplicateRoleCount`, `MEM_NO` → `memNo`, `SENSITIVE_VALUE` → `value`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db145"></a>
## SB_DTI.dbo.upCHK_ClosingStampTemp

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@SUP_MEM_NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BYR_MEM_NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BRK_MEM_NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_WDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BRK_DTI_YN` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISSUCCESS` | `bit` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:45:06.523 |
| 읽기·참조 객체 | `sb_dti.dbo.bizplace_member`, `sb_dti.dbo.dti_closing`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `END`; `END`; `END`; `END`; `END` |

### Mapper 입출력 매핑

- [isUnapprovedStampVisible](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoicePreviewMapper.kt#L18) — 바인딩: `supplierMemberNo`, `buyerMemberNo`, `brokerMemberNo`, `writeDate`, `brokered`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SUP_BIZ_PLACE_CODE = ''
SET @BYR_BIZ_PLACE_CODE = ''
SET @BRK_BIZ_PLACE_CODE = ''
SET @ISSUCCESS = 1
WHERE MEM_NO = @SUP_MEM_NO
WHERE MEM_NO = @BYR_MEM_NO
WHERE MEM_NO = @BRK_MEM_NO
WHERE COM_NO = @SUP_COM_NO AND MEM_NO = @SUP_MEM_NO AND DEL_YN = 'N'
WHERE COM_NO = @BYR_COM_NO AND MEM_NO = @BYR_MEM_NO AND DEL_YN = 'N'
WHERE COM_NO = @BRK_COM_NO AND MEM_NO = @BRK_MEM_NO AND DEL_YN = 'N'
IF EXISTS (SELECT COM_NO FROM DTI_CLOSING WHERE COM_NO = @SUP_COM_NO AND BIZPLACE_CODE = @SUP_BIZ_PLACE_CODE AND PARTY_TYPE = 'BRK'
SET @ISSUCCESS = 0
ELSE IF EXISTS (SELECT COM_NO FROM DTI_CLOSING WHERE COM_NO = @BYR_COM_NO AND BIZPLACE_CODE = @BYR_BIZ_PLACE_CODE AND PARTY_TYPE = 'BYR'
SET @ISSUCCESS = 0
ELSE IF EXISTS (SELECT COM_NO FROM DTI_CLOSING WHERE COM_NO = @BRK_COM_NO AND BIZPLACE_CODE = @BRK_BIZ_PLACE_CODE AND PARTY_TYPE = 'BRK'
SET @ISSUCCESS = 0
WHERE MEM_NO = @SUP_MEM_NO
WHERE MEM_NO = @BYR_MEM_NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db146"></a>
## SB_DTI.dbo.UPMB_GETSVCADMININFO

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:44:25.677 |
| 읽기·참조 객체 | `sb_dti.dbo.service_admin`, `smartbill3.dbo.company`, `smartbill3.dbo.dept_manager`, `smartbill3.dbo.member`, `smartbill3.dbo.tax_admin`, `smartbill3.dbo.tax_main` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findServiceAdmin](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcRightMapper.kt#L49) — 바인딩: `comNo`. 결과 매핑: `DRC_ADM_MEM_NO` → `drcAdmMemNo`, `DRC_ADM_MEM_NAME` → `drcAdmMemName`, `DRC_ADM_MEM_ID` → `drcAdmMemId`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE COM_NO = @COM_NO
INNER JOIN DBO.SERVICE_ADMIN AS B ON A.MEM_NO = B.MEM_NO
WHERE B.COM_NO = @COM_NO
INNER JOIN SMARTBILL3.DBO.DEPT_MANAGER AS B  ON A.MEM_NO = B.MEM_NO
WHERE B.COM_NO = @COM_NO
INNER JOIN SMARTBILL3.DBO.TAX_MAIN AS B  ON A.MEM_NO = B.MEM_NO AND B.COM_NO = @COM_NO
INNER JOIN SMARTBILL3.DBO.TAX_ADMIN AS C ON B.MEM_NO = C.MEM_NO AND B.CAFE_ID = C.CAFE_ID
WHERE A.MEM_DEL_YN = 'N'
INNER JOIN SMARTBILL3.DBO.MEMBER AS B ON A.COM_NO = B.COM_NO
WHERE A.COM_NO = @COM_NO
IF EXISTS (SELECT A.MEM_NO FROM SMARTBILL3.DBO.MEMBER AS A INNER JOIN SMARTBILL3.DBO.DEPT_MANAGER AS B  ON A.MEM_NO = B.MEM_NO WHERE B.COM_NO = @COM_NO AND  A.MEM_DEL_YN = 'N' AND  A.MEM_TYPE <> 'P' AND  B.SERVICE_TYPE = 'DRC')
INNER JOIN SMARTBILL3.DBO.DEPT_MANAGER AS B  ON A.MEM_NO = B.MEM_NO
WHERE B.COM_NO = @COM_NO
SET @DRC_ADM_MEM_NO = @COM_ADM_MEM_NO
SET @DRC_ADM_MEM_NAME = @COM_ADM_MEM_NAME
SET @DRC_ADM_MEM_ID = @COM_ADM_MEM_ID
SET @DRC_ADM_MEM_HP = @COM_ADM_MEM_HP
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db147"></a>
## SB_DTI.dbo.upMg_Save_AutoNtsTransmitInfo

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@MEM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TRANSMIT_METHOD` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TRANSMIT_DAY` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@AUTO_TRANSMIT_YN` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISSUE_STATUS_YN` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ERROR_CODE` | `int` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2017-05-17T11:30:57.077 |
| 읽기·참조 객체 | `sb_dti.dbo.company_link_in`, `sb_dti.dbo.company_link_out`, `sb_dti.dbo.neobill_company_link_in`, `sb_dti.dbo.neobill_company_link_out`, `sb_dti.dbo.nts_transmit_method`, `sb_dti.dbo.nts_transmit_method_his`, `sb_dti.dbo.service_admin` |
| 쓰기 대상 | `sb_dti.dbo.nts_transmit_method`, `sb_dti.dbo.nts_transmit_method_his` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `END`; `END`; `END`; `END` |

### Mapper 입출력 매핑

- [saveAutoNtsTransmitInfo](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L551) — 바인딩: `memNo`, `transmitMethod`, `transmitDay`, `autoTransmitYn`, `issueStatusYn`, `errorCode, mode=OUT, jdbcType=INTEGER`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @ERROR_CODE = 30000
SET @COM_NO = 0
WHERE MEM_NO = @MEM_NO
SET @ERROR_CODE = 10005
SET @ERROR_CODE = 20000
WHERE COM_NO = @COM_NO AND ACTIVE_YN = 'Y' AND PROCESSID IN ('FAR','RAR')
WHERE COM_NO = @COM_NO AND ACTIVE_YN = 'Y' AND PROCESSID IN ('FAR','RAR')
WHERE COM_NO = @COM_NO AND ACTIVE_YN = 'Y' AND PROCESSID IN ('FAR','RAR')
WHERE COM_NO = @COM_NO AND ACTIVE_YN = 'Y' AND PROCESSID IN ('FAR','RAR')
SET @ERROR_CODE = 40000
IF EXISTS(SELECT COM_NO FROM SB_DTI..NTS_TRANSMIT_METHOD WHERE COM_NO = @COM_NO)
WHERE COM_NO = @COM_NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db148"></a>
## SB_DTI.dbo.upSBAdm_QryDTIAttachFile_Info

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@ETC_PCS_NO` | `varchar(35)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-01-13T14:50:36.440 |
| 읽기·참조 객체 | `sb_dti.dbo.attach_file_info` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findAttachFiles](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/taxinvoice/repository/BonabankTaxInvoiceMapper.kt#L175) — 바인딩: `etcPcsNo`. 결과 매핑: `FILE_IDX` → `fileIdx`, `PATH` → `path`, `SIZE` → `size`, `STATE` → `state`, `CDATE` → `cDate`, `UDATE` → `uDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE ETC_PCS_NO = @ETC_PCS_NO
ORDER BY FILE_IDX
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db149"></a>
## SB_DTI.dbo.upSelect_DTI_HEADER

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DTI_IDX` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_WDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2024-07-10T15:50:41.213 |
| 읽기·참조 객체 | `sb_customize.dbo.sec_code`, `sb_dti.dbo.company_quit_status`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti.dbo.dti_header_detail`, `sb_dti.dbo.dti_header_detail_2023_07`, `sb_dti.dbo.dti_header_detail_part`, `sb_dti.dbo.dti_header_detail_prev_buffer`, `sb_dti.dbo.dti_status_his`, `sb_dti.dbo.dti_status_his_2023_07`, `sb_dti.dbo.dti_status_his_part`, `sb_dti.dbo.dti_status_his_prev_buffer`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getDetailHeader](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L269) — 바인딩: `dtiIdx`, `dtiWday`. 결과 매핑: `DTI_IDX` → `dtiIdx`, `DTI_WDAY` → `dtiWday`, `DTI_ISSUEDATE` → `dtiIssuedate`, `DTI_APPROVEDATE` → `dtiApprovedate`, `DIRECTION` → `direction`, `DTI_TYPE` → `dtiType`, `TAX_DEMAND` → `taxDemand`, `DTI_NO` → `dtiNo`, `ISSUE_ID` → `issueId`, `ORI_ISSUE_ID` → `oriIssueId`, `ETC_PCS_NO` → `etcPcsNo`, `DTI_STATUS` → `dtiStatus`, `AMEND_CODE` → `amendCode`, `TAXINVOICE_TYPE` → `taxinvoiceType`, `BLANK_COUNT` → `blankCount`, `VOLUME_NO` → `volumeNo`, `ISSUE_NO` → `issueNo`, `SEQ_NO` → `seqNo`, `INP_TYPE` → `inpType`, `TOT_AMT` → `totAmt`, `SUP_AMT` → `supAmt`, `TAX_AMT` → `taxAmt`, `REMARK` → `remark`, `REMARK2` → `remark2`, `REMARK3` → `remark3`, `SUP_IDX` → `supIdx`, `SUP_COM_REGNO` → `supComRegno`, `SUP_COM_NAME` → `supComName`, `SUP_EMAIL` → `supEmail`, `SUP_MEM_NAME` → `supMemName`, `SUP_MEM_TEL` → `supMemTel`, `SUP_PARTY` → `supParty`, `SUP_BIZTYPE` → `supBiztype`, `SUP_BIZCLASS` → `supBizclass`, `SUP_ADDRESS` → `supAddress`, `SUP_ID` → `supId`, `SUP_DEPT` → `supDept`, `SUP_BIZPLACE_CODE` → `supBizplaceCode`, `SUP_BIZPLACE_NAME` → `supBizplaceName`, `SUP_RCV_EMAIL` → `supRcvEmail`, `SUP_SMS_SEND_YN` → `supSmsSendYn`, `BYR_IDX` → `byrIdx`, `BYR_COM_REGNO` → `byrComRegno`, `BYR_COM_NAME` → `byrComName`, `BYR_EMAIL` → `byrEmail`, `BYR_MEM_NAME` → `byrMemName`, `BYR_MEM_NAME2` → `byrMemName2`, `BYR_EMAIL2` → `byrEmail2`, `BYR_MEM_TEL` → `byrMemTel`, `BYR_PARTY` → `byrParty`, `BYR_BIZTYPE` → `byrBiztype`, `BYR_BIZCLASS` → `byrBizclass`, `BYR_ADDRESS` → `byrAddress`, `BYR_TYPE` → `byrType`, `BYR_ID` → `byrId`, `BYR_DEPT` → `byrDept`, `BYR_BIZPLACE_CODE` → `byrBizplaceCode`, `BYR_BIZPLACE_NAME` → `byrBizplaceName`, `BYR_RCV_EMAIL` → `byrRcvEmail`, `BYR_SMS_SEND_YN` → `byrSmsSendYn`, `BRK_IDX` → `brkIdx`, `BRK_COM_REGNO` → `brkComRegno`, `BRK_COM_NAME` → `brkComName`, `BRK_EMAIL` → `brkEmail`, `BRK_MEM_NAME` → `brkMemName`, `BRK_MEM_TEL` → `brkMemTel`, `BRK_PARTY` → `brkParty`, `BRK_BIZTYPE` → `brkBiztype`, `BRK_BIZCLASS` → `brkBizclass`, `BRK_ADDRESS` → `brkAddress`, `BRK_BIZPLACE_CODE` → `brkBizplaceCode`, `BRK_DTI_YN` → `brkDtiYn`, `NTS_SEND_STATUS` → `ntsSendStatus`, `NTS_SEND_DATE` → `ntsSendDate`, `ISSUE_PATH` → `issuePath`, `DTT_LINK_TYPE` → `dttLinkType`, `SUP_COMQUIT_STATUS` → `supComquitStatus`, `SUP_COMQUIT_ERRORMSG` → `supComquitErrMsg`, `BYR_COMQUIT_STATUS` → `byrComquitStatus`, `BYR_COMQUIT_ERRORMSG` → `byrComquitErrMsg`, `REASON` → `reason`, `FAX_SEND_YN` → `faxSendYn`, `REQ_RCV_IDX` → `reqRcvIdx`, `SEC_YN` → `secYn`, `BYR_ATT01` → `byrAtt01`, `COM_SEAL` → `comSeal`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SUP_COMQUIT_STATUS=''
SET @SUP_COMQUIT_ERRORMSG=''
SET @BYR_COMQUIT_STATUS=''
SET @BYR_COMQUIT_ERRORMSG=''
SET @BRK_COMQUIT_STATUS=''
SET @BRK_COMQUIT_ERRORMSG=''
WHERE
WHERE
WHERE
SET @SEC_YN = 'Y'
SET @BYR_ATT01=''
SET @SEC_YN = 'N'
SET @REASON = ''
DTI_STATUS_HIS WITH (NOLOCK)   WHERE
ORDER  BY
SET @JOINSQL01 = '
JOIN smartbill3..MEMBER M1 ON DM.SUP_IDX = M1.MEM_NO
JOIN smartbill3..COMPANY C1 ON C1.COM_NO = M1.COM_NO '
```

하위 프로시저·함수·뷰: `master.dbo.clr_dec_char_sel_tc`, `master.dbo.dec_char_sel_tc`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_detail`, `sb_dti.dbo.dti_status_his`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db150"></a>
## SB_DTI.dbo.upSelect_DTI_ITEM

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DTI_IDX` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_WDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-06-26T16:25:15.657 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_item`, `sb_dti.dbo.dti_item_2023_07`, `sb_dti.dbo.dti_item_part`, `sb_dti.dbo.dti_item_prev_buffer` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getDetailItems](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L288) — 바인딩: `dtiIdx`, `dtiWday`. 결과 매핑: `ITEM_IDX` → `itemIdx`, `ITEM_MD` → `itemMd`, `ITEM_NAME` → `itemName`, `ITEM_SIZE` → `itemSize`, `ITEM_QNT` → `itemQnt`, `UNIT_PRICE` → `unitPrice`, `SUP_AMT` → `supAmt`, `TAX_AMT` → `taxAmt`, `ITEM_REMARK` → `itemRemark`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_item`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db151"></a>
## SB_DTI.dbo.upSelect_DTI_PAYMETHOD

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DTI_IDX` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_WDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:45:06.600 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_paymethod`, `sb_dti.dbo.dti_paymethod_2023_07`, `sb_dti.dbo.dti_paymethod_part`, `sb_dti.dbo.dti_paymethod_prev_buffer` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getDetailPayMethods](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L302) — 바인딩: `dtiIdx`, `dtiWday`. 결과 매핑: `METHOD` → `method`, `KORCURRENCY` → `korCurrency`, `FORCURRENCY` → `forCurrency`, `CURRENCYCODE` → `currencyCode`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE DTI_WDAY=@DTI_WDAY AND DTI_IDX = @DTI_IDX
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_paymethod`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db152"></a>
## SB_DTI.dbo.upSelect_DTI_STATUS_HIS

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DIV` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_WDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_IDX` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2023-10-11T10:26:48.503 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti.dbo.dti_status_his`, `sb_dti.dbo.dti_status_his_2023_07`, `sb_dti.dbo.dti_status_his_part`, `sb_dti.dbo.dti_status_his_prev_buffer`, `sb_dti_log.dbo.dti_ti_his`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getDocumentHistory](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L443) — 바인딩: `div`, `dtiWday`, `dtiIdx`. 결과 매핑: `DTI_STATUS` → `dtiStatus`, `REASON` → `reason`, `COM_NAME` → `comName`, `MEM_NAME` → `memName`, `CUSER` → `cuser`, `CDATE` → `cdate`.
- [getDocumentHistory](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L322) — 바인딩: `div`, `dtiWday`, `dtiIdx`. 결과 매핑: `DTI_STATUS` → `dtiStatus`, `REASON` → `reason`, `COM_NAME` → `comName`, `MEM_NAME` → `memName`, `CUSER` → `cuser`, `CDATE` → `cdate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE
JOIN SB_DTI..DTI_HEADER_CUB DH WITH(NOLOCK)
JOIN SMARTBILL3..MEMBER MB WITH(NOLOCK)
WHERE
ORDER  BY
ORDER  BY
WHERE
ORDER  BY
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_status_his`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db153"></a>
## SB_DTI.dbo.upSelect_DTIChangeReceiverHis

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DTI_WDAY` | `char(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:45:32.540 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti_log.dbo.dti_change_receiver`, `sb_dti_log.dbo.dti_change_receiver_his`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getReceiverChangeHistory](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L378) — 바인딩: `dtiWday`, `dtiIdx`. 결과 매핑: `CDATE` → `cdate`, `ORI_RCV_EMAIL` → `oriRcvEmail`, `RCV_EMAIL` → `rcvEmail`, `CHG_TYPE` → `chgType`, `CHG` → `chg`, `BYR_TYPE` → `byrType`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE DTI_WDAY = @DTI_WDAY AND DTI_IDX = @DTI_IDX
IF EXISTS (SELECT 1 FROM SB_DTI_LOG..DTI_CHANGE_RECEIVER WITH(NOLOCK) WHERE ETC_PCS_NO = @ETC_PCS_NO)
CASE WHEN H.CHG_TYPE = 'ISSUE' THEN (SELECT RCV_EMAIL FROM SB_DTI_LOG..DTI_CHANGE_RECEIVER_HIS WITH(NOLOCK) WHERE DTI_WDAY = L.DTI_WDAY AND DTI_IDX = L.DTI_IDX AND CHG_TYPE IN ('RDTIREQUEST','RDETAILREQUEST'))
JOIN SB_DTI_LOG..DTI_CHANGE_RECEIVER_HIS H WITH(NOLOCK) ON L.ETC_PCS_NO = H.ETC_PCS_NO
JOIN SB_DTI..DTI_HEADER_CUB HD WITH(NOLOCK) ON L.ETC_PCS_NO = HD.ETC_PCS_NO
LEFT JOIN SMARTBILL3..MEMBER M WITH(NOLOCK) ON H.RCV_MEM_NO = M.MEM_NO
WHERE HD.BYR_TYPE = 'M'
ORDER BY L.DTI_WDAY, L.DTI_IDX, H.CDATE
CASE WHEN H.CHG_TYPE = 'ISSUE' THEN (SELECT RCV_EMAIL FROM SB_DTI_LOG..DTI_CHANGE_RECEIVER_HIS WITH(NOLOCK) WHERE DTI_WDAY = L.DTI_WDAY AND DTI_IDX = L.DTI_IDX AND CHG_TYPE IN ('RDTIREQUEST','RDETAILREQUEST'))
JOIN SB_DTI_LOG..DTI_CHANGE_RECEIVER_HIS H WITH(NOLOCK) ON L.DTI_WDAY = H.DTI_WDAY AND L.DTI_IDX = H.DTI_IDX
JOIN SB_DTI..DTI_HEADER_CUB HD WITH(NOLOCK) ON L.DTI_WDAY = HD.DTI_WDAY AND L.DTI_IDX = HD.DTI_IDX
LEFT JOIN SMARTBILL3..MEMBER M WITH(NOLOCK) ON H.RCV_MEM_NO = M.MEM_NO
WHERE HD.BYR_TYPE = 'M'
ORDER BY L.DTI_WDAY, L.DTI_IDX, H.CDATE
```

하위 프로시저·함수·뷰: `sb_dti.dbo.dti_header_cub`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db154"></a>
## SB_DTI.dbo.upSELECT_MailStatus

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DTI_WDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:45:22.260 |
| 읽기·참조 객체 | `sb_dti_log.dbo.dti_email_his`, `sb_dti_log.dbo.dti_email_rcv_his`, `sb_dti_log.dbo.dti_email_rcv_his_old`, `sb_dti_log.dbo.dti_email_rcv_his_part`, `sb_dti_log.dbo.dti_email_send_his`, `sb_dti_log.dbo.dti_email_send_his_old`, `sb_dti_log.dbo.dti_email_send_his_part` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getMailStatus](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L391) — 바인딩: `dtiWday`, `dtiIdx`. 결과 매핑: `SUCCESS_YN` → `successYn`, `OPEN_YN` → `openYn`, `OPEN_DATE` → `openDate`.
- [getMailStatus](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L382) — 바인딩: `dtiWday`, `dtiIdx`. 결과 매핑: `SUCCESS_YN` → `successYn`, `OPEN_YN` → `openYn`, `OPEN_DATE` → `openDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
FROM (SELECT A1.SB_IDX FROM SB_DTI_LOG..DTI_EMAIL_HIS A1 WITH (NOLOCK) WHERE A1.DTI_WDAY = @DTI_WDAY AND A1.DTI_IDX = @DTI_IDX AND A1.ACTION IN ('ARISSUE' , 'RARISSUE')) A
LEFT JOIN SB_DTI_LOG..DTI_EMAIL_SEND_HIS B WITH (NOLOCK) ON A.SB_IDX = B.SB_IDX
LEFT JOIN SB_DTI_LOG..DTI_EMAIL_RCV_HIS C WITH (NOLOCK) ON A.SB_IDX = C.SB_IDX
```

하위 프로시저·함수·뷰: `sb_dti_log.dbo.dti_email_rcv_his`, `sb_dti_log.dbo.dti_email_send_his`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db155"></a>
## SB_DTI.dbo.upSelect_MultiLinkInfo

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@CONVERSATION_ID` | `varchar(35)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2017-09-06T15:16:43.427 |
| 읽기·참조 객체 | `sb_dti_log.dbo.multi_link_his` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getMultiLinkInfo](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L407) — 바인딩: `conversationId`. 결과 매핑: `IDX` → `idx`, `SIGNAL` → `signal`, `SEND_STATUS` → `sendStatus`, `SEND_DATE` → `sendDate`, `ACTION_PATH` → `actionPath`, `CDATE` → `cdate`.
- [getMultiLinkInfo](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L398) — 바인딩: `conversationId`. 결과 매핑: `IDX` → `idx`, `SIGNAL` → `signal`, `SEND_STATUS` → `sendStatus`, `SEND_DATE` → `sendDate`, `ACTION_PATH` → `actionPath`, `CDATE` → `cdate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE CONVERSATION_ID = @CONVERSATION_ID
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db156"></a>
## SB_DTI.dbo.V_DTT_HEADER

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `DTT_WDAY` | `varchar(10)` | 불가 | 아니오 |
| `DTT_IDX` | `int` | 불가 | 아니오 |
| `DTI_IDX` | `int` | 불가 | 아니오 |
| `DIRECTION` | `char(1)` | 허용 | 아니오 |
| `UPLOAD_IDX` | `int` | 허용 | 아니오 |
| `DTT_NO` | `varchar(12)` | 허용 | 아니오 |
| `DTT_ISSUEDATE` | `datetime` | 허용 | 아니오 |
| `DTT_APPROVEDATE` | `datetime` | 허용 | 아니오 |
| `BLANK_COUNT` | `int` | 허용 | 아니오 |
| `DTT_TYPE` | `char(1)` | 허용 | 아니오 |
| `TAXINVOICE_TYPE` | `varchar(3)` | 허용 | 아니오 |
| `TAX_DEMAND` | `varchar(2)` | 허용 | 아니오 |
| `VOLUME_NO` | `varchar(35)` | 허용 | 아니오 |
| `ISSUE_NO` | `varchar(35)` | 허용 | 아니오 |
| `SEQ_NO` | `varchar(35)` | 허용 | 아니오 |
| `REMARK` | `varchar(150)` | 허용 | 아니오 |
| `REMARK2` | `varchar(150)` | 허용 | 아니오 |
| `REMARK3` | `varchar(150)` | 허용 | 아니오 |
| `INP_TYPE` | `char(1)` | 허용 | 아니오 |
| `TOT_AMT` | `money` | 불가 | 아니오 |
| `SUP_AMT` | `money` | 허용 | 아니오 |
| `TAX_AMT` | `money` | 허용 | 아니오 |
| `SUP_IDX` | `int` | 허용 | 아니오 |
| `SUP_COM_NAME` | `varchar(70)` | 허용 | 아니오 |
| `SUP_COM_REGNO` | `varchar(10)` | 허용 | 아니오 |
| `SUP_PARTY` | `varchar(35)` | 허용 | 아니오 |
| `SUP_BIZTYPE` | `varchar(40)` | 허용 | 아니오 |
| `SUP_BIZCLASS` | `varchar(60)` | 허용 | 아니오 |
| `SUP_ADDRESS` | `varchar(200)` | 허용 | 아니오 |
| `SUP_EMAIL` | `varchar(70)` | 허용 | 아니오 |
| `SUP_DEPT` | `varchar(40)` | 허용 | 아니오 |
| `SUP_MEM_NAME` | `varchar(35)` | 허용 | 아니오 |
| `SUP_MEM_TEL` | `varchar(40)` | 허용 | 아니오 |
| `SUP_ID` | `varchar(12)` | 허용 | 아니오 |
| `BYR_IDX` | `int` | 허용 | 아니오 |
| `BYR_COM_NAME` | `varchar(70)` | 허용 | 아니오 |
| `BYR_COM_REGNO` | `varchar(32)` | 허용 | 아니오 |
| `BYR_COM_REGNO#` | `varchar(52)` | 허용 | 아니오 |
| `BYR_PARTY` | `varchar(35)` | 허용 | 아니오 |
| `BYR_BIZTYPE` | `varchar(40)` | 허용 | 아니오 |
| `BYR_BIZCLASS` | `varchar(60)` | 허용 | 아니오 |
| `BYR_ADDRESS` | `varchar(200)` | 허용 | 아니오 |
| `BYR_TYPE` | `char(1)` | 허용 | 아니오 |
| `BYR_EMAIL` | `varchar(70)` | 허용 | 아니오 |
| `BYR_DEPT` | `varchar(40)` | 허용 | 아니오 |
| `BYR_MEM_NAME` | `varchar(35)` | 허용 | 아니오 |
| `BYR_MEM_TEL` | `varchar(40)` | 허용 | 아니오 |
| `BYR_ID` | `varchar(12)` | 허용 | 아니오 |
| `BYR_EMAIL2` | `varchar(40)` | 허용 | 아니오 |
| `BYR_MEM_NAME2` | `varchar(30)` | 허용 | 아니오 |
| `BRK_IDX` | `int` | 허용 | 아니오 |
| `BRK_COM_NAME` | `varchar(70)` | 허용 | 아니오 |
| `BRK_COM_REGNO` | `varchar(13)` | 허용 | 아니오 |
| `BRK_PARTY` | `varchar(35)` | 허용 | 아니오 |
| `BRK_BIZTYPE` | `varchar(40)` | 허용 | 아니오 |
| `BRK_BIZCLASS` | `varchar(60)` | 허용 | 아니오 |
| `BRK_ADDRESS` | `varchar(200)` | 허용 | 아니오 |
| `BRK_EMAIL` | `varchar(70)` | 허용 | 아니오 |
| `BRK_DEPT` | `varchar(40)` | 허용 | 아니오 |
| `BRK_MEM_NAME` | `varchar(35)` | 허용 | 아니오 |
| `BRK_MEM_TEL` | `varchar(40)` | 허용 | 아니오 |
| `BRK_ID` | `varchar(12)` | 허용 | 아니오 |
| `BRK_DTT_YN` | `char(1)` | 허용 | 아니오 |
| `ETC_PCS_NO` | `varchar(35)` | 허용 | 아니오 |
| `SYS_CD` | `varchar(35)` | 허용 | 아니오 |
| `REQ_RCV_IDX` | `int` | 허용 | 아니오 |
| `SUP_SID` | `varchar(35)` | 허용 | 아니오 |
| `BYR_SID` | `varchar(35)` | 허용 | 아니오 |
| `REFINFO1` | `varchar(35)` | 허용 | 아니오 |
| `REFINFO2` | `varchar(35)` | 허용 | 아니오 |
| `DTT_STATUS` | `varchar(2)` | 불가 | 아니오 |
| `SUP_PRINT_CNT` | `int` | 허용 | 아니오 |
| `BYR_PRINT_CNT` | `int` | 허용 | 아니오 |
| `BRK_PRINT_CNT` | `int` | 허용 | 아니오 |
| `SUP_RCV_EMAIL` | `varchar(70)` | 허용 | 아니오 |
| `BYR_RCV_EMAIL` | `varchar(70)` | 허용 | 아니오 |
| `BRK_RCV_EMAIL` | `varchar(70)` | 허용 | 아니오 |
| `SUP_SMS_SEND_YN` | `varchar(1)` | 허용 | 아니오 |
| `BYR_SMS_SEND_YN` | `varchar(1)` | 허용 | 아니오 |
| `BRK_SMS_SEND_YN` | `varchar(1)` | 허용 | 아니오 |
| `ATTACHEDFILE_FULLPATH` | `varchar(285)` | 허용 | 아니오 |
| `ATTACHEDFILE_SIZE` | `int` | 허용 | 아니오 |
| `CREATE_LINK_IDX` | `int` | 허용 | 아니오 |
| `SUP_DEL_IDX` | `int` | 허용 | 아니오 |
| `BYR_DEL_IDX` | `int` | 허용 | 아니오 |
| `BRK_DEL_IDX` | `int` | 허용 | 아니오 |
| `SUP_BIZPLACE_CODE` | `varchar(35)` | 허용 | 아니오 |
| `BYR_BIZPLACE_CODE` | `varchar(35)` | 허용 | 아니오 |
| `BRK_BIZPLACE_CODE` | `varchar(35)` | 허용 | 아니오 |
| `SUP_VIEW_CNT` | `int` | 허용 | 아니오 |
| `BYR_VIEW_CNT` | `int` | 허용 | 아니오 |
| `BRK_VIEW_CNT` | `int` | 허용 | 아니오 |
| `SUP_SBID` | `varchar(35)` | 허용 | 아니오 |
| `BYR_SBID` | `varchar(35)` | 허용 | 아니오 |
| `BRK_SBID` | `varchar(35)` | 허용 | 아니오 |
| `SUP_BIZPLACE_NAME` | `varchar(70)` | 허용 | 아니오 |
| `BYR_BIZPLACE_NAME` | `varchar(70)` | 허용 | 아니오 |
| `BRK_BIZPLACE_NAME` | `varchar(70)` | 허용 | 아니오 |
| `ETC_NO1` | `varchar(50)` | 허용 | 아니오 |
| `ETC_NO2` | `varchar(50)` | 허용 | 아니오 |
| `ETC_NO3` | `varchar(50)` | 허용 | 아니오 |
| `ETC_NO4` | `varchar(50)` | 허용 | 아니오 |
| `CUSER` | `varchar(12)` | 불가 | 아니오 |
| `AMEND_CODE` | `varchar(2)` | 허용 | 아니오 |
| `ISSUE_ID` | `varchar(24)` | 허용 | 아니오 |
| `TYPECODE` | `char(4)` | 허용 | 아니오 |
| `FAX_SEND_YN` | `varchar(1)` | 허용 | 아니오 |
| `BYR_FAX_NO` | `varchar(20)` | 허용 | 아니오 |
| `SUP_ATT01` | `varchar(100)` | 허용 | 아니오 |
| `SUP_ATT02` | `varchar(100)` | 허용 | 아니오 |
| `SUP_ATT03` | `varchar(100)` | 허용 | 아니오 |
| `SUP_ATT04` | `varchar(100)` | 허용 | 아니오 |
| `SUP_ATT05` | `varchar(100)` | 허용 | 아니오 |
| `SUP_ATT06` | `varchar(100)` | 허용 | 아니오 |
| `SUP_ATT07` | `varchar(100)` | 허용 | 아니오 |
| `SUP_ATT08` | `varchar(100)` | 허용 | 아니오 |
| `SUP_ATT09` | `varchar(100)` | 허용 | 아니오 |
| `SUP_ATT10` | `varchar(100)` | 허용 | 아니오 |
| `SUP_ATT11` | `varchar(100)` | 허용 | 아니오 |
| `BYR_ATT01` | `varchar(100)` | 허용 | 아니오 |
| `BYR_ATT02` | `varchar(100)` | 허용 | 아니오 |
| `BYR_ATT03` | `varchar(100)` | 허용 | 아니오 |
| `BYR_ATT04` | `varchar(100)` | 허용 | 아니오 |
| `BYR_ATT05` | `varchar(100)` | 허용 | 아니오 |
| `BYR_ATT06` | `varchar(100)` | 허용 | 아니오 |
| `BYR_ATT07` | `varchar(100)` | 허용 | 아니오 |
| `BYR_ATT08` | `varchar(100)` | 허용 | 아니오 |
| `BYR_ATT09` | `varchar(100)` | 허용 | 아니오 |
| `BYR_ATT10` | `varchar(100)` | 허용 | 아니오 |
| `BYR_ATT11` | `varchar(100)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | VIEW / 2016-09-02T21:45:07.640 |
| 읽기·참조 객체 | `sb_dti.dbo.dtt_header_cub`, `sb_dti.dbo.dtt_header_cub_2020_01`, `sb_dti.dbo.dtt_header_cub_2021_01`, `sb_dti.dbo.dtt_header_cub_2022_01`, `sb_dti.dbo.dtt_header_cub_2023_01`, `sb_dti.dbo.dtt_header_cub_bf`, `sb_dti.dbo.dtt_header_cub_part`, `sb_dti.dbo.dtt_header_detail`, `sb_dti.dbo.dtt_header_detail_2020_01`, `sb_dti.dbo.dtt_header_detail_2021_01`, `sb_dti.dbo.dtt_header_detail_2022_01`, `sb_dti.dbo.dtt_header_detail_2023_01`, `sb_dti.dbo.dtt_header_detail_bf`, `sb_dti.dbo.dtt_header_detail_part`, `sb_dti.dbo.v_dtt_header` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getDetailHeader](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/transactionstatement/repository/TransactionStatementMapper.kt#L179) — 바인딩: `dttIdx`, `dttWday`. 결과 매핑: `DTT_IDX` → `dttIdx`, `DTT_WDAY` → `dttWday`, `DTI_IDX` → `dtiIdx`, `DIRECTION` → `direction`, `ETC_PCS_NO` → `etcPcsNo`, `DTT_NO` → `dttNo`, `BLANK_COUNT` → `blankCount`, `DTT_TYPE` → `dttType`, `TAX_DEMAND` → `taxDemand`, `VOLUME_NO` → `volumeNo`, `ISSUE_NO` → `issueNo`, `SEQ_NO` → `seqNo`, `REMARK` → `remark`, `REMARK2` → `remark2`, `INP_TYPE` → `inpType`, `TOT_AMT` → `totAmt`, `SUP_AMT` → `supAmt`, `TAX_AMT` → `taxAmt`, `SUP_IDX` → `supIdx`, `SUP_ID` → `supId`, `SUP_COM_NAME` → `supComName`, `SUP_COM_REGNO` → `supComRegno`, `SUP_BIZPLACE_CODE` → `supBizplaceCode`, `SUP_PARTY` → `supParty`, `SUP_BIZTYPE` → `supBiztype`, `SUP_BIZCLASS` → `supBizclass`, `SUP_ADDRESS` → `supAddress`, `SUP_MEM_NAME` → `supMemName`, `SUP_MEM_TEL` → `supMemTel`, `SUP_EMAIL` → `supEmail`, `BYR_ID` → `byrId`, `BYR_TYPE` → `byrType`, `BYR_COM_NAME` → `byrComName`, `BYR_COM_REGNO` → `byrComRegno`, `BYR_BIZPLACE_CODE` → `byrBizplaceCode`, `BYR_PARTY` → `byrParty`, `BYR_BIZTYPE` → `byrBiztype`, `BYR_BIZCLASS` → `byrBizclass`, `BYR_ADDRESS` → `byrAddress`, `BYR_MEM_NAME` → `byrMemName`, `BYR_MEM_TEL` → `byrMemTel`, `BYR_EMAIL` → `byrEmail`, `REQ_RCV_IDX` → `reqRcvIdx`, `ETC_NO1` → `etcNo1`, `ETC_NO2` → `etcNo2`, `ETC_NO3` → `etcNo3`, `ETC_NO4` → `etcNo4`, `DTI_STATUS` → `dtiStatus`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
JOIN DBO.DTT_HEADER_DETAIL B
```

하위 프로시저·함수·뷰: `master.dbo.clr_dec_char_sel_tc`, `master.dbo.dec_char_sel_tc`, `sb_dti.dbo.dtt_header_cub`, `sb_dti.dbo.dtt_header_detail`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db157"></a>
## SB_DTI_DW.dbo.DTI_HEADER_CUB

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `DTI_WDAY` | `varchar(10)` | 불가 | 아니오 |
| `DTI_IDX` | `int` | 불가 | 아니오 |
| `DIRECTION` | `char(1)` | 허용 | 아니오 |
| `UPLOAD_IDX` | `int` | 허용 | 아니오 |
| `DTI_ISSUEDATE` | `datetime` | 허용 | 아니오 |
| `DTI_APPROVEDATE` | `datetime` | 허용 | 아니오 |
| `DTI_TYPE` | `char(1)` | 허용 | 아니오 |
| `TAXINVOICE_TYPE` | `varchar(3)` | 허용 | 아니오 |
| `TAX_DEMAND` | `varchar(2)` | 허용 | 아니오 |
| `VOLUME_NO` | `varchar(35)` | 허용 | 아니오 |
| `ISSUE_NO` | `varchar(35)` | 허용 | 아니오 |
| `SEQ_NO` | `varchar(48)` | 허용 | 아니오 |
| `REMARK` | `varchar(300)` | 허용 | 아니오 |
| `TOT_AMT` | `money` | 불가 | 아니오 |
| `SUP_AMT` | `money` | 허용 | 아니오 |
| `TAX_AMT` | `money` | 허용 | 아니오 |
| `SUP_IDX` | `int` | 허용 | 아니오 |
| `SUP_COM_NAME` | `varchar(400)` | 허용 | 아니오 |
| `SUP_COM_REGNO` | `varchar(10)` | 허용 | 아니오 |
| `SUP_ID` | `varchar(12)` | 허용 | 아니오 |
| `BYR_IDX` | `int` | 허용 | 아니오 |
| `BYR_COM_NAME` | `varchar(400)` | 허용 | 아니오 |
| `BYR_COM_REGNO` | `varchar(32)` | 허용 | 아니오 |
| `BYR_TYPE` | `char(1)` | 허용 | 아니오 |
| `BYR_ID` | `varchar(12)` | 허용 | 아니오 |
| `BRK_IDX` | `int` | 허용 | 아니오 |
| `BRK_COM_NAME` | `varchar(400)` | 허용 | 아니오 |
| `BRK_COM_REGNO` | `varchar(13)` | 허용 | 아니오 |
| `BRK_ID` | `varchar(12)` | 허용 | 아니오 |
| `BRK_DTI_YN` | `char(1)` | 허용 | 아니오 |
| `ETC_PCS_NO` | `varchar(35)` | 허용 | 아니오 |
| `DTT_LINK_TYPE` | `varchar(3)` | 허용 | 아니오 |
| `REQ_RCV_IDX` | `int` | 허용 | 아니오 |
| `DTI_STATUS` | `varchar(2)` | 불가 | 아니오 |
| `SUP_PRINT_CNT` | `int` | 허용 | 아니오 |
| `BYR_PRINT_CNT` | `int` | 허용 | 아니오 |
| `BRK_PRINT_CNT` | `int` | 허용 | 아니오 |
| `SUP_VIEW_CNT` | `int` | 허용 | 아니오 |
| `BYR_VIEW_CNT` | `int` | 허용 | 아니오 |
| `BRK_VIEW_CNT` | `int` | 허용 | 아니오 |
| `SUP_DEL_IDX` | `int` | 허용 | 아니오 |
| `BYR_DEL_IDX` | `int` | 허용 | 아니오 |
| `BRK_DEL_IDX` | `int` | 허용 | 아니오 |
| `SUP_BIZPLACE_CODE` | `varchar(35)` | 허용 | 아니오 |
| `BYR_BIZPLACE_CODE` | `varchar(35)` | 허용 | 아니오 |
| `BRK_BIZPLACE_CODE` | `varchar(35)` | 허용 | 아니오 |
| `CUSER` | `varchar(12)` | 불가 | 아니오 |
| `CDATE` | `datetime` | 불가 | 아니오 |
| `UUSER` | `varchar(12)` | 불가 | 아니오 |
| `UDATE` | `datetime` | 불가 | 아니오 |
| `UPLOAD_DTI_IDX` | `int` | 허용 | 아니오 |
| `VERSION` | `varchar(3)` | 허용 | 아니오 |
| `AMEND_CODE` | `varchar(2)` | 허용 | 아니오 |
| `REMARK2` | `varchar(300)` | 허용 | 아니오 |
| `REMARK3` | `varchar(300)` | 허용 | 아니오 |
| `EXCHANED_DOC_ID` | `varchar(24)` | 허용 | 아니오 |
| `ISSUE_ID` | `varchar(24)` | 허용 | 아니오 |
| `TYPECODE` | `char(4)` | 허용 | 아니오 |
| `NTS_SEND_STATUS` | `numeric(2,0)` | 허용 | 아니오 |
| `NTS_RESULT_CODE` | `varchar(6)` | 허용 | 아니오 |
| `NTS_SEND_DATE` | `datetime` | 허용 | 아니오 |
| `DELAY_ISSUE` | `char(1)` | 허용 | 아니오 |
| `NTS_INSTANCE_TYPE` | `char(1)` | 허용 | 아니오 |
| `ORI_ISSUE_ID` | `varchar(24)` | 허용 | 아니오 |
| `ISENCRYPTED` | `varchar(1)` | 허용 | 아니오 |
| `BYR_COM_REGNO#` | `varchar(52)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | VIEW / 2024-11-19T14:31:50.947 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_header_cub_2020_01`, `sb_dti.dbo.dti_header_cub_2020_02`, `sb_dti.dbo.dti_header_cub_2020_03`, `sb_dti.dbo.dti_header_cub_2020_04`, `sb_dti.dbo.dti_header_cub_2020_05`, `sb_dti.dbo.dti_header_cub_2020_06`, `sb_dti.dbo.dti_header_cub_2020_07`, `sb_dti.dbo.dti_header_cub_2020_08`, `sb_dti.dbo.dti_header_cub_2020_09`, `sb_dti.dbo.dti_header_cub_2020_10`, `sb_dti.dbo.dti_header_cub_2020_11`, `sb_dti.dbo.dti_header_cub_2020_12`, `sb_dti.dbo.dti_header_cub_2021_01`, `sb_dti.dbo.dti_header_cub_2021_02`, `sb_dti.dbo.dti_header_cub_2021_03`, `sb_dti.dbo.dti_header_cub_2021_04`, `sb_dti.dbo.dti_header_cub_2021_05`, `sb_dti.dbo.dti_header_cub_2021_06`, `sb_dti.dbo.dti_header_cub_2021_07`, `sb_dti.dbo.dti_header_cub_2021_08`, `sb_dti.dbo.dti_header_cub_2021_09`, `sb_dti.dbo.dti_header_cub_2021_10`, `sb_dti.dbo.dti_header_cub_2021_11`, `sb_dti.dbo.dti_header_cub_2021_12`, `sb_dti.dbo.dti_header_cub_2022_01`, `sb_dti.dbo.dti_header_cub_2022_02`, `sb_dti.dbo.dti_header_cub_2022_03`, `sb_dti.dbo.dti_header_cub_2022_04`, `sb_dti.dbo.dti_header_cub_2022_05`, `sb_dti.dbo.dti_header_cub_2022_06`, `sb_dti.dbo.dti_header_cub_2022_07`, `sb_dti.dbo.dti_header_cub_2022_08`, `sb_dti.dbo.dti_header_cub_2022_09`, `sb_dti.dbo.dti_header_cub_2022_10`, `sb_dti.dbo.dti_header_cub_2022_11`, `sb_dti.dbo.dti_header_cub_2022_12`, `sb_dti.dbo.dti_header_cub_2023_01`, `sb_dti.dbo.dti_header_cub_2023_02`, `sb_dti.dbo.dti_header_cub_2023_03`, `sb_dti.dbo.dti_header_cub_2023_04`, `sb_dti.dbo.dti_header_cub_2023_05`, `sb_dti.dbo.dti_header_cub_2023_06`, `sb_dti_dw.dbo.dti_header_cub` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getBrokeredFlag](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L348) — 바인딩: `dtiWday`, `dtiIdx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [getDtiWday](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L332) — 바인딩: `dtiIdx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [getNtsResultCode](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L408) — 바인딩: `dtiIdx`, `dtiWday`. 결과 매핑: `NTS_RESULT_CODE` → `ntsResultCode`, `EXCHANED_DOC_ID` → `exchangedDocId`.
- [findKeyByReference](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L342) — 바인딩: `referenceNumber`. 결과 매핑: `DTI_IDX` → `dtiIdx`, `DTI_WDAY` → `dtiWday`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db158"></a>
## SB_DTI_DW.dbo.upSelect_DTI_HEADER_DW

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DTI_IDX` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_WDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:45:03.190 |
| 읽기·참조 객체 | `sb_customize.dbo.sec_code`, `sb_dti.dbo.company_quit_status`, `sb_dti.dbo.dti_header_cub_2020_01`, `sb_dti.dbo.dti_header_cub_2020_02`, `sb_dti.dbo.dti_header_cub_2020_03`, `sb_dti.dbo.dti_header_cub_2020_04`, `sb_dti.dbo.dti_header_cub_2020_05`, `sb_dti.dbo.dti_header_cub_2020_06`, `sb_dti.dbo.dti_header_cub_2020_07`, `sb_dti.dbo.dti_header_cub_2020_08`, `sb_dti.dbo.dti_header_cub_2020_09`, `sb_dti.dbo.dti_header_cub_2020_10`, `sb_dti.dbo.dti_header_cub_2020_11`, `sb_dti.dbo.dti_header_cub_2020_12`, `sb_dti.dbo.dti_header_cub_2021_01`, `sb_dti.dbo.dti_header_cub_2021_02`, `sb_dti.dbo.dti_header_cub_2021_03`, `sb_dti.dbo.dti_header_cub_2021_04`, `sb_dti.dbo.dti_header_cub_2021_05`, `sb_dti.dbo.dti_header_cub_2021_06`, `sb_dti.dbo.dti_header_cub_2021_07`, `sb_dti.dbo.dti_header_cub_2021_08`, `sb_dti.dbo.dti_header_cub_2021_09`, `sb_dti.dbo.dti_header_cub_2021_10`, `sb_dti.dbo.dti_header_cub_2021_11`, `sb_dti.dbo.dti_header_cub_2021_12`, `sb_dti.dbo.dti_header_cub_2022_01`, `sb_dti.dbo.dti_header_cub_2022_02`, `sb_dti.dbo.dti_header_cub_2022_03`, `sb_dti.dbo.dti_header_cub_2022_04`, `sb_dti.dbo.dti_header_cub_2022_05`, `sb_dti.dbo.dti_header_cub_2022_06`, `sb_dti.dbo.dti_header_cub_2022_07`, `sb_dti.dbo.dti_header_cub_2022_08`, `sb_dti.dbo.dti_header_cub_2022_09`, `sb_dti.dbo.dti_header_cub_2022_10`, `sb_dti.dbo.dti_header_cub_2022_11`, `sb_dti.dbo.dti_header_cub_2022_12`, `sb_dti.dbo.dti_header_cub_2023_01`, `sb_dti.dbo.dti_header_cub_2023_02`, `sb_dti.dbo.dti_header_cub_2023_03`, `sb_dti.dbo.dti_header_cub_2023_04`, `sb_dti.dbo.dti_header_cub_2023_05`, `sb_dti.dbo.dti_header_cub_2023_06`, `sb_dti.dbo.dti_header_detail_2020_01`, `sb_dti.dbo.dti_header_detail_2020_02`, `sb_dti.dbo.dti_header_detail_2020_03`, `sb_dti.dbo.dti_header_detail_2020_04`, `sb_dti.dbo.dti_header_detail_2020_05`, `sb_dti.dbo.dti_header_detail_2020_06`, `sb_dti.dbo.dti_header_detail_2020_07`, `sb_dti.dbo.dti_header_detail_2020_08`, `sb_dti.dbo.dti_header_detail_2020_09`, `sb_dti.dbo.dti_header_detail_2020_10`, `sb_dti.dbo.dti_header_detail_2020_11`, `sb_dti.dbo.dti_header_detail_2020_12`, `sb_dti.dbo.dti_header_detail_2021_01`, `sb_dti.dbo.dti_header_detail_2021_02`, `sb_dti.dbo.dti_header_detail_2021_03`, `sb_dti.dbo.dti_header_detail_2021_04`, `sb_dti.dbo.dti_header_detail_2021_05`, `sb_dti.dbo.dti_header_detail_2021_06`, `sb_dti.dbo.dti_header_detail_2021_07`, `sb_dti.dbo.dti_header_detail_2021_08`, `sb_dti.dbo.dti_header_detail_2021_09`, `sb_dti.dbo.dti_header_detail_2021_10`, `sb_dti.dbo.dti_header_detail_2021_11`, `sb_dti.dbo.dti_header_detail_2021_12`, `sb_dti.dbo.dti_header_detail_2022_01`, `sb_dti.dbo.dti_header_detail_2022_02`, `sb_dti.dbo.dti_header_detail_2022_03`, `sb_dti.dbo.dti_header_detail_2022_04`, `sb_dti.dbo.dti_header_detail_2022_05`, `sb_dti.dbo.dti_header_detail_2022_06`, `sb_dti.dbo.dti_header_detail_2022_07`, `sb_dti.dbo.dti_header_detail_2022_08`, `sb_dti.dbo.dti_header_detail_2022_09`, `sb_dti.dbo.dti_header_detail_2022_10`, `sb_dti.dbo.dti_header_detail_2022_11`, `sb_dti.dbo.dti_header_detail_2022_12`, `sb_dti.dbo.dti_header_detail_2023_01`, `sb_dti.dbo.dti_header_detail_2023_02`, `sb_dti.dbo.dti_header_detail_2023_03`, `sb_dti.dbo.dti_header_detail_2023_04`, `sb_dti.dbo.dti_header_detail_2023_05`, `sb_dti.dbo.dti_header_detail_2023_06`, `sb_dti.dbo.dti_status_his`, `sb_dti.dbo.dti_status_his_2023_07`, `sb_dti.dbo.dti_status_his_part`, `sb_dti.dbo.dti_status_his_prev_buffer`, `sb_dti_dw.dbo.dti_header_cub`, `sb_dti_dw.dbo.dti_header_detail`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getDetailHeader](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L195) — 바인딩: `dtiIdx`, `dtiWday`. 결과 매핑: `DTI_IDX` → `dtiIdx`, `DTI_WDAY` → `dtiWday`, `DTI_ISSUEDATE` → `dtiIssuedate`, `DTI_APPROVEDATE` → `dtiApprovedate`, `DIRECTION` → `direction`, `DTI_TYPE` → `dtiType`, `TAX_DEMAND` → `taxDemand`, `DTI_NO` → `dtiNo`, `ISSUE_ID` → `issueId`, `ORI_ISSUE_ID` → `oriIssueId`, `ETC_PCS_NO` → `etcPcsNo`, `DTI_STATUS` → `dtiStatus`, `AMEND_CODE` → `amendCode`, `TAXINVOICE_TYPE` → `taxinvoiceType`, `BLANK_COUNT` → `blankCount`, `VOLUME_NO` → `volumeNo`, `ISSUE_NO` → `issueNo`, `SEQ_NO` → `seqNo`, `INP_TYPE` → `inpType`, `TOT_AMT` → `totAmt`, `SUP_AMT` → `supAmt`, `TAX_AMT` → `taxAmt`, `REMARK` → `remark`, `REMARK2` → `remark2`, `REMARK3` → `remark3`, `SUP_IDX` → `supIdx`, `SUP_COM_REGNO` → `supComRegno`, `SUP_COM_NAME` → `supComName`, `SUP_EMAIL` → `supEmail`, `SUP_MEM_NAME` → `supMemName`, `SUP_MEM_TEL` → `supMemTel`, `SUP_PARTY` → `supParty`, `SUP_BIZTYPE` → `supBiztype`, `SUP_BIZCLASS` → `supBizclass`, `SUP_ADDRESS` → `supAddress`, `SUP_ID` → `supId`, `SUP_DEPT` → `supDept`, `SUP_BIZPLACE_CODE` → `supBizplaceCode`, `SUP_BIZPLACE_NAME` → `supBizplaceName`, `SUP_RCV_EMAIL` → `supRcvEmail`, `SUP_SMS_SEND_YN` → `supSmsSendYn`, `BYR_IDX` → `byrIdx`, `BYR_COM_REGNO` → `byrComRegno`, `BYR_COM_NAME` → `byrComName`, `BYR_EMAIL` → `byrEmail`, `BYR_MEM_NAME` → `byrMemName`, `BYR_MEM_TEL` → `byrMemTel`, `BYR_MEM_NAME2` → `byrMemName2`, `BYR_EMAIL2` → `byrEmail2`, `BYR_PARTY` → `byrParty`, `BYR_BIZTYPE` → `byrBiztype`, `BYR_BIZCLASS` → `byrBizclass`, `BYR_ADDRESS` → `byrAddress`, `BYR_TYPE` → `byrType`, `BYR_ID` → `byrId`, `BYR_DEPT` → `byrDept`, `BYR_BIZPLACE_CODE` → `byrBizplaceCode`, `BYR_BIZPLACE_NAME` → `byrBizplaceName`, `BYR_RCV_EMAIL` → `byrRcvEmail`, `BYR_SMS_SEND_YN` → `byrSmsSendYn`, `BRK_IDX` → `brkIdx`, `BRK_COM_REGNO` → `brkComRegno`, `BRK_COM_NAME` → `brkComName`, `BRK_EMAIL` → `brkEmail`, `BRK_MEM_NAME` → `brkMemName`, `BRK_MEM_TEL` → `brkMemTel`, `BRK_PARTY` → `brkParty`, `BRK_BIZTYPE` → `brkBiztype`, `BRK_BIZCLASS` → `brkBizclass`, `BRK_ADDRESS` → `brkAddress`, `BRK_BIZPLACE_CODE` → `brkBizplaceCode`, `BRK_DTI_YN` → `brkDtiYn`, `NTS_SEND_STATUS` → `ntsSendStatus`, `NTS_SEND_DATE` → `ntsSendDate`, `ISSUE_PATH` → `issuePath`, `DTT_LINK_TYPE` → `dttLinkType`, `SUP_COMQUIT_STATUS` → `supComquitStatus`, `SUP_COMQUIT_ERRORMSG` → `supComquitErrMsg`, `BYR_COMQUIT_STATUS` → `byrComquitStatus`, `BYR_COMQUIT_ERRORMSG` → `byrComquitErrMsg`, `REASON` → `reason`, `FAX_SEND_YN` → `faxSendYn`, `REQ_RCV_IDX` → `reqRcvIdx`, `SEC_YN` → `secYn`, `BYR_ATT01` → `byrAtt01`, `COM_SEAL` → `comSeal`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SUP_COMQUIT_STATUS=''
SET @SUP_COMQUIT_ERRORMSG=''
SET @BYR_COMQUIT_STATUS=''
SET @BYR_COMQUIT_ERRORMSG=''
SET @BRK_COMQUIT_STATUS=''
SET @BRK_COMQUIT_ERRORMSG=''
WHERE
WHERE
WHERE
SET @SEC_YN = 'Y'
SET @BYR_ATT01=''
SET @SEC_YN = 'N'
SET @REASON = ''
WHERE
ORDER  BY
SET @JOINSQL01 = '
JOIN smartbill3..MEMBER M1 ON DM.SUP_IDX = M1.MEM_NO
JOIN smartbill3..COMPANY C1 ON C1.COM_NO = M1.COM_NO '
```

하위 프로시저·함수·뷰: `master.dbo.clr_dec_char_sel_tc`, `master.dbo.dec_char_sel_tc`, `sb_dti.dbo.dti_status_his`, `sb_dti_dw.dbo.dti_header_cub`, `sb_dti_dw.dbo.dti_header_detail`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db159"></a>
## SB_DTI_DW.dbo.upSelect_DTI_ITEM_DW

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DTI_IDX` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_WDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:45:00.910 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_item_2020_01`, `sb_dti.dbo.dti_item_2020_02`, `sb_dti.dbo.dti_item_2020_03`, `sb_dti.dbo.dti_item_2020_04`, `sb_dti.dbo.dti_item_2020_05`, `sb_dti.dbo.dti_item_2020_06`, `sb_dti.dbo.dti_item_2020_07`, `sb_dti.dbo.dti_item_2020_08`, `sb_dti.dbo.dti_item_2020_09`, `sb_dti.dbo.dti_item_2020_10`, `sb_dti.dbo.dti_item_2020_11`, `sb_dti.dbo.dti_item_2020_12`, `sb_dti.dbo.dti_item_2021_01`, `sb_dti.dbo.dti_item_2021_02`, `sb_dti.dbo.dti_item_2021_03`, `sb_dti.dbo.dti_item_2021_04`, `sb_dti.dbo.dti_item_2021_05`, `sb_dti.dbo.dti_item_2021_06`, `sb_dti.dbo.dti_item_2021_07`, `sb_dti.dbo.dti_item_2021_08`, `sb_dti.dbo.dti_item_2021_09`, `sb_dti.dbo.dti_item_2021_10`, `sb_dti.dbo.dti_item_2021_11`, `sb_dti.dbo.dti_item_2021_12`, `sb_dti.dbo.dti_item_2022_01`, `sb_dti.dbo.dti_item_2022_02`, `sb_dti.dbo.dti_item_2022_03`, `sb_dti.dbo.dti_item_2022_04`, `sb_dti.dbo.dti_item_2022_05`, `sb_dti.dbo.dti_item_2022_06`, `sb_dti.dbo.dti_item_2022_07`, `sb_dti.dbo.dti_item_2022_08`, `sb_dti.dbo.dti_item_2022_09`, `sb_dti.dbo.dti_item_2022_10`, `sb_dti.dbo.dti_item_2022_11`, `sb_dti.dbo.dti_item_2022_12`, `sb_dti.dbo.dti_item_2023_01`, `sb_dti.dbo.dti_item_2023_02`, `sb_dti.dbo.dti_item_2023_03`, `sb_dti.dbo.dti_item_2023_04`, `sb_dti.dbo.dti_item_2023_05`, `sb_dti.dbo.dti_item_2023_06`, `sb_dti_dw.dbo.dti_item` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getDetailItems](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L214) — 바인딩: `dtiIdx`, `dtiWday`. 결과 매핑: `ITEM_IDX` → `itemIdx`, `ITEM_MD` → `itemMd`, `ITEM_NAME` → `itemName`, `ITEM_SIZE` → `itemSize`, `ITEM_QNT` → `itemQnt`, `UNIT_PRICE` → `unitPrice`, `SUP_AMT` → `supAmt`, `TAX_AMT` → `taxAmt`, `ITEM_REMARK` → `itemRemark`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE DTI_WDAY=@DTI_WDAY AND DTI_IDX = @DTI_IDX
```

하위 프로시저·함수·뷰: `sb_dti_dw.dbo.dti_item`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db160"></a>
## SB_DTI_DW.dbo.upSelect_DTI_PAYMETHOD_DW

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DTI_IDX` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_WDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:45:00.860 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_paymethod_2020_01`, `sb_dti.dbo.dti_paymethod_2020_02`, `sb_dti.dbo.dti_paymethod_2020_03`, `sb_dti.dbo.dti_paymethod_2020_04`, `sb_dti.dbo.dti_paymethod_2020_05`, `sb_dti.dbo.dti_paymethod_2020_06`, `sb_dti.dbo.dti_paymethod_2020_07`, `sb_dti.dbo.dti_paymethod_2020_08`, `sb_dti.dbo.dti_paymethod_2020_09`, `sb_dti.dbo.dti_paymethod_2020_10`, `sb_dti.dbo.dti_paymethod_2020_11`, `sb_dti.dbo.dti_paymethod_2020_12`, `sb_dti.dbo.dti_paymethod_2021_01`, `sb_dti.dbo.dti_paymethod_2021_02`, `sb_dti.dbo.dti_paymethod_2021_03`, `sb_dti.dbo.dti_paymethod_2021_04`, `sb_dti.dbo.dti_paymethod_2021_05`, `sb_dti.dbo.dti_paymethod_2021_06`, `sb_dti.dbo.dti_paymethod_2021_07`, `sb_dti.dbo.dti_paymethod_2021_08`, `sb_dti.dbo.dti_paymethod_2021_09`, `sb_dti.dbo.dti_paymethod_2021_10`, `sb_dti.dbo.dti_paymethod_2021_11`, `sb_dti.dbo.dti_paymethod_2021_12`, `sb_dti.dbo.dti_paymethod_2022_01`, `sb_dti.dbo.dti_paymethod_2022_02`, `sb_dti.dbo.dti_paymethod_2022_03`, `sb_dti.dbo.dti_paymethod_2022_04`, `sb_dti.dbo.dti_paymethod_2022_05`, `sb_dti.dbo.dti_paymethod_2022_06`, `sb_dti.dbo.dti_paymethod_2022_07`, `sb_dti.dbo.dti_paymethod_2022_08`, `sb_dti.dbo.dti_paymethod_2022_09`, `sb_dti.dbo.dti_paymethod_2022_10`, `sb_dti.dbo.dti_paymethod_2022_11`, `sb_dti.dbo.dti_paymethod_2022_12`, `sb_dti.dbo.dti_paymethod_2023_01`, `sb_dti.dbo.dti_paymethod_2023_02`, `sb_dti.dbo.dti_paymethod_2023_03`, `sb_dti.dbo.dti_paymethod_2023_04`, `sb_dti.dbo.dti_paymethod_2023_05`, `sb_dti.dbo.dti_paymethod_2023_06`, `sb_dti_dw.dbo.dti_paymethod` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getDetailPayMethods](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L228) — 바인딩: `dtiIdx`, `dtiWday`. 결과 매핑: `METHOD` → `method`, `KORCURRENCY` → `korCurrency`, `FORCURRENCY` → `forCurrency`, `CURRENCYCODE` → `currencyCode`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE DTI_WDAY=@DTI_WDAY AND DTI_IDX = @DTI_IDX
```

하위 프로시저·함수·뷰: `sb_dti_dw.dbo.dti_paymethod`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db161"></a>
## SB_DTI_DW.dbo.upSelect_DTI_SIGN_Download_DW

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DTI_IDX` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_WDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:45:00.990 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_sign_cub_2020_01`, `sb_dti.dbo.dti_sign_cub_2020_02`, `sb_dti.dbo.dti_sign_cub_2020_03`, `sb_dti.dbo.dti_sign_cub_2020_04`, `sb_dti.dbo.dti_sign_cub_2020_05`, `sb_dti.dbo.dti_sign_cub_2020_06`, `sb_dti.dbo.dti_sign_cub_2020_07`, `sb_dti.dbo.dti_sign_cub_2020_08`, `sb_dti.dbo.dti_sign_cub_2020_09`, `sb_dti.dbo.dti_sign_cub_2020_10`, `sb_dti.dbo.dti_sign_cub_2020_11`, `sb_dti.dbo.dti_sign_cub_2020_12`, `sb_dti.dbo.dti_sign_cub_2021_01`, `sb_dti.dbo.dti_sign_cub_2021_02`, `sb_dti.dbo.dti_sign_cub_2021_03`, `sb_dti.dbo.dti_sign_cub_2021_04`, `sb_dti.dbo.dti_sign_cub_2021_05`, `sb_dti.dbo.dti_sign_cub_2021_06`, `sb_dti.dbo.dti_sign_cub_2021_07`, `sb_dti.dbo.dti_sign_cub_2021_08`, `sb_dti.dbo.dti_sign_cub_2021_09`, `sb_dti.dbo.dti_sign_cub_2021_10`, `sb_dti.dbo.dti_sign_cub_2021_11`, `sb_dti.dbo.dti_sign_cub_2021_12`, `sb_dti.dbo.dti_sign_cub_2022_01`, `sb_dti.dbo.dti_sign_cub_2022_02`, `sb_dti.dbo.dti_sign_cub_2022_03`, `sb_dti.dbo.dti_sign_cub_2022_04`, `sb_dti.dbo.dti_sign_cub_2022_05`, `sb_dti.dbo.dti_sign_cub_2022_06`, `sb_dti.dbo.dti_sign_cub_2022_07`, `sb_dti.dbo.dti_sign_cub_2022_08`, `sb_dti.dbo.dti_sign_cub_2022_09`, `sb_dti.dbo.dti_sign_cub_2022_10`, `sb_dti.dbo.dti_sign_cub_2022_11`, `sb_dti.dbo.dti_sign_cub_2022_12`, `sb_dti.dbo.dti_sign_cub_2023_01`, `sb_dti.dbo.dti_sign_cub_2023_02`, `sb_dti.dbo.dti_sign_cub_2023_03`, `sb_dti.dbo.dti_sign_cub_2023_04`, `sb_dti.dbo.dti_sign_cub_2023_05`, `sb_dti.dbo.dti_sign_cub_2023_06`, `sb_dti.dbo.dti_sign_xml_2020_01`, `sb_dti.dbo.dti_sign_xml_2020_02`, `sb_dti.dbo.dti_sign_xml_2020_03`, `sb_dti.dbo.dti_sign_xml_2020_04`, `sb_dti.dbo.dti_sign_xml_2020_05`, `sb_dti.dbo.dti_sign_xml_2020_06`, `sb_dti.dbo.dti_sign_xml_2020_07`, `sb_dti.dbo.dti_sign_xml_2020_08`, `sb_dti.dbo.dti_sign_xml_2020_09`, `sb_dti.dbo.dti_sign_xml_2020_10`, `sb_dti.dbo.dti_sign_xml_2020_11`, `sb_dti.dbo.dti_sign_xml_2020_12`, `sb_dti.dbo.dti_sign_xml_2021_01`, `sb_dti.dbo.dti_sign_xml_2021_02`, `sb_dti.dbo.dti_sign_xml_2021_03`, `sb_dti.dbo.dti_sign_xml_2021_04`, `sb_dti.dbo.dti_sign_xml_2021_05`, `sb_dti.dbo.dti_sign_xml_2021_06`, `sb_dti.dbo.dti_sign_xml_2021_07`, `sb_dti.dbo.dti_sign_xml_2021_08`, `sb_dti.dbo.dti_sign_xml_2021_09`, `sb_dti.dbo.dti_sign_xml_2021_10`, `sb_dti.dbo.dti_sign_xml_2021_11`, `sb_dti.dbo.dti_sign_xml_2021_12`, `sb_dti.dbo.dti_sign_xml_2022_01`, `sb_dti.dbo.dti_sign_xml_2022_02`, `sb_dti.dbo.dti_sign_xml_2022_03`, `sb_dti.dbo.dti_sign_xml_2022_04`, `sb_dti.dbo.dti_sign_xml_2022_05`, `sb_dti.dbo.dti_sign_xml_2022_06`, `sb_dti.dbo.dti_sign_xml_2022_07`, `sb_dti.dbo.dti_sign_xml_2022_08`, `sb_dti.dbo.dti_sign_xml_2022_09`, `sb_dti.dbo.dti_sign_xml_2022_10`, `sb_dti.dbo.dti_sign_xml_2022_11`, `sb_dti.dbo.dti_sign_xml_2022_12`, `sb_dti.dbo.dti_sign_xml_2023_01`, `sb_dti.dbo.dti_sign_xml_2023_02`, `sb_dti.dbo.dti_sign_xml_2023_03`, `sb_dti.dbo.dti_sign_xml_2023_04`, `sb_dti.dbo.dti_sign_xml_2023_05`, `sb_dti.dbo.dti_sign_xml_2023_06`, `sb_dti_dw.dbo.dti_sign`, `sb_dti_dw.dbo.dti_sign_cub`, `sb_dti_dw.dbo.dti_sign_xml` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getDtiSignedXml](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L424) — 바인딩: `dtiIdx`, `dtiWday`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE DTI_WDAY = @DTI_WDAY AND DTI_IDX = @DTI_IDX
```

하위 프로시저·함수·뷰: `master.dbo.clr_dec_lob_sel`, `master.dbo.dec_lob_sel`, `sb_dti_dw.dbo.dti_sign`, `sb_dti_dw.dbo.dti_sign_cub`, `sb_dti_dw.dbo.dti_sign_xml`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db162"></a>
## SB_DTI_DW.dbo.upSelect_DTI_SIGN_DW

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DTI_IDX` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_WDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:45:03.073 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_sign_cub_2020_01`, `sb_dti.dbo.dti_sign_cub_2020_02`, `sb_dti.dbo.dti_sign_cub_2020_03`, `sb_dti.dbo.dti_sign_cub_2020_04`, `sb_dti.dbo.dti_sign_cub_2020_05`, `sb_dti.dbo.dti_sign_cub_2020_06`, `sb_dti.dbo.dti_sign_cub_2020_07`, `sb_dti.dbo.dti_sign_cub_2020_08`, `sb_dti.dbo.dti_sign_cub_2020_09`, `sb_dti.dbo.dti_sign_cub_2020_10`, `sb_dti.dbo.dti_sign_cub_2020_11`, `sb_dti.dbo.dti_sign_cub_2020_12`, `sb_dti.dbo.dti_sign_cub_2021_01`, `sb_dti.dbo.dti_sign_cub_2021_02`, `sb_dti.dbo.dti_sign_cub_2021_03`, `sb_dti.dbo.dti_sign_cub_2021_04`, `sb_dti.dbo.dti_sign_cub_2021_05`, `sb_dti.dbo.dti_sign_cub_2021_06`, `sb_dti.dbo.dti_sign_cub_2021_07`, `sb_dti.dbo.dti_sign_cub_2021_08`, `sb_dti.dbo.dti_sign_cub_2021_09`, `sb_dti.dbo.dti_sign_cub_2021_10`, `sb_dti.dbo.dti_sign_cub_2021_11`, `sb_dti.dbo.dti_sign_cub_2021_12`, `sb_dti.dbo.dti_sign_cub_2022_01`, `sb_dti.dbo.dti_sign_cub_2022_02`, `sb_dti.dbo.dti_sign_cub_2022_03`, `sb_dti.dbo.dti_sign_cub_2022_04`, `sb_dti.dbo.dti_sign_cub_2022_05`, `sb_dti.dbo.dti_sign_cub_2022_06`, `sb_dti.dbo.dti_sign_cub_2022_07`, `sb_dti.dbo.dti_sign_cub_2022_08`, `sb_dti.dbo.dti_sign_cub_2022_09`, `sb_dti.dbo.dti_sign_cub_2022_10`, `sb_dti.dbo.dti_sign_cub_2022_11`, `sb_dti.dbo.dti_sign_cub_2022_12`, `sb_dti.dbo.dti_sign_cub_2023_01`, `sb_dti.dbo.dti_sign_cub_2023_02`, `sb_dti.dbo.dti_sign_cub_2023_03`, `sb_dti.dbo.dti_sign_cub_2023_04`, `sb_dti.dbo.dti_sign_cub_2023_05`, `sb_dti.dbo.dti_sign_cub_2023_06`, `sb_dti.dbo.dti_sign_xml_2020_01`, `sb_dti.dbo.dti_sign_xml_2020_02`, `sb_dti.dbo.dti_sign_xml_2020_03`, `sb_dti.dbo.dti_sign_xml_2020_04`, `sb_dti.dbo.dti_sign_xml_2020_05`, `sb_dti.dbo.dti_sign_xml_2020_06`, `sb_dti.dbo.dti_sign_xml_2020_07`, `sb_dti.dbo.dti_sign_xml_2020_08`, `sb_dti.dbo.dti_sign_xml_2020_09`, `sb_dti.dbo.dti_sign_xml_2020_10`, `sb_dti.dbo.dti_sign_xml_2020_11`, `sb_dti.dbo.dti_sign_xml_2020_12`, `sb_dti.dbo.dti_sign_xml_2021_01`, `sb_dti.dbo.dti_sign_xml_2021_02`, `sb_dti.dbo.dti_sign_xml_2021_03`, `sb_dti.dbo.dti_sign_xml_2021_04`, `sb_dti.dbo.dti_sign_xml_2021_05`, `sb_dti.dbo.dti_sign_xml_2021_06`, `sb_dti.dbo.dti_sign_xml_2021_07`, `sb_dti.dbo.dti_sign_xml_2021_08`, `sb_dti.dbo.dti_sign_xml_2021_09`, `sb_dti.dbo.dti_sign_xml_2021_10`, `sb_dti.dbo.dti_sign_xml_2021_11`, `sb_dti.dbo.dti_sign_xml_2021_12`, `sb_dti.dbo.dti_sign_xml_2022_01`, `sb_dti.dbo.dti_sign_xml_2022_02`, `sb_dti.dbo.dti_sign_xml_2022_03`, `sb_dti.dbo.dti_sign_xml_2022_04`, `sb_dti.dbo.dti_sign_xml_2022_05`, `sb_dti.dbo.dti_sign_xml_2022_06`, `sb_dti.dbo.dti_sign_xml_2022_07`, `sb_dti.dbo.dti_sign_xml_2022_08`, `sb_dti.dbo.dti_sign_xml_2022_09`, `sb_dti.dbo.dti_sign_xml_2022_10`, `sb_dti.dbo.dti_sign_xml_2022_11`, `sb_dti.dbo.dti_sign_xml_2022_12`, `sb_dti.dbo.dti_sign_xml_2023_01`, `sb_dti.dbo.dti_sign_xml_2023_02`, `sb_dti.dbo.dti_sign_xml_2023_03`, `sb_dti.dbo.dti_sign_xml_2023_04`, `sb_dti.dbo.dti_sign_xml_2023_05`, `sb_dti.dbo.dti_sign_xml_2023_06`, `sb_dti_dw.dbo.dti_sign`, `sb_dti_dw.dbo.dti_sign_cub`, `sb_dti_dw.dbo.dti_sign_xml` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getDtiXml](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L416) — 바인딩: `dtiIdx`, `dtiWday`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE
```

하위 프로시저·함수·뷰: `master.dbo.clr_dec_lob_sel`, `master.dbo.dec_lob_sel`, `sb_dti_dw.dbo.dti_sign`, `sb_dti_dw.dbo.dti_sign_cub`, `sb_dti_dw.dbo.dti_sign_xml`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db163"></a>
## SB_DTI_DW.sys.schemas

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | VIEW / 2014-02-20T20:48:38.923 |
| 읽기·참조 객체 | `sb_dti_dw.sys.schemas` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findStandaloneArchives](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L428) — 바인딩: . 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT JOIN sys.syssingleobjrefs r ON r.depid = s.id AND r.class = 50 AND r.depsubid = 0
WHERE s.class = 50
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db164"></a>
## SB_DTI_DW.sys.tables

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | VIEW / 2014-02-20T20:48:38.667 |
| 읽기·참조 객체 | `sb_dti_dw.sys.objects`, `sb_dti_dw.sys.tables` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findStandaloneArchives](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L428) — 바인딩: . 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
convert(bit, CASE WHEN EXISTS (SELECT 1 FROM sys.sysmultiobjrefs WHERE depid = o.object_id AND class = 27  ) THEN 1 ELSE 0 END) AS is_remote_data_archive_enabled,
then ISNULL((select value from sys.sysobjvalues where valclass = 123 and objid = o.object_id and valnum = 0), -1)
then ISNULL((select value from sys.sysobjvalues where valclass = 123 and objid = o.object_id and valnum = 1), -1)
case when exists (select value from sys.sysobjvalues where valclass = 123 and objid = o.object_id and valnum = 1)
case (select ISNULL(value, -1) from sys.sysobjvalues where valclass = 123 and objid = o.object_id and valnum = 1)
LEFT JOIN sys.sysidxstats lob ON lob.id = o.object_id AND lob.indid <= 1
LEFT JOIN sys.syssingleobjrefs ds ON ds.depid = o.object_id AND ds.class = 8 AND ds.depsubid <= 1
LEFT JOIN sys.syssingleobjrefs rfs ON rfs.depid = o.object_id AND rfs.class = 42 AND rfs.depsubid = 0
LEFT JOIN sys.syssingleobjrefs ct ON ct.indepid = o.object_id AND ct.class = 112
LEFT JOIN sys.syssingleobjrefs ht ON ht.depid = o.object_id AND ht.class = 112
LEFT JOIN sys.syspalvalues ts ON ts.class = 'LEOP' AND ts.value = o.lock_escalation_option
LEFT JOIN sys.syspalvalues d ON d.class = 'DOPT' AND d.value = o.durability_option
WHERE o.type = 'U'
```

하위 프로시저·함수·뷰: `sb_dti_dw.sys.objects`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db165"></a>
## SB_DTI_LOG.dbo.DORMANT_MEMBER

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `dormant_no` | `int` | 불가 | 예 |
| `mem_no` | `int` | 불가 | 아니오 |
| `com_no` | `int` | 허용 | 아니오 |
| `mem_name` | `varchar(200)` | 허용 | 아니오 |
| `mem_realname` | `varchar(35)` | 허용 | 아니오 |
| `mem_regno` | `varchar(13)` | 불가 | 아니오 |
| `mem_id` | `varchar(12)` | 불가 | 아니오 |
| `mem_pw` | `varchar(35)` | 불가 | 아니오 |
| `mem_type` | `varchar(1)` | 불가 | 아니오 |
| `mem_tel` | `varchar(40)` | 불가 | 아니오 |
| `mem_hp` | `varchar(40)` | 허용 | 아니오 |
| `mem_email` | `varchar(200)` | 허용 | 아니오 |
| `mem_status` | `varchar(1)` | 허용 | 아니오 |
| `mem_entry_date` | `datetime` | 허용 | 아니오 |
| `mem_del_yn` | `varchar(1)` | 허용 | 아니오 |
| `mem_modify_date` | `datetime` | 허용 | 아니오 |
| `Tstamp` | `timestamp` | 불가 | 아니오 |
| `isVirtualYN` | `varchar(1)` | 불가 | 아니오 |
| `name_display_yn` | `varchar(1)` | 허용 | 아니오 |
| `resultmail_send_yn` | `varchar(1)` | 허용 | 아니오 |
| `infomail_receive_yn` | `varchar(1)` | 허용 | 아니오 |
| `mem_fax` | `varchar(40)` | 허용 | 아니오 |
| `INFORSMS_RECEIVE_YN` | `char(1)` | 허용 | 아니오 |
| `SHARP_MAIL` | `varchar(150)` | 허용 | 아니오 |
| `restore_channel` | `varchar(10)` | 허용 | 아니오 |
| `restore_date` | `datetime` | 허용 | 아니오 |
| `restore_yn` | `varchar(1)` | 허용 | 아니오 |
| `cdate` | `datetime` | 허용 | 아니오 |
| `last_login` | `datetime` | 허용 | 아니오 |
| `Tel_Receive_YN` | `varchar(1)` | 허용 | 아니오 |
| `SHA_PW` | `varchar(70)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-02-09T22:52:41.380 |
| 읽기·참조 객체 | `sb_dti_log.dbo.dormant_member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getDormantMemberNos](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L359) — 바인딩: `comNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findSensitiveValue](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankMemberMapper.kt#L82) — 바인딩: `memNo`, `memNo`, `memNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db166"></a>
## SB_DTI_LOG.dbo.upWebHook_SAVE_COMPANY_LINK_INFO_ADMIN

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ROUTINGURL` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PORT` | `varchar(5)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CONTEXT` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@STARTROUTINGDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ENDROUTINGDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ACTIVE_YN` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BIZ_USER` | `varchar(12)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ERR_CODE` | `varchar(5)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2021-02-17T11:34:21.357 |
| 읽기·참조 객체 | `sb_dti_log.dbo.oapi_webhook_company_link_info`, `smartbill3.dbo.company` |
| 쓰기 대상 | `sb_dti_log.dbo.oapi_webhook_company_link_info` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [registerWebhook](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L1092) — 바인딩: `comNo`, `routingUrl`, `port`, `context`, `startDate`, `endDate`, `activeYn`, `bizUser`, `errCode, mode=OUT, jdbcType=VARCHAR`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @ERR_CODE = '30000'
WHERE
SMARTBILL3..COMPANY WITH(NOLOCK) WHERE COM_NO = @COM_NO
SET @ERR_CODE = '40000'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db167"></a>
## SB_DTI_LOG.dbo.upWebHook_SELECT_COMPANY_LINK_INFO_USER

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_REGNO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2021-02-17T16:49:34.657 |
| 읽기·참조 객체 | `sb_dti_log.dbo.oapi_webhook_company_link_info`, `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getWebhookConfig](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L793) — 바인딩: `comRegno`. 결과 매핑: `ROUTINGURL` → `routingUrl`, `PORT` → `port`, `CONTEXT` → `context`, `STARTROUTINGDATE` → `startRoutingDate`, `ENDROUTINGDATE` → `endRoutingDate`, `ACTIVE_YN` → `activeYn`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT JOIN	SmartBill3..COMPANY  COM WITH(NOLOCK)
WHERE
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db168"></a>
## SB_SCRAPER.dbo.SSP_CERT_EXPIRE_VIEW

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@HUB_NAME` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_NAME` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_REGNO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROMDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TODATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2017-04-24T11:43:31.267 |
| 읽기·참조 객체 | `sb_scraper.dbo.use_company_detail`, `sb_scraper.dbo.use_company_info` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchExpiries](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/CertificateExpireMapper.kt#L34) — 바인딩: `hubName`, `comName`, `comRegno`, `fromDate`, `toDate`. 결과 매핑: `HUB_NAME` → `hubName`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `CERT_EXPIRE` → `certExpire`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SQL = 'SELECT A.HUB_NAME,B.COM_NAME,B.COM_REGNO,B.CERT_EXPIRE
LEFT OUTER JOIN USE_COMPANY_DETAIL B
WHERE CERT_EXPIRE BETWEEN
SET @SQL = @SQL +
SET @SQL = @SQL +
SET @SQL = @SQL +
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db169"></a>
## SB_SCRAPER.dbo.SSP_CERT_LOGIN_FAIL_LIST

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@START_DAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DIVISION` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2021-03-29T16:29:43.073 |
| 읽기·참조 객체 | `sb_scraper.dbo.use_company_detail`, `sb_scraper.dbo.use_company_detail_his`, `sb_scraper.dbo.use_company_info`, `sb_scraper.dbo.use_log` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchLoginFails](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/CertificateLoginFailMapper.kt#L34) — 바인딩: `startDay`, `division`. 결과 매핑: `DIVISION` → `division`, `HUB_REALNAME` → `hubRealname`, `COM_REGNO` → `comRegno`, `COM_NAME` → `comName`, `LOG_DATE` → `logDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
INNER JOIN
(SELECT MAX(IDX) AS IDX, COM_REGNO FROM USE_COMPANY_DETAIL_HIS WITH(NOLOCK) GROUP BY COM_REGNO) UCM
INNER JOIN USE_COMPANY_DETAIL_HIS UDH WITH(NOLOCK) ON UCM.IDX = UDH.IDX AND UDH.COM_REGNO = UCM.COM_REGNO	) B
INNER JOIN
WHERE ERR_CODE = '99998'
GROUP BY SB_KEY,COM_REGNO
WHERE
ORDER BY LOG_DATE ASC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db170"></a>
## SB_SCRAPER.dbo.SSP_DETAIL_USE_COMPANY

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@SB_KEY` | `varchar(36)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2019-02-15T14:10:12.843 |
| 읽기·참조 객체 | `office.dbo.business`, `office.dbo.function_code`, `office.dbo.mng_hub`, `sb_scraper.dbo.use_company_detail`, `sb_scraper.dbo.use_company_info` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findDetail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/AuthKeyMapper.kt#L84) — 바인딩: `sbKey`. 결과 매핑: `SB_KEY` → `sbKey`, `HUB_NAME` → `hubName`, `USE_YN` → `useYn`, `DIVISION` → `division`, `COM_REGNO` → `comRegno`, `COM_NAME` → `comName`, `CERT_EXPIRE` → `certExpire`, `HUB_REALNAME` → `hubRealname`, `CLASS` → `klass`, `OLD_NEW` → `oldNew`, `BNS_ID` → `bnsId`, `BNS_SITE` → `bnsSite`, `BNS_PRODUCT` → `bnsProduct`, `EP_SDATE` → `epSdate`, `EP_EDATE` → `epEdate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT OUTER JOIN OFFICE..MNG_HUB H WITH (NOLOCK) ON A.BNS_ID = H.HUB_ID
LEFT OUTER JOIN OFFICE..BUSINESS C WITH (NOLOCK) ON H.BNS_ID = C.BNS_ID
LEFT OUTER JOIN USE_COMPANY_DETAIL B WITH(NOLOCK) ON A.SB_KEY = B.SB_KEY
WHERE
ORDER BY B.COM_REGNO ASC
```

하위 프로시저·함수·뷰: `office.dbo.hubproduct`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db171"></a>
## SB_SCRAPER.dbo.SSP_EP_ESERO_DETAIL

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@KEY` | `varchar(36)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@START` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@END` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PAGENUM` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PAGESIZE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISERROR` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_REGNO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2019-02-20T17:22:24.027 |
| 읽기·참조 객체 | `sb_scraper.dbo.ep_use_log` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchDetail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/EmailParsingMonitoringMapper.kt#L82) — 바인딩: `key`, `startDate`, `endDate`, `pageNum`, `pageSize`, `isError`, `comRegno`. 결과 매핑: `COM_REGNO` → `comRegno`, `LOG_TITLE` → `logTitle`, `LOG_CONTENT` → `logContent`, `LOG_DATE` → `logDate`, `ERR_CODE` → `errCode`, `ERR_MESSAGE` → `errMessage`, `ISSUE_ID` → `issueId`, `TOT_CNT` → `totCnt`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @PAGES = CONVERT(VARCHAR,((@PAGENUM -1) * @PAGESIZE) + 1)
SET @PAGEE = CONVERT(VARCHAR,(@PAGENUM * @PAGESIZE))
SET @SQL = N'
ROW_NUMBER() OVER(ORDER BY LOG_DATE ASC) AS ROWNUM
WHERE SB_KEY = @PKEY AND LOG_DATE BETWEEN @PSTART AND @PEND
SET @SQL = @SQL + N' AND ERR_CODE != ''Y'' '
SET @SQL = @SQL + N' AND COM_REGNO = @PCOM_REGNO '
SET @SQL = @SQL + N'
WHERE
SET @PARAM = N'@PKEY VARCHAR(36), @PSTART DATETIME, @PEND DATETIME, @PAGES INT, @PAGEE INT, @PCOM_REGNO VARCHAR(10)'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db172"></a>
## SB_SCRAPER.dbo.SSP_EP_ESERO_MONITOR_AUTO

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@START` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@END` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@HUBNAME` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@USEYN` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISUSE` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISERROR` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISDIV` | `varchar(6)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISCLASS` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2019-02-22T13:12:10.860 |
| 읽기·참조 객체 | `sb_scraper.dbo.ep_use_log`, `sb_scraper.dbo.use_company_info` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchAuto](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/EmailParsingMonitoringMapper.kt#L47) — 바인딩: `startDate`, `endDate`, `hubName`, `useYn`, `isUse`, `isError`, `isDiv`, `isClass`. 결과 매핑: `SB_KEY` → `sbKey`, `HUB_REALNAME` → `hubRealname`, `START_DAY` → `startDay`, `END_DAY` → `endDay`, `ERR_CNT` → `errCnt`, `MODE` → `mode`, `DIVISION` → `division`, `USE_YN` → `useYn`, `CLASS` → `klass`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SQL1 = N'
LEFT OUTER JOIN
WHERE
GROUP BY A.SB_KEY,A.SGUID,A.LOG_DATE
WHERE
GROUP BY B.SB_KEY,B.SGUID,B.LOG_DATE
GROUP BY TOT.SB_KEY
LEFT OUTER JOIN
WHERE
GROUP BY
WHERE 1=1
SET @SQL1 = @SQL1 + N' ORDER BY HUB_REALNAME,START_DAY ASC'
SET @PARMDEFINITION = N'@PSTART DATETIME, @PEND DATETIME, @PNAME VARCHAR(50), @PDIV VARCHAR(6), @PCLASS CHAR(1)';
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db173"></a>
## SB_SCRAPER.dbo.SSP_ERROR_LOG

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@STARTDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ENDDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@HUB_NAME` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@NUM` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:46:15.320 |
| 읽기·참조 객체 | `sb_scraper.dbo.error_log`, `sb_scraper.dbo.use_company_info` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchErrorLogs](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/ErrorLogMapper.kt#L38) — 바인딩: `startDate`, `endDate`, `hubName`, `num`. 결과 매핑: `NUM` → `num`, `HUB_NAME` → `hubName`, `ERROR_MESSAGE` → `errorMessage`, `CDATE` → `cdate`, `SB_KEY` → `sbKey`, `ERROR_SOURCE` → `errorSource`, `ERROR_STACKTRACE` → `errorStacktrace`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
ORDER BY A.CDATE ASC)AS NUM,
LEFT OUTER JOIN USE_COMPANY_INFO B
WHERE
WHERE
ORDER BY CDATE DESC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db174"></a>
## SB_SCRAPER.dbo.SSP_ESERO_DETAIL

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@KEY` | `varchar(36)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SGUID` | `varchar(36)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@START` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@END` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PAGENUM` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PAGESIZE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISERROR` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_REGNO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2023-04-12T09:42:02.513 |
| 읽기·참조 객체 | `sb_scraper.dbo.use_log` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchDetail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/EseroMonitoringMapper.kt#L87) — 바인딩: `key`, `sguid`, `startDate`, `endDate`, `pageNum`, `pageSize`, `isError`, `comRegno`. 결과 매핑: `COM_REGNO` → `comRegno`, `LOG_TITLE` → `logTitle`, `LOG_CONTENT` → `logContent`, `LOG_DATE` → `logDate`, `ERR_CODE` → `errCode`, `ERR_MESSAGE` → `errMessage`, `ISSUE_ID` → `issueId`, `TOT_CNT` → `totCnt`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @PAGES = CONVERT(VARCHAR,((@PAGENUM -1) * @PAGESIZE) + 1)
SET @PAGEE = CONVERT(VARCHAR,(@PAGENUM * @PAGESIZE))
SET @END = DATEADD(HH, 3, @END)
SET @SQL = N'
ROW_NUMBER() OVER(ORDER BY LOG_DATE ASC) AS ROWNUM,
WHERE
SET @SQL = @SQL + N' AND ERR_CODE != ''Y'' '
SET @SQL = @SQL + N' AND COM_REGNO = @PCOM_REGNO '
SET @SQL = @SQL + N'
WHERE
SET @PARAM = N'@PKEY VARCHAR(36), @PSGUID VARCHAR(36), @PSTART DATETIME, @PEND DATETIME, @PAGES INT, @PAGEE INT, @PCOM_REGNO VARCHAR(10)'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db175"></a>
## SB_SCRAPER.dbo.SSP_ESERO_MONITOR_AUTO

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@START` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@END` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@HUBNAME` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@USEYN` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISUSE` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISERROR` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISDIV` | `varchar(6)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISCLASS` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2023-07-25T20:24:44.020 |
| 읽기·참조 객체 | `sb_scraper.dbo.use_company_info`, `sb_scraper.dbo.use_log` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchAuto](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/EseroMonitoringMapper.kt#L45) — 바인딩: `startDate`, `endDate`, `hubName`, `useYn`, `isUse`, `isError`, `isDiv`, `isClass`. 결과 매핑: `SB_KEY` → `sbKey`, `HUB_REALNAME` → `hubRealname`, `SGUID` → `sguid`, `START_DAY` → `startDay`, `END_DAY` → `endDay`, `ERR_CNT` → `errCnt`, `MODE` → `mode`, `DIVISION` → `division`, `USE_YN` → `useYn`, `CLASS` → `klass`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SQL1 = N'
LEFT OUTER JOIN
WHERE
GROUP BY A.SB_KEY,A.SGUID,A.LOG_DATE, A.CONTENT_CODE
GROUP BY TOT.SB_KEY,TOT.SGUID
LEFT OUTER JOIN
WHERE
GROUP BY
WHERE 1=1
SET @SQL1 = @SQL1 + N' ORDER BY HUB_REALNAME,START_DAY ASC'
SET @PARMDEFINITION = N'@PSTART DATETIME, @PEND DATETIME, @PNAME VARCHAR(50), @PDIV VARCHAR(6), @PCLASS CHAR(1)';
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db176"></a>
## SB_SCRAPER.dbo.SSP_ESERO_MONITOR_MANUAL

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@START` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@END` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@HUBNAME` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@USEYN` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISERROR` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISDIV` | `varchar(6)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISCLASS` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2023-07-25T20:53:59.460 |
| 읽기·참조 객체 | `sb_scraper.dbo.use_company_info`, `sb_scraper.dbo.use_log` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchManual](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/EseroMonitoringMapper.kt#L67) — 바인딩: `startDate`, `endDate`, `hubName`, `useYn`, `isError`, `isDiv`, `isClass`. 결과 매핑: `SB_KEY` → `sbKey`, `HUB_REALNAME` → `hubRealname`, `SGUID` → `sguid`, `START_DAY` → `startDay`, `END_DAY` → `endDay`, `ERR_CNT` → `errCnt`, `MODE` → `mode`, `DIVISION` → `division`, `USE_YN` → `useYn`, `CLASS` → `klass`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SQL2 =N'
WHERE
GROUP BY A.SB_KEY,SGUID, A.LOG_DATE
WHERE LOG_DATE BETWEEN @PSTART AND @PEND
GROUP BY B.SB_KEY,SGUID,B.LOG_DATE
WHERE LOG_DATE BETWEEN @PSTART AND @PEND
GROUP BY C.SB_KEY,SGUID,C.LOG_DATE
GROUP BY TOT.SB_KEY, TOT.SGUID
INNER JOIN USE_COMPANY_INFO COM WITH(NOLOCK)
LEFT OUTER JOIN
WHERE
WHERE 1=1
AND COM.HUB_REALNAME LIKE ''%''+@PNAME+''%'' ORDER BY START_DAY ASC'
ELSE N' ORDER BY START_DAY ASC'
SET @PARMDEFINITION = N'@PSTART DATETIME, @PEND DATETIME, @PNAME VARCHAR(50),@PDIV VARCHAR(6), @PCLASS CHAR(1)';
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db177"></a>
## SB_SCRAPER.dbo.SSP_INSERT_USE_COMPANY

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@HUB_NAME` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DIVISION` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CLASS` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@OLDNEW` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BNS_ID` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CUSER` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@EP_SDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@EP_EDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@OUT_INSERT_YN` | `varchar(1)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2019-02-22T17:32:42.320 |
| 읽기·참조 객체 | `sb_scraper.dbo.use_company_info` |
| 쓰기 대상 | `sb_scraper.dbo.use_company_info` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [insertAuthKey](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/AuthKeyMapper.kt#L114) — 바인딩: `hubName`, `division`, `klass`, `oldNew`, `bnsId`, `cuser`, `epSdate`, `epEdate`, `result, mode=OUT, jdbcType=VARCHAR`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @OUT_INSERT_YN = 'N'
WHERE
SET @OUT_INSERT_YN = 'Y'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db178"></a>
## SB_SCRAPER.dbo.SSP_UPDATE_USE_COMPANY

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@HUBNAME` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DIVISION` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@HUB_REALNAME` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISUSE` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CLASS` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@OLD_NEW` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BNS_ID` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@UUSER` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@EP_SDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@EP_EDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2019-02-15T13:59:37.387 |
| 읽기·참조 객체 | `sb_scraper.dbo.use_company_info` |
| 쓰기 대상 | `sb_scraper.dbo.use_company_info` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [updateAuthKey](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/AuthKeyMapper.kt#L122) — 바인딩: `hubName`, `division`, `hubRealname`, `useYn`, `klass`, `oldNew`, `bnsId`, `uuser`, `epSdate`, `epEdate`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE HUB_NAME = @HUBNAME
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db179"></a>
## SB_SCRAPER.dbo.SSP_UseHubManager_List

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@SB_KEY` | `varchar(36)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2017-02-22T09:25:56.637 |
| 읽기·참조 객체 | `office.dbo.hub_engineer` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findManagers](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/AuthKeyMapper.kt#L95) — 바인딩: `sbKey`. 결과 매핑: `ENG_NAME` → `engName`, `ENG_EMAIL` → `engEmail`, `ENG_TEL` → `engTel`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE ROUTINGURL = @SB_KEY
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db180"></a>
## SB_SCRAPER.dbo.SSP_VIEW_BILL_MANAGEMENT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@FROM_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TO_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SCRAPHUB_NAME` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_REGNO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_NAME` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@USECOUNT` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@HUB_NAME` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SW_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CLASS` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2017-04-07T10:40:46.787 |
| 읽기·참조 객체 | `office.dbo.business`, `office.dbo.mng_hub`, `office.dbo.sawon`, `sb_bill.dbo.dti_share_auto_charge`, `sb_scraper.dbo.use_company_detail`, `sb_scraper.dbo.use_company_info`, `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchRegistrations](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/CertificateRegistrationMapper.kt#L45) — 바인딩: `fromDate`, `toDate`, `scrapHubName`, `comRegno`, `comName`, `usecount`, `hubName`, `swNo`, `klass`. 결과 매핑: `SB_KEY` → `sbKey`, `COM_REGNO` → `comRegno`, `COM_NAME` → `comName`, `HUB_NAME` → `hubName`, `HUB_REALNAME` → `hubRealname`, `CDATE` → `cdate`, `USECOUNT` → `usecount`, `BNS_SITE` → `bnsSite`, `SNAME` → `sname`, `SW_NO` → `swNo`, `CLASS` → `klass`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SQL1 = '
LEFT JOIN SB_SCRAPER..USE_COMPANY_INFO b WITH(NOLOCK) ON a.SB_KEY = b.SB_KEY
LEFT JOIN (SELECT COM_REGNO, COM_NO FROM SMARTBILL3..COMPANY WITH(NOLOCK) WHERE COM_DEL_YN = ''N'') c ON a.COM_REGNO = c.COM_REGNO
LEFT JOIN (select COMNO FROM SB_BILL.DBO.DTI_SHARE_AUTO_CHARGE WITH(NOLOCK) WHERE getdate() between [START_DATE] and [END_DATE] and CHARGE_TYPE = ''USECOUNT'') d ON d.COMNO = c.COM_NO
LEFT JOIN OFFICE..MNG_HUB H WITH(NOLOCK) ON B.BNS_ID = H.HUB_ID
LEFT OUTER JOIN (select BNS_ID, BNS_LEADER, BNS_SITE from OFFICE..BUSINESS with(nolock) where bns_product = ''03'') BI ON H.BNS_ID = BI.BNS_ID
LEFT OUTER JOIN OFFICE..SAWON S ON S.SW_NO = BI.BNS_LEADER
WHERE 1=1
SET @SQL1 = @SQL1 + CASE
SET @SQL1 = @SQL1 + CASE
SET @SQL1 = @SQL1 + CASE
SET @SQL1 = @SQL1 + CASE
SET @SQL1 = @SQL1 + CASE
SET @SQL1 = @SQL1 + CASE
SET @SQL1 = @SQL1 + CASE
SET @SQL1 = @SQL1 + CASE
SET @SQL1 = @SQL1 + ' ORDER BY CDATE DESC '
SET @PARMDEFINITION = N'@SCRAPHUB_NAME VARCHAR(50),@FROM_DATE VARCHAR(10),@TO_DATE VARCHAR(10),  @COM_REGNO VARCHAR(10), @COM_NAME VARCHAR(50), @USECOUNT CHAR(1), @HUB_NAME VARCHAR(50), @SW_NO INT, @CLASS CHAR(1) ';
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db181"></a>
## SB_SCRAPER.dbo.USE_COMPANY_INFO

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `SB_KEY` | `varchar(36)` | 불가 | 아니오 |
| `HUB_NAME` | `varchar(50)` | 불가 | 아니오 |
| `USE_YN` | `char(1)` | 불가 | 아니오 |
| `CDATE` | `datetime` | 허용 | 아니오 |
| `DIVISION` | `varchar(10)` | 허용 | 아니오 |
| `HUB_REALNAME` | `varchar(50)` | 허용 | 아니오 |
| `CLASS` | `char(1)` | 허용 | 아니오 |
| `OLD_NEW` | `char(1)` | 허용 | 아니오 |
| `BNS_ID` | `int` | 허용 | 아니오 |
| `CUSER` | `int` | 허용 | 아니오 |
| `UUSER` | `int` | 허용 | 아니오 |
| `EP_SDATE` | `varchar(10)` | 허용 | 아니오 |
| `EP_EDATE` | `varchar(10)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2019-02-15T11:39:59.170 |
| 읽기·참조 객체 | `sb_scraper.dbo.use_company_info` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findSalesRepNames](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/CertificateRegistrationMapper.kt#L68) — 바인딩: `sbKey`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findPeriods](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/EmailParsingMonitoringMapper.kt#L62) — 바인딩: `key`. 결과 매핑: `SB_KEY` → `sbKey`, `EP_SDATE` → `epSdate`, `EP_EDATE` → `epEdate`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db182"></a>
## SEC_PT.dbo.TBL_PT_CTR

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `CTR_SEQ` | `int` | 불가 | 예 |
| `CTR_NO` | `varchar(100)` | 허용 | 아니오 |
| `CTR_ADR` | `varchar(100)` | 허용 | 아니오 |
| `TX_ID` | `varchar(100)` | 허용 | 아니오 |
| `CTR_STAT` | `char(2)` | 허용 | 아니오 |
| `TRN_STAT` | `char(1)` | 허용 | 아니오 |
| `OWN_ADR` | `varchar(100)` | 허용 | 아니오 |
| `SND_ADR` | `varchar(100)` | 허용 | 아니오 |
| `RCV_ADR` | `varchar(100)` | 허용 | 아니오 |
| `BRK_SND_ADR` | `varchar(100)` | 허용 | 아니오 |
| `BRK_RCV_ADR` | `varchar(100)` | 허용 | 아니오 |
| `OWN_NM` | `nvarchar(200)` | 허용 | 아니오 |
| `SND_NM` | `nvarchar(200)` | 허용 | 아니오 |
| `RCV_NM` | `nvarchar(200)` | 허용 | 아니오 |
| `BRK_SND_NM` | `nvarchar(200)` | 허용 | 아니오 |
| `BRK_RCV_NM` | `nvarchar(200)` | 허용 | 아니오 |
| `CTR_FILE_NM` | `nvarchar(2000)` | 허용 | 아니오 |
| `CTR_FILE_HASH` | `varchar(1000)` | 허용 | 아니오 |
| `CTR_FILE_LINK` | `varchar(2000)` | 허용 | 아니오 |
| `CTR_FIN_FILE_HASH` | `varchar(1000)` | 허용 | 아니오 |
| `CTR_FIN_FILE_LINK` | `varchar(2000)` | 허용 | 아니오 |
| `ETC_FILE_GRP_ID` | `varchar(100)` | 허용 | 아니오 |
| `META_ID` | `varchar(100)` | 허용 | 아니오 |
| `CDATE` | `datetime` | 허용 | 아니오 |
| `UDATE` | `datetime` | 허용 | 아니오 |
| `SDATE` | `datetime` | 허용 | 아니오 |
| `RDATE` | `datetime` | 허용 | 아니오 |
| `CUSR_ID` | `varchar(200)` | 허용 | 아니오 |
| `UUSR_ID` | `varchar(200)` | 허용 | 아니오 |
| `CTR_TYPE` | `char(6)` | 허용 | 아니오 |
| `GROUP_ID` | `int` | 허용 | 아니오 |
| `GROUP_CTR_SEQ` | `int` | 허용 | 아니오 |
| `CTR_SYNC` | `bit` | 불가 | 아니오 |
| `CTR_LOCK_TYPE` | `int` | 허용 | 아니오 |
| `CTR_SIGN_TYPE` | `int` | 허용 | 아니오 |
| `CTR_COMT` | `varchar(200)` | 허용 | 아니오 |
| `PROC_PDF` | `char(1)` | 불가 | 아니오 |
| `RJT_MSG` | `varchar(2000)` | 허용 | 아니오 |
| `MSG_ID` | `varchar(100)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2021-04-15T19:11:24.990 |
| 읽기·참조 객체 | `sec_pt.dbo.tbl_pt_ctr` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findSensitiveValue](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/lockreset/repository/BlockchainLockMapper.kt#L74) — 바인딩: `ctrSeq`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db183"></a>
## SEC_PT.dbo.TBL_PT_CTR_LOCK

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `LOCK_SEQ` | `int` | 불가 | 예 |
| `CTR_SEQ` | `int` | 허용 | 아니오 |
| `CTR_NO` | `varchar(100)` | 허용 | 아니오 |
| `CERT_REG_NO` | `varchar(100)` | 허용 | 아니오 |
| `CERT_PUB_KEY` | `varchar(100)` | 허용 | 아니오 |
| `PSN_NM` | `varchar(100)` | 허용 | 아니오 |
| `PSN_NO` | `varchar(100)` | 허용 | 아니오 |
| `PSN_CI` | `varchar(100)` | 허용 | 아니오 |
| `PW_PIN` | `varchar(100)` | 허용 | 아니오 |
| `FAIL_CNT` | `int` | 허용 | 아니오 |
| `ACQ_DATE` | `datetime` | 허용 | 아니오 |
| `CDATE` | `datetime` | 허용 | 아니오 |
| `UDATE` | `datetime` | 허용 | 아니오 |
| `CUSR_ID` | `varchar(200)` | 허용 | 아니오 |
| `UUSR_ID` | `varchar(200)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2021-04-15T19:11:24.990 |
| 읽기·참조 객체 | `sec_pt.dbo.tbl_pt_ctr_lock` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findSensitiveValue](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/lockreset/repository/BlockchainLockMapper.kt#L74) — 바인딩: `ctrSeq`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db184"></a>
## SEC_PT.dbo.TBL_PT_ORG

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `ORG_SEQ` | `int` | 불가 | 예 |
| `ORG_NM` | `nvarchar(1000)` | 허용 | 아니오 |
| `CN_ADR` | `varchar(100)` | 허용 | 아니오 |
| `ORG_REG_NO` | `varchar(100)` | 허용 | 아니오 |
| `PRE_NM` | `nvarchar(100)` | 허용 | 아니오 |
| `ORG_ADR` | `nvarchar(2000)` | 허용 | 아니오 |
| `ORG_EMAIL` | `nvarchar(2000)` | 허용 | 아니오 |
| `ORG_CTR` | `nvarchar(100)` | 허용 | 아니오 |
| `TOTAL_AMT` | `int` | 허용 | 아니오 |
| `INFX_CODE` | `varchar(100)` | 허용 | 아니오 |
| `CDATE` | `datetime` | 허용 | 아니오 |
| `UDATE` | `datetime` | 허용 | 아니오 |
| `CUSR_ID` | `varchar(200)` | 허용 | 아니오 |
| `UUSR_ID` | `varchar(200)` | 허용 | 아니오 |
| `CN_PUB` | `bit` | 허용 | 아니오 |
| `TMP` | `bit` | 허용 | 아니오 |
| `USR_SW_ID` | `varchar(100)` | 허용 | 아니오 |
| `USR_SW_YN` | `bit` | 허용 | 아니오 |
| `ORG_CERT` | `bit` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2022-03-24T15:07:21.190 |
| 읽기·참조 객체 | `sec_pt.dbo.tbl_pt_org` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findBusinessNumber](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/company/repository/GlosignCompanyMapper.kt#L86) — 바인딩: `orgSeq`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findOrganizationRegistrationNumbers](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/member/repository/GlosignMemberMapper.kt#L57) — 바인딩: `usrSeq`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db185"></a>
## SEC_PT.dbo.TBL_PT_ORG_USR

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `OU_SEQ` | `int` | 불가 | 예 |
| `ORG_SEQ` | `int` | 불가 | 아니오 |
| `USR_SEQ` | `int` | 불가 | 아니오 |
| `ADM` | `bit` | 허용 | 아니오 |
| `CT_DATE` | `datetime` | 허용 | 아니오 |
| `CDATE` | `datetime` | 허용 | 아니오 |
| `UDATE` | `datetime` | 허용 | 아니오 |
| `CUSR_ID` | `varchar(200)` | 허용 | 아니오 |
| `UUSR_ID` | `varchar(200)` | 허용 | 아니오 |
| `ATV` | `bit` | 허용 | 아니오 |
| `TEAM_ID` | `int` | 허용 | 아니오 |
| `USR_EMAIL` | `nvarchar(1000)` | 불가 | 아니오 |
| `CADM` | `bit` | 불가 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2021-04-15T13:48:23.160 |
| 읽기·참조 객체 | `sec_pt.dbo.tbl_pt_org_usr` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findOrganizationRegistrationNumbers](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/member/repository/GlosignMemberMapper.kt#L57) — 바인딩: `usrSeq`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findCompanyAdmin](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/company/repository/GlosignCompanyMapper.kt#L108) — 바인딩: `orgSeq`. 결과 매핑: `ORG_SEQ` → `orgSeq`, `USR_SEQ` → `usrSeq`, `USR_NM` → `usrNm`, `USR_EMAIL` → `usrEmail`, `CADM` → `cadm`, `ATV` → `atv`, `CDATE` → `cdate`.
- [findCompanyUserValue](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/company/repository/GlosignCompanyMapper.kt#L122) — 바인딩: `orgSeq`, `usrSeq`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db186"></a>
## SEC_PT.dbo.TBL_PT_USR

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `USR_SEQ` | `int` | 불가 | 예 |
| `USR_ID` | `varchar(200)` | 불가 | 아니오 |
| `USR_PW` | `varchar(200)` | 불가 | 아니오 |
| `USR_NM` | `nvarchar(200)` | 허용 | 아니오 |
| `USR_ADR` | `nvarchar(2000)` | 허용 | 아니오 |
| `CN_ADR` | `varchar(100)` | 허용 | 아니오 |
| `USR_EMAIL` | `nvarchar(450)` | 허용 | 아니오 |
| `USR_CTR` | `nvarchar(max)` | 허용 | 아니오 |
| `TMP` | `bit` | 허용 | 아니오 |
| `CDATE` | `datetime` | 허용 | 아니오 |
| `UDATE` | `datetime` | 허용 | 아니오 |
| `CN_PUB` | `bit` | 허용 | 아니오 |
| `TERM_CTR_MAIL` | `bit` | 허용 | 아니오 |
| `TERM_MAIL` | `bit` | 허용 | 아니오 |
| `DEV` | `bit` | 허용 | 아니오 |
| `CUSR_ID` | `varchar(200)` | 허용 | 아니오 |
| `UUSR_ID` | `varchar(200)` | 허용 | 아니오 |
| `USR_SW_ID` | `varchar(100)` | 허용 | 아니오 |
| `USR_SW_YN` | `bit` | 허용 | 아니오 |
| `TERM_USR_SW` | `bit` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2021-10-05T15:00:23.543 |
| 읽기·참조 객체 | `sec_pt.dbo.tbl_pt_usr` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findUserValue](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/member/repository/GlosignMemberMapper.kt#L75) — 바인딩: `usrSeq`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findCompanyAdmin](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/company/repository/GlosignCompanyMapper.kt#L108) — 바인딩: `orgSeq`. 결과 매핑: `ORG_SEQ` → `orgSeq`, `USR_SEQ` → `usrSeq`, `USR_NM` → `usrNm`, `USR_EMAIL` → `usrEmail`, `CADM` → `cadm`, `ATV` → `atv`, `CDATE` → `cdate`.
- [findCompanyUserValue](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/company/repository/GlosignCompanyMapper.kt#L122) — 바인딩: `orgSeq`, `usrSeq`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db187"></a>
## SMARTBILL3.dbo.ACCINFO_CANCEL

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `idx` | `int` | 불가 | 예 |
| `order_id` | `varchar(64)` | 허용 | 아니오 |
| `acc_amt` | `money` | 허용 | 아니오 |
| `camount` | `money` | 허용 | 아니오 |
| `com_no` | `int` | 허용 | 아니오 |
| `mem_no` | `int` | 허용 | 아니오 |
| `settle_type` | `varchar(1)` | 허용 | 아니오 |
| `pay_method` | `varchar(2)` | 허용 | 아니오 |
| `prepay_no` | `int` | 허용 | 아니오 |
| `prepay_dti_no` | `int` | 허용 | 아니오 |
| `cdate` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2014-11-12T20:23:39.413 |
| 읽기·참조 객체 | `smartbill3.dbo.accinfo_cancel` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findCancellerName](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/banktransfercancel/repository/BankTransferCancelMapper.kt#L42) — 바인딩: `idx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db188"></a>
## SMARTBILL3.dbo.ACCOUNT_BULK

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `IDX` | `int` | 불가 | 예 |
| `COM_NO` | `int` | 허용 | 아니오 |
| `ISSUE_DATE` | `datetime` | 허용 | 아니오 |
| `BANK_CODE` | `char(2)` | 허용 | 아니오 |
| `BANK_REGNO` | `varchar(30)` | 불가 | 아니오 |
| `SW_NO` | `int` | 허용 | 아니오 |
| `STATUS` | `char(2)` | 허용 | 아니오 |
| `CREATE_DATE` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2014-11-12T20:44:48.680 |
| 읽기·참조 객체 | `smartbill3.dbo.account_bulk` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findRevealAccountNumber](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/bulkaccountdeposit/repository/BulkAccountDepositMapper.kt#L40) — 바인딩: `idx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db189"></a>
## SMARTBILL3.dbo.ACCOUNT_BULK_APP

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `IDX` | `int` | 불가 | 예 |
| `ACCINFO_IDX` | `int` | 허용 | 아니오 |
| `PAYMENT_DATE` | `datetime` | 허용 | 아니오 |
| `BANK_CODE` | `varchar(2)` | 허용 | 아니오 |
| `BANK_REGNO` | `varchar(50)` | 허용 | 아니오 |
| `AMOUT_PAYABLE` | `money` | 허용 | 아니오 |
| `STATUS` | `char(1)` | 허용 | 아니오 |
| `COMPLETION_DATE` | `datetime` | 허용 | 아니오 |
| `DESCRIPTION` | `varchar(200)` | 허용 | 아니오 |
| `SW_NO` | `int` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2014-11-12T20:42:13.343 |
| 읽기·참조 객체 | `smartbill3.dbo.account_bulk_app` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findRevealAccountNumber](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/bulkaccountdeposit/repository/BulkAccountDepositMapper.kt#L40) — 바인딩: `idx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db190"></a>
## SmartBill3.dbo.CMS_ACCOUNT

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `IDX` | `int` | 불가 | 예 |
| `Com_No` | `int` | 불가 | 아니오 |
| `Mem_No` | `int` | 허용 | 아니오 |
| `Bank_Code` | `varchar(2)` | 불가 | 아니오 |
| `Bank_AccNo` | `varchar(16)` | 허용 | 아니오 |
| `Bank_Regno` | `varchar(13)` | 허용 | 아니오 |
| `Bank_AccName` | `varchar(70)` | 허용 | 아니오 |
| `Bank_AccState` | `varchar(1)` | 허용 | 아니오 |
| `Wdate` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | VIEW / 2016-09-02T21:48:32.833 |
| 읽기·참조 객체 | `smartbill3.dbo.cms_account`, `smartbill3.dbo.cms_account_cub` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findCmsAccountNumber](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L629) — 바인딩: `comNo`, `accountId`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

하위 프로시저·함수·뷰: `master.dbo.clr_dec_char_sel_tc`, `master.dbo.dec_char_sel_tc`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db191"></a>
## SmartBill3.dbo.CMS_ACCOUNT_EB11

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `IDX` | `int` | 불가 | 예 |
| `Com_No` | `int` | 불가 | 아니오 |
| `Mem_No` | `int` | 허용 | 아니오 |
| `Bank_Code` | `varchar(2)` | 불가 | 아니오 |
| `Bank_AccNo` | `varchar(16)` | 허용 | 아니오 |
| `Bank_Regno` | `varchar(13)` | 허용 | 아니오 |
| `Bank_AccName` | `varchar(70)` | 허용 | 아니오 |
| `Bank_AccState` | `varchar(1)` | 허용 | 아니오 |
| `Wdate` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | VIEW / 2018-08-08T14:25:49.907 |
| 읽기·참조 객체 | `smartbill3.dbo.cms_account_eb11`, `smartbill3.dbo.cms_account_eb11_cub` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findCmsAccountNumber](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L629) — 바인딩: `comNo`, `accountId`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

하위 프로시저·함수·뷰: `master.dbo.clr_dec_char_sel_tc`, `master.dbo.dec_char_sel_tc`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db192"></a>
## SMARTBILL3.dbo.CMS_EA14

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `IDX` | `int` | 불가 | 예 |
| `File_Appdate` | `varchar(6)` | 허용 | 아니오 |
| `EA14File_Name` | `varchar(8)` | 허용 | 아니오 |
| `New_Cnt` | `int` | 허용 | 아니오 |
| `Mod_Cnt` | `int` | 허용 | 아니오 |
| `End_Cnt` | `int` | 허용 | 아니오 |
| `EndOwn_Cnt` | `int` | 허용 | 아니오 |
| `Total_Cnt` | `int` | 허용 | 아니오 |
| `Write_Yn` | `char(1)` | 허용 | 아니오 |
| `Cret_Date` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2014-11-12T20:44:26.190 |
| 읽기·참조 객체 | `smartbill3.dbo.cms_ea14` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchEb14Detail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) — 바인딩: `idx`, `resultCode`, `resultCode`. 결과 매핑: `IDX` → `idx`, `DETAIL_WDATE` → `detailWriteDate`, `EA14_IDX` → `ea14Idx`, `PAYER_NO` → `payerNo`, `FILE_APPDATE` → `fileAppDate`, `BANK_CODE` → `bankCode`, `BANK_ACCNO` → `bankAccNo`, `BANK_REGNO` → `bankRegNo`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegNo`, `RSLT_CODE` → `resultCode`, `ERR_CODE` → `errorCode`, `CODE_DETAIL_NM` → `errorMessage`, `MEM_EMAIL` → `memberEmail`, `COM_NO` → `comNo`, `MEM_NO` → `memNo`, `MEM_NAME` → `memName`, `BANK_NAME` → `bankName`.
- [findEb14Header](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L55) — 바인딩: `idx`. 결과 매핑: `IDX` → `idx`, `FILE_APPDATE` → `fileAppDate`, `EA14FILE_NAME` → `fileName`, `NEW_CNT` → `newCount`, `END_CNT` → `endCount`, `TOTAL_CNT` → `totalCount`, `WRITE_YN` → `writeYn`, `CRET_DATE` → `createdDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db193"></a>
## SMARTBILL3.dbo.CMS_EA14_DETAIL_CUB

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `IDX` | `int` | 불가 | 예 |
| `EA14_IDX` | `int` | 허용 | 아니오 |
| `Com_No` | `int` | 허용 | 아니오 |
| `Payer_No` | `char(20)` | 허용 | 아니오 |
| `Bank_Code` | `varchar(2)` | 허용 | 아니오 |
| `Bank_AccNo` | `varchar(64)` | 허용 | 아니오 |
| `Bank_Regno` | `varchar(32)` | 허용 | 아니오 |
| `Rslt_Code` | `char(1)` | 허용 | 아니오 |
| `Err_Code` | `varchar(4)` | 허용 | 아니오 |
| `Detail_Wdate` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2014-11-12T20:39:26.853 |
| 읽기·참조 객체 | `smartbill3.dbo.cms_ea14_detail_cub` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchEb14Detail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) — 바인딩: `idx`, `resultCode`, `resultCode`. 결과 매핑: `IDX` → `idx`, `DETAIL_WDATE` → `detailWriteDate`, `EA14_IDX` → `ea14Idx`, `PAYER_NO` → `payerNo`, `FILE_APPDATE` → `fileAppDate`, `BANK_CODE` → `bankCode`, `BANK_ACCNO` → `bankAccNo`, `BANK_REGNO` → `bankRegNo`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegNo`, `RSLT_CODE` → `resultCode`, `ERR_CODE` → `errorCode`, `CODE_DETAIL_NM` → `errorMessage`, `MEM_EMAIL` → `memberEmail`, `COM_NO` → `comNo`, `MEM_NO` → `memNo`, `MEM_NAME` → `memName`, `BANK_NAME` → `bankName`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db194"></a>
## SMARTBILL3.dbo.CMS_EA22

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `IDX` | `int` | 불가 | 예 |
| `Inv_yymm` | `varchar(6)` | 허용 | 아니오 |
| `EA22File_Name` | `varchar(8)` | 허용 | 아니오 |
| `Pay_Date` | `varchar(6)` | 허용 | 아니오 |
| `Invbank_Code` | `varchar(2)` | 허용 | 아니오 |
| `Invbank_AccNo` | `varchar(16)` | 허용 | 아니오 |
| `Total_Cnt` | `int` | 허용 | 아니오 |
| `Pay_Cnt` | `int` | 허용 | 아니오 |
| `Pay_Amt` | `money` | 허용 | 아니오 |
| `Write_Yn` | `char(1)` | 허용 | 아니오 |
| `Cret_Date` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2014-11-12T20:44:37.083 |
| 읽기·참조 객체 | `smartbill3.dbo.cms_ea22` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findEb22Header](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L149) — 바인딩: `idx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [searchEb22Detail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L281) — 바인딩: `idx`. 결과 매핑: `IDX` → `idx`, `DETAIL_WDATE` → `detailWdate`, `EA22FILE_NAME` → `ea22FileName`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `BANK_CODE` → `bankCode`, `BANK_ACCNO` → `bankAccNo`, `BANK_REGNO` → `bankRegno`, `INV_AMT` → `invAmt`, `RSLT_CODE` → `rsltCode`, `ERR_CODE` → `errCode`, `COM_NO` → `comNo`, `CODE_DETAIL_NM` → `codeDetailNm`, `BANK_NAME` → `bankName`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db195"></a>
## SMARTBILL3.dbo.CMS_EA22_DETAIL_CUB

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `IDX` | `int` | 불가 | 예 |
| `EA22_IDX` | `int` | 허용 | 아니오 |
| `Com_No` | `int` | 허용 | 아니오 |
| `Payer_No` | `char(20)` | 허용 | 아니오 |
| `Bank_Code` | `varchar(2)` | 허용 | 아니오 |
| `Bank_AccNo` | `varchar(64)` | 허용 | 아니오 |
| `Bank_Regno` | `varchar(32)` | 허용 | 아니오 |
| `Inv_Amt` | `money` | 허용 | 아니오 |
| `Rslt_Code` | `char(1)` | 허용 | 아니오 |
| `Err_Code` | `varchar(4)` | 허용 | 아니오 |
| `Detail_Wdate` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2014-11-12T20:41:22.643 |
| 읽기·참조 객체 | `smartbill3.dbo.cms_ea22_detail_cub` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchEb22Detail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L281) — 바인딩: `idx`. 결과 매핑: `IDX` → `idx`, `DETAIL_WDATE` → `detailWdate`, `EA22FILE_NAME` → `ea22FileName`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `BANK_CODE` → `bankCode`, `BANK_ACCNO` → `bankAccNo`, `BANK_REGNO` → `bankRegno`, `INV_AMT` → `invAmt`, `RSLT_CODE` → `rsltCode`, `ERR_CODE` → `errCode`, `COM_NO` → `comNo`, `CODE_DETAIL_NM` → `codeDetailNm`, `BANK_NAME` → `bankName`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db196"></a>
## SMARTBILL3.dbo.COMMON_CODE

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `code_idx` | `int` | 불가 | 예 |
| `code_type` | `varchar(50)` | 불가 | 아니오 |
| `code_nm` | `varchar(100)` | 불가 | 아니오 |
| `code` | `varchar(10)` | 불가 | 아니오 |
| `code_detail_nm` | `varchar(200)` | 불가 | 아니오 |
| `remark` | `varchar(200)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2014-11-12T20:41:19.273 |
| 읽기·참조 객체 | `smartbill3.dbo.common_code` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchEb22Detail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L281) — 바인딩: `idx`. 결과 매핑: `IDX` → `idx`, `DETAIL_WDATE` → `detailWdate`, `EA22FILE_NAME` → `ea22FileName`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `BANK_CODE` → `bankCode`, `BANK_ACCNO` → `bankAccNo`, `BANK_REGNO` → `bankRegno`, `INV_AMT` → `invAmt`, `RSLT_CODE` → `rsltCode`, `ERR_CODE` → `errCode`, `COM_NO` → `comNo`, `CODE_DETAIL_NM` → `codeDetailNm`, `BANK_NAME` → `bankName`.
- [searchEb14Detail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) — 바인딩: `idx`, `resultCode`, `resultCode`. 결과 매핑: `IDX` → `idx`, `DETAIL_WDATE` → `detailWriteDate`, `EA14_IDX` → `ea14Idx`, `PAYER_NO` → `payerNo`, `FILE_APPDATE` → `fileAppDate`, `BANK_CODE` → `bankCode`, `BANK_ACCNO` → `bankAccNo`, `BANK_REGNO` → `bankRegNo`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegNo`, `RSLT_CODE` → `resultCode`, `ERR_CODE` → `errorCode`, `CODE_DETAIL_NM` → `errorMessage`, `MEM_EMAIL` → `memberEmail`, `COM_NO` → `comNo`, `MEM_NO` → `memNo`, `MEM_NAME` → `memName`, `BANK_NAME` → `bankName`.
- [findRevealAccountNumber](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/bulkaccountdeposit/repository/BulkAccountDepositMapper.kt#L40) — 바인딩: `idx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db197"></a>
## SMARTBILL3.dbo.COMPANY

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `com_no` | `no` | 불가 | 예 |
| `com_name` | `varchar(400)` | 허용 | 아니오 |
| `com_name_se` | `char(1)` | 허용 | 아니오 |
| `com_regno` | `varchar(13)` | 불가 | 아니오 |
| `com_regno_se` | `char(1)` | 허용 | 아니오 |
| `com_president` | `varchar(200)` | 허용 | 아니오 |
| `com_bizstatus` | `varchar(200)` | 허용 | 아니오 |
| `com_bizclass` | `varchar(200)` | 허용 | 아니오 |
| `com_zipcode` | `zipcode` | 불가 | 아니오 |
| `com_Address` | `varchar(600)` | 허용 | 아니오 |
| `com_status` | `varchar(2)` | 허용 | 아니오 |
| `com_seal` | `file_name` | 허용 | 아니오 |
| `cert_grade` | `varchar(2)` | 허용 | 아니오 |
| `cert_dn` | `certData` | 허용 | 아니오 |
| `cert_data` | `text` | 허용 | 아니오 |
| `biz_ctg` | `varchar(4)` | 허용 | 아니오 |
| `biz_ctg_detail` | `varchar(3)` | 허용 | 아니오 |
| `com_entry_date` | `datetime` | 허용 | 아니오 |
| `com_del_yn` | `varchar(1)` | 허용 | 아니오 |
| `com_modify_date` | `datetime` | 허용 | 아니오 |
| `dct_premium` | `int` | 허용 | 아니오 |
| `ma_id` | `varchar(12)` | 허용 | 아니오 |
| `Tstamp` | `timestamp` | 불가 | 아니오 |
| `cert_expire_date` | `datetime` | 허용 | 아니오 |
| `COM_REGNO#` | `varchar(52)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-10-06T14:00:05.067 |
| 읽기·참조 객체 | `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchEb22Detail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L281) — 바인딩: `idx`. 결과 매핑: `IDX` → `idx`, `DETAIL_WDATE` → `detailWdate`, `EA22FILE_NAME` → `ea22FileName`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `BANK_CODE` → `bankCode`, `BANK_ACCNO` → `bankAccNo`, `BANK_REGNO` → `bankRegno`, `INV_AMT` → `invAmt`, `RSLT_CODE` → `rsltCode`, `ERR_CODE` → `errCode`, `COM_NO` → `comNo`, `CODE_DETAIL_NM` → `codeDetailNm`, `BANK_NAME` → `bankName`.
- [searchEb14Detail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) — 바인딩: `idx`, `resultCode`, `resultCode`. 결과 매핑: `IDX` → `idx`, `DETAIL_WDATE` → `detailWriteDate`, `EA14_IDX` → `ea14Idx`, `PAYER_NO` → `payerNo`, `FILE_APPDATE` → `fileAppDate`, `BANK_CODE` → `bankCode`, `BANK_ACCNO` → `bankAccNo`, `BANK_REGNO` → `bankRegNo`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegNo`, `RSLT_CODE` → `resultCode`, `ERR_CODE` → `errorCode`, `CODE_DETAIL_NM` → `errorMessage`, `MEM_EMAIL` → `memberEmail`, `COM_NO` → `comNo`, `MEM_NO` → `memNo`, `MEM_NAME` → `memName`, `BANK_NAME` → `bankName`.
- [findRevealBusinessNumber](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankCompanyMapper.kt#L45) — 바인딩: `comNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findCompanyDelInfo](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankCompanyMapper.kt#L143) — 바인딩: `comNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findSensitiveValue](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankMemberMapper.kt#L82) — 바인딩: `memNo`, `memNo`, `memNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findPayerName](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/status/repository/PaymentStatusInfoMapper.kt#L102) — 바인딩: `idx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [lookupLatestPrepayByRegno](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DepositProcessMapper.kt#L53) — 바인딩: `comRegno`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findTargetCompanyByRegno](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DepositProcessMapper.kt#L72) — 바인딩: `comRegno`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findRevealAccountNumber](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/bulkaccountdeposit/repository/BulkAccountDepositMapper.kt#L40) — 바인딩: `idx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findCompanyByRegno](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/bulkaccountdeposit/repository/BulkAccountDepositMapper.kt#L145) — 바인딩: `regNo`. 결과 매핑: `comNo` → `comNo`, `companyName` → `companyName`.
- [findUnpaidChargesByMonth](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L181) — 바인딩: `chargeMonth`, `offset`, `pageSize`. 결과 매핑: `TOT_COUNT` → `totCount`, `COM_NO` → `comNo`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `CHARGE_MONTH` → `chargeMonth`, `BILLING_AMOUNT` → `billingAmount`, `CR_CD` → `crCd`, `SERVICE_CD` → `serviceCd`, `SEQ` → `seq`.
- [findCancellerName](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/banktransfercancel/repository/BankTransferCancelMapper.kt#L42) — 바인딩: `idx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findPresidentName](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcRightMapper.kt#L104) — 바인딩: `comNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findAddress](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcRightMapper.kt#L94) — 바인딩: `comNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findCompanyBusinessNumber](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L59) — 바인딩: `comNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [getEContractConfig](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L835) — 바인딩: `comNo`. 결과 매핑: `COM_NO` → `comNo`, `ATTACHFILE_DEL_YN` → `attachfileDelYn`, `ATTACHFILE_LIMIT_SIZE` → `attachfileLimitSize`, `MULTI_USE_YN` → `multiUseYn`, `DCT_DEFAULT_DISK` → `dctDefaultDisk`, `DCT_PREMIUM` → `dctPremium`.
- [getCompanyDelYn](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L242) — 바인딩: `comNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [getCompanyBasicOnly](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L230) — 바인딩: `comNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findSealFileName](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L1160) — 바인딩: `comNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findAdministratorSensitiveValue](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L165) — 바인딩: `comNo`, `comNo`, `comNo`, `comNo`, `comNo`, `memNo`. 결과 매핑: `DUPLICATE_ROLE_COUNT` → `duplicateRoleCount`, `MEM_NO` → `memNo`, `SENSITIVE_VALUE` → `value`.
- [findComNoByBusinessNumber](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L253) — 바인딩: `businessNumber`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findCompanyMemberSensitiveValue](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L82) — 바인딩: `comNo`, `memNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [getCompanyList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/registrationinquiry/repository/RegistrationInquiryMapper.kt#L104) — 바인딩: `cafeId,jdbcType=VARCHAR`, `searchText,jdbcType=NVARCHAR`, `searchText,jdbcType=VARCHAR`, `registrationFilter,jdbcType=VARCHAR`. 결과 매핑: `com_regno` → `comRegno`, `com_name` → `comName`, `email` → `email`, `hp` → `hp`, `SB_YN` → `sbYn`.
- [selectCompanies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptCodeMapper.kt#L71) — 바인딩: `schText,jdbcType=VARCHAR`, `schText,jdbcType=VARCHAR`, `schText,jdbcType=VARCHAR`, `schText,jdbcType=VARCHAR`. 결과 매핑: `com_regno` → `comRegno`, `com_name` → `comName`, `mem_realname` → `memRealname`, `mem_tel` → `memTel`, `routing_type` → `routingType`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db198"></a>
## SmartBill3.dbo.company_history

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `com_history_date` | `datetime` | 불가 | 아니오 |
| `com_no` | `no` | 불가 | 아니오 |
| `com_name` | `varchar(400)` | 허용 | 아니오 |
| `com_name_se` | `char(1)` | 허용 | 아니오 |
| `com_regno` | `varchar(13)` | 불가 | 아니오 |
| `com_regno_se` | `char(1)` | 허용 | 아니오 |
| `com_president` | `varchar(200)` | 허용 | 아니오 |
| `com_bizstatus` | `varchar(200)` | 허용 | 아니오 |
| `com_bizclass` | `varchar(200)` | 허용 | 아니오 |
| `com_zipcode` | `zipcode` | 불가 | 아니오 |
| `com_Address` | `varchar(600)` | 허용 | 아니오 |
| `com_status` | `varchar(2)` | 허용 | 아니오 |
| `com_seal` | `file_name` | 허용 | 아니오 |
| `cert_grade` | `varchar(2)` | 허용 | 아니오 |
| `cert_dn` | `certData` | 허용 | 아니오 |
| `cert_data` | `text` | 허용 | 아니오 |
| `biz_ctg` | `varchar(4)` | 허용 | 아니오 |
| `biz_ctg_detail` | `varchar(3)` | 허용 | 아니오 |
| `com_entry_date` | `datetime` | 허용 | 아니오 |
| `com_del_yn` | `varchar(1)` | 허용 | 아니오 |
| `com_modify_date` | `datetime` | 허용 | 아니오 |
| `dct_premium` | `int` | 허용 | 아니오 |
| `ma_id` | `varchar(12)` | 허용 | 아니오 |
| `Tstamp` | `varchar(255)` | 허용 | 아니오 |
| `update_no` | `no` | 허용 | 아니오 |
| `cert_expire_date` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2019-05-30T10:03:13.370 |
| 읽기·참조 객체 | `smartbill3.dbo.company_history` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getChangeHistory](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L1068) — 바인딩: `comNo`, `page`, `page`, `pageSize`, `pageSize`, `pageSize`, `pageSize`. 결과 매핑: `changeDate` → `changeDate`, `companyName` → `companyName`, `presidentName` → `presidentName`, `businessStatus` → `businessStatus`, `businessClass` → `businessClass`, `address` → `address`, `certDn` → `certDn`, `sealFileName` → `sealFileName`, `totalElements` → `totalElements`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db199"></a>
## SMARTBILL3.dbo.DCT_COMPANY_CONFIG

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `COM_NO` | `int` | 불가 | 아니오 |
| `IDX` | `int` | 불가 | 예 |
| `ATTACHFILE_DEL_YN` | `char(1)` | 허용 | 아니오 |
| `ATTACHFILE_LIMIT_SIZE` | `int` | 허용 | 아니오 |
| `CUSER` | `varchar(12)` | 허용 | 아니오 |
| `CDATE` | `datetime` | 허용 | 아니오 |
| `UUSER` | `varchar(12)` | 허용 | 아니오 |
| `UDATE` | `datetime` | 허용 | 아니오 |
| `DCT_FILE_CONVERT` | `varchar(10)` | 허용 | 아니오 |
| `DCT_DEFAULT_DISK` | `int` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2019-04-30T10:27:11.903 |
| 읽기·참조 객체 | `smartbill3.dbo.dct_company_config` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getEContractConfig](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L835) — 바인딩: `comNo`. 결과 매핑: `COM_NO` → `comNo`, `ATTACHFILE_DEL_YN` → `attachfileDelYn`, `ATTACHFILE_LIMIT_SIZE` → `attachfileLimitSize`, `MULTI_USE_YN` → `multiUseYn`, `DCT_DEFAULT_DISK` → `dctDefaultDisk`, `DCT_PREMIUM` → `dctPremium`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db200"></a>
## SMARTBILL3.dbo.DCT_MULTI_USE

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `COM_NO` | `int` | 허용 | 아니오 |
| `USE_YN` | `varchar(2)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2013-02-06T11:00:50.237 |
| 읽기·참조 객체 | `smartbill3.dbo.dct_multi_use` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getEContractConfig](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L835) — 바인딩: `comNo`. 결과 매핑: `COM_NO` → `comNo`, `ATTACHFILE_DEL_YN` → `attachfileDelYn`, `ATTACHFILE_LIMIT_SIZE` → `attachfileLimitSize`, `MULTI_USE_YN` → `multiUseYn`, `DCT_DEFAULT_DISK` → `dctDefaultDisk`, `DCT_PREMIUM` → `dctPremium`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db201"></a>
## SMARTBILL3.dbo.DEPT_MANAGER

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `manager_no` | `int` | 불가 | 예 |
| `com_no` | `no` | 불가 | 아니오 |
| `service_type` | `varchar(3)` | 불가 | 아니오 |
| `mem_no` | `no` | 불가 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2014-12-04T15:25:07.530 |
| 읽기·참조 객체 | `smartbill3.dbo.dept_manager` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findAdministratorSensitiveValue](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L165) — 바인딩: `comNo`, `comNo`, `comNo`, `comNo`, `comNo`, `memNo`. 결과 매핑: `DUPLICATE_ROLE_COUNT` → `duplicateRoleCount`, `MEM_NO` → `memNo`, `SENSITIVE_VALUE` → `value`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db202"></a>
## SMARTBILL3.dbo.faq

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `FAQ_NO` | `int` | 불가 | 예 |
| `FAQ_TYPE` | `varchar(50)` | 불가 | 아니오 |
| `FAQ_TITLE` | `varchar(1000)` | 불가 | 아니오 |
| `FAQ_TITLE_SE` | `char(1)` | 허용 | 아니오 |
| `FAQ_WRITER` | `varchar(30)` | 허용 | 아니오 |
| `FAQ_WRITER_SE` | `char(1)` | 허용 | 아니오 |
| `FAQ_CONTENTS` | `nvarchar(max)` | 허용 | 아니오 |
| `FAQ_CONTENTS_SE` | `char(1)` | 허용 | 아니오 |
| `FAQ_FILE` | `varchar(100)` | 허용 | 아니오 |
| `FAQ_HIT` | `int` | 허용 | 아니오 |
| `FAQ_WRITE_DATE` | `datetime` | 허용 | 아니오 |
| `MEM_NO` | `int` | 허용 | 아니오 |
| `FAQ_TYPE_DETAIL` | `varchar(30)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2023-11-09T16:11:32.290 |
| 읽기·참조 객체 | `smartbill3.dbo.faq` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchFaqsByCategory](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/faq/repository/AdminFaqMapper.kt#L75) — 바인딩: `category`, `param.offset`, `param.size`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db203"></a>
## SMARTBILL3.dbo.MEMBER

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `mem_no` | `no` | 불가 | 예 |
| `com_no` | `no` | 허용 | 아니오 |
| `mem_name` | `varchar(200)` | 허용 | 아니오 |
| `mem_realname` | `varchar(200)` | 허용 | 아니오 |
| `mem_regno` | `regno` | 불가 | 아니오 |
| `mem_id` | `mem_id` | 불가 | 아니오 |
| `mem_pw` | `mem_pw` | 불가 | 아니오 |
| `mem_type` | `mem_type` | 불가 | 아니오 |
| `mem_tel` | `tel` | 불가 | 아니오 |
| `mem_hp` | `tel` | 허용 | 아니오 |
| `mem_email` | `varchar(200)` | 허용 | 아니오 |
| `mem_status` | `mem_status` | 허용 | 아니오 |
| `mem_entry_date` | `datetime` | 허용 | 아니오 |
| `mem_del_yn` | `varchar(1)` | 허용 | 아니오 |
| `mem_modify_date` | `datetime` | 허용 | 아니오 |
| `Tstamp` | `timestamp` | 불가 | 아니오 |
| `isVirtualYN` | `varchar(1)` | 불가 | 아니오 |
| `name_display_yn` | `varchar(1)` | 허용 | 아니오 |
| `resultmail_send_yn` | `varchar(1)` | 허용 | 아니오 |
| `infomail_receive_yn` | `varchar(1)` | 허용 | 아니오 |
| `mem_fax` | `tel` | 허용 | 아니오 |
| `INFORSMS_RECEIVE_YN` | `char(1)` | 허용 | 아니오 |
| `sha_pw` | `varchar(70)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-10-06T14:00:05.110 |
| 읽기·참조 객체 | `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchEb22Detail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmseb22/repository/Eb22Mapper.kt#L281) — 바인딩: `idx`. 결과 매핑: `IDX` → `idx`, `DETAIL_WDATE` → `detailWdate`, `EA22FILE_NAME` → `ea22FileName`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `BANK_CODE` → `bankCode`, `BANK_ACCNO` → `bankAccNo`, `BANK_REGNO` → `bankRegno`, `INV_AMT` → `invAmt`, `RSLT_CODE` → `rsltCode`, `ERR_CODE` → `errCode`, `COM_NO` → `comNo`, `CODE_DETAIL_NM` → `codeDetailNm`, `BANK_NAME` → `bankName`.
- [searchEb14Detail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/cmsaccount/repository/Eb14AccountMapper.kt#L166) — 바인딩: `idx`, `resultCode`, `resultCode`. 결과 매핑: `IDX` → `idx`, `DETAIL_WDATE` → `detailWriteDate`, `EA14_IDX` → `ea14Idx`, `PAYER_NO` → `payerNo`, `FILE_APPDATE` → `fileAppDate`, `BANK_CODE` → `bankCode`, `BANK_ACCNO` → `bankAccNo`, `BANK_REGNO` → `bankRegNo`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegNo`, `RSLT_CODE` → `resultCode`, `ERR_CODE` → `errorCode`, `CODE_DETAIL_NM` → `errorMessage`, `MEM_EMAIL` → `memberEmail`, `COM_NO` → `comNo`, `MEM_NO` → `memNo`, `MEM_NAME` → `memName`, `BANK_NAME` → `bankName`.
- [getTransferMap](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L351) — 바인딩: `comNo`. 결과 매핑: `MEM_NO` → `memNo`, `TRANSFER_GUBUN` → `transferGubun`.
- [findSensitiveValue](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankMemberMapper.kt#L82) — 바인딩: `memNo`, `memNo`, `memNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findPayerName](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/status/repository/PaymentStatusInfoMapper.kt#L102) — 바인딩: `idx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findCancellerName](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/banktransfercancel/repository/BankTransferCancelMapper.kt#L42) — 바인딩: `idx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [findAdministratorSensitiveValue](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L165) — 바인딩: `comNo`, `comNo`, `comNo`, `comNo`, `comNo`, `memNo`. 결과 매핑: `DUPLICATE_ROLE_COUNT` → `duplicateRoleCount`, `MEM_NO` → `memNo`, `SENSITIVE_VALUE` → `value`.
- [findCompanyMemberSensitiveValue](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L82) — 바인딩: `comNo`, `memNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [selectCompanies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptCodeMapper.kt#L71) — 바인딩: `schText,jdbcType=VARCHAR`, `schText,jdbcType=VARCHAR`, `schText,jdbcType=VARCHAR`, `schText,jdbcType=VARCHAR`. 결과 매핑: `com_regno` → `comRegno`, `com_name` → `comName`, `mem_realname` → `memRealname`, `mem_tel` → `memTel`, `routing_type` → `routingType`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db204"></a>
## SmartBill3.dbo.msg_m_error_code

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `M_IDX` | `int` | 불가 | 예 |
| `DESCRIPTION` | `varchar(60)` | 허용 | 아니오 |
| `ADMIN_NO` | `int` | 허용 | 아니오 |
| `REG_DATE` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2014-11-12T20:20:01.190 |
| 읽기·참조 객체 | `smartbill3.dbo.msg_m_error_code` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectMIdxByDescription](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/errorcode/repository/ErrorCodeMapper.kt#L161) — 바인딩: `description`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [selectProcesses](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/errorcode/repository/ErrorCodeMapper.kt#L152) — 바인딩: . 결과 매핑: `m_idx` → `mIdx`, `description` → `description`.
- [selectByErrorCode](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/errorcode/repository/ErrorCodeMapper.kt#L99) — 바인딩: `errorCode`. 결과 매핑: `n_idx` → `nIdx`, `m_idx` → `mIdx`, `error_code` → `errorCode`, `process_name` → `processName`, `error_desc` → `errorDesc`, `support_desc` → `supportDesc`, `detail_guide` → `detailGuide`, `mng_yn` → `mngYn`, `hit_count` → `hitCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db205"></a>
## SmartBill3.dbo.msg_n_error_code

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `N_IDX` | `int` | 불가 | 예 |
| `M_IDX` | `int` | 허용 | 아니오 |
| `ERROR_CODE` | `varchar(10)` | 허용 | 아니오 |
| `ERROR_DESC` | `varchar(200)` | 허용 | 아니오 |
| `SUPPORT_DESC` | `varchar(2000)` | 허용 | 아니오 |
| `CUSTOMER_SUPPORT_DESC` | `varchar(2000)` | 허용 | 아니오 |
| `DETAIL_GUIDE` | `varchar(2000)` | 허용 | 아니오 |
| `ADMIN_NO` | `int` | 허용 | 아니오 |
| `REG_DATE` | `datetime` | 허용 | 아니오 |
| `MNG_YN` | `varchar(3)` | 허용 | 아니오 |
| `HIT_COUNT` | `int` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2014-11-12T20:42:15.623 |
| 읽기·참조 객체 | `smartbill3.dbo.msg_n_error_code` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectByErrorCode](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/errorcode/repository/ErrorCodeMapper.kt#L99) — 바인딩: `errorCode`. 결과 매핑: `n_idx` → `nIdx`, `m_idx` → `mIdx`, `error_code` → `errorCode`, `process_name` → `processName`, `error_desc` → `errorDesc`, `support_desc` → `supportDesc`, `detail_guide` → `detailGuide`, `mng_yn` → `mngYn`, `hit_count` → `hitCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db206"></a>
## smartbill3.dbo.qna

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `QNA_NO` | `no` | 불가 | 예 |
| `QNA_TYPE` | `varchar(50)` | 허용 | 아니오 |
| `QNA_TITLE` | `title` | 불가 | 아니오 |
| `QNA_TITLE_SE` | `char(1)` | 허용 | 아니오 |
| `QNA_WRITER` | `varchar(200)` | 허용 | 아니오 |
| `QNA_WRITER_SE` | `char(1)` | 허용 | 아니오 |
| `QNA_CONTENTS` | `contents` | 불가 | 아니오 |
| `QNA_CONTENTS_SE` | `char(1)` | 허용 | 아니오 |
| `QNA_REF` | `int` | 불가 | 아니오 |
| `QNA_STEP` | `int` | 불가 | 아니오 |
| `QNA_ANSNUM` | `int` | 허용 | 아니오 |
| `QNA_TN` | `int` | 허용 | 아니오 |
| `QNA_PN` | `int` | 허용 | 아니오 |
| `QNA_HIT` | `hit` | 허용 | 아니오 |
| `QNA_WRITE_DATE` | `datetime` | 허용 | 아니오 |
| `MEM_NO` | `int` | 허용 | 아니오 |
| `SMS_YN` | `char(1)` | 허용 | 아니오 |
| `SMS_HP_NO` | `varchar(20)` | 허용 | 아니오 |
| `SMS_SEND_YN` | `char(1)` | 허용 | 아니오 |
| `DEVICE` | `varchar(1)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-11-03T11:22:41.207 |
| 읽기·참조 객체 | `smartbill3.dbo.qna` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchQnas](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/qna/repository/AdminQnaMapper.kt#L88) — 바인딩: `param.div`, `param.div`, `param.device,jdbcType=VARCHAR`, `param.device,jdbcType=VARCHAR`, `param.schIndex`, `param.schIndex`, `param.schText`, `param.schText`, `param.schIndex`, `param.schText`, `param.schText`, `param.schIndex`, `param.schText`, `param.schText`, `param.schIndex`, `param.schText`. 결과 매핑: `qna_no` → `qnaNo`, `qna_type` → `qnaType`, `qna_title` → `qnaTitle`, `qna_writer` → `qnaWriter`, `qna_step` → `qnaStep`, `qna_hit` → `qnaHit`, `qna_write_date` → `qnaWriteDate`, `is_new` → `isNew`, `device` → `device`.
- [findWriter](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/qna/repository/AdminQnaMapper.kt#L177) — 바인딩: `qnaNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db207"></a>
## SMARTBILL3.dbo.SERVICE_PREPAY

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `prepay_no` | `no` | 불가 | 예 |
| `prepay_date` | `datetime` | 허용 | 아니오 |
| `com_no` | `no` | 허용 | 아니오 |
| `prepay_amt` | `money` | 불가 | 아니오 |
| `carryover_amt` | `money` | 허용 | 아니오 |
| `principal_amt` | `money` | 허용 | 아니오 |
| `use_amt` | `money` | 허용 | 아니오 |
| `prepay_result` | `varchar(2)` | 허용 | 아니오 |
| `pay_method` | `varchar(2)` | 허용 | 아니오 |
| `Prepay_mem_no` | `no` | 허용 | 아니오 |
| `Prepay_dti_no` | `no` | 허용 | 아니오 |
| `order_id` | `varchar(64)` | 허용 | 아니오 |
| `admin_confirm_date` | `smalldatetime` | 허용 | 아니오 |
| `refund_amt` | `money` | 허용 | 아니오 |
| `udate` | `datetime` | 허용 | 아니오 |
| `REFUND_COMMISSION_AMT` | `money` | 허용 | 아니오 |
| `LAPSE_AMT` | `money` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2014-11-12T20:45:48.880 |
| 읽기·참조 객체 | `smartbill3.dbo.service_prepay` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [lookupLatestPrepayByRegno](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DepositProcessMapper.kt#L53) — 바인딩: `comRegno`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db208"></a>
## SmartBill3.dbo.SSP_WITHDRAWAL_LIST

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@FDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DIV` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:32.387 |
| 읽기·참조 객체 | `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchYearly](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/smartbillstatus/repository/WithdrawalBusinessStatisticsMapper.kt#L58) — 바인딩: `startDate`, `endDate`, `div`. 결과 매핑: `YEAR` → `year`, `corporation` → `corporateCount`, `individual` → `individualCount`.
- [searchMonthly](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/smartbillstatus/repository/WithdrawalBusinessStatisticsMapper.kt#L47) — 바인딩: `startDate`, `endDate`, `div`. 결과 매핑: `YEAR` → `year`, `MONTH` → `month`, `corporation` → `corporateCount`, `individual` → `individualCount`.
- [searchDaily](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/smartbillstatus/repository/WithdrawalBusinessStatisticsMapper.kt#L35) — 바인딩: `startDate`, `endDate`, `div`. 결과 매핑: `YEAR` → `year`, `MONTH` → `month`, `DAY` → `day`, `corporation` → `corporateCount`, `individual` → `individualCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE
GROUP BY
WHERE
GROUP BY
GROUP BY COM_MODIFY_DATE
ORDER BY YEAR DESC,MONTH DESC,DAY DESC
WHERE
GROUP BY
WHERE
GROUP BY
GROUP BY YEAR(COM_MODIFY_DATE),MONTH(COM_MODIFY_DATE)
ORDER BY YEAR DESC,MONTH DESC
WHERE
GROUP BY
WHERE
GROUP BY
GROUP BY YEAR(COM_MODIFY_DATE)
ORDER BY YEAR DESC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db209"></a>
## SMARTBILL3.dbo.TAX_ADMIN

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `admin_no` | `no` | 불가 | 예 |
| `cafe_id` | `varchar(15)` | 불가 | 아니오 |
| `mem_no` | `no` | 불가 | 아니오 |
| `mem_rgt` | `varchar(1)` | 불가 | 아니오 |
| `memagr_date` | `datetime` | 불가 | 아니오 |
| `rgt_main` | `varchar(1)` | 허용 | 아니오 |
| `rgt_member` | `varchar(1)` | 허용 | 아니오 |
| `rgt_event` | `varchar(1)` | 허용 | 아니오 |
| `RGT_MENU` | `char(1)` | 허용 | 아니오 |
| `RGT_PAYBOARD` | `char(1)` | 허용 | 아니오 |
| `RGT_GOVER` | `char(1)` | 허용 | 아니오 |
| `RGT_STATIS` | `char(1)` | 허용 | 아니오 |
| `RGT_DTI` | `char(1)` | 허용 | 아니오 |
| `RGT_JOIN` | `varchar(1)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2014-11-12T20:42:19.990 |
| 읽기·참조 객체 | `smartbill3.dbo.tax_admin` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findAdministratorSensitiveValue](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L165) — 바인딩: `comNo`, `comNo`, `comNo`, `comNo`, `comNo`, `memNo`. 결과 매핑: `DUPLICATE_ROLE_COUNT` → `duplicateRoleCount`, `MEM_NO` → `memNo`, `SENSITIVE_VALUE` → `value`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db210"></a>
## SmartBill3.dbo.tax_memcfrm_detail

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `memcfrm_detail_no` | `int` | 불가 | 예 |
| `cafe_id` | `varchar(15)` | 불가 | 아니오 |
| `memcfrm_com_regno` | `varchar(10)` | 허용 | 아니오 |
| `memcfrm_com_name` | `varchar(400)` | 허용 | 아니오 |
| `memcfrm_email` | `varchar(200)` | 허용 | 아니오 |
| `memcfrm_hp` | `varchar(14)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2017-09-22T15:20:08.273 |
| 읽기·참조 객체 | `smartbill3.dbo.tax_memcfrm_detail` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getCompanyList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/registrationinquiry/repository/RegistrationInquiryMapper.kt#L104) — 바인딩: `cafeId,jdbcType=VARCHAR`, `searchText,jdbcType=NVARCHAR`, `searchText,jdbcType=VARCHAR`, `registrationFilter,jdbcType=VARCHAR`. 결과 매핑: `com_regno` → `comRegno`, `com_name` → `comName`, `email` → `email`, `hp` → `hp`, `SB_YN` → `sbYn`.
- [findCompanyEmails](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/registrationinquiry/repository/RegistrationInquiryMapper.kt#L112) — 바인딩: `cafeId`, `businessNumber`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db211"></a>
## SmartBill3.dbo.upAdmSB_BlockChainAddress

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@GUBUN` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SEARCHTEXT` | `varchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2020-06-03T09:41:53.293 |
| 읽기·참조 객체 | `sec_pt.dbo.tbl_pt_org`, `sec_pt.dbo.tbl_pt_usr` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [lookupAddress](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/passwordreset/repository/BlockchainAddressMapper.kt#L26) — 바인딩: `gubun`, `searchText`. 결과 매핑: `CN_ADR` → `cnAdr`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE  ORG_REG_NO = @SEARCHTEXT
WHERE  USR_EMAIL = @SEARCHTEXT
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db212"></a>
## SmartBill3.dbo.upAdmSB_BlockChainLock

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@page` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@top` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RCV_NM` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BRK_RCV_NM` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2021-12-08T18:20:19.490 |
| 읽기·참조 객체 | `sec_pt.dbo.tbl_pt_ctr`, `sec_pt.dbo.tbl_pt_ctr_lock` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchLockRecords](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/lockreset/repository/BlockchainLockMapper.kt#L46) — 바인딩: `page`, `top`, `rcvNm`, `brkRcvNm`. 결과 매핑: `CTR_SEQ` → `ctrSeq`, `CTR_FILE_NM` → `ctrFileNm`, `SND_NM` → `sndNm`, `BRK_SND_NM` → `brkSndNm`, `RCV_NM` → `rcvNm`, `BRK_RCV_NM` → `brkRcvNm`, `CTR_LOCK_TYPE` → `ctrLockType`, `CERT_REG_NO` → `certRegNo`, `PSN_NM` → `psnNm`, `PSN_NO` → `psnNo`, `PW_PIN` → `pwPin`, `CDATE` → `cdate`, `TOT_COUNT` → `totCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @TOP2 = @TOT_COUNT - ( @PAGE - 1 ) * @TOP
SET @TOP2 = @TOP
SET @SQL = '
SELECT CTR_SEQ, CERT_REG_NO, PSN_NM, PSN_NO, PW_PIN, CDATE FROM SEC_PT..TBL_PT_CTR_LOCK WITH(NOLOCK) WHERE FAIL_CNT = 5
LEFT JOIN SEC_PT..TBL_PT_CTR CR WITH(NOLOCK) on CR.CTR_SEQ = CL.CTR_SEQ
WHERE  1=1 '
SET @SQL = @SQL + N'
ORDER BY CL.CDATE DESC
ORDER BY CDATE ASC
INNER JOIN LASTPAGES AS V
ORDER BY L.CDATE DESC '
```

하위 프로시저·함수·뷰: `smartbill3.dbo.upadmsb_blockchainlock_count`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db213"></a>
## SmartBill3.dbo.UPADMSB_CHGMEMTYPE

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SW_NO` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:34.210 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.member`, `smartbill3.dbo.member_history` |
| 쓰기 대상 | `smartbill3.dbo.member`, `smartbill3.dbo.member_history` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `-1`; `@RESULT`; `@RESULT` |

### Mapper 입출력 매핑

- [changeMemberToCorporateAdmin](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankMemberMapper.kt#L245) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `memNo`, `swNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @RESULT = 1
BEGIN TRAN
WHERE MEM_NO = @NO
WHERE M.COM_NO = C.COM_NO
WHERE COM_NO = @COM_NO
WHERE MEM_NO = @MEM_NO
WHERE MEM_DEL_YN = 'N'
WHERE MEM_NO = @NO
WHERE MEM_DEL_YN = 'N'
SET @RESULT = @NO
SET @RESULT = 0
ROLLBACK
COMMIT
ROLLBACK
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db214"></a>
## SMARTBILL3.dbo.upAdmSB_Cnt_QnaVisit

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@qnaNo` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:17.523 |
| 읽기·참조 객체 | `smartbill3.dbo.qna` |
| 쓰기 대상 | `smartbill3.dbo.qna` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [incrementHit](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/qna/repository/AdminQnaMapper.kt#L173) — 바인딩: `qnaNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
where  qna_no = @qnaNo
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db215"></a>
## SmartBill3.dbo.upAdmSB_ComAdmin_lst01

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@com_no` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:18.420 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findCompanyAdmin](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankCompanyMapper.kt#L163) — 바인딩: `comNo`. 결과 매핑: `mem_no` → `memNo`, `mem_name` → `memName`, `mem_realname` → `memRealname`, `mem_tel` → `memTel`, `mem_hp` → `memHp`, `mem_email` → `memEmail`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
join smartbill3.dbo.member m on m.com_no = c.com_no
where c.com_no = @com_no and mem_type = 'F'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db216"></a>
## SMARTBILL3.dbo.upAdmSB_DelFaq

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@num` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:22.110 |
| 읽기·참조 객체 | `smartbill3.dbo.faq`, `smartbill3.dbo.se_delete` |
| 쓰기 대상 | `smartbill3.dbo.faq`, `smartbill3.dbo.se_delete` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `0`; `1` |

### Mapper 입출력 매핑

- [deleteFaq](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/faq/repository/AdminFaqMapper.kt#L115) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `num`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Begin  Tran
where table_name = 'faq'
delete from smartbill3.dbo.faq where faq_no = @num
rollback
Commit
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db217"></a>
## SmartBill3.dbo.upAdmSB_DelNErrCode

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@n_Idx` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:23.663 |
| 읽기·참조 객체 | `smartbill3.dbo.msg_n_error_code` |
| 쓰기 대상 | `smartbill3.dbo.msg_n_error_code` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `0`; `1` |

### Mapper 입출력 매핑

- [delete](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/errorcode/repository/ErrorCodeMapper.kt#L142) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `nIdx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Begin Tran
delete from smartbill3.dbo.msg_n_error_code where n_idx = @n_Idx
RollBack
Commit
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db218"></a>
## SMARTBILL3.dbo.upAdmSB_DelNotice

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@num` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:24.200 |
| 읽기·참조 객체 | `smartbill3.dbo.notice`, `smartbill3.dbo.se_delete` |
| 쓰기 대상 | `smartbill3.dbo.notice`, `smartbill3.dbo.se_delete` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `0`; `1` |

### Mapper 입출력 매핑

- [deleteNotice](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/notice/repository/BonabankNoticeMapper.kt#L84) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `num`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [deleteNotice](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/notice/repository/AdminNoticeMapper.kt#L98) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `num`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Begin  Tran
where table_name = 'notice'
delete from smartbill3.dbo.notice where notice_no = @num
rollback
Commit
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db219"></a>
## SMARTBILL3.dbo.upAdmSB_DelPds

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@pdsNo` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:24.650 |
| 읽기·참조 객체 | `smartbill3.dbo.pds`, `smartbill3.dbo.se_delete` |
| 쓰기 대상 | `smartbill3.dbo.pds`, `smartbill3.dbo.se_delete` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `0`; `1` |

### Mapper 입출력 매핑

- [deletePds](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/pds/repository/AdminPdsMapper.kt#L111) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `pdsNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Begin  Tran
where table_name = 'pds'
delete from smartbill3.dbo.pds where pds_no=@pdsNo
rollback
Commit
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db220"></a>
## SMARTBILL3.dbo.upAdmSB_DelQna

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@num` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:26.037 |
| 읽기·참조 객체 | `smartbill3.dbo.qna`, `smartbill3.dbo.se_delete` |
| 쓰기 대상 | `smartbill3.dbo.qna`, `smartbill3.dbo.se_delete` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `0`; `1` |

### Mapper 입출력 매핑

- [deleteQna](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/qna/repository/AdminQnaMapper.kt#L164) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `num`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Begin Tran
set @strNo = @num
from smartbill3.dbo.qna where qna_no = @strNo
set @strFlag = '0'
where table_name = 'qna'
delete from smartbill3.dbo.qna where qna_no=@strNo
where qna_ref=@strRef and qna_ansnum>@strAnsnum
where qna_no=@strPn
where table_name = 'qna'
delete from smartbill3.dbo.qna where qna_no=@strNo
from smartbill3.dbo.qna where qna_no=@strPn
set @strFlag='0'
where qna_no=@strNo
rollback
commit
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db221"></a>
## SMARTBILL3.dbo.upAdmSB_Lst_AllNotice

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@schItem` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@schText` | `varchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@div` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-07-16T09:23:31.220 |
| 읽기·참조 객체 | `smartbill3.dbo.notice` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchNotices](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/notice/repository/AdminNoticeMapper.kt#L51) — 바인딩: `schItem`, `schText`, `div`. 결과 매핑: `notice_no` → `noticeNo`, `notice_type` → `noticeType`, `notice_title` → `noticeTitle`, `notice_hit` → `noticeHit`, `notice_write_date` → `noticeWriteDate`, `MobileNoticeYN` → `mobileNoticeYn`, `WebNoticeYN` → `webNoticeYn`, `MobilePopYN` → `mobilePopYn`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
set @strSQL = '  select   notice_no, notice_title, notice_contents, notice_hit, notice_write_date, notice_type, MobileNoticeYN, WebNoticeYN, isnull(MobilePopYN, ''N'') AS MobilePopYN
from  notice where ' + @schItem + ' like ''%' + @schText + '%''  and notice_type != ''E'' and notice_type != ''S'' '
set @strSQL = '  select   notice_no, notice_title, notice_contents, notice_hit, notice_write_date, notice_type, MobileNoticeYN, WebNoticeYN, isnull(MobilePopYN, ''N'') AS MobilePopYN
from  notice where 1=1  and notice_type != ''E'' and notice_type != ''S'' '
set @strSQL = @strSQL + ' and notice_type = '''+@div+''''
set @strSQL = @strSQL + ' order by notice_write_date desc '
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db222"></a>
## SMARTBILL3.dbo.upAdmSB_Lst_AllNotice_Bona

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@schItem` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@schText` | `varchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2017-03-16T12:04:02.650 |
| 읽기·참조 객체 | `smartbill3.dbo.notice` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchNotices](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/notice/repository/BonabankNoticeMapper.kt#L46) — 바인딩: `schItem`, `schText`. 결과 매핑: `notice_no` → `noticeNo`, `notice_title` → `noticeTitle`, `notice_hit` → `noticeHit`, `notice_write_date` → `noticeWriteDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
set @strSQL = '  select   notice_no, notice_title, notice_contents, notice_hit, notice_write_date, notice_type, MobileNoticeYN, WebNoticeYN, isnull(MobilePopYN, ''N'') AS MobilePopYN
from  notice where ' + @schItem + ' like ''%' + @schText + '%'' and notice_type = ''E'' '
set @strSQL = '  select   notice_no, notice_title, notice_contents, notice_hit, notice_write_date, notice_type, MobileNoticeYN, WebNoticeYN, isnull(MobilePopYN, ''N'') AS MobilePopYN
from  notice where 1=1 and notice_type = ''E'' '
set @strSQL = @strSQL + ' order by notice_write_date desc '
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db223"></a>
## SMARTBILL3.dbo.upAdmSB_Lst_EachFaq

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@div` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@num` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:15.530 |
| 읽기·참조 객체 | `smartbill3.dbo.faq` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [fetchFaq](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/faq/repository/AdminFaqMapper.kt#L93) — 바인딩: `div`, `num`. 결과 매핑: `faq_no` → `faqNo`, `faq_type` → `faqType`, `faq_title` → `faqTitle`, `faq_contents` → `faqContents`, `faq_hit` → `faqHit`, `faq_write_date` → `faqWriteDate`, `faq_writer` → `faqWriter`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
set @strSQL = ' select * from faq where faq_type = ''' + @div + ''''
set @strSQL = ' select  * from faq where 1=1 '
set @strSQL = @strSQL + ' and faq_no = ' + cast(@num as varchar(12))
set @strSQL = @strSQL + ' order by faq_write_date desc '
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db224"></a>
## SMARTBILL3.dbo.upAdmSB_Lst_EachNotice

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@div` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@num` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:15.713 |
| 읽기·참조 객체 | `smartbill3.dbo.notice` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [fetchNotice](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/notice/repository/BonabankNoticeMapper.kt#L62) — 바인딩: `div`, `num`. 결과 매핑: `notice_no` → `noticeNo`, `notice_title` → `noticeTitle`, `notice_contents` → `noticeContents`, `notice_hit` → `noticeHit`, `notice_write_date` → `noticeWriteDate`.
- [fetchNotice](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/notice/repository/AdminNoticeMapper.kt#L73) — 바인딩: `div`, `num`. 결과 매핑: `notice_no` → `noticeNo`, `notice_type` → `noticeType`, `notice_title` → `noticeTitle`, `notice_contents` → `noticeContents`, `notice_hit` → `noticeHit`, `notice_write_date` → `noticeWriteDate`, `MobileNoticeYN` → `mobileNoticeYn`, `WebNoticeYN` → `webNoticeYn`, `MobilePopYN` → `mobilePopYn`, `MobilePopBeginDate` → `mobilePopBeginDate`, `MobilePopEndDate` → `mobilePopEndDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
set @strSQL = ' select * from notice where notice_type = ''' + @div + ''''
set @strSQL = ' select  * from notice where 1=1 '
set @strSQL = @strSQL + ' and notice_no = ' + cast(@num as varchar(12))
set @strSQL = @strSQL + ' order by notice_write_date desc '
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db225"></a>
## SMARTBILL3.dbo.upAdmSB_Lst_EachQna

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@div` | `varchar(12)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@cnt` | `varchar(12)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@num` | `varchar(12)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-05-28T11:12:17.927 |
| 읽기·참조 객체 | `smartbill3.dbo.qna` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [fetchQna](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/qna/repository/AdminQnaMapper.kt#L115) — 바인딩: `div`, `cnt`, `num`. 결과 매핑: `QNA_NO` → `qnaNo`, `QNA_TYPE` → `qnaType`, `QNA_TITLE` → `qnaTitle`, `QNA_WRITER` → `qnaWriter`, `QNA_CONTENTS` → `qnaContents`, `QNA_REF` → `qnaRef`, `QNA_STEP` → `qnaStep`, `QNA_TN` → `qnaTn`, `QNA_PN` → `qnaPn`, `QNA_HIT` → `qnaHit`, `QNA_WRITE_DATE` → `qnaWriteDate`, `MEM_NO` → `memNo`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
set @strSQL = ' select top '+@cnt+' QNA_NO, QNA_TYPE, QNA_TITLE, QNA_TITLE_SE, QNA_WRITER, QNA_WRITER_SE,
QNA_CONTENTS_SE, QNA_REF, QNA_STEP, QNA_ANSNUM, QNA_TN, QNA_TN, QNA_HIT, QNA_WRITE_DATE, MEM_NO, SMS_YN, SMS_HP_NO, SMS_SEND_YN from qna where qna_step=0 '
set @strSQL = ' select QNA_NO, QNA_TYPE, QNA_TITLE, QNA_TITLE_SE, QNA_WRITER, QNA_WRITER_SE,
QNA_CONTENTS_SE, QNA_REF, QNA_STEP, QNA_ANSNUM, QNA_TN, QNA_TN, QNA_HIT, QNA_WRITE_DATE, MEM_NO, SMS_YN, SMS_HP_NO, SMS_SEND_YN from qna where 1=1 '
set @strSQL = ' select top '+@cnt+' QNA_NO, QNA_TYPE, QNA_TITLE, QNA_TITLE_SE, QNA_WRITER, QNA_WRITER_SE,
QNA_CONTENTS_SE, QNA_REF, QNA_STEP, QNA_ANSNUM, QNA_TN, QNA_TN, QNA_HIT, QNA_WRITE_DATE, MEM_NO, SMS_YN, SMS_HP_NO, SMS_SEND_YN from qna where qna_type ='''+@div+''' and qna_step=0'
set @strSQL = ' select QNA_NO, QNA_TYPE, QNA_TITLE, QNA_TITLE_SE, QNA_WRITER, QNA_WRITER_SE,
QNA_CONTENTS_SE, QNA_REF, QNA_STEP, QNA_ANSNUM, QNA_TN, QNA_TN, QNA_HIT, QNA_WRITE_DATE, MEM_NO, SMS_YN, SMS_HP_NO, SMS_SEND_YN from qna where qna_type='''+@div+' and 1=1 '
set @strSQL = @strSQL + ' and qna_no =  '+ @num
set @strSQL = @strSQL + ' order by qna_write_date desc'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db226"></a>
## SmartBill3.dbo.upAdmSB_Lst_SumDailyDTI01

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@yymm` | `varchar(7)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:29.400 |
| 읽기·참조 객체 | `smartbill3.dbo.mng_daily_sum` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectDailyGeneralTaxInvoiceUsage](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/dailygeneraltaxinvoiceusage/repository/DailyGeneralTaxInvoiceUsageMapper.kt#L35) — 바인딩: `yymm, mode=IN, jdbcType=VARCHAR`. 결과 매핑: `use_date` → `useDate`, `ar_com_count` → `arComCount`, `ar_dti_count` → `arDtiCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
where  convert(varchar(7),use_date,120)=@yymm
order by use_date
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db227"></a>
## SmartBill3.dbo.upAdmSB_LstCom

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2020-01-08T13:50:16.803 |
| 읽기·참조 객체 | `migration_etcasp.dbo.migration_mapping_company`, `sb_dti.dbo.company_dticonfig`, `sb_dti.dbo.company_mng_info`, `sb_dti.dbo.company_quit_status`, `sb_dti.dbo.nts_all_send`, `sb_dti.dbo.nts_transmit_method`, `smartbill3.dbo.company`, `smartbill3.dbo.dct_company_config`, `smartbill3.dbo.dct_multi_use` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [fetchDetail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankCompanyMapper.kt#L131) — 바인딩: `comNo`. 결과 매핑: `COM_NO` → `comNo`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `COM_PRESIDENT` → `comPresident`, `COM_ZIPCODE` → `comZipcode`, `COM_ADDRESS` → `comAddress`, `COM_STATUS` → `comStatus`, `COM_SEAL` → `comSeal`, `CERT_DN` → `certDn`, `COM_ENTRY_DATE` → `comEntryDate`, `COM_BIZSTATUS` → `comBizstatus`, `COM_BIZCLASS` → `comBizclass`, `TAX_TYPE` → `taxType`, `NTS_APPLY_DATE` → `ntsApplyDate`, `SEARCH_DATE` → `searchDate`, `M_FLAG` → `mFlag`, `DELAY_ISSUE_YN` → `delayIssueYn`, `TAXFREE_ISSUE_YN` → `taxfreeIssueYn`, `DELAY_NTS_YN` → `delayNtsYn`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT JOIN SB_DTI.DBO.COMPANY_DTICONFIG CD WITH (NOLOCK) ON C.COM_NO = CD.COM_NO
LEFT JOIN SB_DTI.DBO.NTS_TRANSMIT_METHOD NTM WITH (NOLOCK) ON C.COM_NO = NTM.COM_NO
LEFT JOIN SB_DTI.DBO.COMPANY_MNG_INFO MI WITH (NOLOCK) ON C.COM_NO = MI.COM_NO
LEFT JOIN SB_DTI.DBO.COMPANY_QUIT_STATUS Q WITH (NOLOCK) ON C.COM_REGNO=Q.COM_REGNO
LEFT JOIN SB_DTI.DBO.NTS_ALL_SEND NN WITH (NOLOCK) ON C.COM_REGNO = NN.COM_REGNO
LEFT JOIN SMARTBILL3.DBO.DCT_MULTI_USE MULTI WITH (NOLOCK) ON C.COM_NO = MULTI.COM_NO
LEFT JOIN SMARTBILL3.DBO.DCT_COMPANY_CONFIG DCTCON WITH (NOLOCK) ON C.COM_NO = DCTCON.COM_NO
LEFT JOIN MIGRATION_ETCASP..MIGRATION_MAPPING_COMPANY MIG WITH (NOLOCK) ON C.COM_NO = MIG.COM_NO
WHERE C.COM_NO = @COM_NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db228"></a>
## SmartBill3.dbo.upAdmSB_LstDeptMng

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@service_type` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@com_no` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-02-01T10:28:25.470 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.dept_manager`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findDeptManager](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankCompanyMapper.kt#L178) — 바인딩: `serviceType`, `comNo`. 결과 매핑: `mem_no` → `memNo`, `mem_name` → `memName`, `mem_realname` → `memRealname`, `mem_tel` → `memTel`, `mem_hp` → `memHp`, `mem_email` → `memEmail`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
left outer join smartbill3.dbo.company c on dm.com_no = c.com_no
left outer join smartbill3.dbo.member m on dm.mem_no = m.mem_no
where  dm.com_no = @com_no and dm.service_type = @service_type  and m.mem_del_yn = 'N'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db229"></a>
## SmartBill3.dbo.upAdmSB_LstMem

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@no` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@GUBUN` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2023-04-17T10:01:08.060 |
| 읽기·참조 객체 | `sb_dti_log.dbo.dormant_member`, `sb_dti_log.dbo.member_login_his`, `sb_mobile.dbo.member`, `smartbill3.dbo.company`, `smartbill3.dbo.member`, `smartbill3.dbo.member_agreement` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [fetchDormantMember](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankMemberMapper.kt#L180) — 바인딩: `memNo`. 결과 매핑: `COM_NO` → `comNo`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `MEM_NO` → `memNo`, `MEM_NAME` → `memName`, `MEM_REGNO` → `memRegno`, `MEM_ID` → `memId`, `MEM_TYPE` → `memType`, `MEM_TEL` → `memTel`, `MEM_EMAIL` → `memEmail`, `MEM_ENTRY_DATE` → `memEntryDate`, `MEM_HP` → `memHp`, `MEM_REALNAME` → `memRealname`, `MEM_MODIFY_DATE` → `memModifyDate`, `RESULTMAIL_SEND_YN` → `resultMailSendYn`, `INFOMAIL_RECEIVE_YN` → `infoMailReceiveYn`, `INFORSMS_RECEIVE_YN` → `infoSmsReceiveYn`, `TEL_RECEIVE_YN` → `telReceiveYn`.
- [fetchActiveMember](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankMemberMapper.kt#L149) — 바인딩: `memNo`. 결과 매핑: `COM_NO` → `comNo`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `MEM_NO` → `memNo`, `MEM_NAME` → `memName`, `MEM_REGNO` → `memRegno`, `MEM_ID` → `memId`, `MEM_TYPE` → `memType`, `MEM_TEL` → `memTel`, `MEM_EMAIL` → `memEmail`, `MEM_STATUS` → `memStatus`, `MEM_ENTRY_DATE` → `memEntryDate`, `MEM_HP` → `memHp`, `MEM_REALNAME` → `memRealname`, `MEM_MODIFY_DATE` → `memModifyDate`, `last_login` → `lastLogin`, `RESULTMAIL_SEND_YN` → `resultMailSendYn`, `INFOMAIL_RECEIVE_YN` → `infoMailReceiveYn`, `INFORSMS_RECEIVE_YN` → `infoSmsReceiveYn`, `TEL_RECEIVE_YN` → `telReceiveYn`.
- [fetchMemberCompany](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/qna/repository/AdminQnaMapper.kt#L137) — 바인딩: `no`, `gubun`. 결과 매핑: `COM_REGNO` → `comRegno`, `COM_NAME` → `comName`, `MEM_NAME` → `memName`, `MEM_ID` → `memId`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
join sb_dti_log..dormant_MEMBER M WITH (NOLOCK) on C.COM_NO=M.COM_NO
LEFT OUTER JOIN SmartBill3..MEMBER_Agreement MA WITH(NOLOCK) ON M.mem_no = MA.mem_no
WHERE  M.MEM_NO = @NO AND (M.RESTORE_YN !='Y' OR M.RESTORE_YN IS NULL)
FROM  COMPANY C WITH (NOLOCK)join MEMBER M WITH (NOLOCK) on C.COM_NO=M.COM_NO
left join (select mem_no, max(login_date) as last_login from sb_dti_log..member_login_his with(nolock) group by mem_no) h on m.mem_no = h.mem_no
LEFT OUTER JOIN SmartBill3..MEMBER_Agreement MA WITH(NOLOCK) ON M.mem_no = MA.mem_no
LEFT JOIN SB_MOBILE..MEMBER MB WITH(NOLOCK) ON M.MEM_NO = MB.MEM_NO
WHERE  M.MEM_NO = @NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db230"></a>
## SmartBill3.dbo.upAdmSB_LstSttDelMem

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DIV` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2014-10-21T18:01:04.317 |
| 읽기·참조 객체 | `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchYearly](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/smartbillstatus/repository/WithdrawalMemberStatisticsMapper.kt#L55) — 바인딩: `div`, `startDate`, `endDate`. 결과 매핑: `YEAR` → `year`, `F_CNT` → `totalWithdrawals`.
- [searchMonthly](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/smartbillstatus/repository/WithdrawalMemberStatisticsMapper.kt#L45) — 바인딩: `div`, `startDate`, `endDate`. 결과 매핑: `YEAR` → `year`, `MONTH` → `month`, `F_CNT` → `totalWithdrawals`.
- [searchDaily](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/smartbillstatus/repository/WithdrawalMemberStatisticsMapper.kt#L34) — 바인딩: `div`, `startDate`, `endDate`. 결과 매핑: `YEAR` → `year`, `MONTH` → `month`, `DAY` → `day`, `F_CNT` → `totalWithdrawals`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @STRSQL =
WHERE
GROUP BY
ORDER BY
SET @STRSQL =
WHERE
GROUP BY YEAR(T1.MODIFY_DATE), MONTH(T1.MODIFY_DATE)
ORDER BY YEAR(T1.MODIFY_DATE) DESC,
SET @STRSQL =
WHERE
GROUP BY YEAR(T1.MODIFY_DATE)
ORDER BY YEAR(T1.MODIFY_DATE) DESC'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db231"></a>
## SmartBill3.dbo.upAdmSB_LstSttMem01

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@div` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@fDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@tDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2014-10-21T18:01:04.307 |
| 읽기·참조 객체 | `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchYearly](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/smartbillstatus/repository/MemberRegistrationStatisticsMapper.kt#L57) — 바인딩: `div`, `startDate`, `endDate`. 결과 매핑: `YEAR` → `year`, `F_CNT` → `corporateCount`, `G_CNT` → `individualCount`.
- [searchMonthly](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/smartbillstatus/repository/MemberRegistrationStatisticsMapper.kt#L46) — 바인딩: `div`, `startDate`, `endDate`. 결과 매핑: `YEAR` → `year`, `MONTH` → `month`, `F_CNT` → `corporateCount`, `G_CNT` → `individualCount`.
- [searchDaily](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/smartbillstatus/repository/MemberRegistrationStatisticsMapper.kt#L34) — 바인딩: `div`, `startDate`, `endDate`. 결과 매핑: `YEAR` → `year`, `MONTH` → `month`, `DAY` → `day`, `F_CNT` → `corporateCount`, `G_CNT` → `individualCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @STRSQL =
WHERE
GROUP BY YEAR(T1.MEM_ENTRY_DATE), MONTH(T1.MEM_ENTRY_DATE), DAY(T1.MEM_ENTRY_DATE)
ORDER BY YEAR(T1.MEM_ENTRY_DATE), MONTH(T1.MEM_ENTRY_DATE), DAY(T1.MEM_ENTRY_DATE)
SET @STRSQL =
WHERE
GROUP BY YEAR(T1.MEM_ENTRY_DATE), MONTH(T1.MEM_ENTRY_DATE)
ORDER BY YEAR(T1.MEM_ENTRY_DATE), MONTH(T1.MEM_ENTRY_DATE)
SET @STRSQL =
WHERE
GROUP BY YEAR(T1.MEM_ENTRY_DATE)
ORDER BY YEAR(T1.MEM_ENTRY_DATE)'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db232"></a>
## SmartBill3.dbo.upAdmSB_memOut

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@mem_no` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-04-26T11:26:16.790 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.company_history`, `smartbill3.dbo.dct_premium`, `smartbill3.dbo.dct_premium_balance`, `smartbill3.dbo.dct_premium_his`, `smartbill3.dbo.dept_admin`, `smartbill3.dbo.dept_admin_history`, `smartbill3.dbo.dept_manager`, `smartbill3.dbo.dept_manager_history`, `smartbill3.dbo.dept_member`, `smartbill3.dbo.dept_member_history`, `smartbill3.dbo.member`, `smartbill3.dbo.member_history`, `smartbill3.dbo.member_right`, `smartbill3.dbo.tax_member`, `smartbill3.dbo.tax_memgroup`, `smartbill3.dbo.tax_memgroup_detail` |
| 쓰기 대상 | `smartbill3.dbo.company`, `smartbill3.dbo.company_history`, `smartbill3.dbo.dct_premium`, `smartbill3.dbo.dct_premium_balance`, `smartbill3.dbo.dct_premium_his`, `smartbill3.dbo.dept_admin`, `smartbill3.dbo.dept_admin_history`, `smartbill3.dbo.dept_manager`, `smartbill3.dbo.dept_manager_history`, `smartbill3.dbo.dept_member`, `smartbill3.dbo.dept_member_history`, `smartbill3.dbo.member`, `smartbill3.dbo.member_history`, `smartbill3.dbo.member_right`, `smartbill3.dbo.tax_member`, `smartbill3.dbo.tax_memgroup_detail` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `2`; `0`; `1` |

### Mapper 입출력 매핑

- [withdrawMember](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankMemberMapper.kt#L234) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `memNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
select @strComNo = com_no, @strMemType = mem_type from smartbill3.dbo.member where mem_no = @mem_no
IF EXISTS (SELECT * FROM MEMBER WITH(NOLOCK) WHERE COM_NO = @STRCOMNO AND MEM_TYPE = 'G' AND MEM_STATUS = '1' AND MEM_DEL_YN = 'N')
Begin  Tran
mem_hp,mem_email,mem_status,mem_entry_date,mem_del_yn,mem_modify_date,tstamp , @mem_no from smartbill3.dbo.member where mem_no = @mem_no
where mem_no = @mem_no
delete from smartbill3.dbo.member_right where mem_no = @mem_no
WHERE COM_NO = @strComNo  AND GETDATE() BETWEEN start_date AND END_DATE  AND TOTAL_DISK > 0 )
WHERE COM_NO = @strComNo
ORDER BY ENTRY_DATE DESC
ma_id,tstamp , @mem_no from smartbill3.dbo.company where com_no = @strComNo
where com_no = @strComNo
where  mem_no = @mem_no
delete smartbill3.dbo.dept_manager where mem_no = @mem_no
where  mem_no = @mem_no
delete dept_admin where mem_no = @mem_no
where  mem_no = @mem_no
delete smartbill3.dbo.dept_member where mem_no = @mem_no
if exists(select tax_mem_no from smartbill3.dbo.tax_member where  mem_no=@mem_no and charindex(memagr,'AY')>0 )
```

하위 프로시저·함수·뷰: `smartbill3.dbo.updct_savpremium`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db233"></a>
## SmartBill3.dbo.upAdmSB_MemOutUse

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@service_type` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@mem_no` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:24.333 |
| 읽기·참조 객체 | `smartbill3.dbo.dct_main`, `smartbill3.dbo.tax_admin`, `smartbill3.dbo.tax_main` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findTaxCafe](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankMemberMapper.kt#L194) — 바인딩: `memNo`. 결과 매핑: `cafe_no` → `cafeNo`, `cafe_id` → `cafeId`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
join smartbill3.dbo.dti_status ds on dm.dti_idx=ds.dti_idx
where   (sup_idx = @mem_no or byr_idx = @mem_no )
where  reg_memno  = @mem_no
join  smartbill3.dbo.tax_main tm on ta.cafe_id = tm.cafe_id
where   ta.mem_no=@mem_no
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db234"></a>
## SmartBill3.dbo.upAdmSB_memSchPay

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@no` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2006-05-20T14:50:17.780 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_refund` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findPrepay](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankMemberMapper.kt#L208) — 바인딩: `comNo`. 결과 매핑: `amount` → `amount`, `ause` → `ause`, `arefund` → `arefund`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
set @strSql = ' select  c.com_no,c.com_name,c.com_regno ,sum(s.prepay_amt) amount, sum(s.use_amt) ause,
from  service_prepay s join company c on s.com_no=c.com_no
left outer join service_refund r on s.prepay_no = r.prepay_no
where c.com_no = '''+@no+'''
group by c.com_no, c.com_name, c.com_entry_date, c.com_regno '
Set @strSql = @strSql + 'order by c.com_entry_date desc'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db235"></a>
## SmartBill3.dbo.upAdmSB_ModNErrCode

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@n_idx` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@m_idx` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@error_code` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@description` | `varchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@support_desc` | `varchar(2000)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@detail_guide` | `varchar(2000)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@admin_no` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:29.017 |
| 읽기·참조 객체 | `smartbill3.dbo.msg_n_error_code` |
| 쓰기 대상 | `smartbill3.dbo.msg_n_error_code` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `0`; `1` |

### Mapper 입출력 매핑

- [update](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/errorcode/repository/ErrorCodeMapper.kt#L124) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `nIdx`, `mIdx`, `errorCode`, `errorDesc`, `supportDesc`, `detailGuide`, `adminNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
where n_idx = @n_idx
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db236"></a>
## SmartBill3.dbo.upAdmSB_PaymentRevocation

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@com_no` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@sw_no` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@rlstTxt` | `varchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:12.640 |
| 읽기·참조 객체 | `smartbill3.dbo.com_result_text`, `smartbill3.dbo.company`, `smartbill3.dbo.company_history` |
| 쓰기 대상 | `smartbill3.dbo.com_result_text`, `smartbill3.dbo.company`, `smartbill3.dbo.company_history` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `0`; `1` |

### Mapper 입출력 매핑

- [releaseUnpaidStatus](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoMapper.kt#L98) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `comNo`, `swNo`, `reason`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
from smartbill3.dbo.company where com_no = @com_no
where com_no = @com_no
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db237"></a>
## SMARTBILL3.dbo.upAdmSB_QSav

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@mod` | `varchar(5)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@no` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@id` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@com_no` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@mem_no` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@tel_no` | `tel` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@kind` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@title` | `title` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@contents` | `contents` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@status` | `varchar(5)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@req_name` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@slvcontents` | `contents` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@dept` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@name` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@com_name` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@com_regno` | `varchar(13)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@callback_date` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@div_market` | `char(2)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_bns_id` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@calsubkind` | `varchar(4)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@remote_yn` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:33.563 |
| 읽기·참조 객체 | `smartbill3.dbo.admin_call`, `smartbill3.dbo.admin_call_detail` |
| 쓰기 대상 | `smartbill3.dbo.admin_call`, `smartbill3.dbo.admin_call_detail` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `0`; `@sav_no` |

### Mapper 입출력 매핑

- [saveCallback](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptCtiMapper.kt#L80) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `call.callId`, `userId`, `call.companyId, jdbcType=INTEGER`, `call.memberId, jdbcType=INTEGER`, `call.phone, jdbcType=VARCHAR`, `call.kind, jdbcType=VARCHAR`, `call.title, jdbcType=VARCHAR`, `call.content, jdbcType=LONGVARCHAR`, `call.requesterName, jdbcType=VARCHAR`, `content, jdbcType=LONGVARCHAR`, `call.companyName, jdbcType=VARCHAR`, `call.businessNumber, jdbcType=VARCHAR`, `callbackDate`, `call.marketType, jdbcType=CHAR`, `call.hubCompanyId, jdbcType=INTEGER`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Begin Tran
set @sav_no = @@identity
where call_no = @no
set @sav_no = @no
rollback
commit
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db238"></a>
## SMARTBILL3.dbo.upAdmSB_SavFaq

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@gubun` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@div` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@num` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Faq_title` | `varchar(1000)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Faq_contents` | `text` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Faq_writer` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:06.550 |
| 읽기·참조 객체 | `smartbill3.dbo.faq` |
| 쓰기 대상 | `smartbill3.dbo.faq` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `0`; `1` |

### Mapper 입출력 매핑

- [saveFaq](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/faq/repository/AdminFaqMapper.kt#L108) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `gubun`, `div`, `num`, `faqTitle`, `faqContents`, `faqWriter`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Begin  Tran
where Faq_no = @num
set @strFaqTitleSe = 'u'
set @strFaqContentsSe = 'u'
where Faq_no = @num
rollback
Commit
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db239"></a>
## SmartBill3.dbo.upAdmSB_SavNErrCode

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@m_idx` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@error_code` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@description` | `varchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@support_desc` | `varchar(2000)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@detail_guide` | `varchar(2000)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@admin_no` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@mng_yn` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:29.873 |
| 읽기·참조 객체 | `smartbill3.dbo.msg_n_error_code` |
| 쓰기 대상 | `smartbill3.dbo.msg_n_error_code` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `-1`; `-1`; `1` |

### Mapper 입출력 매핑

- [insert](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/errorcode/repository/ErrorCodeMapper.kt#L112) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `mIdx`, `errorCode`, `errorDesc`, `supportDesc`, `detailGuide`, `adminNo`, `mngYn`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
If Exists(select n_idx from smartbill3.dbo.msg_n_error_code where error_code = @error_code)
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db240"></a>
## SMARTBILL3.dbo.upAdmSB_SavNotice

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@gubun` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@div` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@num` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Notice_title` | `title` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Notice_contents` | `contents` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MobileNoticeYN` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@WebNoticeYN` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MobilePopYN` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MobilePopBeginDate` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MobilePopEndDate` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:06.437 |
| 읽기·참조 객체 | `smartbill3.dbo.notice` |
| 쓰기 대상 | `smartbill3.dbo.notice` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `0`; `1` |

### Mapper 입출력 매핑

- [saveNotice](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/notice/repository/AdminNoticeMapper.kt#L90) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `gubun`, `div`, `num`, `noticeTitle`, `noticeContents`, `mobileNoticeYn`, `webNoticeYn`, `mobilePopYn`, `mobilePopBeginDate, jdbcType=TIMESTAMP`, `mobilePopEndDate, jdbcType=TIMESTAMP`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Begin  Tran
where notice_no = @num
set @strNoticeTitleSe = 'u'
set @strNoticeContentsSe = 'u'
where Notice_no = @num
rollback
Commit
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db241"></a>
## SMARTBILL3.dbo.upAdmSB_SavNotice_Bona

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@gubun` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@num` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Notice_title` | `title` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Notice_contents` | `contents` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2017-03-16T15:01:20.717 |
| 읽기·참조 객체 | `smartbill3.dbo.notice` |
| 쓰기 대상 | `smartbill3.dbo.notice` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `0`; `1` |

### Mapper 입출력 매핑

- [saveNotice](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/notice/repository/BonabankNoticeMapper.kt#L76) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `gubun`, `num`, `noticeTitle`, `noticeContents`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
Begin  Tran
where notice_no = @num
set @strNoticeTitleSe = 'u'
set @strNoticeContentsSe = 'u'
where Notice_no = @num
rollback
Commit
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db242"></a>
## SMARTBILL3.dbo.upAdmSB_SavPds

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@div` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@num` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@title` | `title` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@writer` | `name` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@contents` | `contents` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@file` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:09.010 |
| 읽기·참조 객체 | `smartbill3.dbo.pds` |
| 쓰기 대상 | `smartbill3.dbo.pds` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `0`; `1` |

### Mapper 입출력 매핑

- [savePds](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/pds/repository/AdminPdsMapper.kt#L103) — 바인딩: `result, mode=OUT, jdbcType=INTEGER`, `gubun`, `num`, `title`, `writer`, `contents`, `file, jdbcType=NVARCHAR`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
begin tran
where pds_no=@num
set @strPdsTitleSe = 'u'
set @strPdsContentsSe = 'u'
set @strPdsWriterSe = 'u'
where pds_no=@num
where pds_no=@num
rollback
commit
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db243"></a>
## SmartBill3.dbo.upAdmSB_Sch_SumMonthDTI01

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@from_yymm` | `varchar(7)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@to_yymm` | `varchar(7)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:11.620 |
| 읽기·참조 객체 | `smartbill3.dbo.mng_monthly_sum` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectMonthlyTaxInvoiceUsage](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/monthlytaxinvoiceusage/repository/MonthlyTaxInvoiceUsageMapper.kt#L40) — 바인딩: `fromYymm, mode=IN, jdbcType=VARCHAR`, `toYymm,   mode=IN, jdbcType=VARCHAR`. 결과 매핑: `use_yymm` → `useYymm`, `ar_com_count` → `arComCount`, `ar_dti_count` → `arDtiCount`, `mem_count` → `memCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
where use_yymm between @from_yymm and @to_yymm
order by use_yymm
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db244"></a>
## SMARTBILL3.dbo.upAdmSB_SchCMSAccount

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@com_no` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-08-09T17:31:02.533 |
| 읽기·참조 객체 | `sb_bill.dbo.bill_common_code`, `smartbill3.dbo.cms_account`, `smartbill3.dbo.cms_account_cub`, `smartbill3.dbo.cms_account_eb11`, `smartbill3.dbo.cms_account_eb11_cub`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getCmsAccountList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L600) — 바인딩: `comNo`. 결과 매핑: `IDX` → `idx`, `BANK_CODE` → `bankCode`, `BANK_ACCNO` → `bankAccno`, `BANK_REGNO` → `bankRegno`, `BANK_ACCNAME` → `bankAccname`, `BANK_ACCSTATE` → `bankAccstate`, `WDATE` → `wdate`, `MEM_NAME` → `memName`, `BANK_NAME` → `bankName`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE COM_NO = @COM_NO
WHERE COM_NO = @COM_NO
LEFT OUTER join smartbill3.dbo.member m on cm.mem_no = m.mem_no
LEFT OUTER JOIN SB_BILL..BILL_COMMON_CODE BCC WITH (NOLOCK)
where  cm.com_no = @com_no
order by WDATE desc,IDX DESC
```

하위 프로시저·함수·뷰: `master.dbo.clr_dec_char_sel_tc`, `master.dbo.dec_char_sel_tc`, `smartbill3.dbo.cms_account`, `smartbill3.dbo.cms_account_eb11`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db245"></a>
## SmartBill3.dbo.upAdmSB_SchCom_bona

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@page` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@top` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@fromDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@toDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@strItem` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@strContents` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@cStatus` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-10-28T15:01:07.217 |
| 읽기·참조 객체 | `migration_etcasp.dbo.migration_mapping_company`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchCompanies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankCompanyMapper.kt#L69) — 바인딩: `page`, `top`, `fromDate`, `toDate`, `strItem`, `strContents`, `cStatus`. 결과 매핑: `com_no` → `comNo`, `com_name` → `comName`, `com_regno` → `comRegno`, `com_president` → `comPresident`, `com_entry_date` → `comEntryDate`, `com_status` → `comStatus`, `com_del_yn` → `comDelYn`, `com_address` → `comAddress`, `mem_hp` → `memHp`, `mem_tel` → `memTel`, `cert_dn` → `certDn`, `TOT_COUNT` → `totCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @TOP2 = @TOT_COUNT - ( @PAGE - 1 ) * @TOP
SET @TOP2 = @TOP
SET @SQL = '
join smartbill3.dbo.company c with(nolock)
left join  smartbill3.dbo.member m
where  1=1 '
SET @SQL = @SQL + N'
ORDER BY c.com_entry_date DESC
ORDER BY com_entry_date ASC
join smartbill3.dbo.company c with(nolock)
left join  smartbill3.dbo.member m
INNER JOIN LASTPAGES AS V
ORDER BY c.com_entry_date DESC'
```

하위 프로시저·함수·뷰: `smartbill3.dbo.upadmsb_schcom_bona_count`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db246"></a>
## SmartBill3.dbo.upAdmSB_SchCom_bona_Excel

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@fromDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@toDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@strItem` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@strContents` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@cStatus` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-08-07T09:20:49.340 |
| 읽기·참조 객체 | `migration_etcasp.dbo.migration_mapping_company`, `sb_dti.dbo.company_dticonfig`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [fetchForExport](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankCompanyMapper.kt#L96) — 바인딩: `fromDate`, `toDate`, `strItem`, `strContents`, `cStatus`. 결과 매핑: `com_no` → `comNo`, `com_name` → `comName`, `com_regno` → `comRegno`, `com_president` → `comPresident`, `com_entry_date` → `comEntryDate`, `com_status` → `comStatus`, `com_del_yn` → `comDelYn`, `com_address` → `comAddress`, `mem_hp` → `memHp`, `mem_tel` → `memTel`, `cert_dn` → `certDn`, `Delay_Issue_YN` → `delayIssueYn`, `TAXFREE_ISSUE_YN` → `taxFreeIssueYn`, `DELAY_NTS_YN` → `delayNtsYn`, `DATA_MIGRATION` → `dataMigration`, `M_COMREGNO` → `mComRegno`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SQL = '
join smartbill3.dbo.company c with(nolock)
left join  smartbill3.dbo.member m
LEFT JOIN SB_DTI.DBO.COMPANY_DTICONFIG CD WITH (NOLOCK) ON C.COM_NO = CD.COM_NO
LEFT JOIN (select M_comregno from MIGRATION_ETCASP..MIGRATION_DATA_AGREE_COMINFO WITH(NOLOCK) WHERE M_FALG_DESC = ''ETAXBILL'') MI ON C.COM_REGNO = MI.M_COMREGNO
where  1=1 '
SET @SQL = @SQL + N'
ORDER BY c.com_entry_date DESC'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db247"></a>
## SmartBill3.dbo.upAdmSB_SchCREDITACCOUNT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:34.620 |
| 읽기·참조 객체 | `sb_bill.dbo.cardbilling_auth`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getCreditCardList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L610) — 바인딩: `comNo`. 결과 매핑: `MEM_REALNAME` → `memRealname`, `FINANCENAME` → `financeName`, `CDATE` → `cdate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
JOIN SMARTBILL3.dbo.MEMBER M ON A.MEMNO = M.MEM_NO
WHERE COMNO = @COM_NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db248"></a>
## SmartBill3.dbo.upAdmSB_SchInvAmt

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2018-03-08T15:03:37.387 |
| 읽기·참조 객체 | `sb_bill.dbo.invoice`, `sb_bill.dbo.payment`, `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findInvoice](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankMemberMapper.kt#L224) — 바인딩: `comNo`. 결과 매핑: `SUM_INV_AMT` → `sumInvAmt`, `SUM_UNPAY_AMT` → `sumUnpayAmt`, `INV_RESULT` → `invResult`, `PAY_AMT` → `payAmt`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @CHARGE_MONTH = cast(year(getdate()) as varchar) + dbo.fnfillDigit(2,'0',cast(month(getdate()) as varchar))
WHERE DIVISION = 'UNPAY' AND COMNO = @COM_NO AND CHARGEMONTH = @CHARGE_MONTH   ORDER BY CHARGEMONTH DESC)AS SUM_UNPAY_AMT,
JOIN SMARTBILL3..COMPANY B
LEFT JOIN (SELECT SUM(PAYMENTAMOUNT)AS PAY_AMT, COMNO FROM SB_BILL..PAYMENT WHERE COMNO = @COM_NO
AND CHARGEMONTH = @CHARGE_MONTH  GROUP BY COMNO) C
WHERE COM_NO = @COM_NO AND A.CHARGEMONTH = @CHARGE_MONTH
GROUP BY A.CHARGEMONTH ORDER BY A.CHARGEMONTH DESC
```

하위 프로시저·함수·뷰: `smartbill3.dbo.fnfilldigit`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db249"></a>
## SMARTBILL3.dbo.upAdmSB_SchPds

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@pdsNo` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:16.993 |
| 읽기·참조 객체 | `smartbill3.dbo.pds` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [fetchFilePathByNo](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/pds/repository/AdminPdsMapper.kt#L81) — 바인딩: `pdsNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
where  	pds_no=@pdsNo
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db250"></a>
## SmartBill3.dbo.upAdmSB_TaxAdm_lst

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@com_no` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:18.027 |
| 읽기·참조 객체 | `smartbill3.dbo.member`, `smartbill3.dbo.tax_admin` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findTaxAdmin](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankCompanyMapper.kt#L196) — 바인딩: `comNo`. 결과 매핑: `mem_no` → `memNo`, `mem_name` → `memName`, `mem_realname` → `memRealname`, `mem_tel` → `memTel`, `mem_hp` → `memHp`, `mem_email` → `memEmail`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
join 	smartbill3.dbo.member me on ca.mem_no = me.mem_no
where me.com_no = @com_no  and mem_rgt='F'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db251"></a>
## SMARTBILL3.dbo.upCMS_LstEachCMS

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2022-08-23T15:33:31.040 |
| 읽기·참조 객체 | `sb_bill.dbo.bill_common_code`, `smartbill3.dbo.cms_account`, `smartbill3.dbo.cms_account_cub`, `smartbill3.dbo.cms_account_eb11`, `smartbill3.dbo.cms_account_eb11_cub`, `smartbill3.dbo.cms_withdrawal_agreement`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getCmsHistoryList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L650) — 바인딩: `comNo`. 결과 매핑: `COM_NO` → `comNo`, `MEM_NO` → `memNo`, `BANK_CODE` → `bankCode`, `BANK_ACCNO` → `bankAccno`, `BANK_REGNO` → `bankRegno`, `BANK_ACCNAME` → `bankAccname`, `WDATE` → `wdate`, `MEM_REALNAME` → `memRealname`, `BANK_ACCSTATE` → `bankAccstate`, `NPKI` → `npki`, `BANK_NAME` → `bankName`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE COM_NO = @COM_NO
WHERE COM_NO = @COM_NO
LEFT OUTER JOIN SMARTBILL3.DBO.MEMBER M WITH(NOLOCK) ON CA.MEM_NO = M.MEM_NO
LEFT OUTER JOIN SMARTBILL3.DBO.CMS_WITHDRAWAL_AGREEMENT  CW WITH(NOLOCK) ON CW.ACCOUNT_IDX = CA.IDX
LEFT OUTER JOIN SB_BILL..BILL_COMMON_CODE BCC WITH (NOLOCK)  ON CA.BANK_CODE = BCC.CODE  AND BCC.CODE_TYPE = 'BANKCODE'
WHERE
ORDER BY WDATE DESC
```

하위 프로시저·함수·뷰: `master.dbo.clr_dec_char_sel_tc`, `master.dbo.dec_char_sel_tc`, `smartbill3.dbo.cms_account`, `smartbill3.dbo.cms_account_eb11`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db252"></a>
## SMARTBILL3.dbo.upDCT_MultiUse_YN

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@USE_YN` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:18.980 |
| 읽기·참조 객체 | `smartbill3.dbo.dct_multi_use` |
| 쓰기 대상 | `smartbill3.dbo.dct_multi_use` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [saveMultiUseYn](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L919) — 바인딩: `comNo`, `useYn`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
IF NOT EXISTS (SELECT * FROM dbo.DCT_MULTI_USE WHERE COM_NO = @COM_NO)
WHERE
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db253"></a>
## SMARTBILL3.dbo.upDCT_SavDctDefaultDisk

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DEFAULT_DISK` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ATTACHFILE_DEL_YN` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ATTACHFILE_LIMIT_SIZE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2019-04-30T13:37:19.553 |
| 읽기·참조 객체 | `smartbill3.dbo.dct_company_config` |
| 쓰기 대상 | `smartbill3.dbo.dct_company_config` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [saveDctDefaultDisk](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L907) — 바인딩: `comNo`, `defaultDisk`, `attachfileDelYn`, `attachfileLimitSize`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
IF EXISTS(SELECT COM_NO FROM SMARTBILL3..DCT_COMPANY_CONFIG WHERE COM_NO = @COM_NO)
WHERE COM_NO = @COM_NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db254"></a>
## SMARTBILL3.dbo.upGW_CompanyException_Info

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-26T16:39:09.340 |
| 읽기·참조 객체 | `smartbill3.dbo.company_exception` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getExceptionSettings](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L807) — 바인딩: `comNo`. 결과 매핑: `BRK_GUESTSUP_YN` → `brkGuestsupYn`, `OAPI_SNDMAIL_ADM_RREQ_YN` → `oapiSndmailAdmRreqYn`, `RREQ_CANCEL_NON_MEM_RECV_MAIL_YN` → `rreqCancelNonMemRecvMailYn`, `OAPI_MULTI_ISSUE_RESTRICTION_YN_FAP` → `oapiMultiIssueRestrictionYnFap`, `OAPI_MULTI_ISSUE_RESTRICTION_YN_FAR` → `oapiMultiIssueRestrictionYnFar`, `OAPI_MULTI_ISSUE_RESTRICTION_YN_RAR` → `oapiMultiIssueRestrictionYnRar`, `OAPI_MULTI_ISSUE_RESTRICTION_YN_RAP` → `oapiMultiIssueRestrictionYnRap`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db255"></a>
## SMARTBILL3.dbo.upGW_CompanyException_Info_Reg

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@USE_YN` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@USER` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@EXCEPT_CODE` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2024-08-07T16:48:49.780 |
| 읽기·참조 객체 | `smartbill3.dbo.company_exception` |
| 쓰기 대상 | `smartbill3.dbo.company_exception` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [updateExceptionSetting](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L849) — 바인딩: `comNo`, `useYn`, `user`, `exceptCode`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE 	COM_NO 		= @COM_NO
WHERE 	COM_NO 		= @COM_NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db256"></a>
## SMARTBILL3.dbo.upMem_CfmInvAmt

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@com_no` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:33.317 |
| 읽기·참조 객체 | `sb_bill.dbo.invoice`, `sb_bill.dbo.payment`, `smartbill3.dbo.sum_invoice` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getInvoiceAmount](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L576) — 바인딩: `comNo`. 결과 매핑: `inv_amt` → `invAmt`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
set @strInvYYMM = convert(varchar(6),getdate(),112)
set @strPreYYMM = convert(varchar(6),dateadd(m,-1,getdate()),112)
if exists(select * from admin_demand_company where ((dti_wdate between '01' and '10') or dti_wdate in ('30', '31')) and com_no = @com_no)
set @strSQL = '  select   isnull(sum(sum_inv_amt),0) as inv_amt
where inv_yn = ''1''
set @strSQL = '  select   isnull(sum(sum_inv_amt),0) as inv_amt
where inv_yn = ''1''
set @strSQL = '  select   sum(sum_inv_amt) as inv_amt
where inv_yn = ''1''
WHERE COMNO = @COM_NO ORDER BY CHARGEMONTH DESC
(SELECT SUM(AMOUNT) FROM SB_BILL..INVOICE WHERE COMNO = @COM_NO AND CHARGEMONTH = @CHARGE_MONTH
(SELECT SUM(PAYMENTAMOUNT) FROM SB_BILL..PAYMENT WHERE COMNO = @COM_NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db257"></a>
## SMARTBILL3.dbo.upMem_CfmPrepayAmt

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@com_no` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:10.473 |
| 읽기·참조 객체 | `smartbill3.dbo.service_prepay` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getPrepaymentBalance](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L584) — 바인딩: `comNo`. 결과 매핑: `balance_amt` → `balanceAmt`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
select @strMaxNo = max(prepay_no) from smartbill3.dbo.service_prepay where com_no = cast(@com_no as integer)
set @strSQL = '  select  (principal_amt - use_amt) as balance_amt
where prepay_no = ' + cast( @strMaxNo as varchar(10))
set @strSQL = ' select (principal_amt - use_amt) as balance_amt from smartbill3.dbo.service_prepay where 1=0 '
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db258"></a>
## SMARTBILL3.dbo.upMem_DelComSeal

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@com_no` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:10.660 |
| 읽기·참조 객체 | `smartbill3.dbo.company` |
| 쓰기 대상 | `smartbill3.dbo.company` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [deleteSeal](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L1165) — 바인딩: `comNo, mode=IN, jdbcType=INTEGER`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
where    	com_no = @com_no
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db259"></a>
## SMARTBILL3.dbo.upMem_LstPds

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@cnt` | `varchar(12)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@num` | `varchar(12)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2006-05-20T14:51:12.780 |
| 읽기·참조 객체 | `smartbill3.dbo.pds` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [fetchPds](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/pds/repository/AdminPdsMapper.kt#L70) — 바인딩: `cnt`, `num`. 결과 매핑: `PDS_NO` → `pdsNo`, `PDS_TITLE` → `pdsTitle`, `PDS_WRITER` → `pdsWriter`, `PDS_CONTENTS` → `pdsContents`, `PDS_FILE` → `pdsFile`, `PDS_HIT` → `pdsHit`, `PDS_WRITE_DATE` → `pdsWriteDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
set @strSQL = ' select top '+@cnt+' * from pds '
set @strSQL = ' select * from pds where 1=1 '
set @strSQL = @strSQL + ' and pds_no = ''' + @num + ''''
set @strSQL = @strSQL + ' order by pds_write_date desc '
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db260"></a>
## SmartBill3.dbo.upMem_LstPrePay2

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@com_no` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@fromdate` | `varchar(8)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@todate` | `varchar(8)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2016-09-02T21:48:13.347 |
| 읽기·참조 객체 | `smartbill3.dbo.member`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getPrepayHistory](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L517) — 바인딩: `comNo`, `fromDate`, `toDate`. 결과 매핑: `prepay_date` → `prepayDate`, `prepay_amt` → `prepayAmt`, `carryover_amt` → `carryoverAmt`, `principal_amt` → `principalAmt`, `use_amt` → `useAmt`, `pay_method` → `payMethod`, `refund_amt` → `refundAmt`, `mem_name` → `memName`, `statementAmount` → `statementAmount`, `cdate` → `lapseDate`, `prepay_no` → `prepayNo`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
from 	smartbill3.dbo.service_prepay sp left outer join smartbill3.dbo.member m on sp.prepay_mem_no = m.mem_no
left outer join (select idx, statementAmount, cdate from smartbill3.dbo.service_prepay_his where channel = 'LAPSE') sph on sp.prepay_no = sph.idx
where 	sp.com_no = @com_no
order by sp.prepay_date desc
from 	smartbill3.dbo.service_prepay sp left outer join smartbill3.dbo.member m on sp.prepay_mem_no = m.mem_no
left outer join (select idx, statementAmount, cdate from smartbill3.dbo.service_prepay_his where channel = 'LAPSE') sph on sp.prepay_no = sph.idx
where 	sp.com_no = @com_no
order by sp.prepay_date desc
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db261"></a>
## SMARTBILL3.dbo.upMem_LstSettleHis

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@service_type` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@com_no` | `no` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2019-09-30T12:01:24.100 |
| 읽기·참조 객체 | `sb_bill.dbo.package_fee_mapping`, `sb_bill.dbo.package_fee_mapping_history`, `smartbill3.dbo.member`, `smartbill3.dbo.settlement`, `smartbill3.dbo.settlement_history` |
| 쓰기 대상 | 쓰기문 존재; 별칭·임시 객체 또는 동적 대상의 영향은 추가 확인 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getPricingPlanHistory](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L663) — 바인딩: `serviceType`, `comNo`. 결과 매핑: `FROM_DATE` → `fromDate`, `TO_DATE` → `toDate`, `BILL_TYPE` → `billType`, `MOD_DATE` → `modDate`, `NAME` → `name`, `PACKAGE_CODE` → `packageCode`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
left outer join smartbill3.dbo.member m on s.update_no = m.mem_no
LEFT OUTER JOIN (SELECT COM_NO,PACKAGE_CODE  FROM SB_BILL..PACKAGE_FEE_MAPPING  WHERE COM_NO=@com_no AND USE_YN = 'Y' ) P ON S.COM_NO = P.COM_NO
where s.com_no = @com_no and s.service_type = @service_type
left outer join smartbill3.dbo.member m on sh.update_no = m.mem_no
LEFT OUTER JOIN (SELECT SETTLE_HISTORY_NO,COM_NO,PACKAGE_CODE  FROM SB_BILL..[PACKAGE_FEE_MAPPING_HISTORY]  WHERE COM_NO=@COM_NO AND USE_YN = 'Y' ) PH ON SH.SETTLE_HISTORY_NO = PH.SETTLE_HISTORY_NO
where sh.com_no = @com_no and sh.service_type = @service_type  ) a
order by a.from_date desc
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db262"></a>
## SMARTBILL3.dbo.upMem_SchPds

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@SchItem` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SchText` | `varchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2006-05-20T14:51:15.293 |
| 읽기·참조 객체 | `smartbill3.dbo.pds` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchPds](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/pds/repository/AdminPdsMapper.kt#L52) — 바인딩: `schItem`, `schText`. 결과 매핑: `pds_no` → `pdsNo`, `pds_title` → `pdsTitle`, `pds_writer` → `pdsWriter`, `pds_file` → `pdsFile`, `pds_hit` → `pdsHit`, `pds_write_date` → `pdsWriteDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
set @strSQL = ' 	select  pds_no, pds_title, pds_writer, pds_contents, pds_file, pds_hit, pds_write_date
where '+@SchItem+' like ''%'+@SchText+'%''
order by pds_no desc '
set @strSQL = '	select  pds_no, pds_title, pds_writer, pds_contents, pds_file, pds_hit, pds_write_date
order by pds_no desc '
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db263"></a>
## SmartBill3.dbo.upSave_BlockChain_Admin_Change

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@ORG_SEQ` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@USR_SEQ` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2021-12-07T16:02:29.660 |
| 읽기·참조 객체 | `sec_pt.dbo.tbl_pt_org_usr` |
| 쓰기 대상 | `sec_pt.dbo.tbl_pt_org_usr` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [changeCompanyAdmin](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/company/repository/GlosignCompanyMapper.kt#L82) — 바인딩: `orgSeq`, `usrSeq`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
UPDATE SEC_PT..TBL_PT_ORG_USR SET CADM = 0 WHERE ORG_SEQ = @ORG_SEQ;
UPDATE SEC_PT..TBL_PT_ORG_USR SET CADM = 1 WHERE ORG_SEQ = @ORG_SEQ AND USR_SEQ = @USR_SEQ;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db264"></a>
## SmartBill3.dbo.upSave_BlockChain_LockFail_Reset

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@CTR_SEQ` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2021-12-02T14:12:57.547 |
| 읽기·참조 객체 | `sec_pt.dbo.tbl_pt_ctr_lock` |
| 쓰기 대상 | `sec_pt.dbo.tbl_pt_ctr_lock` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [resetLockFail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/lockreset/repository/BlockchainLockMapper.kt#L54) — 바인딩: `ctrSeq`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
UPDATE SEC_PT..TBL_PT_CTR_LOCK SET FAIL_CNT = 0 WHERE CTR_SEQ = @CTR_SEQ
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db265"></a>
## SmartBill3.dbo.V_DUMMY_COMPANY_EXCEPTION

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `COM_NO` | `int` | 불가 | 아니오 |
| `USE_YN` | `varchar(1)` | 허용 | 아니오 |
| `COM_REGNO` | `varchar(13)` | 불가 | 아니오 |
| `COM_REGNO#` | `varchar(52)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | VIEW / 2021-09-14T15:50:18.597 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.company_exception`, `smartbill3.dbo.v_dummy_company_exception` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getCompanyList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/registrationinquiry/repository/RegistrationInquiryMapper.kt#L104) — 바인딩: `cafeId,jdbcType=VARCHAR`, `searchText,jdbcType=NVARCHAR`, `searchText,jdbcType=VARCHAR`, `registrationFilter,jdbcType=VARCHAR`. 결과 매핑: `com_regno` → `comRegno`, `com_name` → `comName`, `email` → `email`, `hp` → `hp`, `SB_YN` → `sbYn`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
INNER JOIN SMARTBILL3..COMPANY C WITH(NOLOCK) ON C.COM_NO = CE.COM_NO
WHERE
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db266"></a>
## smartwork.dbo.action_reason

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `idx` | `bigint` | 불가 | 예 |
| `action_type` | `varchar(20)` | 불가 | 아니오 |
| `target_type` | `varchar(50)` | 불가 | 아니오 |
| `target_idx` | `varchar(max)` | 불가 | 아니오 |
| `reason` | `varchar(500)` | 불가 | 아니오 |
| `sw_no` | `int` | 불가 | 아니오 |
| `reg_date` | `datetime` | 불가 | 아니오 |
| `metadata` | `varchar(max)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-10-14T13:47:04.337 |
| 읽기·참조 객체 | `smartwork.dbo.action_reason` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [save](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/shared/actionreason/repository/ActionReasonMapper.kt#L16) — 바인딩: `actionType`, `targetType`, `targetIdx`, `reason`, `swNo`, `metadata`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db267"></a>
## smartwork.dbo.COMPANY_CHANGE_LOG

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `IDX` | `int` | 불가 | 예 |
| `COM_NO` | `int` | 불가 | 아니오 |
| `CHANGED_FIELD` | `nvarchar(100)` | 불가 | 아니오 |
| `BEFORE_VALUE` | `nvarchar(500)` | 허용 | 아니오 |
| `AFTER_VALUE` | `nvarchar(500)` | 허용 | 아니오 |
| `CHANGED_BY` | `nvarchar(100)` | 허용 | 아니오 |
| `CHANGE_DATE` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-03-27T15:25:58.853 |
| 읽기·참조 객체 | `smartwork.dbo.company_change_log` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [insertChangeLog](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L1144) — 바인딩: `comNo`, `changedField`, `beforeValue`, `afterValue`, `changedBy`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db268"></a>
## smartwork.dbo.COMPANY_TAX_INVOICE_EXT

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `COM_NO` | `int` | 불가 | 아니오 |
| `DELAY_ISSUE_DAYS` | `int` | 불가 | 아니오 |
| `UPDATED_AT` | `datetime` | 불가 | 아니오 |
| `UPDATED_BY` | `varchar(50)` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-04-09T09:45:58.730 |
| 읽기·참조 객체 | `smartwork.dbo.company_tax_invoice_ext` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getTaxInvoiceExt](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L294) — 바인딩: `comNo`. 결과 매핑: `DELAY_ISSUE_DAYS` → `delayIssueDays`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db269"></a>
## smartwork.dbo.COMPANY_UNIT_TAXATION_CONFIG

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `COM_NO` | `int` | 불가 | 아니오 |
| `TAX_INVOICE_START_DATE` | `varchar(10)` | 허용 | 아니오 |
| `UNIT_TAXATION_START_DATE` | `varchar(10)` | 허용 | 아니오 |
| `UDATE` | `datetime` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-03-30T10:35:30.280 |
| 읽기·참조 객체 | `smartwork.dbo.company_unit_taxation_config` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getUnitTaxationConfig](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L1120) — 바인딩: `comNo`. 결과 매핑: `COM_NO` → `comNo`, `TAX_INVOICE_START_DATE` → `taxInvoiceStartDate`, `UNIT_TAXATION_START_DATE` → `unitTaxationStartDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db270"></a>
## smartwork.dbo.deposit_deduction

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `idx` | `bigint` | 불가 | 예 |
| `channel` | `varchar(20)` | 불가 | 아니오 |
| `deposit_idx` | `int` | 불가 | 아니오 |
| `deduct_amount` | `money` | 불가 | 아니오 |
| `reason` | `varchar(500)` | 불가 | 아니오 |
| `status` | `varchar(1)` | 불가 | 아니오 |
| `create_date` | `datetime` | 불가 | 아니오 |
| `sw_no` | `int` | 불가 | 아니오 |
| `cancel_date` | `datetime` | 허용 | 아니오 |
| `cancel_sw_no` | `int` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-08-18T15:50:50.513 |
| 읽기·참조 객체 | `smartwork.dbo.deposit_deduction` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findActive](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/depositdeduction/repository/DepositDeductionMapper.kt#L40) — 바인딩: `channel`, `depositIdx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db271"></a>
## smartwork.dbo.error_receipt_attachment_meta

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `stored_path` | `nvarchar(255)` | 불가 | 아니오 |
| `original_file_name` | `nvarchar(255)` | 불가 | 아니오 |
| `file_size` | `bigint` | 불가 | 아니오 |
| `created_at` | `datetime` | 불가 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-05-04T11:13:37.033 |
| 읽기·참조 객체 | `smartwork.dbo.error_receipt_attachment_meta` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectOriginalNames](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptAttachmentMetaMapper.kt#L59) — 바인딩: `p`. 결과 매핑: `stored_path` → `storedPath`, `original_file_name` → `originalFileName`.
- [upsert](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptAttachmentMetaMapper.kt#L37) — 바인딩: `storedPath`, `originalFileName`, `fileSize`, `storedPath`, `originalFileName`, `fileSize`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db272"></a>
## smartwork.dbo.headoffice_deposit_register

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `idx` | `int` | 불가 | 예 |
| `idx_upload` | `int` | 불가 | 아니오 |
| `gubun` | `varchar(10)` | 허용 | 아니오 |
| `deposit_name` | `varchar(30)` | 불가 | 아니오 |
| `deposit_amount` | `money` | 불가 | 아니오 |
| `deposit_date` | `datetime` | 불가 | 아니오 |
| `matching_type` | `varchar(1)` | 불가 | 아니오 |
| `company_confirm` | `varchar(1)` | 불가 | 아니오 |
| `create_date` | `datetime` | 불가 | 아니오 |
| `update_date` | `datetime` | 허용 | 아니오 |
| `sw_no` | `int` | 불가 | 아니오 |
| `deposit_idx` | `int` | 허용 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-08-18T13:46:26.923 |
| 읽기·참조 객체 | `smartwork.dbo.headoffice_deposit_register` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findRegisterDepositName](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositMapper.kt#L156) — 바인딩: `itemId`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db273"></a>
## smartwork.dbo.OS_IV_PAYMENT

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `IDX` | `bigint` | 불가 | 예 |
| `CR_CD` | `varchar(20)` | 불가 | 아니오 |
| `SERVICE_CD` | `varchar(20)` | 불가 | 아니오 |
| `SEQ` | `smallint` | 불가 | 아니오 |
| `CHANNEL` | `varchar(10)` | 불가 | 아니오 |
| `DEPOSIT_IDX` | `int` | 불가 | 아니오 |
| `COM_NO` | `int` | 허용 | 아니오 |
| `DEPOSIT_NAME` | `varchar(30)` | 허용 | 아니오 |
| `IC_AMT` | `money` | 불가 | 아니오 |
| `IC_DT` | `varchar(8)` | 불가 | 아니오 |
| `SW_NO` | `int` | 불가 | 아니오 |
| `CRM_RESULT` | `varchar(10)` | 허용 | 아니오 |
| `CRM_LOG_IDX` | `bigint` | 허용 | 아니오 |
| `CREATE_DATE` | `datetime` | 불가 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-06-29T11:29:34.637 |
| 읽기·참조 객체 | `smartwork.dbo.os_iv_payment` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [updateCrmResult](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L59) — 바인딩: `crmResult`, `crmLogIdx, jdbcType=BIGINT`, `idx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db274"></a>
## smartwork.dbo.pds_attachment_meta

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `stored_path` | `nvarchar(255)` | 불가 | 아니오 |
| `original_file_name` | `nvarchar(255)` | 불가 | 아니오 |
| `file_size` | `bigint` | 불가 | 아니오 |
| `created_at` | `datetime` | 불가 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-05-08T13:28:37.453 |
| 읽기·참조 객체 | `smartwork.dbo.pds_attachment_meta` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findOne](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/pds/repository/PdsAttachmentMetaMapper.kt#L58) — 바인딩: `storedPath`. 결과 매핑: `stored_path` → `storedPath`, `original_file_name` → `originalFileName`, `file_size` → `fileSize`.
- [upsert](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/pds/repository/PdsAttachmentMetaMapper.kt#L38) — 바인딩: `storedPath`, `originalFileName`, `fileSize`, `storedPath`, `originalFileName`, `fileSize`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db275"></a>
## smartwork.dbo.spf_board_attachment_meta

선언 파라미터 없음. 테이블·뷰는 아래 컬럼과 Mapper 바인딩을 확인한다.

**테이블·뷰 컬럼 메타데이터**

| 컬럼 | SQL 타입 | NULL | IDENTITY |
|---|---|---|---|
| `stored_file_path` | `nvarchar(500)` | 불가 | 아니오 |
| `noti_type` | `char(1)` | 불가 | 아니오 |
| `original_file_name` | `nvarchar(255)` | 불가 | 아니오 |
| `file_size` | `bigint` | 불가 | 아니오 |
| `created_at` | `datetime2` | 불가 | 아니오 |
| `updated_at` | `datetime2` | 불가 | 아니오 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | USER_TABLE / 2026-05-11T15:00:57.497 |
| 읽기·참조 객체 | `smartwork.dbo.spf_board_attachment_meta` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findOne](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/spfBoard/repository/SpfBoardAttachmentMetaMapper.kt#L59) — 바인딩: `storedFilePath`. 결과 매핑: `stored_file_path` → `storedFilePath`, `noti_type` → `notiType`, `original_file_name` → `originalFileName`, `file_size` → `fileSize`.
- [delete](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/spfBoard/repository/SpfBoardAttachmentMetaMapper.kt#L62) — 바인딩: `storedFilePath`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.
- [upsert](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/spfBoard/repository/SpfBoardAttachmentMetaMapper.kt#L37) — 바인딩: `storedFilePath`, `notiType`, `originalFileName`, `fileSize`, `storedFilePath`, `notiType`, `originalFileName`, `fileSize`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db276"></a>
## smartwork.dbo.SSP_JOIN_LIST

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@FDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TDAY` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DIV` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:42.753 |
| 읽기·참조 객체 | `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchYearly](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/smartbillstatus/repository/BusinessRegistrationStatisticsMapper.kt#L60) — 바인딩: `startDate`, `endDate`, `div`. 결과 매핑: `YEAR` → `year`, `corporation` → `corporateCount`, `individual` → `individualCount`.
- [searchMonthly](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/smartbillstatus/repository/BusinessRegistrationStatisticsMapper.kt#L49) — 바인딩: `startDate`, `endDate`, `div`. 결과 매핑: `YEAR` → `year`, `MONTH` → `month`, `corporation` → `corporateCount`, `individual` → `individualCount`.
- [searchDaily](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/smartbillstatus/repository/BusinessRegistrationStatisticsMapper.kt#L37) — 바인딩: `startDate`, `endDate`, `div`. 결과 매핑: `YEAR` → `year`, `MONTH` → `month`, `DAY` → `day`, `corporation` → `corporateCount`, `individual` → `individualCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE COM_ENTRY_DATE BETWEEN @FROM AND @TO
GROUP BY YEAR(COM_ENTRY_DATE), MONTH(COM_ENTRY_DATE), DAY(COM_ENTRY_DATE)
ORDER BY [YEAR] DESC, [MONTH] DESC, [DAY] DESC;
WHERE COM_ENTRY_DATE BETWEEN @FROM AND @TO
GROUP BY YEAR(COM_ENTRY_DATE), MONTH(COM_ENTRY_DATE)
ORDER BY [YEAR] DESC, [MONTH] DESC;
WHERE COM_ENTRY_DATE BETWEEN @FROM AND @TO
GROUP BY YEAR(COM_ENTRY_DATE)
ORDER BY [YEAR] DESC;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db277"></a>
## smartwork.dbo.upAdmSB_SchMem_Bona

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@page` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@top` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROMDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TODATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MITEM` | `varchar(80)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MTEXT` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MITEM2` | `varchar(80)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MTEXT2` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MTYPE` | `varchar(5)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MSTATUS` | `varchar(5)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-09-16T10:18:41.073 |
| 읽기·참조 객체 | `migration_etcasp.dbo.migration_mapping_company`, `sb_dti_log.dbo.dormant_member`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchMembers](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankMemberMapper.kt#L113) — 바인딩: `page`, `top`, `fromDate`, `toDate`, `mItem`, `mText`, `mItem2`, `mText2`, `mType`, `mStatus`. 결과 매핑: `MEM_NO` → `memNo`, `COM_NO` → `comNo`, `MEM_NAME` → `memName`, `MEM_ID` → `memId`, `MEM_TYPE` → `memType`, `MEM_TEL` → `memTel`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `CDATE` → `cDate`, `MEM_DEL_YN` → `memDelYn`, `MEM_EMAIL` → `memEmail`, `MEM_REALNAME` → `memRealname`, `COM_ADDRESS` → `comAddress`, `MEM_HP` → `memHp`, `TOT_COUNT` → `totCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @MTEXT2 = LTRIM(RTRIM(@MTEXT2));
JOIN SmartBill3.dbo.MEMBER M WITH(NOLOCK) ON Bo.COM_NO = M.COM_NO
JOIN SmartBill3.dbo.COMPANY C WITH(NOLOCK) ON M.COM_NO = C.COM_NO
WHERE Bo.M_FLAG = 'ETAXBILL'
JOIN sb_dti_log.dbo.dormant_member M WITH(NOLOCK) ON Bo.COM_NO = M.COM_NO
JOIN SmartBill3.dbo.COMPANY C WITH(NOLOCK) ON M.COM_NO = C.COM_NO
WHERE Bo.M_FLAG = 'ETAXBILL' AND (M.restore_yn != 'Y' OR M.restore_yn IS NULL)
WHERE (@FROMDATE = '' OR @TODATE = '' OR (
ORDER BY CDATE DESC, MEM_NO DESC, MEM_DEL_YN, COM_NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db278"></a>
## smartwork.dbo.upSBAdm_LstDTI_Bona

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DATE_TYPE` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FMDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TODATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SUP_INDEX` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SUP_TEXT` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BYR_INDEX` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BYR_TEXT` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REF_ID` | `varchar(35)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@STATUS` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BYR_NAME` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-09-16T10:18:41.693 |
| 읽기·참조 객체 | `migration_etcasp.dbo.migration_mapping_company`, `sb_common.dbo.free_service`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti.dbo.dti_header_detail`, `sb_dti.dbo.dti_header_detail_2023_07`, `sb_dti.dbo.dti_header_detail_part`, `sb_dti.dbo.dti_header_detail_prev_buffer`, `sb_dti.dbo.dti_sign_cub`, `sb_dti.dbo.dti_sign_cub_2023_07`, `sb_dti.dbo.dti_sign_cub_part`, `sb_dti.dbo.dti_sign_cub_prev_buffer` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchTaxInvoices](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/taxinvoice/repository/BonabankTaxInvoiceMapper.kt#L68) — 바인딩: `page`, `top`, `dateType`, `fromDate`, `toDate`, `supIndex`, `supText`, `byrIndex`, `byrText`, `refId`, `status`, `byrName`. 결과 매핑: `DTI_IDX` → `dtiIdx`, `DTI_WDAY` → `dtiWday`, `DTI_ISSUEDATE` → `dtiIssueDate`, `NTS_SEND_DATE` → `ntsSendDate`, `SUP_COM_REGNO` → `supComRegno`, `SUP_COM_NAME` → `supComName`, `BYR_COM_REGNO` → `byrComRegno`, `BYR_COM_NAME` → `byrComName`, `BYR_TYPE` → `byrType`, `SUP_AMT` → `supAmt`, `DTI_TYPE` → `dtiType`, `DTI_STATUS` → `dtiStatus`, `NTS_SEND_STATUS` → `ntsSendStatus`, `TOT_COUNT` → `totCount`, `SUP_MEM_NAME` → `supMemName`, `BYR_MEM_NAME` → `byrMemName`, `AMEND_CODE` → `amendCode`, `DTT_LINK_TYPE` → `dttLinkType`, `DIRECTION` → `direction`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @BYR_TEXT# = [master].[dbo].[enc_index_char_sel_tc]('SSN', @BYR_TEXT, 'DTI_HEADER_GIRO', 'BYR_COM_REGNO');
SET @SQL = N'
SB_DTI..DTI_HEADER_CUB DM WITH(NOLOCK) JOIN SB_DTI..DTI_HEADER_DETAIL DD WITH(NOLOCK) ON DM.DTI_WDAY = DD.DTI_WDAY AND DM.DTI_IDX = DD.DTI_IDX
LEFT OUTER JOIN SB_DTI..DTI_SIGN_CUB DS WITH(NOLOCK) ON DD.DTI_WDAY = DS.DTI_WDAY AND DD.DTI_IDX = DS.DTI_IDX
LEFT OUTER JOIN SB_COMMON..FREE_SERVICE FS ON DS.FREE_NO = FS.IDX
INNER JOIN (SELECT COM_REGNO FROM MIGRATION_ETCASP..MIGRATION_MAPPING_COMPANY WITH(NOLOCK) WHERE M_FLAG=''ETAXBILL'' AND USE_YN=''Y'')MC ON DM.SUP_COM_REGNO = MC.COM_REGNO
WHERE DS.BILL_TYPE = ''90'' '
SET @SQL = @SQL + N'
ORDER BY DM.DTI_IDX DESC, DM.DTI_WDAY DESC
```

하위 프로시저·함수·뷰: `master.dbo.clr_enc_index_tc`, `master.dbo.enc_index_char_sel_tc`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_detail`, `sb_dti.dbo.dti_sign_cub`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db279"></a>
## smartwork.dbo.upSBAdm_LstDTI_Bona_excel

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DATE_TYPE` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FMDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TODATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SUP_INDEX` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SUP_TEXT` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BYR_INDEX` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BYR_TEXT` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REF_ID` | `varchar(35)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@STATUS` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BYR_NAME` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-09-16T10:18:41.993 |
| 읽기·참조 객체 | `migration_etcasp.dbo.migration_mapping_company`, `sb_common.dbo.free_service`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_cub_2023_07`, `sb_dti.dbo.dti_header_cub_part`, `sb_dti.dbo.dti_header_cub_prev_buffer`, `sb_dti.dbo.dti_header_detail`, `sb_dti.dbo.dti_header_detail_2023_07`, `sb_dti.dbo.dti_header_detail_part`, `sb_dti.dbo.dti_header_detail_prev_buffer`, `sb_dti.dbo.dti_sign_cub`, `sb_dti.dbo.dti_sign_cub_2023_07`, `sb_dti.dbo.dti_sign_cub_part`, `sb_dti.dbo.dti_sign_cub_prev_buffer` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [fetchForExport](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/taxinvoice/repository/BonabankTaxInvoiceMapper.kt#L208) — 바인딩: `dateType`, `fromDate`, `toDate`, `supIndex`, `supText`, `byrIndex`, `byrText`, `refId`, `status`, `byrName`. 결과 매핑: `DTI_IDX` → `dtiIdx`, `DTI_WDAY` → `dtiWday`, `DTI_ISSUEDATE` → `dtiIssueDate`, `NTS_SEND_DATE` → `ntsSendDate`, `SUP_COM_REGNO` → `supComRegno`, `SUP_COM_NAME` → `supComName`, `BYR_COM_REGNO` → `byrComRegno`, `BYR_COM_NAME` → `byrComName`, `BYR_TYPE` → `byrType`, `SUP_AMT` → `supAmt`, `DTI_TYPE` → `dtiType`, `DTI_STATUS` → `dtiStatus`, `NTS_SEND_STATUS` → `ntsSendStatus`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @BYR_TEXT# = [master].[dbo].[enc_index_char_sel_tc]('SSN',@BYR_TEXT,'DTI_HEADER_GIRO','BYR_COM_REGNO')
SET @BYR_TEXT# = NULL
SET @SQL = '
SB_DTI..DTI_HEADER_CUB DM WITH(NOLOCK) JOIN SB_DTI..DTI_HEADER_DETAIL DD WITH(NOLOCK) ON DM.DTI_WDAY = DD.DTI_WDAY AND DM.DTI_IDX = DD.DTI_IDX
LEFT OUTER JOIN SB_DTI..DTI_SIGN_CUB DS WITH(NOLOCK) ON DD.DTI_WDAY = DS.DTI_WDAY AND DD.DTI_IDX = DS.DTI_IDX
LEFT OUTER JOIN SB_COMMON..FREE_SERVICE FS ON DS.FREE_NO = FS.IDX
INNER JOIN (SELECT COM_REGNO FROM MIGRATION_ETCASP..MIGRATION_MAPPING_COMPANY WITH(NOLOCK) WHERE M_FLAG=''ETAXBILL'' AND USE_YN=''Y'')MC ON DM.SUP_COM_REGNO = MC.COM_REGNO
WHERE DS.BILL_TYPE = ''90''
SET @SQL = @SQL + N'
ORDER BY DM.DTI_IDX DESC, DM.DTI_WDAY DESC'
```

하위 프로시저·함수·뷰: `master.dbo.clr_enc_index_tc`, `master.dbo.enc_index_char_sel_tc`, `sb_dti.dbo.dti_header_cub`, `sb_dti.dbo.dti_header_detail`, `sb_dti.dbo.dti_sign_cub`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db280"></a>
## smartwork.dbo.upSelect_DTIChangeReceiverHis_DW

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DTI_WDAY` | `char(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:51.710 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_header_cub_2020_01`, `sb_dti.dbo.dti_header_cub_2020_02`, `sb_dti.dbo.dti_header_cub_2020_03`, `sb_dti.dbo.dti_header_cub_2020_04`, `sb_dti.dbo.dti_header_cub_2020_05`, `sb_dti.dbo.dti_header_cub_2020_06`, `sb_dti.dbo.dti_header_cub_2020_07`, `sb_dti.dbo.dti_header_cub_2020_08`, `sb_dti.dbo.dti_header_cub_2020_09`, `sb_dti.dbo.dti_header_cub_2020_10`, `sb_dti.dbo.dti_header_cub_2020_11`, `sb_dti.dbo.dti_header_cub_2020_12`, `sb_dti.dbo.dti_header_cub_2021_01`, `sb_dti.dbo.dti_header_cub_2021_02`, `sb_dti.dbo.dti_header_cub_2021_03`, `sb_dti.dbo.dti_header_cub_2021_04`, `sb_dti.dbo.dti_header_cub_2021_05`, `sb_dti.dbo.dti_header_cub_2021_06`, `sb_dti.dbo.dti_header_cub_2021_07`, `sb_dti.dbo.dti_header_cub_2021_08`, `sb_dti.dbo.dti_header_cub_2021_09`, `sb_dti.dbo.dti_header_cub_2021_10`, `sb_dti.dbo.dti_header_cub_2021_11`, `sb_dti.dbo.dti_header_cub_2021_12`, `sb_dti.dbo.dti_header_cub_2022_01`, `sb_dti.dbo.dti_header_cub_2022_02`, `sb_dti.dbo.dti_header_cub_2022_03`, `sb_dti.dbo.dti_header_cub_2022_04`, `sb_dti.dbo.dti_header_cub_2022_05`, `sb_dti.dbo.dti_header_cub_2022_06`, `sb_dti.dbo.dti_header_cub_2022_07`, `sb_dti.dbo.dti_header_cub_2022_08`, `sb_dti.dbo.dti_header_cub_2022_09`, `sb_dti.dbo.dti_header_cub_2022_10`, `sb_dti.dbo.dti_header_cub_2022_11`, `sb_dti.dbo.dti_header_cub_2022_12`, `sb_dti.dbo.dti_header_cub_2023_01`, `sb_dti.dbo.dti_header_cub_2023_02`, `sb_dti.dbo.dti_header_cub_2023_03`, `sb_dti.dbo.dti_header_cub_2023_04`, `sb_dti.dbo.dti_header_cub_2023_05`, `sb_dti.dbo.dti_header_cub_2023_06`, `sb_dti_dw.dbo.dti_header_cub`, `sb_dti_log.dbo.dti_change_receiver`, `sb_dti_log.dbo.dti_change_receiver_his`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getReceiverChangeHistory](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L306) — 바인딩: `dtiWday`, `dtiIdx`. 결과 매핑: `CDATE` → `cdate`, `ORI_RCV_EMAIL` → `oriRcvEmail`, `RCV_EMAIL` → `rcvEmail`, `CHG_TYPE` → `chgType`, `CHG` → `chg`, `BYR_TYPE` → `byrType`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE DTI_WDAY = @DTI_WDAY AND DTI_IDX = @DTI_IDX
IF EXISTS (SELECT 1 FROM SB_DTI_LOG..DTI_CHANGE_RECEIVER WITH(NOLOCK) WHERE ETC_PCS_NO = @ETC_PCS_NO)
CASE WHEN H.CHG_TYPE = 'ISSUE' THEN (SELECT RCV_EMAIL FROM SB_DTI_LOG..DTI_CHANGE_RECEIVER_HIS WITH(NOLOCK) WHERE DTI_WDAY = L.DTI_WDAY AND DTI_IDX = L.DTI_IDX AND CHG_TYPE IN ('RDTIREQUEST','RDETAILREQUEST'))
JOIN SB_DTI_LOG..DTI_CHANGE_RECEIVER_HIS H WITH(NOLOCK) ON L.ETC_PCS_NO = H.ETC_PCS_NO
JOIN SB_DTI_DW..DTI_HEADER_CUB HD WITH(NOLOCK) ON L.ETC_PCS_NO = HD.ETC_PCS_NO
LEFT JOIN SMARTBILL3..MEMBER M WITH(NOLOCK) ON H.RCV_MEM_NO = M.MEM_NO
WHERE HD.BYR_TYPE = 'M'
ORDER BY L.DTI_WDAY, L.DTI_IDX, H.CDATE
CASE WHEN H.CHG_TYPE = 'ISSUE' THEN (SELECT RCV_EMAIL FROM SB_DTI_LOG..DTI_CHANGE_RECEIVER_HIS WITH(NOLOCK) WHERE DTI_WDAY = L.DTI_WDAY AND DTI_IDX = L.DTI_IDX AND CHG_TYPE IN ('RDTIREQUEST','RDETAILREQUEST'))
JOIN SB_DTI_LOG..DTI_CHANGE_RECEIVER_HIS H WITH(NOLOCK) ON L.DTI_WDAY = H.DTI_WDAY AND L.DTI_IDX = H.DTI_IDX
JOIN SB_DTI_DW..DTI_HEADER_CUB HD WITH(NOLOCK) ON L.DTI_WDAY = HD.DTI_WDAY AND L.DTI_IDX = HD.DTI_IDX
LEFT JOIN SMARTBILL3..MEMBER M WITH(NOLOCK) ON H.RCV_MEM_NO = M.MEM_NO
WHERE HD.BYR_TYPE = 'M'
ORDER BY L.DTI_WDAY, L.DTI_IDX, H.CDATE
```

하위 프로시저·함수·뷰: `sb_dti_dw.dbo.dti_header_cub`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db281"></a>
## smartwork.dbo.usp_admin_coupon_detail

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COUPON_NO` | `varchar(25)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:52.510 |
| 읽기·참조 객체 | `sb_common.dbo.coupon_kind_info`, `sb_common.dbo.coupon_manage_his`, `sb_common.dbo.coupon_manage_info`, `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [fetchCoupon](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/coupon/repository/AdminCouponMapper.kt#L82) — 바인딩: `couponNo`. 결과 매핑: `COUPON_NO` → `couponNo`, `TITLE` → `title`, `CDATE` → `cdate`, `FROMDATE` → `fromdate`, `TODATE` → `todate`, `USE_STATE` → `useState`, `CONTENTS` → `contents`, `com_regno` → `comRegno`, `com_name` → `comName`, `REASON` → `reason`, `STATE_DESC` → `stateDesc`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
JOIN    SB_COMMON..COUPON_MANAGE_INFO AS MI WITH (NOLOCK) ON KI.COUPONKIND_NO = MI.COUPONKIND_NO
JOIN    SmartBill3..COMPANY AS C WITH (NOLOCK) ON MI.COM_NO = C.COM_NO
JOIN    SB_COMMON..COUPON_MANAGE_HIS  AS MH WITH (NOLOCK) ON MH.COUPON_NO = MI.COUPON_NO
WHERE   MI.USE_STATE <> 'NPOSSIBLE'
GROUP BY KI.TITLE, MI.CDATE, KI.FROMDATE, KI.TODATE, MI.USE_STATE, KI.CONTENTS,
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db282"></a>
## smartwork.dbo.usp_admin_coupon_list

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SUP_INDEX` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SUP_TEXT` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:52.607 |
| 읽기·참조 객체 | `sb_common.dbo.coupon_kind_info`, `sb_common.dbo.coupon_manage_info`, `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchCoupons](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/coupon/repository/AdminCouponMapper.kt#L54) — 바인딩: `page`, `top`, `supIndex`, `supText`. 결과 매핑: `RN` → `rn`, `COM_REGNO` → `comRegno`, `COUPON_NO` → `couponNo`, `TITLE` → `title`, `CONTENTS` → `contents`, `ISSUE_GRADE` → `issueGrade`, `USE_STATE` → `useState`, `CDATE` → `cdate`, `TOTALCOUNT` → `totalCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
ROW_NUMBER() OVER (ORDER BY MI.CDATE DESC) AS RN,
JOIN    SB_COMMON..COUPON_MANAGE_INFO AS MI WITH (NOLOCK) ON KI.COUPONKIND_NO = MI.COUPONKIND_NO
JOIN    SmartBill3..COMPANY AS C WITH (NOLOCK) ON MI.COM_NO = C.COM_NO
WHERE   MI.USE_STATE <> 'NPOSSIBLE'
JOIN    SB_COMMON..COUPON_MANAGE_INFO AS MI WITH (NOLOCK) ON KI.COUPONKIND_NO = MI.COUPONKIND_NO
JOIN    SmartBill3..COMPANY AS C WITH (NOLOCK) ON MI.COM_NO = C.COM_NO
JOIN    ALLPAGES AS V ON V.IDX = MI.IDX
WHERE   V.RN BETWEEN @START_ROWNO AND @END_ROWNO
ORDER BY V.RN ASC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db283"></a>
## smartwork.dbo.usp_admin_faq_list

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@page` | `int` | IN | 1 |
| `@size` | `int` | IN | 10 |
| `@schItem` | `varchar(100)` | IN | '' |
| `@schText` | `varchar(200)` | IN | '' |
| `@otherFlag` | `bit` | IN | 0 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:52.663 |
| 읽기·참조 객체 | `smartbill3.dbo.faq` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchFaqs](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/support/board/faq/repository/AdminFaqMapper.kt#L59) — 바인딩: `page`, `size`, `schItem`, `schText`, `otherFlag`. 결과 매핑: `faq_no` → `faqNo`, `faq_type` → `faqType`, `faq_title` → `faqTitle`, `faq_hit` → `faqHit`, `faq_write_date` → `faqWriteDate`, `is_new` → `isNew`, `total_count` → `totalCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE 1 = 1
ORDER BY faq_write_date DESC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db284"></a>
## smartwork.dbo.usp_company_info_list_select

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@STRITEM` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@STRCONTENTS` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROMDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TODATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CSTATUS` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CSTATUS2` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DTI_BILLTYPE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DCT_BILLTYPE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISSUANCE_SCHEDULE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-09-16T10:18:43.230 |
| 읽기·참조 객체 | `sb_dti.dbo.company_dticonfig`, `smartbill3.dbo.cms_account_cub`, `smartbill3.dbo.company`, `smartbill3.dbo.settlement` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchCompanyList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoMapper.kt#L51) — 바인딩: `strItem`, `strContents`, `fromDate`, `toDate`, `cStatus`, `cStatus2`, `dtiBillType`, `dctBillType`, `issuanceSchedule`. 결과 매핑: `COM_NO` → `comNo`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `COM_PRESIDENT` → `comPresident`, `COM_ENTRY_DATE` → `comEntryDate`, `COM_STATUS` → `comStatus`, `DTI_TYPE` → `dtiType`, `DCT_TYPE` → `dctType`, `COM_DEL_YN` → `comDelYn`, `COM_ADDRESS` → `comAddress`, `MEM_HP` → `memHp`, `MEM_TEL` → `memTel`, `BANK_ACCSTATE` → `bankAccState`, `DCT_PREMIUM` → `dctPremium`, `CERT_DN` → `certDn`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE CA.COM_NO = C.COM_NO
ORDER BY CA.IDX DESC
INNER JOIN SMARTBILL3..SETTLEMENT S1 WITH (NOLOCK)
INNER JOIN SMARTBILL3..SETTLEMENT S2 WITH (NOLOCK)
LEFT JOIN SB_DTI..COMPANY_DTICONFIG DCFG WITH (NOLOCK)
WHERE 1 = 1
ORDER BY C.COM_ENTRY_DATE DESC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db285"></a>
## smartwork.dbo.usp_error_deal_time_sum

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@err_idx` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:54.750 |
| 읽기·참조 객체 | `office.dbo.error_deal` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectDealTimeSum](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptMapper.kt#L144) — 바인딩: `errIdx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE err_idx = @err_idx;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db286"></a>
## smartwork.dbo.usp_error_receipt_detail

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@err_idx` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-27T16:36:04.190 |
| 읽기·참조 객체 | `office.dbo.dept`, `office.dbo.error_managemennt`, `office.dbo.function_code`, `office.dbo.sawon` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectViewRow](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptMapper.kt#L134) — 바인딩: `errIdx`. 결과 매핑: `err_idx` → `errIdx`, `err_num` → `errNum`, `writer_name` → `writerName`, `err_com_regno` → `errComRegno`, `err_com_name` → `errComName`, `err_com_admin` → `errComAdmin`, `err_com_phone` → `errComPhone`, `err_title` → `errTitle`, `err_content` → `errContent`, `err_file` → `errFile`, `err_date` → `errDate`, `err_type` → `errType`, `err_bns_name` → `errBnsName`, `routing_type` → `routingType`, `err_code` → `errCode`, `err_status` → `errStatus`, `err_bns_id` → `errBnsId`, `req_team` → `reqTeam`, `write_sw_no` → `writeSwNo`, `sms_chk` → `smsChk`, `svc_title` → `svcTitle`, `processor_name` → `processorName`, `dept_name` → `deptName`, `call_no` → `callNo`, `svc_type` → `svcType`, `error_dtl_code` → `errorDtlCode`, `error_etc` → `errorEtc`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT JOIN   Office.dbo.sawon reg WITH(NOLOCK) ON reg.sw_no = e.write_sw_no
LEFT JOIN   Office.dbo.sawon prc WITH(NOLOCK) ON prc.sw_no = e.sw_no
LEFT JOIN   Office.dbo.function_code f WITH(NOLOCK)
LEFT JOIN   Office.dbo.dept d WITH(NOLOCK) ON d.dept_no = e.req_team
WHERE e.err_idx = @err_idx;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db287"></a>
## smartwork.dbo.usp_error_receipt_download

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@from_date` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@to_date` | `varchar(23)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@status` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@company_name` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@bns_name` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@routing_csv` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@svc_concat` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@type_concat` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_code` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@business_number` | `varchar(13)` | IN | '' |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-09-02T17:03:15.207 |
| 읽기·참조 객체 | `office.dbo.error_deal`, `office.dbo.error_managemennt`, `office.dbo.function_code`, `office.dbo.sawon` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectDownloadRows](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptMapper.kt#L92) — 바인딩: `fromDate`, `toDate`, `status`, `companyName`, `bnsName`, `routingCsv`, `svcConcat`, `typeConcat`, `errCode`, `businessNumber`. 결과 매핑: `err_num` → `errNum`, `reg_name` → `regName`, `err_title` → `errTitle`, `err_content` → `errContent`, `err_com_name` → `errComName`, `err_bns_name` → `errBnsName`, `routing_type` → `routingType`, `err_code` → `errCode`, `svc_title` → `svcTitle`, `svc_type` → `svcType`, `err_type` → `errType`, `error_dtl_code` → `errorDtlCode`, `err_status` → `errStatus`, `err_date` → `errDate`, `err_end_date` → `errEndDate`, `proc_name` → `procName`, `proc_time_sum` → `procTimeSum`, `deal_contents` → `dealContents`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @business_number = REPLACE(LTRIM(RTRIM(ISNULL(@business_number, ''))), '-', '');
FROM Office.dbo.error_deal dd WITH(NOLOCK) WHERE dd.err_idx = e.err_idx) AS proc_time_sum,
WITHIN GROUP (ORDER BY dd.err_dtl_idx)
WHERE dd.err_idx = e.err_idx
LEFT JOIN   Office.dbo.sawon reg WITH(NOLOCK) ON reg.sw_no = e.write_sw_no
LEFT JOIN   Office.dbo.sawon prc WITH(NOLOCK) ON prc.sw_no = e.sw_no
LEFT JOIN   Office.dbo.function_code f WITH(NOLOCK)
WHERE   (@from_date = '' OR @to_date = '' OR e.err_date BETWEEN @from_date AND @to_date)
ORDER BY e.err_date DESC;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db288"></a>
## smartwork.dbo.usp_error_receipt_list_all

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@from_date` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@to_date` | `varchar(23)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@status` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@company_name` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@bns_name` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@routing_csv` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@svc_concat` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@type_concat` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@err_code` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@business_number` | `varchar(13)` | IN | '' |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-09-16T10:18:43.377 |
| 읽기·참조 객체 | `office.dbo.error_deal`, `office.dbo.error_managemennt`, `office.dbo.sawon` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/error/repository/ErrorReceiptMapper.kt#L56) — 바인딩: `fromDate`, `toDate`, `status`, `companyName`, `bnsName`, `routingCsv`, `svcConcat`, `typeConcat`, `errCode`, `businessNumber`. 결과 매핑: `err_idx` → `errIdx`, `err_num` → `errNum`, `err_bns_id` → `errBnsId`, `err_bns_name` → `errBnsName`, `err_title` → `errTitle`, `err_status` → `errStatus`, `err_file` → `errFile`, `err_date` → `errDate`, `err_com_name` → `errComName`, `err_end_date` → `errEndDate`, `processor_name` → `processorName`, `proc_time_sum` → `procTimeSum`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @business_number = REPLACE(LTRIM(RTRIM(ISNULL(@business_number, ''))), '-', '');
FROM Office.dbo.error_deal dd WITH(NOLOCK) WHERE dd.err_idx = t.err_idx) AS proc_time_sum
LEFT JOIN   Office.dbo.sawon z WITH(NOLOCK) ON z.sw_no = t.sw_no
WHERE   (@from_date = '' OR @to_date = '' OR t.err_date BETWEEN @from_date AND @to_date)
ORDER BY t.err_date DESC;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db289"></a>
## smartwork.dbo.usp_member_history_list_select

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PAGESIZE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MEM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:56.763 |
| 읽기·참조 객체 | `office.dbo.sawon`, `smartbill3.dbo.member`, `smartbill3.dbo.member_history` |
| 쓰기 대상 | 쓰기문 존재; 별칭·임시 객체 또는 동적 대상의 영향은 추가 확인 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectMemberHistory](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/member/repository/MemberInfoMapper.kt#L244) — 바인딩: `page`, `pageSize`, `memNo`. 결과 매핑: `TOT_COUNT` → `totCount`, `MEM_HISTORY_DATE` → `memHistoryDate`, `FIELD_NAME` → `fieldName`, `PREV_VALUE` → `prevValue`, `CURR_VALUE` → `currValue`, `UPDATE_NO` → `updateNo`, `UPDATE_SW_NO` → `updateSwNo`, `UPDATE_NAME` → `updateName`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
ROW_NUMBER() OVER (PARTITION BY MEM_NO ORDER BY MEM_HISTORY_DATE ASC) AS rn,
MEM_REALNAME,       LAG(MEM_REALNAME)       OVER (PARTITION BY MEM_NO ORDER BY MEM_HISTORY_DATE ASC) AS prev_MEM_REALNAME,
MEM_REGNO,          LAG(MEM_REGNO)          OVER (PARTITION BY MEM_NO ORDER BY MEM_HISTORY_DATE ASC) AS prev_MEM_REGNO,
MEM_NAME,           LAG(MEM_NAME)           OVER (PARTITION BY MEM_NO ORDER BY MEM_HISTORY_DATE ASC) AS prev_MEM_NAME,
MEM_ID,             LAG(MEM_ID)             OVER (PARTITION BY MEM_NO ORDER BY MEM_HISTORY_DATE ASC) AS prev_MEM_ID,
MEM_TYPE,           LAG(MEM_TYPE)           OVER (PARTITION BY MEM_NO ORDER BY MEM_HISTORY_DATE ASC) AS prev_MEM_TYPE,
MEM_TEL,            LAG(MEM_TEL)            OVER (PARTITION BY MEM_NO ORDER BY MEM_HISTORY_DATE ASC) AS prev_MEM_TEL,
MEM_HP,             LAG(MEM_HP)             OVER (PARTITION BY MEM_NO ORDER BY MEM_HISTORY_DATE ASC) AS prev_MEM_HP,
MEM_EMAIL,          LAG(MEM_EMAIL)          OVER (PARTITION BY MEM_NO ORDER BY MEM_HISTORY_DATE ASC) AS prev_MEM_EMAIL,
MEM_STATUS,         LAG(MEM_STATUS)         OVER (PARTITION BY MEM_NO ORDER BY MEM_HISTORY_DATE ASC) AS prev_MEM_STATUS,
RESULTMAIL_SEND_YN, LAG(RESULTMAIL_SEND_YN) OVER (PARTITION BY MEM_NO ORDER BY MEM_HISTORY_DATE ASC) AS prev_RESULTMAIL_SEND_YN,
INFOMAIL_RECEIVE_YN,LAG(INFOMAIL_RECEIVE_YN)OVER (PARTITION BY MEM_NO ORDER BY MEM_HISTORY_DATE ASC) AS prev_INFOMAIL_RECEIVE_YN,
INFORSMS_RECEIVE_YN,LAG(INFORSMS_RECEIVE_YN)OVER (PARTITION BY MEM_NO ORDER BY MEM_HISTORY_DATE ASC) AS prev_INFORSMS_RECEIVE_YN,
WHERE MEM_NO = @MEM_NO
WHERE o.rn > 1
LEFT JOIN office..SAWON s ON c.update_sw_no = s.SW_NO
LEFT JOIN SmartBill3..MEMBER m ON c.update_no = m.MEM_NO
ORDER BY c.MEM_HISTORY_DATE DESC, c.field_order ASC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db290"></a>
## smartwork.dbo.usp_member_info_update

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@NO` | `bigint` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REALNAME` | `varchar(35)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MEM_REGNO` | `varchar(8)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT_EMAIL` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@INFO_MAIL` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@INFO_SNS` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@INFO_TEL` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@UPDATE_SW_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@EMAIL` | `varchar(200)` | IN | '' |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:56.970 |
| 읽기·참조 객체 | `smartbill3.dbo.member`, `smartbill3.dbo.member_agreement`, `smartbill3.dbo.member_history` |
| 쓰기 대상 | `smartbill3.dbo.member`, `smartbill3.dbo.member_agreement`, `smartbill3.dbo.member_history` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [updateMemberProfile](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bonabank/repository/BonabankMemberMapper.kt#L258) — 바인딩: `no`, `realname`, `memRegno`, `resultEmail`, `infoMail`, `infoSns`, `infoTel`, `updateSwNo`, `email`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
BEGIN TRAN;
WHERE MEM_NO = @NO;
WHERE MEM_NO = @NO
WHERE MEM_NO = @NO;
WHERE MEM_NO = @NO;
SET @INFOMARKETING_RECEIVE_YN = 'Y';
IF EXISTS (SELECT MEM_NO FROM SmartBill3..MEMBER_Agreement WITH(NOLOCK) WHERE MEM_NO = @NO)
FROM SmartBill3..MEMBER_Agreement WITH(NOLOCK) WHERE MEM_NO = @NO;
UPDATE SmartBill3..MEMBER_Agreement SET Email_Modify_Date = GETDATE() WHERE MEM_NO = @NO;
UPDATE SmartBill3..MEMBER_Agreement SET Tel_Modify_Date = GETDATE() WHERE MEM_NO = @NO;
UPDATE SmartBill3..MEMBER_Agreement SET SMS_Modify_Date = GETDATE() WHERE MEM_NO = @NO;
WHERE MEM_NO = @NO;
WHERE MEM_NO = @NO;
COMMIT;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db291"></a>
## smartwork.dbo.Usp_msg_n_error_code_mng_yn_update

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@n_idx` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@mng_yn` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:48.510 |
| 읽기·참조 객체 | `smartbill3.dbo.msg_n_error_code` |
| 쓰기 대상 | `smartbill3.dbo.msg_n_error_code` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [updateMngYn](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/errorcode/repository/ErrorCodeMapper.kt#L133) — 바인딩: `nIdx`, `mngYn`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE n_idx = @n_idx
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db292"></a>
## smartwork.dbo.Usp_msg_n_error_code_select

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@m_idx` | `int` | IN | NULL |
| `@keyword` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:48.633 |
| 읽기·참조 객체 | `smartbill3.dbo.msg_m_error_code`, `smartbill3.dbo.msg_n_error_code` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/operations/errorcode/repository/ErrorCodeMapper.kt#L47) — 바인딩: `mIdx, jdbcType=INTEGER`, `keyword, jdbcType=VARCHAR`. 결과 매핑: `n_idx` → `nIdx`, `m_idx` → `mIdx`, `error_code` → `errorCode`, `process_name` → `processName`, `error_desc` → `errorDesc`, `support_desc` → `supportDesc`, `detail_guide` → `detailGuide`, `mng_yn` → `mngYn`, `hit_count` → `hitCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
JOIN  SmartBill3.dbo.msg_m_error_code  m WITH (NOLOCK)
WHERE  (@m_idx   IS NULL OR @m_idx = 0  OR m.m_idx = @m_idx)
ORDER BY n.hit_count DESC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db293"></a>
## smartwork.dbo.usp_sales_purchases_usage_select

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@div` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@fmdate` | `varchar(8)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@todate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@schItem` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@schText` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@count` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-20T10:15:29.277 |
| 읽기·참조 객체 | `sb_dti.dbo.dti_header_cub_2020_01`, `sb_dti.dbo.dti_header_cub_2020_02`, `sb_dti.dbo.dti_header_cub_2020_03`, `sb_dti.dbo.dti_header_cub_2020_04`, `sb_dti.dbo.dti_header_cub_2020_05`, `sb_dti.dbo.dti_header_cub_2020_06`, `sb_dti.dbo.dti_header_cub_2020_07`, `sb_dti.dbo.dti_header_cub_2020_08`, `sb_dti.dbo.dti_header_cub_2020_09`, `sb_dti.dbo.dti_header_cub_2020_10`, `sb_dti.dbo.dti_header_cub_2020_11`, `sb_dti.dbo.dti_header_cub_2020_12`, `sb_dti.dbo.dti_header_cub_2021_01`, `sb_dti.dbo.dti_header_cub_2021_02`, `sb_dti.dbo.dti_header_cub_2021_03`, `sb_dti.dbo.dti_header_cub_2021_04`, `sb_dti.dbo.dti_header_cub_2021_05`, `sb_dti.dbo.dti_header_cub_2021_06`, `sb_dti.dbo.dti_header_cub_2021_07`, `sb_dti.dbo.dti_header_cub_2021_08`, `sb_dti.dbo.dti_header_cub_2021_09`, `sb_dti.dbo.dti_header_cub_2021_10`, `sb_dti.dbo.dti_header_cub_2021_11`, `sb_dti.dbo.dti_header_cub_2021_12`, `sb_dti.dbo.dti_header_cub_2022_01`, `sb_dti.dbo.dti_header_cub_2022_02`, `sb_dti.dbo.dti_header_cub_2022_03`, `sb_dti.dbo.dti_header_cub_2022_04`, `sb_dti.dbo.dti_header_cub_2022_05`, `sb_dti.dbo.dti_header_cub_2022_06`, `sb_dti.dbo.dti_header_cub_2022_07`, `sb_dti.dbo.dti_header_cub_2022_08`, `sb_dti.dbo.dti_header_cub_2022_09`, `sb_dti.dbo.dti_header_cub_2022_10`, `sb_dti.dbo.dti_header_cub_2022_11`, `sb_dti.dbo.dti_header_cub_2022_12`, `sb_dti.dbo.dti_header_cub_2023_01`, `sb_dti.dbo.dti_header_cub_2023_02`, `sb_dti.dbo.dti_header_cub_2023_03`, `sb_dti.dbo.dti_header_cub_2023_04`, `sb_dti.dbo.dti_header_cub_2023_05`, `sb_dti.dbo.dti_header_cub_2023_06`, `sb_dti_dw.dbo.dti_header_cub` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [selectPurchases](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/salespurchasesusage/repository/SalesPurchasesUsageMapper.kt#L77) — 바인딩: `fromYymm, mode=IN, jdbcType=VARCHAR`, `toDate,   mode=IN, jdbcType=VARCHAR`, `schItem,  mode=IN, jdbcType=VARCHAR`, `schText,  mode=IN, jdbcType=VARCHAR`, `count,    mode=IN, jdbcType=INTEGER`. 결과 매핑: `byr_com_regno` → `businessNumber`, `com_name` → `vendorName`, `YEAR` → `year`, `MONTH` → `month`, `SUP` → `counterCompanyCount`, `dti_count` → `dtiCount`.
- [selectSales](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/statistics/salespurchasesusage/repository/SalesPurchasesUsageMapper.kt#L52) — 바인딩: `fromYymm, mode=IN, jdbcType=VARCHAR`, `toDate,   mode=IN, jdbcType=VARCHAR`, `schItem,  mode=IN, jdbcType=VARCHAR`, `schText,  mode=IN, jdbcType=VARCHAR`, `count,    mode=IN, jdbcType=INTEGER`. 결과 매핑: `sup_com_regno` → `businessNumber`, `com_name` → `vendorName`, `YEAR` → `year`, `MONTH` → `month`, `BYR` → `counterCompanyCount`, `dti_count` → `dtiCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE DTI_WDAY BETWEEN @wFrom AND @wTo
GROUP BY YEAR(DTI_ISSUEDATE), MONTH(DTI_ISSUEDATE), SUP_COM_REGNO
ORDER BY [YEAR] DESC, [MONTH] DESC
WHERE DTI_WDAY BETWEEN @wFrom AND @wTo
GROUP BY YEAR(DTI_ISSUEDATE), MONTH(DTI_ISSUEDATE), BYR_COM_REGNO
SET @decVal = ISNULL(CONVERT(VARCHAR(13), MASTER.DBO.DEC_CHAR_SEL_TC(0, 'SSN', @encVal, 'DTI_HEADER', 'BYR_COM_REGNO')), '')
SET @decVal = ''
JOIN #decMap d ON a.byr_enc = d.byr_enc
ORDER BY a.[YEAR] DESC, a.[MONTH] DESC
```

하위 프로시저·함수·뷰: `master.dbo.clr_dec_char_sel_tc`, `master.dbo.clr_enc_index_tc`, `master.dbo.dec_char_sel_tc`, `master.dbo.enc_index_char_sel_tc`, `sb_dti_dw.dbo.dti_header_cub`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db294"></a>
## smartwork.dbo.usp_sw_log_access_event_insert

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@EVENT_TYPE` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@STATUS` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@USER_ID` | `bigint` | IN | NULL |
| `@MEMBER_ID` | `nvarchar(50)` | IN | NULL |
| `@USER_NAME` | `nvarchar(100)` | IN | NULL |
| `@DEPARTMENT_NAME` | `nvarchar(100)` | IN | NULL |
| `@PAGE_TITLE` | `nvarchar(200)` | IN | NULL |
| `@PATH` | `nvarchar(500)` | IN | NULL |
| `@MENU_PATH` | `nvarchar(500)` | IN | NULL |
| `@MENU_LABEL` | `nvarchar(200)` | IN | NULL |
| `@CATEGORY_NAME` | `nvarchar(200)` | IN | NULL |
| `@SUB_CATEGORY_NAME` | `nvarchar(200)` | IN | NULL |
| `@MENU_ORDER` | `int` | IN | NULL |
| `@IP_ADDRESS` | `varchar(45)` | IN | NULL |
| `@USER_AGENT` | `nvarchar(1000)` | IN | NULL |
| `@BROWSER` | `varchar(100)` | IN | NULL |
| `@OS` | `varchar(100)` | IN | NULL |
| `@REFERRER` | `nvarchar(500)` | IN | NULL |
| `@DETAIL` | `nvarchar(1000)` | IN | NULL |
| `@RESULT` | `int` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COUNTS_AS_VISIT` | `bit` | IN | 1 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-09-28T10:15:55.647 |
| 읽기·참조 객체 | `smartwork.dbo.sw_log_access_event` |
| 쓰기 대상 | `smartwork.dbo.sw_log_access_event` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [insertAccessEvent](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/settings/logmanagement/repository/LogManagementMapper.kt#L92) — 바인딩: `eventType`, `status`, `userId, jdbcType=BIGINT`, `memberId, jdbcType=NVARCHAR`, `userName, jdbcType=NVARCHAR`, `departmentName, jdbcType=NVARCHAR`, `pageTitle, jdbcType=NVARCHAR`, `path, jdbcType=NVARCHAR`, `menuPath, jdbcType=NVARCHAR`, `menuLabel, jdbcType=NVARCHAR`, `categoryName, jdbcType=NVARCHAR`, `subCategoryName, jdbcType=NVARCHAR`, `menuOrder, jdbcType=INTEGER`, `ipAddress, jdbcType=VARCHAR`, `userAgent, jdbcType=NVARCHAR`, `browser, jdbcType=VARCHAR`, `os, jdbcType=VARCHAR`, `referrer, jdbcType=NVARCHAR`, `detail, jdbcType=NVARCHAR`, `result, mode=OUT, jdbcType=INTEGER`, `countsAsVisit, jdbcType=BIT`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @RESULT = SCOPE_IDENTITY();
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db295"></a>
## smartwork.dbo.usp_unpaid_exception_list_select

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PAGESIZE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROM_MONTH` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TO_MONTH` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SEARCH_CODE` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SEARCH_TEXT` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@USE_YN` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:18:04.360 |
| 읽기·참조 객체 | `office.dbo.sawon`, `sb_bill.dbo.unpaid_charge_clear`, `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/unpaidexception/repository/UnpaidExceptionMapper.kt#L36) — 바인딩: `page`, `top`, `fromMonth`, `toMonth`, `searchCode`, `searchText`, `useYn`. 결과 매핑: `TOT_COUNT` → `totCount`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `FROMMONTH` → `fromMonth`, `TOMONTH` → `toMonth`, `SNAME` → `sname`, `COMNO` → `comNo`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @FROM_MONTH = REPLACE(ISNULL(@FROM_MONTH, ''), '-', '');
SET @TO_MONTH   = REPLACE(ISNULL(@TO_MONTH, ''),   '-', '');
JOIN SMARTBILL3..COMPANY B WITH(NOLOCK)
JOIN OFFICE..SAWON C WITH(NOLOCK)
WHERE 1 = 1
ORDER BY A.COMNO DESC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db296"></a>
## smartwork.dbo.UspBill_BalanceCheckByDate_USE_List_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@GUBUN1` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@GUBUN2` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SCH_TEXT` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROM_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TO_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-20T10:15:26.227 |
| 읽기·참조 객체 | `office.dbo.sawon`, `sb_bill.dbo.payment`, `smartbill3.dbo.company`, `smartbill3.dbo.member`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchDeductionList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DailyDepositMapper.kt#L82) — 바인딩: `page`, `top`, `gubun1`, `gubun2`, `schText`, `fromDate`, `toDate`. 결과 매핑: `TOT_COUNT` → `totCount`, `PREPAY_DATE` → `prepayDate`, `CHANNEL` → `channel`, `MEM_ID` → `memId`, `STATEMENT` → `statement`, `USE_AMT` → `useAmt`, `PREPAY_AMT` → `prepayAmt`, `CARRYOVER_AMT` → `carryoverAmt`, `BALANCE_AMT` → `balanceAmt`, `COM_REGNO` → `comRegno`, `COM_NO` → `comNo`, `COM_NAME` → `comName`, `COM_DEL_YN` → `comDelYn`, `PAY_METHOD` → `payMethod`, `PREPAY_NO` → `prepayNo`, `ORDER_ID` → `orderId`, `RNUM` → `rnum`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SCH_TEXT = '%' + @SCH_TEXT + '%'
SET @SCH_TEXT = REPLACE(@SCH_TEXT, '-', '')
SET @SQL = N'
ROW_NUMBER() OVER (ORDER BY B.CDATE DESC) AS RNUM,
JOIN SMARTBILL3..SERVICE_PREPAY_HIS B WITH(NOLOCK) ON A.PREPAY_NO = B.IDX
LEFT JOIN SMARTBILL3..COMPANY C WITH(NOLOCK) ON A.COM_NO = C.COM_NO
LEFT JOIN SMARTBILL3..MEMBER MB WITH(NOLOCK) ON B.MemNo = MB.MEM_NO
LEFT JOIN OFFICE..SAWON M WITH(NOLOCK) ON B.SWNO = M.SW_NO
LEFT JOIN SB_BILL..PAYMENT D WITH(NOLOCK) ON B.CHANNELIDX = D.IDX AND D.COMNO = A.COM_NO
WHERE
WHERE RNUM BETWEEN ((@PAGE - 1) * @TOP + 1) AND (@PAGE * @TOP)
ORDER BY RNUM
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db297"></a>
## smartwork.dbo.UspBill_BalanceCheckByDate_USE_List_SELECT_Excel

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@GUBUN1` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@GUBUN2` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SCH_TEXT` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROM_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TO_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-20T10:15:26.467 |
| 읽기·참조 객체 | `office.dbo.sawon`, `sb_bill.dbo.payment`, `smartbill3.dbo.company`, `smartbill3.dbo.member`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchDeductionListForExcel](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DailyDepositMapper.kt#L110) — 바인딩: `gubun1`, `gubun2`, `schText`, `fromDate`, `toDate`. 결과 매핑: `TOT_COUNT` → `totCount`, `PREPAY_DATE` → `prepayDate`, `CHANNEL` → `channel`, `MEM_ID` → `memId`, `STATEMENT` → `statement`, `USE_AMT` → `useAmt`, `PREPAY_AMT` → `prepayAmt`, `CARRYOVER_AMT` → `carryoverAmt`, `BALANCE_AMT` → `balanceAmt`, `COM_REGNO` → `comRegno`, `COM_NO` → `comNo`, `COM_NAME` → `comName`, `COM_DEL_YN` → `comDelYn`, `PAY_METHOD` → `payMethod`, `PREPAY_NO` → `prepayNo`, `ORDER_ID` → `orderId`, `RNUM` → `rnum`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SCH_TEXT = '%' + @SCH_TEXT + '%'
SET @SCH_TEXT = REPLACE(@SCH_TEXT, '-', '')
SET @SQL = N'
ROW_NUMBER() OVER (ORDER BY B.CDATE DESC) AS RNUM,
JOIN SMARTBILL3..SERVICE_PREPAY_HIS B WITH(NOLOCK) ON A.PREPAY_NO = B.IDX
LEFT JOIN SMARTBILL3..COMPANY C WITH(NOLOCK) ON A.COM_NO = C.COM_NO
LEFT JOIN SMARTBILL3..MEMBER MB WITH(NOLOCK) ON B.MemNo = MB.MEM_NO
LEFT JOIN OFFICE..SAWON M WITH(NOLOCK) ON B.SWNO = M.SW_NO
LEFT JOIN SB_BILL..PAYMENT D WITH(NOLOCK) ON B.CHANNELIDX = D.IDX AND D.COMNO = A.COM_NO
WHERE
ORDER BY RNUM'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db298"></a>
## smartwork.dbo.UspBill_BalanceDepositProcess2

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@AMOUNT` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SW_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT` | `varchar(5)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-10T13:05:03.253 |
| 읽기·참조 객체 | `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 쓰기 대상 | `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `END`; `END TRY`; `END CATCH` |

### Mapper 입출력 매핑

- [processBalanceDeduction](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DepositProcessMapper.kt#L107) — 바인딩: `idx`, `amount`, `swNo`, `result, mode=OUT, jdbcType=VARCHAR`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @RESULT = '9'
WHERE PREPAY_NO = @IDX
SET @RESULT = '1'
BEGIN TRAN
WHERE PREPAY_NO = @IDX
WHERE PREPAY_NO = @IDX
SET @RESULT = '0'
COMMIT TRAN
ROLLBACK TRAN
SET @RESULT = '0'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db299"></a>
## smartwork.dbo.UspBill_BulkAccountDepositHistoryInfo

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-20T10:15:26.717 |
| 읽기·참조 객체 | `office.dbo.sawon`, `sb_bill_linked.dbo.crm_t_cr_os_iv`, `smartbill3.dbo.account_bulk_app_his_new`, `smartbill3.dbo.company`, `smartwork.dbo.os_iv_payment` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getProcessHistory](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/bulkaccountdeposit/repository/BulkAccountDepositMapper.kt#L100) — 바인딩: `idx`. 결과 매핑: `COM_REGNO` → `comRegno`, `COM_NAME` → `comName`, `AMOUNT` → `amount`, `DIVISION` → `division`, `CREATE_DATE` → `createDate`, `SNAME` → `sName`, `CHARGE_GUBUN` → `chargeGubun`, `CHARGE_MONTH` → `chargeMonth`, `CHARGE_AMOUNT` → `chargeAmount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT JOIN SMARTBILL3..COMPANY B ON A.COM_NO = B.COM_NO
LEFT JOIN OFFICE..SAWON C ON A.SW_NO = C.SW_NO
JOIN SB_BILL_LINKED..CRM_T_CR_OS_IV IV WITH (NOLOCK)
WHERE A.CHARGE_GUBUN = 'OSIV'
ORDER BY OP.IDX
WHERE A.ACCOUNT_BULK_APP_IDX = @IDX
ORDER BY A.CREATE_DATE DESC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db300"></a>
## smartwork.dbo.UspBill_BulkAccountDepositList_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROM_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TO_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SEARCH_CODE` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SEARCH_TEXT` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BANK_CODE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DEPOSIT_APPLY` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@GUBUN` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-20T10:15:26.970 |
| 읽기·참조 객체 | `smartbill3.dbo.account_bulk`, `smartbill3.dbo.account_bulk_app`, `smartbill3.dbo.account_bulk_app_his_new`, `smartbill3.dbo.common_code`, `smartbill3.dbo.company`, `smartwork.dbo.deposit_deduction`, `smartwork.dbo.os_iv_payment` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchBulkAccountDepositList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/bulkaccountdeposit/repository/BulkAccountDepositMapper.kt#L58) — 바인딩: `page`, `top`, `fromDate`, `toDate`, `searchCode`, `searchText`, `bankCode`, `depositApply`, `gubun`. 결과 매핑: `TOT_COUNT` → `totCount`, `IDX` → `idx`, `AMOUT_PAYABLE` → `amountPayable`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `CODE_DETAIL_NM` → `codeDetailNm`, `BANK_REGNO` → `bankRegno`, `PAYMENT_DATE` → `paymentDate`, `STATUS` → `status`, `COM_DEL_YN` → `comDelYn`, `AMOUNT` → `amount`, `GUBUN` → `gubun`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @D_TO_DATE = DATEADD(MS, -3, DATEADD(DD, 1, CONVERT(DATETIME, @TO_DATE, 121)))
JOIN (
(SELECT TOP 1 DIVISION FROM SMARTBILL3..ACCOUNT_BULK_APP_HIS_NEW WHERE ACCOUNT_BULK_APP_IDX = A.IDX ORDER BY DIVISION) AS HISTORY1,
(SELECT TOP 1 DIVISION FROM SMARTBILL3..ACCOUNT_BULK_APP_HIS_NEW WHERE ACCOUNT_BULK_APP_IDX = A.IDX ORDER BY DIVISION DESC) AS HISTORY2
LEFT JOIN SMARTBILL3..ACCOUNT_BULK_APP_HIS_NEW B ON A.IDX = B.ACCOUNT_BULK_APP_IDX
GROUP BY A.IDX, B.DIVISION, BANK_CODE, BANK_REGNO
LEFT JOIN (
GROUP BY ACCOUNT_BULK_APP_IDX
LEFT JOIN SMARTBILL3..ACCOUNT_BULK C ON AB.BANK_REGNO = C.BANK_REGNO
LEFT JOIN SMARTBILL3..COMPANY D ON C.COM_NO = D.COM_NO
LEFT JOIN SMARTBILL3..COMMON_CODE E ON A.BANK_CODE = E.CODE AND CODE_TYPE = 'BULK'
WHERE OP.CHANNEL = 'BULK' AND OP.DEPOSIT_IDX = AB.IDX) AS OSIV_CNT,
WHERE H.ACCOUNT_BULK_APP_IDX = AB.IDX AND H.DIVISION = 'PAYMENT') AS PAY_CNT
WHERE D.channel = 'BULK' AND D.deposit_idx = AB.IDX AND D.status = 'A'
WHERE 1=1
GROUP BY AB.IDX, HISTORY1, HISTORY2, A.IDX, D.COM_NAME, D.COM_REGNO, E.CODE_DETAIL_NM, A.BANK_REGNO, COM_DEL_YN, OG.OSIV_CNT, OG.PAY_CNT
ROW_NUMBER() OVER (ORDER BY IDX DESC) AS RN,
WHERE (@DEPOSIT_APPLY = ''
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db301"></a>
## smartwork.dbo.UspBill_BulkAccountDepositProcessInfo_INSERT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CHARGE_MONTH` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@AMOUNT` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@STATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REMARK` | `varchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SW_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CUSTOM_APPLY_DATE` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT` | `varchar(1)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-20T10:15:27.220 |
| 읽기·참조 객체 | `sb_bill.dbo.invoice`, `sb_bill.dbo.payment`, `sb_bill.dbo.payment_his`, `smartbill3.dbo.account_bulk_app`, `smartbill3.dbo.account_bulk_app_his_new`, `smartbill3.dbo.company`, `smartbill3.dbo.company_history`, `smartbill3.dbo.member`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his`, `smartwork.dbo.deposit_deduction` |
| 쓰기 대상 | `sb_bill.dbo.invoice`, `sb_bill.dbo.payment`, `sb_bill.dbo.payment_his`, `smartbill3.dbo.account_bulk_app_his_new`, `smartbill3.dbo.company`, `smartbill3.dbo.company_history`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | `END`; `END CATCH` |

### Mapper 입출력 매핑

- [processDeposit](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/bulkaccountdeposit/repository/BulkAccountDepositMapper.kt#L150) — 바인딩: `idx`, `comNo`, `chargeMonth`, `amount`, `state`, `remark`, `swNo`, `customApplyDate`, `result, mode=OUT, jdbcType=NVARCHAR`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE D.channel = 'BULK' AND D.deposit_idx = @IDX AND D.status = 'A'
LEFT JOIN SMARTBILL3..ACCOUNT_BULK_APP_HIS_NEW B
WHERE
WHERE
SET @RESULT = '1'
WHERE
SET @CURRENT_CHARGE_MONTH = CONVERT(VARCHAR(6), GETDATE(), 112)
SET @RESULT = '0'
WHERE P.COMNO = @COM_NO AND P.CHARGEMONTH = @CHARGE_MONTH), 0)
WHERE I.COMNO = @COM_NO AND I.CHARGEMONTH = @CHARGE_MONTH
BEGIN TRAN
SET @CUSTOM_APPLY_DATE = CONVERT(DATETIME, @CHARGE_MONTH+'01')
SET @DEPOSIT_DATE = @CUSTOM_APPLY_DATE
WHERE
WHERE
WHERE
SET @UNPAY = @UNPAY - @PAY_AMT
WHERE
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db302"></a>
## smartwork.dbo.UspBill_DailyDepositChargeList_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@GUBUN1` | `varchar(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@GUBUN2` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PAY_METHODE` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SCH_TEXT` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROM_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TO_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CHANNEL_FILTER` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-09-16T10:18:38.910 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.member`, `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchChargeList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DailyDepositMapper.kt#L54) — 바인딩: `page`, `top`, `gubun1`, `gubun2`, `payMethode`, `schText`, `fromDate`, `toDate`, `channelFilter`. 결과 매핑: `TOT_COUNT` → `totCount`, `PREPAY_DATE` → `prepayDate`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `PREPAY_AMT` → `prepayAmt`, `CARRYOVER_AMT` → `carryoverAmt`, `USE_AMT` → `useAmt`, `BALANCE_AMT` → `balanceAmt`, `PREPAY_NO` → `prepayNo`, `PAY_METHOD` → `payMethod`, `COM_NO` → `comNo`, `COM_DEL_YN` → `comDelYn`, `MEM_ID` → `memId`, `STATEMENT` → `statement`, `CHANNEL` → `channel`, `RN` → `rn`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SCH_TEXT = '%' + @SCH_TEXT + '%'
SET @SCH_TEXT = REPLACE(@SCH_TEXT, '-', '')
SET @SQL = N'
ROW_NUMBER() OVER (ORDER BY A.PREPAY_DATE DESC, A.PREPAY_NO DESC) AS RN,
LEFT JOIN SMARTBILL3..COMPANY C WITH(NOLOCK) ON A.COM_NO = C.COM_NO
LEFT JOIN SMARTBILL3..MEMBER M WITH(NOLOCK) ON A.PREPAY_MEM_NO = M.MEM_NO
LEFT JOIN (
ROW_NUMBER() OVER (PARTITION BY IDX ORDER BY CDATE ASC) AS SEQ
WHERE STATEMENT = ''PAYMENT''
WHERE 1=1 '
WHERE RN BETWEEN ((@PAGE - 1) * @TOP + 1) AND (@PAGE * @TOP)
ORDER BY RN
```

하위 프로시저·함수·뷰: `sb_bill.dbo.fnfillsinglequt`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db303"></a>
## smartwork.dbo.UspBill_DepositCancelDate_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@IDX_LIST` | `varchar(max)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:43.367 |
| 읽기·참조 객체 | `smartbill3.dbo.service_prepay_his` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getCancelDates](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/deposit/repository/DepositDetailMapper.kt#L114) — 바인딩: `idxList`. 결과 매핑: `ID` → `id`, `CANCEL_DATE` → `cancelDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE D.Idx = B.Idx
ORDER BY D.CDate DESC
WHERE B.Channel = 'CANCEL'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db304"></a>
## smartwork.dbo.UspBill_DepositCancelVerify_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@ORDER_ID` | `varchar(64)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:43.457 |
| 읽기·참조 객체 | `smartbill3.dbo.accinfo_cancel`, `smartbill3.dbo.accinfo_history` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [verifyDepositCancel](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/status/repository/PaymentStatusInfoMapper.kt#L176) — 바인딩: `orderId`. 결과 매핑: `SETTLE_TYPE` → `settleType`, `CANCEL_COUNT` → `cancelCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE H.ORDER_ID = @ORDER_ID AND H.ACC_AMT >= 0
ORDER BY H.WRITE_DATE ASC) AS SETTLE_TYPE,
WHERE C.ORDER_ID = @ORDER_ID) AS CANCEL_COUNT;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db305"></a>
## smartwork.dbo.UspBill_HeadOfficeDepositCompanySearch_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@SEARCH_TEXT` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DEPOSIT_AMOUNT` | `money` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SEARCH_MODE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PAGESIZE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-18T15:50:53.763 |
| 읽기·참조 객체 | `sb_bill.dbo.invoice`, `sb_bill.dbo.payment`, `sb_bill_linked.dbo.crm_t_cr_os_iv`, `smartbill3.dbo.company` |
| 쓰기 대상 | 쓰기문 존재; 별칭·임시 객체 또는 동적 대상의 영향은 추가 확인 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchCompanies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/headofficedeposit/repository/HeadOfficeDepositMapper.kt#L152) — 바인딩: `searchText`, `depositAmount`, `searchMode`, `page`, `pageSize`. 결과 매핑: `TOT_COUNT` → `totCount`, `COM_NO` → `comNo`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `CHARGEMONTH` → `chargeMonth`, `BILLING_AMOUNT` → `billingAmount`, `GUBUN` → `gubun`, `CR_CD` → `crCd`, `SERVICE_CD` → `serviceCd`, `SEQ` → `seq`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @CLEAN_NAME = @SEARCH_TEXT;
SET @CLEAN_NAME = REPLACE(@CLEAN_NAME, '(주)', '');
SET @CLEAN_NAME = REPLACE(@CLEAN_NAME, '주식회사', '');
SET @CLEAN_NAME = REPLACE(@CLEAN_NAME, '(유)', '');
SET @CLEAN_NAME = REPLACE(@CLEAN_NAME, '유한회사', '');
SET @CLEAN_NAME = REPLACE(@CLEAN_NAME, '(사)', '');
SET @CLEAN_NAME = REPLACE(@CLEAN_NAME, '사단법인', '');
SET @CLEAN_NAME = REPLACE(@CLEAN_NAME, '(재)', '');
SET @CLEAN_NAME = REPLACE(@CLEAN_NAME, '재단법인', '');
SET @CLEAN_NAME = REPLACE(@CLEAN_NAME, ' ', '');
SET @CLEAN_NAME = LTRIM(RTRIM(@CLEAN_NAME));
WHERE C.COM_DEL_YN = 'N' AND C.COM_REGNO != ''
WHERE CN.CLEAN_COM_NAME = @CLEAN_NAME;
- ISNULL((SELECT SUM(P.PaymentAmount) FROM Sb_Bill..PAYMENT P WHERE P.ComNo = C.COM_NO AND P.ChargeMonth = I.CHARGEMONTH), 0) AS BILLING_AMOUNT
FROM Sb_Bill..INVOICE I WHERE I.COMNO = C.COM_NO GROUP BY I.CHARGEMONTH
WHERE INV.BILLING_AMOUNT > 0 ORDER BY INV.CHARGEMONTH DESC
WHERE C.IS_EXACT = 1
- ISNULL((SELECT SUM(P.PaymentAmount) FROM Sb_Bill..PAYMENT P WHERE P.ComNo = C.COM_NO AND P.ChargeMonth = I.CHARGEMONTH), 0) AS BILLING_AMOUNT
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db306"></a>
## smartwork.dbo.UspBill_OsIvBulkProcess_INSERT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DEPOSIT_IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CR_CD` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SERVICE_CD` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SEQ` | `smallint` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DEPOSIT_NAME` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@AMOUNT` | `money` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@IC_DT` | `varchar(8)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SW_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REMARK` | `varchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT` | `varchar(1)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |
| `@OS_IV_PAYMENT_IDX` | `bigint` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-20T10:15:28.447 |
| 읽기·참조 객체 | `sb_bill_linked.dbo.crm_t_cr_os_iv`, `smartbill3.dbo.account_bulk_app`, `smartbill3.dbo.account_bulk_app_his_new`, `smartwork.dbo.deposit_deduction`, `smartwork.dbo.os_iv_payment` |
| 쓰기 대상 | `sb_bill_linked.dbo.crm_t_cr_os_iv`, `smartbill3.dbo.account_bulk_app_his_new`, `smartwork.dbo.os_iv_payment` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [processBulk](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L53) — 바인딩: `depositIdx`, `crCd`, `serviceCd`, `seq`, `comNo, jdbcType=INTEGER`, `depositName`, `amount`, `icDt`, `swNo`, `remark`, `result, mode=OUT, jdbcType=VARCHAR`, `osIvPaymentIdx, mode=OUT, jdbcType=BIGINT`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @RESULT = '0';
BEGIN TRAN
WHERE D.channel = 'BULK' AND D.deposit_idx = @DEPOSIT_IDX AND D.status = 'A';
LEFT JOIN SMARTBILL3..ACCOUNT_BULK_APP_HIS_NEW B ON A.IDX = B.ACCOUNT_BULK_APP_IDX
WHERE A.IDX = @DEPOSIT_IDX;
BEGIN SET @RESULT = '1'; ROLLBACK TRAN; RETURN; END
WHERE CR_CD=@CR_CD AND SERVICE_CD=@SERVICE_CD AND SEQ=@SEQ;
IF (@TOTAL IS NULL) BEGIN SET @RESULT = '4'; ROLLBACK TRAN; RETURN; END
IF (@TOTAL > 0 AND @PAID >= @TOTAL) BEGIN SET @RESULT = '3'; ROLLBACK TRAN; RETURN; END
WHERE CR_CD=@CR_CD AND SERVICE_CD=@SERVICE_CD AND SEQ=@SEQ;
SET @OS_IV_PAYMENT_IDX = SCOPE_IDENTITY();
COMMIT TRAN
SET @RESULT = '2';
IF @@TRANCOUNT > 0 ROLLBACK TRAN;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db307"></a>
## smartwork.dbo.UspBill_OsIvHeadOfficeProcess_INSERT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@DEPOSIT_IDX` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CR_CD` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SERVICE_CD` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SEQ` | `smallint` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DEPOSIT_NAME` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@AMOUNT` | `money` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@IC_DT` | `varchar(8)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SW_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REMARK` | `varchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@RESULT` | `varchar(1)` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |
| `@OS_IV_PAYMENT_IDX` | `bigint` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-20T10:15:28.740 |
| 읽기·참조 객체 | `sb_bill.dbo.headoffice_deposit`, `sb_bill.dbo.headoffice_deposit_his`, `sb_bill_linked.dbo.crm_t_cr_os_iv`, `smartwork.dbo.deposit_deduction`, `smartwork.dbo.os_iv_payment` |
| 쓰기 대상 | `sb_bill.dbo.headoffice_deposit_his`, `sb_bill_linked.dbo.crm_t_cr_os_iv`, `smartwork.dbo.os_iv_payment` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [processHeadOffice](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/osivdeposit/repository/OsIvDepositMapper.kt#L39) — 바인딩: `depositIdx`, `crCd`, `serviceCd`, `seq`, `comNo, jdbcType=INTEGER`, `depositName`, `amount`, `icDt`, `swNo`, `remark`, `result, mode=OUT, jdbcType=VARCHAR`, `osIvPaymentIdx, mode=OUT, jdbcType=BIGINT`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @RESULT = '0';
BEGIN TRAN
WHERE D.channel = 'HEADOFFICE' AND D.deposit_idx = @DEPOSIT_IDX AND D.status = 'A';
LEFT JOIN Sb_Bill..HEADOFFICE_DEPOSIT_HIS B ON A.IDX = B.IDX
WHERE A.IDX = @DEPOSIT_IDX;
BEGIN SET @RESULT = '1'; ROLLBACK TRAN; RETURN; END
WHERE CR_CD=@CR_CD AND SERVICE_CD=@SERVICE_CD AND SEQ=@SEQ;
IF (@TOTAL IS NULL) BEGIN SET @RESULT = '4'; ROLLBACK TRAN; RETURN; END
IF (@TOTAL > 0 AND @PAID >= @TOTAL) BEGIN SET @RESULT = '3'; ROLLBACK TRAN; RETURN; END
WHERE CR_CD=@CR_CD AND SERVICE_CD=@SERVICE_CD AND SEQ=@SEQ;
SET @OS_IV_PAYMENT_IDX = SCOPE_IDENTITY();
COMMIT TRAN
SET @RESULT = '2';
IF @@TRANCOUNT > 0 ROLLBACK TRAN;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db308"></a>
## smartwork.dbo.UspBill_PayMentCanCelList_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@GUBUN1` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@GUBUN2` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SCH_TEXT` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROM_DATE` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TO_DATE` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PAY_DIV` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-10-08T17:41:40.857 |
| 읽기·참조 객체 | `smartbill3.dbo.accinfo_cancel`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchCancelList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/banktransfercancel/repository/BankTransferCancelMapper.kt#L33) — 바인딩: `page`, `top`, `gubun1`, `gubun2`, `schText`, `fromDate`, `toDate`, `payDiv`. 결과 매핑: `TOT_COUNT` → `totCount`, `IDX` → `idx`, `CDATE` → `cdate`, `ORDER_ID` → `orderId`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `COM_DEL_YN` → `comDelYn`, `SETTLE_TYPE` → `settleType`, `CAMOUNT` → `camount`, `MEM_NAME` → `memName`, `PREPAY_DTI_NO` → `prepayDtiNo`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @TOP2 = @TOT_COUNT - (@PAGE - 1) * @TOP
SET @TOP2 = @TOP
SET @SCH_TEXT = '%' + @SCH_TEXT + '%'
SET @SCH_TEXT = REPLACE(@SCH_TEXT, '-', '')
SET @SQL = N'
JOIN SMARTBILL3..COMPANY C
JOIN SMARTBILL3..MEMBER M
WHERE 1 = 1 AND A.pay_method = ''01'' '
+ N' ORDER BY IDX DESC
ORDER BY IDX ASC
JOIN SMARTBILL3..COMPANY C
JOIN SMARTBILL3..MEMBER M
INNER JOIN LASTPAGES AS D ON A.IDX = D.LAST_IDX
ORDER BY A.IDX DESC   '
```

하위 프로시저·함수·뷰: `sb_bill.dbo.fnfillsinglequt2`, `sb_bill.dbo.uspbill_paymentcancellistcount_select`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db309"></a>
## smartwork.dbo.UspBill_PayMentComNo_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@IDX` | `bigint` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:44.317 |
| 읽기·참조 객체 | `sb_bill.dbo.payment` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getPaymentComNo](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/status/repository/PaymentStatusInfoMapper.kt#L106) — 바인딩: `idx`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE IDX = @IDX;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db310"></a>
## smartwork.dbo.UspBill_PayMentDetailHistory_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@IDX` | `bigint` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:44.407 |
| 읽기·참조 객체 | `office.dbo.sawon`, `sb_bill.dbo.payment`, `sb_bill.dbo.payment_his`, `smartbill3.dbo.company`, `smartbill3.dbo.service_prepay` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getPaymentDetailHistory](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/status/repository/PaymentStatusInfoMapper.kt#L83) — 바인딩: `idx`. 결과 매핑: `COM_REGNO` → `comRegno`, `COM_NAME` → `comName`, `STATEMENTAMOUNT` → `statementAmount`, `STATEMENT` → `statement`, `CDATE` → `cdate`, `SNAME` → `sname`, `PAYMENTDIVISION` → `paymentDivision`, `OrderID` → `orderId`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
JOIN SMARTBILL3..SERVICE_PREPAY B
JOIN SMARTBILL3..COMPANY C
LEFT JOIN OFFICE..SAWON D
JOIN SB_BILL..PAYMENT E
WHERE A.IDX = @IDX
ORDER BY A.CDATE DESC;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db311"></a>
## smartwork.dbo.UspBill_PayMentList_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@GUBUN1` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@GUBUN2` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SCH_TEXT` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROM_DATE` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TO_DATE` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PAY_DIV` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@GUBUN3` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROM_MONTH` | `varchar(6)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TO_MONTH` | `varchar(6)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@STATUSES` | `nvarchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-09-16T10:18:39.133 |
| 읽기·참조 객체 | `sb_bill.dbo.invoice`, `sb_bill.dbo.payment`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 쓰기문 존재; 별칭·임시 객체 또는 동적 대상의 영향은 추가 확인 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchPaymentStatusList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/status/repository/PaymentStatusInfoMapper.kt#L50) — 바인딩: `page`, `top`, `gubun1`, `gubun2`, `schText`, `fromDate`, `toDate`, `payDiv`, `gubun3`, `fromMonth`, `toMonth`, `statuses`. 결과 매핑: `IDX` → `idx`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `CHARGEMONTH` → `chargeMonth`, `INVOICE_AMOUNT` → `invoiceAmount`, `PAYMENTAMOUNT` → `paymentAmount`, `PAYMENTDIVISION` → `paymentDivision`, `PAYMENTDATE` → `paymentDate`, `MEM_NAME` → `memName`, `DTIIDX` → `dtiIdx`, `COM_DEL_YN` → `comDelYn`, `PAYMENT_STATUS` → `paymentStatus`, `TOT_COUNT` → `totCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
IF (@GUBUN1 = 'A' AND @SCH_TEXT <> '') SET @SCH_TEXT = '%' + @SCH_TEXT + '%';
ELSE IF (@GUBUN1 = 'B' AND @SCH_TEXT <> '') SET @SCH_TEXT = REPLACE(@SCH_TEXT, '-', '');
FROM (SELECT TOP (LEN(@PAY_DIV) / 2) ROW_NUMBER() OVER (ORDER BY (SELECT NULL)) AS n
JOIN SMARTBILL3..COMPANY C WITH (NOLOCK) ON A.COMNO = C.COM_NO
LEFT JOIN SMARTBILL3..MEMBER M WITH (NOLOCK) ON A.MEMNO = M.MEM_NO
WHERE (@GUBUN1 <> 'A' OR @SCH_TEXT = '' OR C.COM_NAME LIKE @SCH_TEXT)
GROUP BY A.IDX, A.CHARGEMONTH, A.COMNO, A.PAYMENTAMOUNT, A.PAYMENTDIVISION,
SELECT *, ROW_NUMBER() OVER (ORDER BY IDX DESC) AS RN, COUNT(*) OVER() AS TOT_COUNT
WHERE RN > @OFFSET AND RN <= @OFFSET + @TOP;
WHERE I.COMNO = P.COMNO AND I.CHARGEMONTH = P.CHARGEMONTH
ORDER BY IDX DESC;
WHERE value IN (N'완납',N'부분납',N'과납',N'입금전',N'미납',N'입금 취소'))
JOIN SMARTBILL3..COMPANY C WITH (NOLOCK) ON A.COMNO = C.COM_NO
LEFT JOIN SMARTBILL3..MEMBER M WITH (NOLOCK) ON A.MEMNO = M.MEM_NO
WHERE (@GUBUN1 <> 'A' OR @SCH_TEXT = '' OR C.COM_NAME LIKE @SCH_TEXT)
GROUP BY A.IDX, A.CHARGEMONTH, A.COMNO, A.PAYMENTAMOUNT, A.PAYMENTDIVISION,
WHERE COMNO IS NOT NULL AND CHARGEMONTH IS NOT NULL;
LEFT JOIN SB_BILL..INVOICE I WITH (NOLOCK)
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db312"></a>
## smartwork.dbo.UspBill_PayMentList_SELECT_Excel

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@GUBUN1` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@GUBUN2` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SCH_TEXT` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROM_DATE` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TO_DATE` | `datetime` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PAY_DIV` | `varchar(30)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@GUBUN3` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROM_MONTH` | `varchar(6)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TO_MONTH` | `varchar(6)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@STATUSES` | `nvarchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-11T18:27:22.863 |
| 읽기·참조 객체 | `sb_bill.dbo.invoice`, `sb_bill.dbo.payment`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 쓰기문 존재; 별칭·임시 객체 또는 동적 대상의 영향은 추가 확인 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchPaymentStatusExcel](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/status/repository/PaymentStatusInfoMapper.kt#L128) — 바인딩: `gubun1`, `gubun2`, `schText`, `fromDate`, `toDate`, `payDiv`, `gubun3`, `fromMonth`, `toMonth`, `statuses`. 결과 매핑: `CHARGEMONTH` → `chargeMonth`, `PAYMENTDATE` → `paymentDate`, `COM_NAME` → `comName`, `COM_REGNO` → `comRegno`, `PAYMENTDIVISION` → `paymentDivision`, `INVOICE_AMOUNT` → `invoiceAmount`, `PAYMENTAMOUNT` → `paymentAmount`, `MEM_NAME` → `memName`, `ORDERID` → `orderId`, `PAYMENT_STATUS` → `paymentStatus`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
IF (@GUBUN1 = 'A' AND @SCH_TEXT <> '') SET @SCH_TEXT = '%' + @SCH_TEXT + '%';
ELSE IF (@GUBUN1 = 'B' AND @SCH_TEXT <> '') SET @SCH_TEXT = REPLACE(@SCH_TEXT, '-', '');
FROM (SELECT TOP (LEN(@PAY_DIV) / 2) ROW_NUMBER() OVER (ORDER BY (SELECT NULL)) AS n
JOIN SMARTBILL3..COMPANY C WITH (NOLOCK) ON A.COMNO = C.COM_NO
LEFT JOIN SMARTBILL3..MEMBER M WITH (NOLOCK) ON A.MEMNO = M.MEM_NO
LEFT JOIN SB_BILL..INVOICE I WITH (NOLOCK) ON A.COMNO = I.COMNO AND A.CHARGEMONTH = I.CHARGEMONTH
WHERE (@GUBUN1 <> 'A' OR @SCH_TEXT = '' OR C.COM_NAME LIKE @SCH_TEXT)
GROUP BY A.IDX, A.ORDERID, A.CHARGEMONTH, A.COMNO, A.PAYMENTAMOUNT, A.PAYMENTDIVISION,
WHERE (@STATUSES = '' OR PAYMENT_STATUS IN (SELECT value FROM STRING_SPLIT(@STATUSES, ',')))
ORDER BY IDX DESC;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db313"></a>
## smartwork.dbo.UspBill_PayMentWaitingDeposit_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@IDX_LIST` | `nvarchar(max)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:44.480 |
| 읽기·참조 객체 | `sb_bill.dbo.headoffice_deposit`, `sb_bill.dbo.headoffice_deposit_his`, `sb_bill.dbo.payment`, `smartbill3.dbo.account_bulk`, `smartbill3.dbo.account_bulk_app`, `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [checkWaitingDeposits](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/status/repository/PaymentStatusInfoMapper.kt#L92) — 바인딩: `idxList`. 결과 매핑: `IDX` → `idx`, `waitingDeposit` → `waitingDeposit`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
JOIN SMARTBILL3..COMPANY c
WHERE c.COM_NO = P.ComNo
WHERE hdh.Idx = hd.Idx
JOIN SMARTBILL3..ACCOUNT_BULK_APP aba
WHERE ab.COM_NO = P.ComNo
WHERE P.IDX IN
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db314"></a>
## smartwork.dbo.UspBill_RefundChargeDetail_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REFUND_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@GROUP_NO` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PREPAY_NO` | `varchar(16)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:44.553 |
| 읽기·참조 객체 | `smartbill3.dbo.service_prepay`, `smartbill3.dbo.service_prepay_his` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getRefundChargeDetails](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/refund/repository/RefundDetailMapper.kt#L57) — 바인딩: `comNo`, `refundDate`, `groupNo`, `prepayNo`. 결과 매핑: `PREPAY_NO` → `prepayNo`, `PREPAY_DATE` → `prepayDate`, `PREPAY_AMT` → `prepayAmt`, `PRINCIPAL_AMT` → `principalAmt`, `SUBTRACTION` → `subtraction`, `CHARGE` → `charge`, `USE_AMT` → `useAmt`, `REFUND_YN` → `refundYn`, `REFUND_AMT` → `refundAmt`, `REFUND_COMMISSION_AMT` → `refundCommissionAmt`, `ONE_REFUND_AMT` → `oneRefundAmt`, `ONE_REFUND_COMMISSION_AMT` → `oneRefundCommissionAmt`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
JOIN (SELECT COM_NO, SUM(USE_AMT) AS USE_AMT,
WHERE COM_NO = @COM_NO
GROUP BY COM_NO) B ON A.COM_NO = B.COM_NO
LEFT OUTER JOIN (SELECT IDX, STATEMENTAMOUNT FROM SMARTBILL3..SERVICE_PREPAY_HIS
WHERE CHANNEL = 'REFUND') C ON A.PREPAY_NO = C.IDX
WHERE A.COM_NO = @COM_NO
ORDER BY A.PREPAY_DATE
WHERE A.COM_NO = @COM_NO
ORDER BY A.PREPAY_NO DESC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db315"></a>
## smartwork.dbo.UspBill_RefundExpiredCharge_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_REGNO` | `varchar(16)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REFUND_DATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-10-08T17:01:23.017 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.service_prepay` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchExpiredCharges](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/refund/repository/RefundAmountMapper.kt#L45) — 바인딩: `comRegno`, `refundDate`. 결과 매핑: `PREPAY_NO` → `prepayNo`, `PREPAY_DATE` → `prepayDate`, `PREPAY_AMT` → `prepayAmt`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
CREATE   PROCEDURE dbo.UspBill_RefundExpiredCharge_SELECT @COM_REGNO VARCHAR(16), @REFUND_DATE VARCHAR(10) AS BEGIN SET NOCOUNT ON SET @COM_REGNO = REPLACE(@COM_REGNO, '-', '') DECLARE @COM_NO INT SELECT @COM_NO = COM_NO FROM SMARTBILL3..COMPANY WITH(NOLOCK) WHERE COM_REGNO = @COM_REGNO AND COM_DEL_YN = 'N' SELECT P.PREPAY_NO, P.PREPAY_DATE, ISNULL(P.PREPAY_AMT, 0) AS PREPAY_AMT FROM SMARTBILL3..SERVICE_PREPAY P WITH(NOLOCK) WHERE P.COM_NO = @COM_NO AND P.PREPAY_DATE < DATEADD(DAY, -90, @REFUND_DATE) ORDER BY P.PREPAY_DATE DESC, P.PREPAY_NO DESC SET NOCOUNT OFF END
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db316"></a>
## smartwork.dbo.UspBill_RefundHistoryInfo

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@REFUND_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-10-08T15:50:42.537 |
| 읽기·참조 객체 | `office.dbo.sawon`, `smartbill3.dbo.service_refund_his` |
| 쓰기 대상 | 쓰기문 존재; 별칭·임시 객체 또는 동적 대상의 영향은 추가 확인 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getRefundHistories](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/refund/repository/RefundDetailMapper.kt#L89) — 바인딩: `refundNo`. 결과 매핑: `UPDATE_DATE` → `updateDate`, `REFUND_STATE` → `refundState`, `CONTENT` → `content`, `SNAME` → `sname`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT JOIN OFFICE..SAWON B WITH(NOLOCK)
WHERE A.REFUND_NO = @REFUND_NO
ORDER BY A.UPDATE_DATE DESC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db317"></a>
## smartwork.dbo.UspCompanyAdmin_ChangeCorporate

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `bigint` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MEM_NO` | `bigint` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:44.893 |
| 읽기·참조 객체 | `smartbill3.dbo.member` |
| 쓰기 대상 | `smartbill3.dbo.member` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [changeCorporateAdmin](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L1008) — 바인딩: `comNo`, `memNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
BEGIN TRAN;
WHERE COM_NO = @COM_NO AND MEM_TYPE = 'F';
WHERE MEM_NO = @MEM_NO;
COMMIT;
IF @@TRANCOUNT > 0 ROLLBACK;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db318"></a>
## smartwork.dbo.UspCompanyAdmin_ChangeDeptManager

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `bigint` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SERVICE_TYPE` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MEM_NO` | `bigint` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:44.983 |
| 읽기·참조 객체 | `smartbill3.dbo.dept_manager` |
| 쓰기 대상 | `smartbill3.dbo.dept_manager` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [changeDeptManager](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L1023) — 바인딩: `comNo`, `serviceType`, `memNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db319"></a>
## smartwork.dbo.UspCompanyAdmin_ChangeTaxCafe

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MEM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:45.073 |
| 읽기·참조 객체 | `smartbill3.dbo.member`, `smartbill3.dbo.tax_admin` |
| 쓰기 대상 | `smartbill3.dbo.tax_admin` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [changeTaxCafeAdmin](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L1018) — 바인딩: `comNo`, `memNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
JOIN SmartBill3..MEMBER M WITH (NOLOCK) ON TA.MEM_NO = M.MEM_NO
WHERE M.COM_NO = @COM_NO AND TA.MEM_RGT = 'F'
WHERE MEM_NO IN (
JOIN SmartBill3..MEMBER M WITH (NOLOCK) ON TA.MEM_NO = M.MEM_NO
WHERE M.COM_NO = @COM_NO AND TA.MEM_RGT = 'F'
SELECT @CAFE_ID = MEM_ID FROM SmartBill3..MEMBER WITH (NOLOCK) WHERE MEM_NO = @MEM_NO;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db320"></a>
## smartwork.dbo.UspCompanyAdmin_ChangeTaxInvoice

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `bigint` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MEM_NO` | `bigint` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:45.197 |
| 읽기·참조 객체 | `sb_dti.dbo.service_admin` |
| 쓰기 대상 | `sb_dti.dbo.service_admin` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [changeTaxInvoiceAdmin](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L1013) — 바인딩: `comNo`, `memNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
IF EXISTS (SELECT 1 FROM SB_DTI..SERVICE_ADMIN WHERE COM_NO = @COM_NO)
WHERE COM_NO = @COM_NO;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db321"></a>
## smartwork.dbo.UspCompanyMaintenanceBilling_Select

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:45.313 |
| 읽기·참조 객체 | `sb_bill.dbo.usecount_step3` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getMaintenanceBillingYn](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L844) — 바인딩: `comNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE s.ComNo = @COM_NO
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db322"></a>
## smartwork.dbo.UspCompanyMember_Withdraw

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@MEM_NO` | `bigint` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-09-03T14:24:44.300 |
| 읽기·참조 객체 | `sb_dti_log.dbo.dormant_member`, `smartbill3.dbo.member` |
| 쓰기 대상 | `sb_dti_log.dbo.dormant_member`, `smartbill3.dbo.member` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [withdrawMember](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L1028) — 바인딩: `memNo`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
BEGIN TRAN;
WHERE MEM_NO = @MEM_NO;
WHERE MEM_NO = @MEM_NO;
COMMIT;
IF @@TRANCOUNT > 0 ROLLBACK;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db323"></a>
## smartwork.dbo.UspDrcCompanyInfo

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@ComNo` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:45.817 |
| 읽기·참조 객체 | `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findCompany](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcRightMapper.kt#L59) — 바인딩: `comNo`. 결과 매핑: `com_name` → `comName`, `com_regno` → `comRegno`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE com_no = @ComNo AND com_del_yn = 'N'
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db324"></a>
## smartwork.dbo.UspDrcCompanyLinkSearch

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@SchCode` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SchContent` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-10-16T11:20:30.200 |
| 읽기·참조 객체 | `sb_drc.dbo.drc_company_link`, `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchCompanyLinks](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcCompanyLinkMapper.kt#L39) — 바인딩: `schCode`, `schContent`. 결과 매핑: `Com_No` → `comNo`, `COM_REGNO` → `comRegno`, `COM_NAME` → `comName`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT JOIN SmartBill3..COMPANY c WITH(NOLOCK)
WHERE (@SchCode = 'A'
ORDER BY link.Start_RoutingDate DESC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db325"></a>
## smartwork.dbo.UspDrcCompanySearch

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@SearchText` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:45.970 |
| 읽기·참조 객체 | `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchCompanies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcRightMapper.kt#L38) — 바인딩: `searchText`. 결과 매핑: `com_no` → `comNo`, `com_name` → `comName`, `com_regno` → `comRegno`, `com_president` → `comPresident`, `com_address` → `comAddress`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE (com_name LIKE '%' + @SearchText + '%' OR com_regno LIKE '%' + @SearchText + '%')
ORDER BY com_name
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db326"></a>
## smartwork.dbo.UspDrcCompanySearchForRegist

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@Keyword` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:46.047 |
| 읽기·참조 객체 | `smartbill3.dbo.company`, `smartbill3.dbo.settlement` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchCompaniesForRegistration](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcCompanyLinkMapper.kt#L112) — 바인딩: `keyword`. 결과 매핑: `com_no` → `comNo`, `com_regno` → `comRegno`, `com_name` → `comName`, `bill_type` → `billType`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT JOIN SmartBill3..SETTLEMENT s ON c.com_no = s.com_no AND s.service_type = 'DRC'
WHERE c.com_del_yn = 'N'
ORDER BY c.com_name, c.com_regno ASC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db327"></a>
## smartwork.dbo.UspDrcContractComLst

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@StartDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@EndDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SearchType` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SearchText` | `varchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Com_Type` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Status_Code` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:46.093 |
| 읽기·참조 객체 | `sb_drc.dbo.drc_company`, `sb_drc.dbo.drc_main`, `sb_drc.dbo.drc_status`, `sb_drc.dbo.drc_use`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 쓰기문 존재; 별칭·임시 객체 또는 동적 대상의 영향은 추가 확인 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchMembers](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/CreditorBalanceCertificateMapper.kt#L56) — 바인딩: `startDate`, `endDate`, `searchType`, `searchText`, `comType`, `statusCode`. 결과 매핑: `DRC_No` → `drcNo`, `Basic_Date` → `basicDate`, `Receivable_Balance` → `receivableBalance`, `creditor_com_regno` → `creditorComRegno`, `creditor_com_name` → `creditorComName`, `creditor_mem_name` → `creditorMemName`, `debtor_com_regno` → `debtorComRegno`, `debtor_com_name` → `debtorComName`, `debtor_mem_name` → `debtorMemName`, `Status_Code` → `statusLabel`, `Transfer_Status` → `transferStatusLabel`, `creditor_Bill_Type` → `creditorBillType`, `debtor_Bill_Type` → `debtorBillType`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

하위 프로시저·함수·뷰: `smartbill3.dbo.upadmsb_lst_drc_contract_comlst`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db328"></a>
## smartwork.dbo.UspDrcContractComLstNm

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@StartDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@EndDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SearchType` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SearchText` | `varchar(200)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Com_Type` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@Status_Code` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:46.147 |
| 읽기·참조 객체 | `sb_drc.dbo.drc_company_nm`, `sb_drc.dbo.drc_main`, `sb_drc.dbo.drc_status_nm`, `sb_drc.dbo.drc_use`, `smartbill3.dbo.company`, `smartbill3.dbo.member` |
| 쓰기 대상 | 쓰기문 존재; 별칭·임시 객체 또는 동적 대상의 영향은 추가 확인 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchNonMembers](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/CreditorBalanceCertificateMapper.kt#L79) — 바인딩: `startDate`, `endDate`, `searchType`, `searchText`, `comType`, `statusCode`. 결과 매핑: `DRC_No` → `drcNo`, `Basic_Date` → `basicDate`, `Receivable_Balance` → `receivableBalance`, `creditor_com_regno` → `creditorComRegno`, `creditor_com_name` → `creditorComName`, `creditor_mem_name` → `creditorMemName`, `debtor_com_regno` → `debtorComRegno`, `debtor_com_name` → `debtorComName`, `debtor_mem_name` → `debtorMemName`, `Status_Code` → `statusLabel`, `Transfer_Status` → `transferStatusLabel`, `creditor_Bill_Type` → `creditorBillType`, `debtor_Bill_Type` → `debtorBillType`.

### 필터·조인·정렬 규칙 (정의 발췌)

정적으로 발췌할 필터·정렬문 없음.

하위 프로시저·함수·뷰: `smartbill3.dbo.upadmsb_lst_drc_contract_comlst_nm`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db329"></a>
## smartwork.dbo.UspDrcHubErrorPortList

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@ROUTINGURL` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:46.217 |
| 읽기·참조 객체 | `sb_drc.dbo.drc_company_link` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findPortList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcHubErrorMapper.kt#L86) — 바인딩: `routingUrl`. 결과 매핑: `port` → `port`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE routingurl = @ROUTINGURL
GROUP BY port
ORDER BY port
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db330"></a>
## smartwork.dbo.UspDrcHubErrorRegDetail

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@ROUTINGURL` | `varchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@PORT` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:46.290 |
| 읽기·참조 객체 | `sb_drc.dbo.drc_routing_error_reg` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findDetail](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcHubErrorMapper.kt#L77) — 바인딩: `routingUrl`, `port`. 결과 매핑: `idx` → `idx`, `routingUrl` → `routingUrl`, `error_YN` → `errorYn`, `error_reg_date` → `errorRegDate`, `error_msg` → `errorMsg`, `sw_no` → `swNo`, `from_datetime` → `fromDatetime`, `to_datetime` → `toDatetime`, `port` → `port`, `sb_use_code` → `sbUseCode`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE routingurl = @ROUTINGURL
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db331"></a>
## smartwork.dbo.UspDrcLogConversationSearch

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@FindCondition` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ConversationId` | `varchar(36)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SchContent` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@StartDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@EndDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:46.370 |
| 읽기·참조 객체 | `sb_drc.dbo.drc_log` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchConversations](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcLogMapper.kt#L35) — 바인딩: `findCondition`, `conversationId`, `schContent`, `startDate`, `endDate`. 결과 매핑: `conversation_id` → `conversationId`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE conversation_id = @ConversationId
WHERE (SndIdentifier = @SchContent OR RcvIdentifier = @SchContent)
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db332"></a>
## smartwork.dbo.UspDrcLogEntryList

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@ConversationId` | `varchar(36)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:46.480 |
| 읽기·참조 객체 | `sb_drc.dbo.drc_log`, `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findLogEntries](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcLogMapper.kt#L53) — 바인딩: `conversationId`. 결과 매핑: `conversation_id` → `conversationId`, `SndIdentifier` → `sndIdentifier`, `SND_COM_NAME` → `sndComName`, `RcvIdentifier` → `rcvIdentifier`, `RCV_COM_NAME` → `rcvComName`, `Signal` → `signal`, `Transfer_Status` → `transferStatus`, `Error_Code` → `errorCode`, `Error_Description` → `errorDescription`, `Reg_Date` → `regDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE C.COM_REGNO = L.SndIdentifier
ORDER BY C.COM_NO
WHERE C.COM_REGNO = L.RcvIdentifier
ORDER BY C.COM_NO
WHERE L.conversation_id = @ConversationId
ORDER BY L.Reg_Date ASC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db333"></a>
## smartwork.dbo.UspDrcMemberList

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@ComNo` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:46.560 |
| 읽기·참조 객체 | `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findMembers](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/DrcRightMapper.kt#L72) — 바인딩: `comNo`. 결과 매핑: `MEM_NO` → `memNo`, `MEM_NAME` → `memName`, `MEM_REALNAME` → `memRealName`, `MEM_ID` → `memId`, `MEM_EMAIL` → `memEmail`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE A.COM_NO = @ComNo AND A.MEM_DEL_YN = 'N'
ORDER BY A.MEM_REALNAME
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db334"></a>
## smartwork.dbo.UspDrcMonitoringLogList

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@ConversationId` | `varchar(35)` | IN | NULL |
| `@LogIdx` | `int` | IN | 0 |
| `@ActionStatus` | `varchar(10)` | IN | NULL |
| `@TransferStatus` | `varchar(10)` | IN | NULL |
| `@DrcNo` | `int` | IN | 0 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:46.603 |
| 읽기·참조 객체 | `sb_drc.dbo.drc_log`, `sb_drc.dbo.drc_main` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [findLogs](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/bondservice/repository/ReceivableBalanceTransferMapper.kt#L104) — 바인딩: `conversationId`, `logIdx`, `actionStatus`, `transferStatus`, `drcNo`. 결과 매핑: `Log_Idx` → `logIdx`, `DRC_No` → `drcNo`, `Conversation_Id` → `conversationId`, `Message_Id` → `messageId`, `ServiceCode` → `serviceCode`, `SndSystemId` → `sndSystemId`, `SndIdentifier` → `sndIdentifier`, `RcvSystemId` → `rcvSystemId`, `RcvIdentifier` → `rcvIdentifier`, `Signal` → `signal`, `Action_Status` → `actionStatus`, `Transfer_Status` → `transferStatus`, `Header_Msg` → `headerMsg`, `Body_Msg` → `bodyMsg`, `Whole_Msg` → `wholeMsg`, `File_Path` → `filePath`, `Error_Code` → `errorCode`, `Error_Description` → `errorDescription`, `Reg_Date` → `regDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT JOIN SB_DRC..Drc_Main drcMain WITH(NOLOCK)
WHERE (@ConversationId IS NULL OR @ConversationId = '' OR drclog.Conversation_Id = @ConversationId)
ORDER BY drclog.Reg_Date DESC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db335"></a>
## smartwork.dbo.UspGlosignCompany_Select

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FromDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ToDate` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@strItem` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@strContents` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SortOrder` | `varchar(4)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-09-23T09:16:13.377 |
| 읽기·참조 객체 | `sec_pt.dbo.tbl_pt_org` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchCompanies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/company/repository/GlosignCompanyMapper.kt#L44) — 바인딩: `page`, `top`, `fromDate`, `toDate`, `strItem`, `strContents`, `sortOrder`. 결과 매핑: `ORG_SEQ` → `orgSeq`, `ORG_NM` → `orgNm`, `CN_ADR` → `cnAdr`, `ORG_REG_NO` → `orgRegNo`, `PRE_NM` → `preNm`, `CDATE` → `cdate`, `TOTAL_AMT` → `totalAmt`, `TOT_COUNT` → `totCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE 1 = 1
ORDER BY
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db336"></a>
## smartwork.dbo.UspGlosignCompanyUser_Select

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ORG_SEQ` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:46.710 |
| 읽기·참조 객체 | `sec_pt.dbo.tbl_pt_org_usr`, `sec_pt.dbo.tbl_pt_usr` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchCompanyUsers](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/company/repository/GlosignCompanyMapper.kt#L65) — 바인딩: `page`, `top`, `orgSeq`. 결과 매핑: `ORG_SEQ` → `orgSeq`, `USR_SEQ` → `usrSeq`, `USR_NM` → `usrNm`, `USR_EMAIL` → `usrEmail`, `CADM` → `cadm`, `ATV` → `atv`, `CDATE` → `cdate`, `TOT_COUNT` → `totCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT JOIN SEC_PT..TBL_PT_USR U WITH (NOLOCK) ON OU.USR_SEQ = U.USR_SEQ
WHERE OU.ORG_SEQ = @ORG_SEQ
ORDER BY OU.CDATE DESC
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db337"></a>
## smartwork.dbo.UspGlosignMember_Select

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FROMDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TODATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MITEM` | `varchar(80)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MTEXT` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MITEM2` | `varchar(80)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@MTEXT2` | `varchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SortOrder` | `varchar(4)` | IN | 'DESC' |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-09-23T09:16:21.070 |
| 읽기·참조 객체 | `sec_pt.dbo.tbl_pt_org`, `sec_pt.dbo.tbl_pt_org_usr`, `sec_pt.dbo.tbl_pt_usr` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchMembers](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/member/repository/GlosignMemberMapper.kt#L45) — 바인딩: `page`, `top`, `fromDate`, `toDate`, `companyItem`, `companyText`, `memberItem`, `memberText`, `sortOrder`. 결과 매핑: `USR_SEQ` → `usrSeq`, `USR_NM` → `usrNm`, `USR_ID` → `usrId`, `USR_CTR` → `usrCtr`, `USR_EMAIL` → `usrEmail`, `CN_ADR` → `cnAdr`, `CN_PUB` → `cnPub`, `ORG_NM` → `orgNm`, `ORG_REG_NO` → `orgRegNo`, `CDATE` → `cdate`, `TOT_COUNT` → `totCount`, `WITHDRAWAL_DATE` → `withdrawalDate`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT JOIN SEC_PT..TBL_PT_ORG_USR OU WITH (NOLOCK) ON U.USR_SEQ = OU.USR_SEQ
LEFT JOIN SEC_PT..TBL_PT_ORG O      WITH (NOLOCK) ON OU.ORG_SEQ = O.ORG_SEQ
WHERE 1 = 1
ORDER BY
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db338"></a>
## smartwork.dbo.UspGlosignMember_Withdraw

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@ORG_SEQ` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@USR_SEQ` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:46.880 |
| 읽기·참조 객체 | `sec_pt.dbo.tbl_pt_org_usr` |
| 쓰기 대상 | `sec_pt.dbo.tbl_pt_org_usr` |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [withdrawMember](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/glosign/company/repository/GlosignCompanyMapper.kt#L73) — 바인딩: `orgSeq`, `usrSeq`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
WHERE ORG_SEQ = @ORG_SEQ
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db339"></a>
## smartwork.dbo.UspMemberPermissions_Select

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@COM_NO` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:47.013 |
| 읽기·참조 객체 | `sb_dti.dbo.dept_admin`, `sb_dti.dbo.dept_member`, `sb_dti.dbo.dti_right`, `sb_dti.dbo.service_admin`, `smartbill3.dbo.member`, `smartwork.dbo.dct_member_right` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [getMemberPermissions](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/customer/company/repository/CompanyInfoDetailMapper.kt#L952) — 바인딩: `comNo`. 결과 매핑: `DIV` → `div`, `DEPT_NAME` → `deptName`, `MEM_NO` → `memNo`, `MEM_NAME` → `memName`, `MEM_REALNAME` → `memRealname`, `DEPT_NO` → `deptNo`, `COM_NO` → `comNo`, `MEM_ID` → `memId`, `MEM_EMAIL` → `memEmail`, `MEM_ENTRY_DATE` → `memEntryDate`, `RCV_YN` → `rcvYn`, `ISSUE_YN` → `issueYn`, `REQUEST_YN` → `requestYn`, `TOTALTABLE_YN` → `totaltableYn`, `ALLDTI_YN` → `alldtiYn`, `BDTI_SUP_RCV_YN` → `bdtiSupRcvYn`, `NTS_SEND_YN` → `ntsSendYn`, `DCT_CREATE_CONTRACT` → `dctCreateContract`, `DCT_DELETE_FILE` → `dctDeleteFile`, `DCT_VIEW_ALL_CONTRACTS` → `dctViewAllContracts`, `DCT_SIGN_FILE` → `dctSignFile`, `DCT_RECEIVE_CONTRACT` → `dctReceiveContract`, `DCT_VIEW_PURCHASE_CONFIRMATION` → `dctViewPurchaseConfirmation`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
LEFT OUTER JOIN (
FROM SB_DTI..SERVICE_ADMIN WHERE COM_NO = @COM_NO
FROM SB_DTI..DEPT_ADMIN WHERE COM_NO = @COM_NO
JOIN SB_DTI..DEPT_ADMIN DA ON DM.DEPT_NO = DA.DEPT_NO
WHERE DM.COM_NO = @COM_NO
LEFT OUTER JOIN SB_DTI..DTI_RIGHT DR ON M.MEM_NO = DR.MEM_NO
LEFT OUTER JOIN smartwork..DCT_MEMBER_RIGHT DCR ON M.MEM_NO = DCR.MEM_NO
WHERE M.COM_NO = @COM_NO
ORDER BY MEM_REALNAME
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db340"></a>
## smartwork.dbo.UspSelectDttSingleList

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@PAGE` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TOP` | `int` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DATE_TYPE` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@FMDATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TODATE` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SUP_INDEX` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@SUP_TEXT` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BYR_INDEX` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BYR_TEXT` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BRK_INDEX` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BRK_TEXT` | `varchar(70)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@REF_ID` | `varchar(35)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@STATUS` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@BYR_NAME` | `varchar(20)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@EVENT_RESULT` | `varchar(3)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@TAX_TYPES` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISSUANCE_DIRECTIONS` | `varchar(5)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISSUE_PATH` | `varchar(10)` | IN | '' |
| `@CREATED_DATE` | `varchar(10)` | IN | '' |
| `@ISSUE_ID` | `varchar(24)` | IN | '' |
| `@ARCHIVE_SOURCE` | `bit` | IN | 0 |
| `@TOTAL_COUNT` | `int` | IN/OUT | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-09-16T10:18:40.073 |
| 읽기·참조 객체 | `sb_dti_dw.sys.objects`, `sb_dti_dw.sys.schemas`, `sb_dti_dw.sys.tables`, `smartbill3.dbo.member` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchDttSingleList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/repository/TaxInvoiceMapper.kt#L149) — 바인딩: `page`, `top`, `dateType`, `fmDate`, `toDate`, `supIndex`, `supText`, `byrIndex`, `byrText`, `brkIndex`, `brkText`, `refId`, `status`, `byrName`, `eventResult`, `taxTypes`, `issuanceDirections`, `issuePath`, `createdDate`, `issueId`. 결과 매핑: `DTI_IDX` → `dtiIdx`, `DTI_WDAY` → `dtiWday`, `DTI_ISSUEDATE` → `dtiIssuedate`, `SUP_COM_REGNO` → `supComRegno`, `SUP_COM_NAME` → `supComName`, `BYR_COM_REGNO` → `byrComRegno`, `BYR_COM_NAME` → `byrComName`, `SUP_AMT` → `supAmt`, `DTI_STATUS` → `dtiStatus`, `BYR_TYPE` → `byrType`, `DIRECTION` → `direction`, `ETC_PCS_NO` → `etcPcsNo`, `SUP_MEM_NAME` → `supMemName`, `BYR_MEM_NAME` → `byrMemName`, `DTT_LINK_TYPE` → `dtiLinkType`, `AMEND_CODE` → `amendCode`, `NTS_SEND_STATUS` → `ntsSendStatus`, `DTI_TYPE` → `dtiType`, `TOT_COUNT` → `totCount`, `isVirtualYN` → `isVirtualYN`, `TAX_AMT` → `taxAmt`, `BILL_TYPE` → `billType`, `EVENT_NO` → `eventNo`, `DIV` → `div`, `NTS_RESULT_CODE` → `ntsResultCode`, `ISSUE_ID` → `issueId`, `BRK_DTI_YN` → `brkDtiYn`, `ISSUE_PATH` → `issuePath`.
- [searchStandaloneList](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/taxinvoice/legacytaxinvoice/repository/LegacyTaxInvoiceMapper.kt#L439) — 바인딩: `search.page`, `search.top`, `search.dateType`, `search.fmDate`, `search.toDate`, `search.supIndex`, `search.supText`, `search.byrIndex`, `search.byrText`, `search.brkIndex`, `search.brkText`, `search.refId`, `search.status`, `search.byrName`, `search.eventResult`, `search.taxTypes`, `search.issuanceDirections`, `search.issuePath`, `search.createdDate`, `search.issueId`, `totalCount, mode=OUT, jdbcType=INTEGER`. 결과 매핑: 명시 Result 매핑 없음; 반환 타입/VO 및 원천 정의 참조.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
IF @TAX_TYPES IS NULL SET @TAX_TYPES = '';
IF @ISSUANCE_DIRECTIONS IS NULL SET @ISSUANCE_DIRECTIONS = '';
SET @TAX_TYPES = CASE WHEN CHARINDEX('T', @TAX_TYPES)>0 THEN 'T' ELSE '' END
IF @TAX_TYPES = 'TPF' SET @TAX_TYPES = '';
SET @ISSUANCE_DIRECTIONS = CASE WHEN CHARINDEX('F', @ISSUANCE_DIRECTIONS)>0 THEN 'F' ELSE '' END
IF @ISSUANCE_DIRECTIONS = 'FR' SET @ISSUANCE_DIRECTIONS = '';
+ N' H WITH(NOLOCK) INNER JOIN SB_DTI_DW.dbo.'
JOIN SB_DTI_DW.sys.schemas S ON S.schema_id=T.schema_id
WHERE S.name='dbo'
ORDER BY T.name
SET @SOURCE=N'(' + @SOURCE + N') DM';
SET @BYR_TEXT# = [master].[dbo].[enc_index_char_sel_tc]('SSN', @BYR_TEXT, 'DTT_HEADER', 'BYR_COM_REGNO');
SET @BYR_TEXT# = NULL;
SET @TOTAL_COUNT = @TOT_COUNT;
SET @TOP2 = CASE WHEN CAST(@PAGE - 1 AS BIGINT) * @TOP >= @TOT_COUNT THEN 0 ELSE @TOT_COUNT - CAST(@PAGE - 1 AS BIGINT) * @TOP END;
SET @TOP2 = @TOP;
SET @SQL = N'
WHERE DM.DTI_IDX = -1 ';
```

하위 프로시저·함수·뷰: `master.dbo.clr_enc_index_tc`, `master.dbo.enc_index_char_sel_tc`, `sb_dti_dw.sys.objects`, `sb_dti_dw.sys.schemas`, `sb_dti_dw.sys.tables`, `smartwork.dbo.uspselectdttsinglelistcount`.

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db341"></a>
## smartwork.dbo.UspUnpaidException_CompanySearch_SELECT

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@SEARCH_TERM` | `nvarchar(100)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-08-04T17:17:48.327 |
| 읽기·참조 객체 | `smartbill3.dbo.company` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 조사한 정의에서 변수 기반 EXEC/sp_executesql 미검출 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchCompanies](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/status/payment/unpaidexception/repository/UnpaidExceptionMapper.kt#L58) — 바인딩: `searchTerm`. 결과 매핑: `COM_NO` → `comNo`, `COM_REGNO` → `comRegno`, `COM_NAME` → `comName`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @CLEANED_TERM = REPLACE(@SEARCH_TERM, '-', '');
WHERE C.COM_DEL_YN <> 'Y'
ORDER BY C.COM_NAME;
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.

<a id="db342"></a>
## smartwork.dbo.UspViewUseCompany

| 파라미터 | SQL 타입 | 방향 | 정의 기본값 |
|---|---|---|---|
| `@HUB_NAME` | `nvarchar(50)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@ISUSE` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DIVISION` | `varchar(10)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@CLASS` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@EMAILPARSING` | `char(1)` | IN | 선언 기본값 없음 또는 정의에서 미확정 |
| `@DB_TYPE` | `varchar(100)` | IN | '' |
| `@ERP_MISSING` | `char(1)` | IN | '' |
| `@CERT_MISSING` | `char(1)` | IN | '' |
| `@EXEC_INTERVAL` | `int` | IN | NULL |

| 항목 | 확인 내용 |
|---|---|
| 객체 유형·수정일 | SQL_STORED_PROCEDURE / 2026-09-22T11:18:01.667 |
| 읽기·참조 객체 | `office.dbo.sawon`, `sb_scraper.dbo.use_company_detail`, `sb_scraper.dbo.use_company_info` |
| 쓰기 대상 | 정적으로 확인한 테이블 쓰기 없음 |
| 동적 SQL | 있음. 정적으로 드러난 대상만 추적, 런타임 조합 대상은 DB 담당자 실행 환경 확인 필요 |
| RETURN 본문 | 명시적 RETURN 식 미검출 |

### Mapper 입출력 매핑

- [searchAuthKeys](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/backend/src/main/kotlin/com/bizon/smartwork/core/service/hometaxdti/esero/repository/AuthKeyMapper.kt#L61) — 바인딩: `hubName,jdbcType=NVARCHAR`, `useYn`, `division`, `klass`, `emailParsing`, `dbType`, `erpMissing`, `certMissing`, `execInterval,jdbcType=INTEGER`. 결과 매핑: `SB_KEY` → `sbKey`, `HUB_NAME` → `hubName`, `USE_YN` → `useYn`, `DIVISION` → `division`, `CDATE` → `cdate`, `HUB_REALNAME` → `hubRealname`, `CLASS` → `klass`, `OLD_NEW` → `oldNew`, `UNAME` → `uname`, `CNAME` → `cname`, `VERSION` → `version`, `DB_TYPE` → `dbType`, `SCHEDULER` → `scheduler`, `EXEC_INTERVAL` → `execInterval`, `ERP_SAP` → `erpSap`, `ERP_NONSAP` → `erpNonSap`, `DEPT_USER_ID` → `deptUserId`, `CERT_CNT` → `certCount`.

### 필터·조인·정렬 규칙 (정의 발췌)

아래는 개발 DB 본문에서 발췌한 규칙이다. 전체 분기와 계약은 Mapper·하위 객체 정의를 함께 확인한다.

```sql
SET @SQL = N'
LEFT OUTER JOIN (
GROUP BY SB_KEY
LEFT OUTER JOIN SB_SCRAPER..HOMETAX_AUTOLOG B WITH(NOLOCK) ON A.SB_KEY = B.SB_KEY
LEFT OUTER JOIN OFFICE..SAWON C WITH(NOLOCK) ON A.UUSER = C.SW_NO
LEFT OUTER JOIN OFFICE..SAWON D WITH(NOLOCK) ON A.CUSER = D.SW_NO
WHERE 1=1
SET @SQL = @SQL + N' AND A.HUB_REALNAME LIKE N''%'' + @PNAME + N''%'' ';
SET @SQL = @SQL + N' AND A.DIVISION = @PDIVISION ';
SET @SQL = @SQL + N' AND A.CLASS = @PCLASS ';
SET @SQL = @SQL + N' AND EP.ACTIVE_YN = @PEMAILPARSING ';
SET @SQL = @SQL + N' AND A.USE_YN = @PISUSE ';
SET @SQL = @SQL + N' AND B.DB = @PDBTYPE ';
SET @SQL = @SQL + N' AND B.COMREGNO_CNT <> B.SAP_CNT + B.NONSAP_CNT ';
SET @SQL = @SQL + N' AND B.COMREGNO_CNT = B.SAP_CNT + B.NONSAP_CNT ';
SET @SQL = @SQL + N' AND B.COMREGNO_CNT = 0 ';
SET @SQL = @SQL + N' AND B.COMREGNO_CNT > 0 ';
SET @SQL = @SQL + N' AND B.[interval] = @PINTERVAL ';
```

검증: 개발 DB 정의 확인, 2026-11-09. 고객 행·실행 결과·데모/스테이지/운영 적용은 미확인. 후속 확인: 해당 업무 기술 담당·DB 담당.
