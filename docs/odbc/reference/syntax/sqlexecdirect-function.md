---
title: SQLExecDirect 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a1c66c9ab423a6bb722c422450b99c1a47118f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537194"
---
# <a name="sqlexecdirect-function"></a>SQLExecDirect 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLExecDirect** 문에 매개 변수가 있으면 매개 변수 표식 변수의 현재 값을 사용 하 여 preparable 문을 실행 합니다. **SQLExecDirect** 일회 실행에 대 한 SQL 문을 제출 하는 가장 빠른 방법은 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
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
 [입력] 길이 **StatementText* 문자에서입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_NO_DATA, SQL_INVALID_HANDLE, 또는 SQL_PARAM_DATA_AVAILABLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLExecDirect** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 연관된 된 SQLSTATE 값을 가져올 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* 호출 및 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLExecDirect** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01001|커서 작업이 충돌 합니다.|\**StatementText* 포함을 위치 지정 update 또는 delete 문, 및 둘 이상의 행 또는 행이 없는 업데이트 하거나 삭제 합니다. (둘 이상의 행에 대 한 업데이트에 대 한 자세한 내용은 참조는 SQL_ATTR_SIMULATE_CURSOR에 대 한 설명을 *특성* 에 **SQLSetStmtAttr**.)<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01003|Set 함수에서 제거 하는 NULL 값|인수 *StatementText* set 함수를 포함 (같은 **AVG**, **최대**, **MIN**등), 있지만 **수**  함수 및 값 함수를 적용 하기 전에 제거 된 NULL 인수를 설정 합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|공백이 아닌 문자 또는 NULL이 아닌 이진 데이터 잘림이 발생 한 출력 매개 변수 또는 입력/출력에 대 한 문자열 또는 이진 데이터 반환. 문자열 값이 오른쪽 잘림 이었습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01006|권한이 취소 되지 않았습니다|\**StatementText* 포함 된를 **해지** 문 및 사용자 지정된 권한을 있지 않았습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01007|권한이 부여 되지 않았습니다|*\*StatementText* 된를 **부여** 문과 사용자 부여할 수 없습니다 지정 된 권한입니다.|  
|01S02|옵션 값이 변경 됨|지정 된 문 특성을 일시적으로 유사한 값에 대체 되므로 구현 작업 조건으로 인해 잘못 되었습니다. (**SQLGetStmtAttr** 일시적으로 대체 값 결정 호출할 수 있습니다.) 대체 값이 적합 합니다 *StatementHandle* 커서를 닫을 때까지 시점에서 문 특성 값으로 되돌리는 경우 해당 이전 합니다. 변경할 수 있는 문 특성은 다음과 같습니다.<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT  SQL_ ATTR_SIMULATE_CURSOR<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S07|소수 잘림|입/출력에 대 한 데이터를 반환 하거나 출력 매개 변수는 숫자 데이터 형식의 소수 부분이 잘린 또는 시간 구성 요소는 시간, 타임 스탬프 또는 간격 데이터 형식의 소수 부분이 잘린 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07002|COUNT 필드가 잘못 되었습니다|지정 된 매개 변수 수가 **SQLBindParameter** 에 포함 된 SQL 문의 매개 변수 개수 보다 작다고 \* *StatementText*합니다.<br /><br /> **SQLBindParameter** 사용 하 여 호출한 *ParameterValuePtr* null 포인터로 설정 *StrLen_or_IndPtr* SQL_NULL_DATA 또는 SQL_DATA_AT_EXEC로 설정 되지 않은 및 *InputOutputType*  에 지정 된 매개 변수의 수 있도록 SQL_PARAM_OUTPUT로 설정 되지 않습니다 **SQLBindParameter** 에 포함 된 SQL 문의 매개 변수 개수 보다 **StatementText* .|  
|07006|제한 된 데이터 형식 특성을 위반 했습니다.|로 식별 된 데이터 값을 *ValueType* 에서 인수 **SQLBindParameter** 바인딩된 매개 변수에서 식별 되는 데이터 형식 변환 하지 못했습니다에 대 한는 *ParameterType*에 인수 **SQLBindParameter**합니다.<br /><br /> SQL_PARAM_OUTPUT 또는 SQL_PARAM_INPUT_OUTPUT 수 변환할 없습니다으로 식별 되는 데이터 형식으로 바인딩된 매개 변수에 대해 반환 되는 데이터 값을 *ValueType* 에서 인수 **SQLBindParameter**합니다.<br /><br /> (하나 이상의 행에 대 한 데이터 값을 변환할 수 없습니다. 하나 이상의 행이 성공적으로 반환 하지만이 함수 SQL_SUCCESS_WITH_INFO를 반환 합니다.)|  
|07007|제한 된 매개 변수 값 위반|부분에서 데이터를 송수신 하는 매개 변수의 매개 변수 형식이 SQL_PARAM_INPUT_OUTPUT_STREAM만 사용 됩니다. 이 매개 변수 형식에 대해 바인딩된 입력된 버퍼 허용 되지 않습니다.<br /><br /> 매개 변수 유형이 SQL_PARAM_INPUT_OUTPUT, 시간과 때이 오류가 발생 합니다 \* *StrLen_or_IndPtr* 에 지정 된 **SQLBindParameter** SQL_DEFAULT_은 모두 SQL_NULL_DATA로 같지 않은 매개 변수, SQL_LEN_DATA_AT_EXEC(len), 또는 SQL_DATA_AT_EXEC입니다.|  
|07S01|기본 매개 변수를 잘못 사용 했습니다.|매개 변수 값을 사용 하 여 설정할 **SQLBindParameter**SQL_DEFAULT_PARAM으로 되었으며 해당 매개 변수에 기본값이 없습니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|21S01|삽입 값 목록이 열 목록과 일치 하지 않습니다.|\**StatementText* 포함 된 **삽입** 문과 값을 삽입할 수는 파생된 테이블의 정도 일치 하지 않습니다.|  
|21S02|파생된 테이블의 단계가 열 목록과 일치 하지 않습니다.|\**StatementText* 포함 된를 **CREATE VIEW** 문과 정규화 되지 않은 열 목록 (의 뷰에 대 한 지정 된 열의 수는 *열 식별자* SQL의 인수 문)으로 정의 하는 파생된 테이블의 열 수보다 더 많은 이름을 포함 합니다 *쿼리 사양* SQL 문의 인수입니다.|  
|22001|문자열 데이터, 오른쪽이 잘렸습니다.|공백이 아닌 문자 데이터 또는 null이 아닌 이진 데이터의 잘림 문자나 이진 열 값을 할당이 했습니다.|  
|22002|지표 변수가 필요 하지만 제공 되지|출력 매개 변수에 NULL 데이터 바인딩된입니다 *StrLen_or_IndPtr* 설정한 **SQLBindParameter** 가 null 포인터입니다.|  
|22003|숫자 값 범위를 벗어났습니다.|**StatementText* 바인딩된 숫자 매개 변수 또는 리터럴, 포함 된 SQL 문을 포함 하 고 값 (소수) 대신 전체 부분을 잘릴 숫자를 연결 된 테이블 열에 할당 된 경우 발생 합니다.<br /><br /> 하나 이상의 입/출력 또는 출력 매개 변수의 숫자 값 (숫자 또는 문자열)으로 반환 되 었어야 하지만 (소수) 대신 전체 부분 숫자를 자를 수입니다.|  
|22007|잘못 된 날짜/시간 형식|**StatementText* 매개 변수를 각각는 잘못 된 날짜, 시간 또는 타임 스탬프 및 날짜, 시간 또는 바인딩된 매개 변수로 타임 스탬프 구조를 포함 하는 SQL 문을 포함 합니다.<br /><br /> 입/출력 또는 출력 매개 변수를 날짜, 시간 또는 타임 스탬프 C 구조에 바인딩 되었습니다 및 반환된 매개 변수 값을 각각는 잘못 된 날짜, 시간 또는 타임 스탬프입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|22008|Datetime 필드 오버플로|**StatementText* 올바르지 않아는 발생 한 날짜를 계산 하는 경우 시간 또는 타임 스탬프 구조체는 날짜/시간 식이 포함 된 SQL 문을 포함 합니다.<br /><br /> 입/출력에 대해 계산 된 datetime 식 또는 출력 매개 변수는 날짜, 시간 또는 타임 스탬프 C 구조에 잘못 된 발생 합니다.|  
|22012|0으로 나누기|**StatementText* 0으로 나누기를 발생 시킨 산술 식을 포함 하는 SQL 문을 포함 합니다.<br /><br /> 입/출력에 대 한 계산 된 산술 식 또는 출력 매개 변수가 0으로 나누기 했습니다.|  
|22015|간격 필드 오버플로|*\*StatementText* 정확한 숫자 또는 간격 매개 변수를 포함 하는, 했기 때문에 유효 자릿수의 손실 간격 SQL 데이터 형식으로 변환 하는 경우.<br /><br /> *\*StatementText* 둘 이상의 필드를 사용 하 여 간격 매개 변수는 포함 된 열에서 숫자 데이터 형식으로 변환 하는 경우 숫자 데이터 형식에서으로 표시 되지 했습니다는 합니다.<br /><br /> *\*StatementText* 간격 SQL 형식에 할당 된 매개 변수 데이터를 포함 했는데 간격 SQL 형식 표현 방식이 없기 C 형식의 값입니다.<br /><br /> 정확한 수치 또는 간격 했기 때문에 유효 자릿수의 손실 C 간격 유형 SQL 형식은 입/출력 또는 출력 매개 변수를 할당 합니다.<br /><br /> 입/출력 또는 출력 매개 변수를 C 간격 구조에 할당 된 경우 간격 데이터 구조의 데이터를에서 표현 방식이 없기 있었습니다.|  
|22018|캐스트 사양의 문자 값|*\*StatementText* C 형식을 포함 하는 정확 하거나 대략적인 숫자, datetime, 또는 간격 데이터 형식 된; 열의 SQL 형식을 문자 데이터 형식으로 되어 열의 값이 바인딩된 C 형식의 유효한 리터럴이 됩니다.<br /><br /> 입/출력 또는 출력 매개 변수를 반환 하는 경우 SQL 형식 되었거나는 정확 하거나 대략적인 숫자, 날짜/시간을를 간격 데이터 형식 C 형식을 SQL_C_CHAR; 및 값 열에 바인딩된 SQL 형식의 올바른 리터럴 없습니다.|  
|22019|잘못 된 이스케이프 문자|\**StatementText* 포함 된 SQL 문을 포함할를 **와 같은** 조건자와 함께 **이스케이프** 에 **여기서** 절과 이스케이프의 길이 다음 문자 **이스케이프** 1 없습니다.|  
|22025|잘못 된 이스케이프 시퀀스|\**StatementText* 포함 된 SQL 문을 포함 된 "**와 같은** _패턴 값_ **이스케이프** _이스케이프 문자_ "에 **여기서** 절 및 패턴 값의 이스케이프 문자 뒤의 문자 중 하나가 아니었습니다"%"또는"_"합니다.|  
|23000|무결성 제약 조건 위반|**StatementText* 리터럴 또는 매개 변수를 포함 하는 SQL 문을 포함 합니다. 매개 변수 값을 NULL 연결 된 테이블 열에 NOT NULL로 정의 된 열에 대 한, 중복 된 값을 고유한 값만 포함 하도록 제한 열에 대해 제공한 되었거나 일부 다른 무결성 제약 조건을 위반 했습니다.|  
|24000|잘못된 커서 상태|에 커서가 있었기 합니다 *StatementHandle* 하 여 **SQLFetch** 하거나 **SQLFetchScroll**합니다. 이 오류는 경우 드라이버 관리자에 의해 반환 됩니다 **SQLFetch** 하거나 **SQLFetchScroll** 에서 SQL_NO_DATA를 반환 하지 않은 한 경우 드라이버에서 반환 됩니다 **SQLFetch** 또는**SQLFetchScroll** SQL_NO_DATA를 반환 했습니다.<br /><br /> 커서를 배치 하지 않습니다 하지만 열려 있었던 합니다 *StatementHandle*합니다.<br /><br /> **StatementText* 시작 결과 집합 또는 결과 집합의 끝 뒤에 커서가 있었기를 위치 지정 update 또는 delete 문, 및에 포함 합니다.|  
|34000|잘못된 커서 이름|**StatementText* 실행 중인 문에 의해 참조 되는 커서가 열리지 않았습니다.는 현재 위치 update 또는 delete 문, 및에 포함 합니다.|  
|3D000|잘못 된 카탈로그 이름|에 지정 된 카탈로그 이름을 *StatementText* 올바르지 않습니다.|  
|3F000|잘못 된 스키마 이름|에 지정 된 스키마 이름이 *StatementText* 올바르지 않습니다.|  
|40001|Serialization 오류|트랜잭션은 다른 트랜잭션과 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 하지 못했으며 트랜잭션의 상태를 확인할 수 없습니다.|  
|42000|구문 오류 또는 액세스 위반|\**StatementText* preparable 되었거나 구문 오류가 포함 된 SQL 문을 포함 합니다.<br /><br /> 사용자에 포함 된 SQL 문을 실행할 수 있는 권한이 없는 **StatementText*합니다.|  
|42S01|기본 테이블 또는 뷰가 이미 있습니다.|\**StatementText* 포함 된를 **CREATE TABLE** 하거나 **CREATE VIEW** 문 및 테이블 이름 또는 뷰 이름이 이미 지정 되어 있습니다.|  
|42S02|기본 테이블 또는 뷰를 찾을 수 없음|\**StatementText* 포함 된를 **DROP TABLE** 또는 **DROP VIEW** 문 및 지정한 테이블 이름 또는 뷰 이름이 존재 하지 않았습니다.<br /><br /> \**StatementText* 포함 된를 **ALTER TABLE** 문 및 지정된 된 테이블 이름이 없었습니다.<br /><br /> \**StatementText* 포함 된를 **CREATE VIEW** 문 및 테이블 이름 또는 뷰를 쿼리 사양에 정의 된 이름이 존재 하지 않았습니다.<br /><br /> \**StatementText* 포함 된를 **CREATE INDEX** 문 및 지정된 된 테이블 이름이 없었습니다.<br /><br /> \**StatementText* 포함 된를 **권한 부여** 또는 **해지** 문 및 지정한 테이블 이름 또는 뷰 이름이 존재 하지 않았습니다.<br /><br /> \**StatementText* 포함 된를 **선택** 문 및 지정한 테이블 이름 또는 뷰 이름이 존재 하지 않았습니다.<br /><br /> \**StatementText* 포함 된를 **삭제**를 **삽입**, 또는 **업데이트** 문 및 지정된 된 테이블 이름이 없었습니다.<br /><br /> \**StatementText* 포함 된를 **CREATE TABLE** 문과 (참조 테이블 이외의 만들어지는 것) 제약 조건이 지정 된 테이블이 없습니다.<br /><br /> \**StatementText* 포함 된를 **CREATE SCHEMA** 문 및 지정한 테이블 이름 또는 뷰 이름이 존재 하지 않았습니다.|  
|42S11|인덱스가 이미 있습니다.|\**StatementText* 포함 된를 **CREATE INDEX** 문 및 지정 된 인덱스 이름이 이미 존재 합니다.<br /><br /> \**StatementText* 포함 된를 **CREATE SCHEMA** 문 및 지정 된 인덱스 이름이 이미 존재 합니다.|  
|42S12|인덱스가 없습니다.|\**StatementText* 포함 된를 **DROP INDEX** 문 및 지정 된 인덱스 이름이 없습니다.|  
|42S21|열이 이미|\**StatementText* 포함 된를 **ALTER TABLE** 문과에 지정 된 열을 **추가** 절 고유 하지 않거나 기본 테이블의 기존 열을 식별 합니다.|  
|42S22|열이 없습니다|\**StatementText* 포함 된 **CREATE INDEX** 문에서 하나 이상의 열 목록에 지정 된 이름이 없는 열입니다.<br /><br /> \**StatementText* 포함 된를 **GRANT** 또는 **해지** 문과 지정한 열 이름이 없습니다.<br /><br /> \**StatementText* 포함 된를 **선택**를 **삭제**를 **삽입**, 또는 **업데이트** 문 및 지정된 된 열 이름 존재 하지 않습니다.<br /><br /> \**StatementText* 포함 된 **CREATE TABLE** 문과 (참조 테이블 이외의 만들어지는 것) 제약 조건에 지정 된 열이 없는 것입니다.<br /><br /> \**StatementText* 포함 된를 **CREATE SCHEMA** 문과 지정한 열 이름이 없습니다.|  
|44000|WITH CHECK OPTION 위반|인수 *StatementText* 포함 된 **삽입** 표시 된 테이블에서 수행 하는 문 또는 지정 하 여 생성 된 표시 테이블에서 파생 테이블 **WITH CHECK OPTION**같은 영향을 받는 하나 이상의 행에는 **삽입** 문을 표시 하는 테이블에 더 이상.<br /><br /> 인수 *StatementText* 포함 된 **업데이트** 표시 된 테이블에서 수행 하는 문 또는 지정 하 여 생성 된 표시 테이블에서 파생 테이블 **WITH CHECK OPTION**같은 영향을 받는 하나 이상의 행에는 **업데이트** 문을 표시 하는 테이블에 더 이상.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*합니다. 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 가 호출 된 *StatementHandle*합니다. 함수에서 다시 호출 된 다음 합니다 *StatementHandle*합니다.<br /><br /> 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|(DM) **StatementText* 가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLExecDirect** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|(DM) 인수 *TextLength* 보다 작거나 0에 있지만 같지 않음 SQL_NTS 되었습니다.<br /><br /> 매개 변수 값을 사용 하 여 설정 **SQLBindParameter**가 null 포인터, 및 매개 변수 길이 값이 0, SQL_NULL_DATA, SQL_DATA_AT_EXEC SQL_DEFAULT_PARAM으로 SQL_LEN_DATA_AT_EXEC_OFFSET 보다 작거나 합니다.<br /><br /> 매개 변수 값을 사용 하 여 설정할 **SQLBindParameter**, null 포인터 없습니다; C 데이터 형식 SQL_C_BINARY 되었거나 SQL_C_CHAR; 및 매개 변수 길이 값이 0 보다 작은 하지만 SQL_NTS, SQL_NULL_DATA, SQL_DATA_AT_EXEC SQL_DEFAULT_ 없습니다 PARAM SQL_LEN_DATA_AT_EXEC_OFFSET 보다 작거나 합니다.<br /><br /> 매개 변수 길이 값을 읽었으며 **SQLBindParameter** ; SQL_DATA_AT_EXEC로 설정 했습니다. SQL 형식 된 SQL_LONGVARCHAR, SQL_LONGVARBINARY, 또는 long 데이터 소스 특정 데이터 형식 및 SQL_NEED_LONG_DATA_LEN 정보 입력 **SQLGetInfo** "Y" 되었습니다.|  
|HY105|잘못 된 매개 변수 형식|인수에 지정 된 값 *InputOutputType* 에 **SQLBindParameter** SQL_PARAM_OUTPUT, 개이고 매개 변수는 입력된 매개 변수 였습니다.|  
|HY109|잘못 된 커서 위치|\**StatementText* 에 커서가 있었기를 위치 지정 update 또는 delete 문, 및 포함 된 (하 여 **SQLSetPos** 또는 **SQLFetchScroll**)에 한 행을 삭제 하거나 가져올 수 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|SQL_ATTR_CURSOR_TYPE 및 SQL_ATTR_CONCURRENCY 문 특성의 현재 설정 조합 된 드라이버 또는 데이터 원본에서 지원 되지 않습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE로 설정 된 및 SQL_ATTR_CURSOR_TYPE 문 특성 드라이버는 책갈피를 지원 하지 않으면 커서 유형으로 설정 되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|쿼리 제한 시간에는 데이터 원본의 결과 집합을 반환 하기 전에 만료 되었습니다. 시간 제한 기간을 통해 설정 됩니다 **SQLSetStmtAttr**을 SQL_ATTR_QUERY_TIMEOUT입니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램 호출 **SQLExecDirect** 데이터 원본에는 SQL 문을 보내야 합니다. 직접 실행에 대 한 자세한 내용은 참조 하세요. [직접 실행](../../../odbc/reference/develop-app/direct-execution-odbc.md)합니다. 드라이버가는 형식의 데이터 소스에 사용 되는 SQL 사용 하도록 문을 수정 및 데이터 원본에 전달 합니다. 특히, 드라이버는 SQL에 특정 기능을 정의 하는 이스케이프 시퀀스를 수정 합니다. 이스케이프 시퀀스의 구문에 대 한 참조 [ODBC의 이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)합니다.  
  
 응용 프로그램은 SQL 문에서 하나 이상의 매개 변수 표식을 포함할 수 있습니다. 매개 변수 마커를 포함 하려면 응용 프로그램이 적절 한 위치에 있는 SQL 문으로 물음표 (?)를 포함 합니다. 매개 변수에 대 한 자세한 내용은 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)합니다.  
  
 SQL 문의 경우는 **선택** 문과 응용 프로그램 호출 **SQLSetCursorName** 문을 사용 하 여 커서에 연결 하려면 다음 드라이버를 사용 하 여 지정된 된 커서입니다. 그렇지 않으면 드라이버 커서 이름을 생성합니다.  
  
 데이터 원본이 수동 커밋 모드 (명시적 트랜잭션을 시작 필요) 하는 경우 트랜잭션이 이미 시작 되지 않았습니다 드라이버 SQL 문을 보내기 전에 트랜잭션을 시작 합니다. 자세한 내용은 [수동 커밋 모드로](../../../odbc/reference/develop-app/manual-commit-mode.md)합니다.  
  
 응용 프로그램에서 사용 하는 경우 **SQLExecDirect** 전송할를 **커밋** 또는 **롤백** 문이 되지 않는 DBMS 제품 간의 상호 운용 가능 합니다. 응용 프로그램이 호출에서는 커밋하거나 트랜잭션을 롤백하려면 **SQLEndTran**합니다.  
  
 하는 경우 **SQLExecDirect** 실행 시 데이터 매개 변수를 발견 하면 SQL_NEED_DATA를 반환 합니다. 응용 프로그램을 사용 하 여 데이터를 보냅니다 **SQLParamData** 하 고 **SQLPutData**합니다. 참조 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)합니다 [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), 및 [Long 데이터 전송](../../../odbc/reference/develop-app/sending-long-data.md)합니다.  
  
 하는 경우 **SQLExecDirect** 검색 결과 업데이트, 삽입 또는 데이터 원본에 대 한 호출에서 모든 행에 영향을 미치지 않는 delete 문을 실행 **SQLExecDirect** SQL_NO_DATA를 반환 합니다.  
  
 SQL_ATTR_PARAMSET_SIZE 문 특성의 값이 1 보다 큰 경우 SQL 문에 하나 이상의 매개 변수 표식에 포함 된 **SQLExecDirect** 각 집합에서 매개 변수 값에 대해 한 번 SQL 문을 실행 합니다 가리키는 배열 합니다 *ParameterValuePointer* 호출에서 인수 **SQLBindParameter**합니다. 자세한 내용은 [매개 변수 값의 배열](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)합니다.  
  
 책갈피 설정 및 쿼리를 실행 하는 경우를 책갈피를 지원할 수 없습니다, 드라이버를 특성 값을 변경 하 고 SQLSTATE 01S02 반환 하 여 책갈피를 지원 하도록 환경의 강제 변환 하려고 시도 합니다 (옵션 값이 변경 됨). 드라이버 SQLSTATE HY024 반환할 특성을 변경할 수 없는 경우 (잘못 된 특성 값).  
  
> [!NOTE]  
>  응용 프로그램 연결 풀링을 사용 하는 경우와 같은 데이터베이스 또는 데이터베이스의 컨텍스트를 변경 하는 SQL 문을 실행 하지 해야 합니다 **사용 하 여** _데이터베이스_ 변경 하는 SQL Server에서 문 데이터 원본에서 사용 하는 카탈로그입니다.  
  
## <a name="code-example"></a>코드 예  
 참조 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)하십시오 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md), 및 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|커밋 또는 롤백 작업을 실행합니다.|[SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|여러 행의 데이터를 가져오는 중|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록을 인출 또는 결과 통해 스크롤 설정|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|커서 이름을 반환합니다.|[SQLGetCursorName 함수](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|일부 또는 전체 열의 데이터 페치|[SQLGetData 함수](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|에 대 한 데이터를 보내도록 다음 매개 변수를 반환 합니다.|[SQLParamData 함수](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|실행할 문을 준비합니다.|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|실행 시 매개 변수 데이터 전송|[SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|커서 이름을 설정합니다.|[SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
