---
title: SQLExec다이렉트 기능 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5739e397467deb684a4cd6c7b13a507f30b53fa7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286113"
---
# <a name="sqlexecdirect-function"></a>SQLExecDirect 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLExecDirect는** 문안에 매개 변수가 있는 경우 매개 변수 마커 변수의 현재 값을 사용하여 예비 문을 실행합니다. **SQLExecDirect는** 일회성 실행을 위해 SQL 문을 제출하는 가장 빠른 방법입니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLExecDirect(  
     SQLHSTMT     StatementHandle,  
     SQLCHAR *    StatementText,  
     SQLINTEGER   TextLength);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *명령문 텍스트*  
 [입력] 실행할 SQL 문입니다.  
  
 *TextLength*  
 [입력] **문자* 텍스트의 길이입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_NO_DATA, SQL_INVALID_HANDLE 또는 SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLExecDirect가** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 유형* SQL_HANDLE_STMT 및 *명령문* *핸들* 핸들을 사용하는 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 **SQLExecDirect에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01001|커서 작업 충돌|\**StatementText위치* 된 업데이트 또는 삭제 문을 포함 하 고 행 또는 하나 이상의 행 업데이트 또는 삭제 되지 않았습니다. 하나 이상의 행에 대한 업데이트에 대한 자세한 내용은 **SQLSetStmtAttr의**SQL_ATTR_SIMULATE_CURSOR *특성에* 대한 설명을 참조하십시오.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01003|설정 함수에서 NULL 값 제거|인수 *StatementText에는* 집합 함수(예: **AVG,** **MAX,** **MIN**등)가 포함되어 있지만 **COUNT** 집합 함수는 포함되지 않았으며 NULL 인수 값은 함수가 적용되기 전에 제거되었습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|입력/출력 또는 출력 매개 변수에 대해 반환된 문자열 또는 이진 데이터는 비빈 문자 또는 NULL이 아닌 이진 데이터의 잘림을 초래했습니다. 문자열 값인 경우 오른쪽 잘린 값입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01006|권한 취소되지 않음|\**StatementText에* **해지** 문이 포함되었으며 사용자에게 지정된 권한이 없습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01007|권한이 부여되지 않음|StatementText는 **GRANT** 문이며 사용자에게 지정된 권한을 부여할 수 없습니다. * \**|  
|01S02|옵션 값이 변경되었습니다.|구현 작업 조건으로 인해 지정된 문 특성이 잘못되었기 때문에 유사한 값이 일시적으로 대체되었습니다. **(SQLGetStmtAttr** 일시적으로 대체 된 값이 무엇인지 확인 하려면 호출할 수 있습니다.) 대체 값은 커서가 닫혀있을 때까지 *StatementHandle에* 대해 유효하며, 이 때 문 특성이 이전 값으로 되돌아갑니다. 변경할 수 있는 문 특성은 다음과 같습니다.<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ ATTR_SIMULATE_CURSOR<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01S07|분수 잘림|입력/출력 또는 출력 매개 변수에 대해 반환된 데이터는 숫자 데이터 형식의 소수 부분이 잘리거나 시간, 타임스탬프 또는 간격 데이터 형식의 시간 구성 요소의 분수 부분이 잘리게 되도록 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07002|카운트 필드가 올바르지 않습니다.|**SQLBindParameter에** 지정된 매개 변수의 수는 \* *문 텍스트*에 포함 된 SQL 문에 매개 변수의 수 보다 적었습니다 .<br /><br /> **SQLBindParameter는** null 포인터로 설정된 *parameterValuePtr을* 사용하여 *호출되었으며,* SQL_NULL_DATA SQL_DATA_AT_EXEC 설정되지 StrLen_or_IndPtr *InputOutputType은* SQL_PARAM_OUTPUT 설정되지 않았기 때문에 **SQLBindParameter에** 지정된 매개 변수 수가 **StatementText*에 포함된 SQL 문의 매개 변수 수보다 큽니까?|  
|07006|제한된 데이터 형식 특성 위반|바인딩된 매개 변수에 대 한 **SQLBindParameter의** *ValueType* 인수로 식별 된 데이터 **값은 SQLBindParameter**에서 *ParameterType* 인수에 의해 식별 된 데이터 유형으로 변환할 수 없습니다.<br /><br /> SQL_PARAM_INPUT_OUTPUT 또는 SQL_PARAM_OUTPUT 바인딩된 매개 변수에 대해 반환된 데이터 값은 **SQLBindParameter**에서 *ValueType* 인수로 식별된 데이터 유형으로 변환할 수 없습니다.<br /><br /> 하나 이상의 행에 대한 데이터 값을 변환할 수 없지만 하나 이상의 행이 성공적으로 반환된 경우 이 함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07007|제한된 매개 변수 값 위반|SQL_PARAM_INPUT_OUTPUT_STREAM 매개 변수 유형은 부분적으로 데이터를 보내고 받는 매개 변수에만 사용됩니다. 이 매개 변수 형식에는 입력 바인딩 버퍼가 허용되지 않습니다.<br /><br /> 이 오류는 매개 변수 형식이 SQL_PARAM_INPUT_OUTPUT \*때 발생하며 **SQLBindParameter에** 지정된 *StrLen_or_IndPtr* SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_LEN_DATA_AT_EXEC(len) 또는 SQL_DATA_AT_EXEC 같지 않은 경우 발생합니다.|  
|07S01|기본 매개 변수의 잘못된 사용|**SQLBindParameter로**설정된 매개 변수 값이 SQL_DEFAULT_PARAM 해당 매개 변수에 기본값이 없습니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|21S01|삽입 값 목록이 열 목록과 일치하지 않음|\**StatementText* **INSERT** 문을 포함 하 고 삽입 할 값의 수가 파생 된 테이블의 정도와 일치 하지 않습니다.|  
|21S02|파생 테이블의 정도가 열 목록과 일치하지 않음|\**StatementText는* **CREATE VIEW** 문을 포함하고 정규화되지 않은 열 목록(SQL 문의 *열 식별자* 인수에서 뷰에 지정된 열 수)에는 SQL 문의 *쿼리 사양* 인수에 의해 정의된 파생 테이블의 열 수보다 많은 이름이 포함되어 있습니다.|  
|22001|문자열 데이터, 오른쪽 잘림|문자 또는 이진 값을 열에 할당하면 비공백 문자 데이터 또는 null이 아닌 이진 데이터가 잘림됩니다.|  
|22002|표시기 변수가 필요하지만 제공되지 않음|NULL 데이터는 **SQLBindParameter에서** 설정한 *StrLen_or_IndPtr* null 포인터인 출력 매개 변수에 바인딩되었습니다.|  
|22003|범위를 벗어난 숫자 값|**StatementText* 바인딩된 숫자 매개 변수 또는 리터럴을 포함 하는 SQL 문을 포함 하 고 값이 발생 전체 (분수 반대로) 관련 된 테이블 열에 할당 될 때 잘린 될 수 있는 숫자의 일부.<br /><br /> 하나 이상의 입력/출력 또는 출력 매개 변수에 대해 숫자 값(숫자 또는 문자열)을 반환하면 숫자의 전체(분수와 반대)가 잘릴 수 있습니다.|  
|22007|잘못된 날짜 시간 형식|**StatementText는* 날짜, 시간 또는 타임스탬프 구조를 바인딩된 매개 변수로 포함하는 SQL 문을 포함하고 매개 변수는 각각 잘못된 날짜, 시간 또는 타임스탬프였습니다.<br /><br /> 입력/출력 또는 출력 매개 변수는 날짜, 시간 또는 타임스탬프 C 구조에 바인딩되었으며 반환된 매개 변수의 값은 각각 잘못된 날짜, 시간 또는 타임스탬프였습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|22008|일시 필드 오버플로|**StatementText에는* 계산할 때 유효하지 않은 날짜, 시간 또는 타임스탬프 구조가 생성되는 datetime 식이 포함된 SQL 문이 포함되어 있습니다.<br /><br /> 입력/출력 또는 출력 매개 변수에 대해 계산된 datetime 식으로 인해 날짜, 시간 또는 타임스탬프 C 구조가 잘못되었습니다.|  
|22012|0으로 나누기|**StatementText* 0으로 분할을 발생 하는 산술 식을 포함 하는 SQL 문을 포함 했다.<br /><br /> 입력/출력 또는 출력 매개 변수에 대해 계산된 산술 식은 0으로 분할됩니다.|  
|22015|간격 필드 오버플로|StatementText 간격 SQL 데이터 유형으로 변환 될 때 중요 한 숫자의 손실을 발생 하는 정확한 숫자 또는 간격 매개 변수를 포함 했다. * \**<br /><br /> StatementText열의 숫자 데이터 유형으로 변환할 때 숫자 데이터 형식에 표현이 없는 두 개 이상의 필드가 있는 간격 매개 변수가 포함되어 있습니다. * \**<br /><br /> StatementText 간격 SQL 형식에 할당 된 매개 변수 데이터를 포함 하 고 간격 SQL 형식에서 C 형식의 값에 대 한 표현이 없었다. * \**<br /><br /> 정확한 숫자 또는 간격 SQL 형식인 입력/출력 또는 출력 매개 변수를 간격 C 유형에 할당하면 상당한 자릿수가 손실되었습니다.<br /><br /> 입력/출력 또는 출력 매개 변수가 간격 C 구조에 할당된 경우 간격 데이터 구조에 데이터의 표현이 없었습니다.|  
|22018|캐스트 사양에 대해 잘못된 문자 값|StatementText에는 정확하거나 대략적인 숫자, 날짜 시간 또는 간격 데이터 형식인 C 형식이 포함되어 있습니다. * \** 열의 SQL 형식은 문자 데이터 형식입니다. 열의 값이 바인딩된 C 형식의 유효한 리터럴이 아닙니다.<br /><br /> 입력/출력 또는 출력 매개 변수가 반환된 경우 SQL 형식은 정확하거나 대략적인 숫자, 날짜 시간 또는 간격 데이터 형식이었습니다. C 형은 SQL_C_CHAR. 열의 값이 바인딩된 SQL 형식의 유효한 리터럴이 아닙니다.|  
|22019|유효하지 않은 이스케이프 문자|\**StatementText는* **WHERE** 절에서 **ESCAPE가** 포함된 **LIKE** 조건어가 포함된 SQL 문을 포함하고 ESCAPE **다음** 의 이스케이프 문자 의 길이가 1과 같지 않았습니다.|  
|22025|잘못된 이스케이프 시퀀스|\**StatementText에는* **WHERE** 절에 **"LIKE** _패턴 값_ **ESCAPE** _ESCAPE 문자"가_포함된 SQL 문이 포함되어 있으며 패턴 값의 이스케이프 문자 다음 문자는 "%" 또는 "_"가 아닙니다.|  
|23000|무결성 제약 조건 위반|**StatementText* 매개 변수 또는 리터럴을 포함 하는 SQL 문을 포함 했다. 매개 변수 값은 연결된 테이블 열에서 NOT NULL로 정의된 열에 대해 NULL이었으며, 고유 값만 포함하도록 제한된 열에 대해 중복 값이 제공되거나 다른 무결성 제약 조건이 위반되었습니다.|  
|24000|잘못된 커서 상태|커서는 **SQLFetch** 또는 **SQLFetchScroll에**의해 *문 핸들에* 위치 했다 . **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA 반환 되지 않은 경우 이 오류는 드라이버 관리자에 의해 반환 됩니다 및 **SQLFetch** 또는 **SQLFetchScroll** SQL_NO_DATA 반환 하는 경우 드라이버에 의해 반환 됩니다.<br /><br /> 커서가 열려 있었지만 *명령문 핸들에*위치하지 않았습니다.<br /><br /> **StatementText* 위치 업데이트 또는 삭제 문을 포함 하 고 커서는 결과 집합의 시작 하기 전에 또는 결과 집합의 끝 후에 위치 했다.|  
|34000|잘못된 커서 이름|**StatementText* 위치 업데이트 또는 삭제 문을 포함 하 고 실행 되는 문에서 참조 하는 커서가 열려 있지 않았습니다.|  
|3D000|카탈로그 이름이 잘못되었습니다.|*StatementText에* 지정된 카탈로그 이름이 잘못되었습니다.|  
|3F000|잘못된 스키마 이름|*StatementText에* 지정된 스키마 이름이 잘못되었습니다.|  
|40001|직렬화 실패|다른 트랜잭션이 있는 리소스 교착 상태로 인해 트랜잭션이 롤백되었습니다.|  
|40003|명령문 완료를 알 수 없음|이 함수를 실행하는 동안 연결된 연결이 실패했으며 트랜잭션 상태를 확인할 수 없습니다.|  
|42000|구문 오류 또는 액세스 위반|\**StatementText에는* 비교할 수 없거나 구문 오류가 포함된 SQL 문이 포함되어 있습니다.<br /><br /> 사용자는 **StatementText*에 포함된 SQL 문을 실행할 수 있는 권한이 없습니다.|  
|42S01|기본 테이블 또는 뷰가 이미 있습니다.|\**StatementText에는* **CREATE 테이블** 또는 **CREATE VIEW** 문이 포함되어 있으며 지정된 테이블 이름 또는 뷰 이름이 이미 있습니다.|  
|42S02|기본 테이블 또는 뷰를 찾을 수 없습니다.|\**StatementText에는* **DROP 테이블** 또는 **DROP VIEW** 문이 포함되어 있으며 지정된 테이블 이름 또는 뷰 이름이 없습니다.<br /><br /> \**StatementText는* **ALTER TABLE** 문을 포함하고 지정된 테이블 이름이 존재하지 않았습니다.<br /><br /> \**StatementText* **CREATE VIEW** 문을 포함 하 고 쿼리 사양에 의해 정의 된 테이블 이름 또는 뷰 이름이 존재 하지 않았습니다.<br /><br /> \**StatementText* **CREATE INDEX** 문을 포함 하 고 지정 된 테이블 이름이 존재 하지 않았습니다.<br /><br /> \**StatementText* **는 GRANT** 또는 **해지** 문을 포함하고 지정된 테이블 이름 또는 뷰 이름이 존재하지 않습니다.<br /><br /> \**StatementText* **SELECT** 문을 포함 하 고 지정 된 테이블 이름 또는 뷰 이름이 존재 하지 않습니다.<br /><br /> \**StatementText는* **DELETE**, **INSERT**또는 **UPDATE** 문을 포함하고 지정된 테이블 이름이 존재하지 않습니다.<br /><br /> \**StatementText는* **CREATE TABLE** 문을 포함하고 제약 조건에 지정된 테이블(생성되는 테이블이 아닌 테이블을 참조)은 존재하지 않았습니다.<br /><br /> \**StatementText에는* **Create SCHEMA** 문이 포함되었으며 지정된 테이블 이름 또는 뷰 이름이 없습니다.|  
|42S11|인덱스가 이미 있습니다.|\**StatementText에는* **CREATE INDEX** 문이 포함되었으며 지정된 인덱스 이름이 이미 존재했습니다.<br /><br /> \**StatementText에는* **Create SCHEMA** 문이 포함되어 있으며 지정된 인덱스 이름이 이미 존재했습니다.|  
|42S12|인덱스를 찾을 수 없습니다.|\**StatementTextDROP* **INDEX** 문을 포함 하 고 지정 된 인덱스 이름이 존재 하지 않았습니다.|  
|42S21|열이 이미 있습니다.|\**StatementText는* **ALTER TABLE** 문을 포함하고 **ADD** 절에 지정된 열은 고유하지 않거나 기본 테이블의 기존 열을 식별합니다.|  
|42S22|열을 찾을 수 없습니다.|\**StatementText* **에는 CREATE INDEX** 문이 포함되었으며 열 목록에 지정된 열 이름 중 하나 이상이 존재하지 않았습니다.<br /><br /> \**StatementText는* **GRANT** 또는 **해지** 문을 포함하고 지정된 열 이름이 없습니다.<br /><br /> \**StatementText* **SELECT,** **DELETE**, **INSERT**또는 **UPDATE** 문을 포함 하 고 지정 된 열 이름이 없습니다.<br /><br /> \**StatementText는* **CREATE TABLE** 문을 포함하고 제약 조건에 지정된 열(생성되는 테이블이 아닌 테이블을 참조)은 존재하지 않았습니다.<br /><br /> \**StatementText에는* **Create SCHEMA** 문이 포함되었으며 지정된 열 이름이 없습니다.|  
|44000|WITH CHECK OPTION 위반|인수 *StatementText는* 확인 **옵션WITH을**지정하여 만든 테이블또는 본 테이블에서 수행된 **INSERT** 문을 포함하며 INSERT **문의** 영향을 받는 하나 이상의 행이 더 이상 본 테이블에 존재하지 않도록 합니다.<br /><br /> 인수 *StatementText는* 확인 **옵션WITH을**지정하여 만든 테이블또는 조회된 테이블에서 수행된 **UPDATE** 문을 포함하며, 이 경우 **UPDATE** 문의 영향을 받는 하나 이상의 행이 더 이상 본 테이블에 존재하지 않습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *명령문 핸들*에서 호출되었습니다. 그런 다음 *함수가 StatementHandle*에서 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY09|null 포인터의 잘못된 사용|(DM) **문텍스트는* null 포인터였습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. **SQLExecDirect** 함수가 호출될 때 이 비동기 함수가 계속 실행중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) *인수 TextLength는* 0보다 작거나 같지만 SQL_NTS 같지 는 않습니다.<br /><br /> **SQLBindParameter로**설정된 매개 변수 값은 null 포인터였으며 매개 변수 길이 값은 0, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM, SQL_LEN_DATA_AT_EXEC_OFFSET 이하가 아닙니다.<br /><br /> **SQLBindParameter로**설정된 매개 변수 값은 null 포인터가 아닙니다. C 데이터 형식이 SQL_C_BINARY 또는 SQL_C_CHAR. 매개 변수 길이 값이 0보다 작지만 SQL_NTS, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM, SQL_LEN_DATA_AT_EXEC_OFFSET 이하가 아닙니다.<br /><br /> **SQLBindParameter에** 의해 바인딩된 매개 변수 길이 값이 SQL_DATA_AT_EXEC 설정되었습니다. SQL 형식은 SQL_LONGVARCHAR, SQL_LONGVARBINARY 또는 긴 데이터 원본별 데이터 형식이었습니다. **SQLGetInfo의** SQL_NEED_LONG_DATA_LEN 정보 형식은 "Y"입니다.|  
|HY105|잘못된 매개 변수 유형|**SQLBindParameter에서** 인수 *입력OutputType에* 대해 지정된 값은 SQL_PARAM_OUTPUT 및 매개 변수는 입력 매개 변수입니다.|  
|HY109|잘못된 커서 위치|\**StatementText* 위치 업데이트 또는 삭제 문을 포함 하 고 커서는 **(SQLSetPos** 또는 **SQLFetchScroll)** 삭제 되었거나 가져올 수 없는 행에 위치 했다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|SQL_ATTR_CONCURRENCY 및 SQL_ATTR_CURSOR_TYPE 명령문 특성의 현재 설정 의 조합은 드라이버 또는 데이터 원본에서 지원되지 않았습니다.<br /><br /> SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE 설정되었으며 SQL_ATTR_CURSOR_TYPE 문 특성은 드라이버가 책갈피를 지원하지 않는 커서 유형으로 설정되었습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본이 결과 집합을 반환하기 전에 쿼리 시간 시간 만료 기간이 만료되었습니다. 시간 설정 기간은 **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT 통해 설정됩니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 응용 프로그램은 **SQLExecDirect를** 호출하여 데이터 원본에 SQL 문을 보냅니다. 직접 실행에 대한 자세한 내용은 [직접 실행](../../../odbc/reference/develop-app/direct-execution-odbc.md)을 참조하십시오. 드라이버는 데이터 원본에서 사용하는 SQL 형식을 사용하도록 문을 수정한 다음 데이터 원본에 제출합니다. 특히 드라이버는 SQL의 특정 기능을 정의하는 데 사용되는 이스케이프 시퀀스를 수정합니다. 이스케이프 시퀀스의 구문은 [ODBC의 이스케이프 시퀀스를](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)참조하십시오.  
  
 응용 프로그램은 SQL 문에 하나 이상의 매개 변수 마커를 포함할 수 있습니다. 매개 변수 마커를 포함하기 위해 응용 프로그램은 적절한 위치에 SQL 문에 물음표(?)를 포함합니다. 매개 변수에 대한 자세한 내용은 [문 매개 변수를](../../../odbc/reference/develop-app/statement-parameters.md)참조하십시오.  
  
 SQL 문이 **SELECT** 문이고 **SQLSetCursorName이라는** 응용 프로그램이 커서를 문과 연결하면 드라이버는 지정된 커서를 사용합니다. 그렇지 않으면 드라이버는 커서 이름을 생성합니다.  
  
 데이터 원본이 수동 커밋 모드(명시적 트랜잭션 시작 필요)이고 트랜잭션이 아직 시작되지 않은 경우 드라이버는 SQL 문을 보내기 전에 트랜잭션을 시작합니다. 자세한 내용은 [수동 커밋 모드를](../../../odbc/reference/develop-app/manual-commit-mode.md)참조하십시오.  
  
 응용 프로그램이 **SQLExecDirect를** 사용하여 **커밋** 또는 **롤백** 문을 제출하는 경우 DBMS 제품 간에 상호 운용되지 않습니다. 트랜잭션을 커밋하거나 롤백하기 위해 응용 프로그램은 **SQLEndTran**을 호출합니다.  
  
 **SQLExecDirect가** 실행 시 데이터 매개 변수를 만나면 SQL_NEED_DATA 반환합니다. 응용 프로그램은 **SQLParamData** 및 **SQLPutData를**사용하여 데이터를 보냅니다. [SQLBind매개 변수,](../../../odbc/reference/syntax/sqlbindparameter-function.md) [SQLParamData,](../../../odbc/reference/syntax/sqlparamdata-function.md) [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)및 [긴 데이터 전송을](../../../odbc/reference/develop-app/sending-long-data.md)참조하십시오.  
  
 **SQLExecDirect가** 데이터 원본의 행에 영향을 주지 않는 검색된 업데이트, 삽입 또는 삭제 문을 실행하는 경우 **SQLExecDirect에** 대한 호출은 SQL_NO_DATA 반환합니다.  
  
 SQL_ATTR_PARAMSET_SIZE 문 특성의 값이 1보다 크고 SQL 문에 하나 이상의 매개 변수 마커가 포함되어 있는 경우 **SQLExecDirect는** **SQLBindParameter**호출에서 *ParameterValuePointer* 인수로 가리키는 배열의 각 매개 변수 값 집합에 대해 SQL 문을 한 번 실행합니다. 자세한 내용은 [매개 변수 값의 배열을](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)참조하십시오.  
  
 책갈피를 켜고 책갈피를 지원할 수 없는 쿼리가 실행되는 경우 드라이버는 특성 값을 변경하고 SQLSTATE 01S02(옵션 값이 변경됨)를 반환하여 책갈피를 지원하는 환경으로 환경을 강제 변환하려고 시도해야 합니다. 특성을 변경할 수 없는 경우 드라이버는 SQLSTATE HY024(잘못된 특성 값)를 반환해야 합니다.  
  
> [!NOTE]  
>  연결 풀링을 사용하는 경우 응용 프로그램은 데이터 원본에서 사용하는 카탈로그를 변경하는 SQL Server의 **USE** _데이터베이스_ 문과 같이 데이터베이스 또는 데이터베이스컨텍스트를 변경하는 SQL 문을 실행해서는 안 됩니다.  
  
## <a name="code-example"></a>코드 예  
 [SQLBindCol,](../../../odbc/reference/syntax/sqlbindcol-function.md) [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)및 [샘플 ODBC 프로그램을](../../../odbc/reference/sample-odbc-program.md)참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|커밋 또는 롤백 작업 실행|[SQLEndTran 함수(SQLEndTran Function)](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|준비된 SQL 문 실행|[SQL실행 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|여러 데이터 행 가져오기|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 블록 가져오기 또는 결과 집합 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|커서 이름 반환|[SQLGetCursorName 함수](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|데이터 열의 일부 또는 전체 가져오기|[SQLGetData 함수(SQLGetData Function)](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|다음 매개 변수를 반환하여 데이터를|[SQLParamData 함수](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|실행을 위한 명령문 준비|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|실행 시 매개 변수 데이터 전송|[SQLPutData 함수](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|커서 이름 설정|[SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
