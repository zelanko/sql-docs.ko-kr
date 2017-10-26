---
title: "SQLExecDirect 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLExecDirect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExecDirect
helpviewer_keywords:
- SQLExecDirect function [ODBC]
ms.assetid: 985fcee1-f204-425c-bdd1-deb0e7d7bbd9
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fdf6183eda2b66263a8ff27664d046640b94ea95
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlexecdirect-function"></a>SQLExecDirect 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLExecDirect** 문에 매개 변수가 있는 경우 매개 변수 표식 변수의 현재 값을 사용 하 여, 준비할 수 있는 문을 실행 합니다. **SQLExecDirect** 일회 실행에 대 한 SQL 문을 제출 하는 가장 빠른 방법은 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLExecDirect(  
     SQLHSTMT     StatementHandle,  
     SQLCHAR *    StatementText,  
     SQLINTEGER   TextLength);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *StatementText*  
 [입력] 실행할 SQL 문입니다.  
  
 *TextLength*  
 [입력] 길이 **StatementText* 문자 수입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_NO_DATA, SQL_INVALID_HANDLE, 또는 SQL_PARAM_DATA_AVAILABLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLExecDirect** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 관련된 된 SQLSTATE 값을 가져올 수 있습니다 **SQLGetDiagRec** 와 *HandleType* 여의 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLExecDirect** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01001|커서 작업이 충돌 합니다.|\**StatementText* 포함 한 위치 지정 업데이트 또는 delete 문의 및 둘 이상의 행 또는 행이 없는 업데이트 하거나 삭제 합니다. (둘 이상의 행에 대 한 업데이트에 대 한 자세한 내용은 참조는 SQL_ATTR_SIMULATE_CURSOR에 대 한 설명을 *특성* 에 **SQLSetStmtAttr**.)<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01003|Set 함수에서 제거 하는 NULL 값|인수 *StatementText* set 함수를 포함 (같은 **AVG**, **최대**, **MIN**등), 하지 않고는 **개수 ** 함수 및 값 함수를 적용 하기 전에 제거 된 NULL 인수를 설정 합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|문자열 또는 이진 데이터는 입/출력에 대 한 반환 또는 출력 매개 변수 공백이 아닌 문자 또는 NULL이 아닌 이진 데이터 잘림이 발생 했습니다. 문자열 값 경우 오른쪽 잘림 없었습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01006|권한이 취소 되지 않았습니다|\**StatementText* 포함 된 한 **해지** 문과 사용자 지정된 권한을 있지 않습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01007|권한이 부여 되지 않았습니다|*\*StatementText* 가 **GRANT** 문과 사용자 충족 시킬 수 없는 지정 된 권한입니다.|  
|01 S 02|옵션 값이 변경 됨|지정 된 문 특성 유사한 값에 일시적으로 대체 하므로 구현 작업 조건 때문에 잘못 되었습니다. (**SQLGetStmtAttr** 일시적으로 대체 값 결정 호출할 수 있습니다.) 대체 값이 적합는 *StatementHandle* 커서를 닫을 때까지 시점 문 특성 되돌아갑니다 이전 값입니다. 변경할 수 있는 문 특성은 합니다.<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ ATTR_SIMULATE_CURSOR<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S07|일부가 잘렸습니다.|입력/출력에 대해 반환 되는 데이터 또는 숫자 데이터 형식의 소수 부분이 잘린 있거나의 시간 구성 요소는 시간, 타임 스탬프 또는 간격 데이터 형식의 소수 부분이 잘린 되도록 출력 매개 변수 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07002|잘못 된 수 필드|에 지정 된 매개 변수 개수 **SQLBindParameter** 에 포함 된 SQL 문의 매개 변수 개수 보다 작습니다 \* *StatementText*합니다.<br /><br /> **SQLBindParameter** 로 호출 했습니다 *ParameterValuePtr* null 포인터를 설정 *StrLen_or_IndPtr* SQL_NULL_DATA 또는 SQL_DATA_AT_EXEC로 설정 하지 및 * InputOutputType* 에 지정 된 매개 변수 수 있도록 SQL_PARAM_OUTPUT,으로 설정 되지 **SQLBindParameter** 에 포함 된 SQL 문의 매개 변수 개수 보다 큰 **StatementText*합니다.|  
|07006|제한 된 데이터 형식 특성 위반|데이터 값으로 식별 된 *ValueType* 인수에 **SQLBindParameter** 바인딩된 매개 변수에서 식별 되는 데이터 형식 변환 하지 못했습니다에 대 한는 *ParameterType*인수 **SQLBindParameter**합니다.<br /><br /> SQL_PARAM_OUTPUT 또는 SQL_PARAM_INPUT_OUTPUT 하지 변환 못했습니다으로 식별 되는 데이터 형식으로 바인딩된 매개 변수에 대해 반환 되는 데이터 값의 *ValueType* 인수 **SQLBindParameter**합니다.<br /><br /> (하나 이상의 행에 대 한 데이터 값을 변환할 수 없는 하지만 성공적으로 반환 된 하나 이상의 행을이 함수 SQL_SUCCESS_WITH_INFO를 반환 합니다.)|  
|07007|제한 된 매개 변수 값 위반|부분에서 데이터를 송수신 하는 매개 변수의 매개 변수 형식 SQL_PARAM_INPUT_OUTPUT_STREAM만 사용 됩니다. 이 매개 변수 형식에 대해 바인딩된 입력된 버퍼를 허용 되지 않습니다.<br /><br /> 매개 변수 형식이 SQL_PARAM_INPUT_OUTPUT, 경우에이 오류가 발생 합니다는 \* *StrLen_or_IndPtr* 에 지정 된 **SQLBindParameter** SQL_NULL_DATA에 SQL_DEFAULT_과 같지 않은 PARAM, SQL_LEN_DATA_AT_EXEC(len), 또는 SQL_DATA_AT_EXEC입니다.|  
|07S01|기본 매개 변수를 잘못 사용 했습니다.|매개 변수 값을 사용 하 여 설정 **SQLBindParameter**SQL_DEFAULT_PARAM으로 되어 해당 매개 변수에 기본값이 없는 합니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|21S01|삽입 값 목록이 열 목록과 일치 하지 않습니다.|\**StatementText* 포함 된 프로그램 **삽입** 문과 개수 값을 삽입할 수 정도 파생된 테이블의 일치 하지 않습니다.|  
|21S02|파생된 테이블의 수준이 열 목록과 일치 하지 않습니다.|\**StatementText* 포함 한 **CREATE VIEW** 문과 정규화 되지 않은 열 목록 (의 뷰에 대 한 지정 된 열 수는 *열 식별자* SQL의 인수 문)에 의해 정의 된 파생된 테이블의 열 개수 보다 많은 이름이 포함 된는 *쿼리 사양* SQL 문의 인수입니다.|  
|22001|문자열 데이터, 오른쪽이 잘렸습니다.|문자 또는 이진 열 값을 할당 공백이 아닌 문자 데이터 또는 null이 아닌 이진 데이터의 잘림은 발생 했습니다.|  
|22002|지표 변수가 필요 하지만 제공 되지 않았습니다.|NULL 데이터를 출력 매개 변수로 바인딩된 인 *StrLen_or_IndPtr* 설정한 **SQLBindParameter** 는 null 포인터입니다.|  
|22003|숫자 값 범위를 벗어났습니다.|**StatementText* 바운드 숫자 매개 변수 또는 리터럴, 포함 하는 SQL 문을 포함 한 값 (소수) 대비 전체 부분은 연결 된 테이블 열에 할당 된 경우 잘릴 수 있습니다.<br /><br /> 하나 이상의 입/출력 또는 출력 매개 변수 (숫자 또는 문자열)으로 숫자 값을 반환는 발생할 (소수) 대비 전체 부분의 잘릴 수 있습니다.|  
|22007|잘못 된 날짜/시간 형식|**StatementText* 매개 변수를 각각는 잘못 된 날짜, 시간 또는 타임 스탬프 및 날짜, 시간 또는 타임 스탬프 구조는 바인딩된 매개 변수를 포함 하는 SQL 문을 포함 합니다.<br /><br /> 날짜, 시간 또는 타임 스탬프 C 구조에는 입/출력 또는 출력 매개 변수가 바인딩된 되었으며 반환 된 매개 변수 값을 각각는 잘못 된 날짜, 시간 또는 타임 스탬프. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|22008|Datetime 필드 오버플로|**StatementText* 포함는 날짜/시간 식, 계산, 날짜, 발생 하는 경우 시간 또는 타임 스탬프 구조를 포함 하는 SQL 문을 사용할 수 없습니다.<br /><br /> 입력/출력에 대해 계산 된 datetime 식 또는 출력 매개 변수는 날짜, 시간 또는 유효 하지 않는 C 타임 스탬프 구조에서 발생 했습니다.|  
|22012|0으로 나누기|**StatementText* 0으로 나누기 발생 하는 산술 식을 포함 하는 SQL 문을 포함 합니다.<br /><br /> 산술 식 입력/출력에 대 한 계산 또는 0으로 나누기에서 발생 한 출력 매개 변수입니다.|  
|22015|간격 필드 오버플로|*\*StatementText* 정확한 숫자 또는 간격 매개 변수를 포함 하는, 했기 때문에 유효 자릿수의 손실 간격 SQL 데이터 형식으로 변환 합니다.<br /><br /> *\*StatementText* 둘 이상의 필드와 간격 매개 변수는 포함 된 열에 숫자 데이터 형식으로 변환 될 때 숫자 데이터 형식으로 표시 되지 입력과, 합니다.<br /><br /> *\*StatementText* 간격 SQL 형식에 할당 된 매개 변수 데이터를 포함 하 고 간격 SQL 형식에서에서 C 형식의 값의 표시가 없을 했습니다.<br /><br /> 정확한 수치 또는 간격 했기 때문에 유효 자릿수의 손실 C 간격 유형 SQL 형식과 입/출력 또는 출력 매개 변수를 할당 합니다.<br /><br /> 입/출력 또는 출력 매개 변수는이 간격 C 구조에 할당 된 간격 데이터 구조에서 데이터의 표시가 없을 했습니다.|  
|22018|캐스트 사양의 문자 값|*\*StatementText* C 형식을 포함 하 고 정확한 수 또는 대략적인 숫자, datetime, 나 간격 데이터 유형을; 열의 SQL 형식을 문자 데이터 형식 되어 값 열에 바인딩된 C 형식의 올바른 리터럴 수 없습니다.<br /><br /> 입/출력 또는 출력 매개 변수는 반환 된 SQL 형식을 정확한 수 또는 대략적인 숫자, datetime, 또는 간격 데이터 형식입니다. 가 SQL_C_CHAR; C 유형은 고 값 열에 바인딩된 SQL 형식의 올바른 리터럴 수 없습니다.|  
|22019|잘못 된 이스케이프 문자|\**StatementText* 포함 하는 SQL 문을 포함 한 **같은** 조건자와 함께 **이스케이프** 에 **여기서** 절과 이스케이프의 길이 문자 다음 **이스케이프** 1과 같을 수 없습니다.|  
|22025|잘못 된 이스케이프 시퀀스|\**StatementText* 포함 하는 SQL 문을 포함 된 "**같은** *패턴 값* **이스케이프** *이스케이프 문자*"에 **여기서** 절 및 패턴 값의 이스케이프 문자 뒤의 문자 없습니다"%"또는"_"중 하나입니다.|  
|23000|무결성 제약 조건 위반|**StatementText* 매개 변수 또는 리터럴을 포함 하는 SQL 문을 포함 합니다. 매개 변수 값은 연결 된 테이블 열에 NOT NULL로 정의 된 열에 대 한 NULL 이었습니다, 그리고을 고유 값만 포함 하도록 제한 하는 열에 대 한 중복 값이 제공 되었습니다 또는 일부 다른 무결성 제약 조건을 위반 했습니다.|  
|24000|잘못된 커서 상태|에 커서가 있었기는 *StatementHandle* 여 **SQLFetch** 또는 **SQLFetchScroll**합니다. 이 오류는 경우 드라이버 관리자에서 반환 됩니다 **SQLFetch** 또는 **SQLFetchScroll** 에서 SQL_NO_DATA를 반환 되지 않은 경우 드라이버에서 반환 되 고 **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA를 반환 했습니다.<br /><br /> 커서가 없습니다에 배치 되어 있지만 열린는 *StatementHandle*합니다.<br /><br /> **StatementText* 는 위치 지정 업데이트 또는 delete 문의 결과 집합의 또는 결과 집합의 끝 이후에 시작 되기 전에 커서가 있었기 하 고 포함 합니다.|  
|34000|잘못된 커서 이름|**StatementText* 는 위치 지정 업데이트 또는 delete 문의 하 고 실행 중인 문에 의해 참조 되는 커서가 열려 있었던 포함 합니다.|  
|3D000|잘못 된 카탈로그 이름|에 지정 된 카탈로그 이름을 *StatementText* 올바르지 않습니다.|  
|3F000|잘못 된 스키마 이름|지정 된 스키마 이름이 *StatementText* 올바르지 않습니다.|  
|40001|Serialization 오류|트랜잭션이 다른 트랜잭션 사용 하 여 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 실패 및 트랜잭션의 상태를 확인할 수 없습니다.|  
|42000|구문 오류 또는 액세스 위반|\**StatementText* 준비할 수 있는 되었거나 구문 오류를 포함 하는 SQL 문을 포함 합니다.<br /><br /> 사용자에 포함 된 SQL 문을 실행할 수 있는 권한이 없는 **StatementText*합니다.|  
|42S01|기본 테이블 또는 뷰가 이미 있습니다.|\**StatementText* 포함 한 **CREATE TABLE** 또는 **CREATE VIEW** 문 및 테이블 이름 또는 뷰 이름이 이미 지정 되어 있습니다.|  
|42S02|기본 테이블 또는 뷰를 찾을 수 없음|\**StatementText* 포함 한 **DROP TABLE** 또는 **DROP VIEW** 문 지정한 테이블 이름 또는 뷰 이름이 존재 하지 않습니다.<br /><br /> \**StatementText* 포함 된 프로그램 **ALTER TABLE** 문과 지정한 테이블 이름 존재 하지 않습니다.<br /><br /> \**StatementText* 포함 한 **CREATE VIEW** 문 및 테이블 이름 또는 뷰를 쿼리 사양에 정의 된 이름이 존재 하지 않습니다.<br /><br /> \**StatementText* 포함 한 **CREATE INDEX** 문과 지정한 테이블 이름 존재 하지 않습니다.<br /><br /> \**StatementText* 포함 된 한 **GRANT** 또는 **해지** 문 지정한 테이블 이름 또는 뷰 이름이 존재 하지 않습니다.<br /><br /> \**StatementText* 포함 한 **선택** 문에서 지정한 테이블 이름 또는 뷰 이름이 존재 하지 않습니다.<br /><br /> \**StatementText* 포함 한 **삭제**, **삽입**, 또는 **업데이트** 문과 지정한 테이블 이름 존재 하지 않습니다.<br /><br /> \**StatementText* 포함 한 **CREATE TABLE** 문과 (참조 테이블 이외의 생성 되 고) 제약 조건에 지정 된 테이블이 존재 하지 않습니다.<br /><br /> \**StatementText* 포함 한 **CREATE SCHEMA** 문에서 지정한 테이블 이름 또는 뷰 이름이 존재 하지 않습니다.|  
|42S11|인덱스가 이미 있습니다.|\**StatementText* 포함 한 **CREATE INDEX** 문과 지정 된 인덱스 이름이 이미 존재 합니다.<br /><br /> \**StatementText* 포함 한 **CREATE SCHEMA** 문과 지정 된 인덱스 이름이 이미 존재 합니다.|  
|42S12|인덱스를 찾을 수 없음|\**StatementText* 포함 한 **DROP INDEX** 문과 지정 된 인덱스 이름이 존재 하지 않습니다.|  
|42S21|열이 이미 있습니다.|\**StatementText* 포함 된 프로그램 **ALTER TABLE** 문과에 지정 된 열은 **추가** 절 고유 하지 않거나 기본 테이블의 기존 열을 식별 합니다.|  
|42S22|열이 없습니다|\**StatementText* 포함 한 **CREATE INDEX** 문, 하나 이상의 열 목록에 지정 된 이름이 없습니다. 열입니다.<br /><br /> \**StatementText* 포함 된 한 **GRANT** 또는 **해지** 문과 지정한 열 이름이 존재 하지 않습니다.<br /><br /> \**StatementText* 포함 한 **선택**, **삭제**, **삽입**, 또는 **업데이트** 문 및 지정된 된 열 이름이 존재 하지 않습니다.<br /><br /> \**StatementText* 포함 한 **CREATE TABLE** 문과 (참조 테이블 이외의 생성 되 고) 제약 조건에 지정 된 열이 없는 것입니다.<br /><br /> \**StatementText* 포함 한 **CREATE SCHEMA** 문과 지정한 열 이름이 존재 하지 않습니다.|  
|44000|WITH CHECK OPTION 위반|인수 *StatementText* 포함 된 프로그램 **삽입** 표시 된 테이블에서 수행 하는 문 또는 지정 하 여 만든 본된 테이블에서 파생 된 테이블 **WITH CHECK OPTION**는 영향을 받는 하나 이상의 행에서 **삽입** 문이 더 이상 표시 테이블에 표시 됩니다.<br /><br /> 인수 *StatementText* 포함 된 프로그램 **업데이트** 표시 된 테이블에서 수행 하는 문 또는 지정 하 여 만든 본된 테이블에서 파생 된 테이블 **WITH CHECK OPTION**는 영향을 받는 하나 이상의 행에서 **업데이트** 문이 더 이상 표시 테이블에 표시 됩니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에 * \*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *StatementHandle*합니다. 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle*합니다. 함수에서 다시 호출 된 후의 *StatementHandle*합니다.<br /><br /> 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle* 의 서로 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|(DM) **StatementText* 는 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 비동기 함수 계속 실행 될 때는 **SQLExecDirect** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대 한 호출 된는 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서 * StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 인수 *TextLength* 가 보다 작거나 같으면 0 하지만 SQL_NTS 같지는있지 않습니다.<br /><br /> 매개 변수 값을 사용 하 여 설정 **SQLBindParameter**가 null 포인터, 및 매개 변수 길이 값이 0, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM으로 또는 SQL_LEN_DATA_AT_EXEC_OFFSET 합니다.<br /><br /> 매개 변수 값을 사용 하 여 설정 **SQLBindParameter**,이 null 포인터 하지 않으면 C 데이터 형식 SQL_C_BINARY 되었거나 SQL_C_CHAR; 및 매개 변수 길이 값이 0 보다 작지 않음 SQL_NTS, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_ 없습니다 PARAM 또는 SQL_LEN_DATA_AT_EXEC_OFFSET 합니다.<br /><br /> 매개 변수 길이 값을 읽었으며 **SQLBindParameter** ; SQL_DATA_AT_EXEC로 설정 했습니다; SQL 유형이 SQL_LONGVARCHAR, SQL_LONGVARBINARY, 또는 long 데이터 원본에 따른 특정 데이터 형식 및 SQL_NEED_LONG_DATA_LEN 정보 에 입력 **SQLGetInfo** "Y"가 있습니다.|  
|HY105|잘못 된 매개 변수 형식|인수에 대해 지정 된 값 *InputOutputType* 에 **SQLBindParameter** SQL_PARAM_OUTPUT, 이며 매개 변수는 입력된 매개 변수입니다.|  
|HY109|잘못 된 커서 위치|\**StatementText* 에 커서가 있었기 및에 위치 지정 업데이트 또는 삭제 문의 포함 된 (여 **SQLSetPos** 또는 **SQLFetchScroll**)에서 삭제 되거나 수 없는 행을 인출 합니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|SQL_ATTR_CURSOR_TYPE 및 SQL_ATTR_CONCURRENCY 문 특성의 현재 설정의 조합 드라이버 또는 데이터 원본에서 지원 되지 않았습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE로 설정 된 및 SQL_ATTR_CURSOR_TYPE 문 특성 드라이버 책갈피에 지원 하지 않으면 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|쿼리 제한 시간에는 데이터 원본의 결과 집합을 반환 하기 전에 만료 되었습니다. 제한 시간을 통해 설정 됩니다 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT 합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>설명  
 응용 프로그램 호출 **SQLExecDirect** 데이터 원본에는 SQL 문을 보내야 합니다. 직접 실행 하는 방법에 대 한 자세한 내용은 참조 [직접 실행](../../../odbc/reference/develop-app/direct-execution-odbc.md)합니다. 드라이버 문을 수정 하 여 데이터 원본에서 사용 하는 SQL 형식을 사용 하 고 데이터 원본에 전달 합니다. 특히, 드라이버는 SQL의 특정 기능을 정의 하는 데 이스케이프 시퀀스를 수정 합니다. 이스케이프 시퀀스의 구문에 대 한 참조 [odbc에서 이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)합니다.  
  
 응용 프로그램은 SQL 문에서 하나 이상의 매개 변수 표식을 포함할 수 있습니다. 응용 프로그램 매개 변수 표식에 포함 하려면 적절 한 위치에서 SQL 문을에 물음표 (?)를 포함 시킵니다. 매개 변수에 대 한 정보를 참조 하십시오. [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)합니다.  
  
 SQL 문이 **선택** 문과 응용 프로그램이 호출 하는 경우 **SQLSetCursorName** 커서를 문으로 연결 하려면 다음 드라이버 사용 하 여 지정된 된 커서입니다. 그렇지 않은 경우 드라이버는 커서 이름을 생성합니다.  
  
 수동 커밋 모드 (명시적 트랜잭션 시작 필요)에서 데이터 원본이 고 트랜잭션이 이미 시작 되지 않았습니다, 드라이버 SQL 문을 보내기 전에 트랜잭션을 시작 합니다. 자세한 내용은 참조 [수동 커밋 모드](../../../odbc/reference/develop-app/manual-commit-mode.md)합니다.  
  
 응용 프로그램에서 사용 **SQLExecDirect** 제출 하는 **커밋** 또는 **롤백** 문, 되지 않는 DBMS 제품 간의 상호 운용 가능 합니다. 응용 프로그램이 호출 커밋하거나 트랜잭션을 롤백하려면 **SQLEndTran**합니다.  
  
 경우 **SQLExecDirect** 실행 시 데이터 매개 변수를 발견할 SQL_NEED_DATA를 반환 합니다. 사용 하 여 데이터를 보낼 **SQLParamData** 및 **SQLPutData**합니다. 참조 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), 및 [긴 데이터를 보내는](../../../odbc/reference/develop-app/sending-long-data.md)합니다.  
  
 경우 **SQLExecDirect** 검색 결과 업데이트, 삽입 또는 데이터 원본에 대 한 호출에서 모든 행에 영향을 미치지 않는 delete 문을 실행 **SQLExecDirect** SQL_NO_DATA를 반환 합니다.  
  
 SQL_ATTR_PARAMSET_SIZE 문 특성의 값이 1 보다 큰 경우 SQL 문에 하나 이상의 매개 변수 표식에 포함 된 **SQLExecDirect** 각 집합에서 매개 변수 값에 대해 한 번 SQL 문을 실행 합니다 배열에서 가리키는 *ParameterValuePointer* 호출에 인수 **SQLBindParameter**합니다. 자세한 내용은 참조 [매개 변수 값의 배열](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)합니다.  
  
 책갈피 사용 하 고 쿼리를 실행 하는 경우를 책갈피를 지원할 수 없습니다, 드라이버를 특성 값을 변경 하 고 SQLSTATE 01 s 02를 반환 하 여 책갈피를 지 원하는 지 환경 강제 하려고 해야 (옵션 값이 변경 됨). 드라이버 SQLSTATE HY024 반환할지 특성을 변경할 수 없는 경우 (잘못 된 특성 값).  
  
> [!NOTE]  
>  응용 프로그램 연결 풀링을 사용 하는 경우와 같은 데이터베이스 또는 데이터베이스의 컨텍스트를 변경 하는 SQL 문을 실행 해서는 안 된 **사용** *데이터베이스* 변경 하는 SQL Server에서 문 데이터 원본에서 사용 하는 카탈로그입니다.  
  
## <a name="code-example"></a>코드 예  
 참조 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md), 및 [ODBC 프로그램 샘플](../../../odbc/reference/sample-odbc-program.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|커밋 또는 롤백 작업 실행|[SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|여러 데이터 행을 인출합니다.|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록을 인출 또는 스크롤 하는 결과 집합|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|커서 이름 반환|[SQLGetCursorName 함수](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|일부 또는 전체 데이터 열을 인출합니다.|[SQLGetData 함수](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|에 대 한 데이터를 보내는 다음 매개 변수를 반환 합니다.|[SQLParamData 함수](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|실행할 문을 준비합니다.|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|실행 시 매개 변수 데이터 보내기|[SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|커서 이름 설정|[SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

