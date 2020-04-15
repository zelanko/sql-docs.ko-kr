---
title: SQLSetPos 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetPos
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetPos
helpviewer_keywords:
- SQLSetPos function [ODBC]
ms.assetid: 80190ee7-ae3b-45e5-92a9-693eb558f322
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a8839f1ae540ac9e5f29e144f7f57fb754e50ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287333"
---
# <a name="sqlsetpos-function"></a>SQLSetPos 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ODBC  
  
 **요약**  
 **SQLSetPos는** 행 집합에서 커서 위치를 설정하고 응용 프로그램이 행 집합에서 데이터를 새로 고치거나 결과 집합의 데이터를 업데이트하거나 삭제할 수 있도록 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLSetPos(  
      SQLHSTMT        StatementHandle,  
      SQLSETPOSIROW   RowNumber,  
      SQLUSMALLINT    Operation,  
      SQLUSMALLINT    LockType);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *행 번호*  
 [입력] *작업* 인수로 지정된 작업을 수행할 행 집합의 행 위치입니다. *RowNumber가* 0이면 행 집합의 모든 행에 작업이 적용됩니다.  
  
 자세한 내용은 '댓글'을 참조하세요.  
  
 *작업*  
 [입력] 수행할 작업:  
  
 SQL_POSITION SQL_REFRESH SQL_UPDATE SQL_DELETE  
  
> [!NOTE]
>  *ODBC* *3.x에*대해 작업 인수의 SQL_ADD 값이 더 이상 사용되지 않았습니다. ODBC *3.x* 드라이버는 이전 버전과의 호환성을 위해 SQL_ADD 지원해야 합니다. 이 기능은 **SQLBulkOperations에** 대한 호출로 *Operation* 대체되었습니다SQL_ADD. ODBC *3.x* 응용 프로그램이 ODBC *2.x* 드라이버와 함께 작동하면 드라이버 관리자는 SQL_ADD *작업으로* **SQLSetPos에** SQL_ADD *작업으로* **SQLBulkOperations에** 대한 호출을 매핑합니다.  
  
 자세한 내용은 '댓글'을 참조하세요.  
  
 *잠금 유형*  
 [입력] *Operation* 인수에 지정된 작업을 수행한 후 행을 잠그는 방법을 지정합니다.  
  
 SQL_LOCK_NO_CHANGE SQL_LOCK_EXCLUSIVE SQL_LOCK_UNLOCK  
  
 자세한 내용은 '댓글'을 참조하세요.  
  
 **반환**  
  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLSetPosSQL_ERROR** 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 유형* SQL_HANDLE_STMT 및 *문 핸들*핸들을 사용하는 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 얻을 수 있습니다. *Handle* 다음 표에서는 **SQLSetPos에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
 SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR 반환할 수 있는 모든 SQLSTAT(01xxx SQLSTAT)에 대해 하나 이상의 오류가 발생하는 경우 SQL_SUCCESS_WITH_INFO 반환되지만 전부는 아니지만 다중 행 작업의 행이 반환되고 단일 행 작업에서 오류가 발생하면 SQL_ERROR 반환됩니다.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01001|커서 작업 충돌|*작업* 인수가 SQL_DELETE 또는 SQL_UPDATE 행또는 둘 이상의 행이 삭제되거나 업데이트되지 않았습니다. 하나 이상의 행에 대한 업데이트에 대한 자세한 내용은 **SQLSetStmtAttr의**SQL_ATTR_SIMULATE_CURSOR *특성에* 대한 설명을 참조하십시오. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)<br /><br /> *작업* 인수가 SQL_DELETE 또는 SQL_UPDATE 낙관적 동시성으로 인해 작업이 실패했습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|*작업* 인수가 SQL_REFRESH 및 SQL_C_CHAR 또는 SQL_C_BINARY 데이터 형식이 있는 열 또는 열에 대해 반환된 문자열 또는 이진 데이터가 비NULL 이진 데이터의 잘림으로 이어졌습니다.|  
|01S01|행의 오류|*RowNumber* 인수가 0이고 *Operation* 인수로 지정된 작업을 수행하는 동안 하나 이상의 행에서 오류가 발생했습니다.<br /><br /> (SQL_SUCCESS_WITH_INFO 다중 행 연산의 행이 하나 이상에서 오류가 발생하는 경우 반환되며 단일 행 작업에서 오류가 발생하면 SQL_ERROR 반환됩니다.<br /><br /> 이 SQLSTATE는 **SQLSetPos가** **SQLExtendedFetch**이후에 호출될 때만 반환되며 드라이버가 ODBC *2.x* 드라이버이고 커서 라이브러리가 사용되지 않는 경우 반환됩니다.|  
|01S07|분수 잘림|*작업* 인수가 SQL_REFRESH, 응용 프로그램 버퍼의 데이터 형식이 SQL_C_CHAR 또는 SQL_C_BINARY 않았으며 하나 이상의 열에 대한 응용 프로그램 버퍼에 반환된 데이터가 잘렸습니다. 숫자 데이터 형식의 경우 숫자의 소수 부분이 잘렸습니다. 시간 구성 요소를 포함하는 시간, 타임스탬프 및 간격 데이터 형식의 경우 시간의 소수 부분이 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07006|제한된 데이터 형식 특성 위반|결과 집합에 있는 열의 데이터 값을 **SQLBindCol**에 대한 호출에서 *TargetType에* 의해 지정된 데이터 유형으로 변환할 수 없습니다.|  
|07009|잘못된 설명자 인덱스|인수 *작업이* SQL_REFRESH 또는 SQL_UPDATE 열은 결과 집합의 열 수보다 큰 열 번호로 바인딩되었습니다.|  
|21S02|파생 테이블의 정도가 열 목록과 일치하지 않음|인수 *작업이* SQL_UPDATE 모든 열이 언바운드, 읽기 전용또는 바인딩된 길이/표시기 버퍼의 값이 SQL_COLUMN_IGNORE 때문에 열이 업데이터 분석되지 않았습니다.|  
|22001|문자열 데이터, 오른쪽 잘림|*작업* 인수가 SQL_UPDATE 문자 또는 이진 값을 열에 할당하면 비공백(문자용) 또는 null이 아닌(이진 문자또는 바이트)이 잘림되었습니다.|  
|22003|범위를 벗어난 숫자 값|인수 *작업이* SQL_UPDATE 결과 집합의 열에 숫자 값을 할당하면 숫자의 전체(분수와 반대)가 잘립니다.<br /><br /> 인수 *작업이* SQL_REFRESH 하나 이상의 바인딩된 열에 대한 숫자 값을 반환하면 상당한 자릿수가 손실됩니다.|  
|22007|잘못된 날짜 시간 형식|인수 *작업이* SQL_UPDATE 결과 집합의 열에 날짜 또는 타임스탬프 값을 할당하면 연도, 월 또는 일 필드가 범위를 벗어났습니다.<br /><br /> 인수 *작업이* SQL_REFRESH 하나 이상의 바인딩된 열에 대한 날짜 또는 타임스탬프 값을 반환하면 연도, 월 또는 일 필드가 범위를 벗어났습니다.|  
|22008|날짜/시간 필드 오버플로|*작업* 인수가 SQL_UPDATE 결과 집합의 열로 전송되는 데이터에 대한 datetime 산술 연산의 성능으로 인해 결과가 필드의 허용 값 범위를 벗어나거나 날짜 시간에 대한 그레고리오 력의 자연 규칙에 따라 유효하지 않은 결과의 datetime 필드(연도, 월, 일, 시간, 분 또는 두 번째 필드)가 발생했습니다.<br /><br /> *작업* 인수가 SQL_REFRESH 결과 집합에서 검색되는 데이터에 대한 datetime 산술 연산의 성능으로 인해 결과가 필드의 허용 값 범위를 벗어나거나 날짜 시간에 대한 그레고리오력의 자연 규칙에 따라 유효하지 않은 결과의 datetime 필드(연도, 월, 일, 시간, 분 또는 두 번째 필드)가 발생했습니다.|  
|22015|간격 필드 오버플로|*작업* 인수가 SQL_UPDATE, 간격 SQL 데이터 형식에 정확한 숫자 또는 간격 C 형식을 할당하면 상당한 자릿수가 손실되었습니다.<br /><br /> *작업* 인수가 SQL_UPDATE. 간격 SQL 형식에 할당할 때 INTERVAL SQL 형식에서 C 형식의 값을 표현할 수 없습니다.<br /><br /> *작업* 인수가 SQL_REFRESH 정확한 숫자 또는 간격 SQL 형식에서 간격 C 형식에 할당하면 선행 필드에서 상당한 자릿수가 손실되었습니다.<br /><br /> *작업* 인수가 새로 고침을 SQL_. 간격 C 유형에 할당할 때 간격 C 형식에서 SQL 형식의 값을 표현할 수 없습니다.|  
|22018|캐스트 사양에 대해 잘못된 문자 값|*작업* 인수가 SQL_REFRESH. C 형식은 정확하거나 대략적인 숫자, 날짜 시간 또는 간격 데이터 형식이었습니다. 열의 SQL 형식은 문자 데이터 형식입니다. 열의 값이 바인딩된 C 형식의 유효한 리터럴이 아닙니다.<br /><br /> 인수 *작업은* SQL_UPDATE. SQL 형식은 정확하거나 대략적인 숫자, 날짜 시간 또는 간격 데이터 형식입니다. C 형은 SQL_C_CHAR. 열의 값이 바인딩된 SQL 형식의 유효한 리터럴이 아닙니다.|  
|23000|무결성 제약 조건 위반|인수 *작업이* SQL_DELETE 또는 SQL_UPDATE 및 무결성 제약 조건을 위반 했습니다.|  
|24000|잘못된 커서 상태|*StatementHandle* 실행 된 상태에 있었지만 결과 *집합은 StatementHandle*.<br /><br /> (DM) *명령문 핸들에서*커서가 열려 있지만 **SQLFetch** 또는 **SQLFetchScroll이** 호출되지 않았습니다.<br /><br /> *명령문 핸들에서*커서가 열려 있고 **SQLFetch** 또는 **SQLFetchScroll가** 호출되었지만 결과 집합이 시작되기 전이나 결과 집합이 끝난 후에 커서가 배치되었습니다.<br /><br /> 인수 *작업은* SQL_DELETE SQL_REFRESH 또는 SQL_UPDATE 결과 집합이 시작되기 전에 또는 결과 집합이 끝난 후에 커서가 배치되었습니다.|  
|40001|직렬화 실패|다른 트랜잭션이 있는 리소스 교착 상태로 인해 트랜잭션이 롤백되었습니다.|  
|40003|명령문 완료를 알 수 없음|이 함수를 실행하는 동안 연결된 연결이 실패했으며 트랜잭션 상태를 확인할 수 없습니다.|  
|42000|구문 오류 또는 액세스 위반|드라이버는 인수 *작업에서*요청된 작업을 수행하기 위해 필요에 따라 행을 잠글 수 없습니다.<br /><br /> 드라이버는 인수 *LockType에서*요청 된 대로 행을 잠글 수 없습니다.|  
|44000|WITH CHECK OPTION 위반|*작업* 인수가 SQL_UPDATE 업데이트가 수행되었으며, 업데이트가 확인 **옵션(WITH CHECK OPTION)을**지정하여 만든 테이블또는 조회된 테이블에서 수행되어 업데이트의 영향을 받는 하나 이상의 행이 더 이상 검토된 테이블에 존재하지 않도록 합니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *StatementHandle에서*호출된 다음 *명령문 핸들*에서 함수가 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 SQLSetPos 함수가 호출될 때 계속 실행 중이었습니다.<br /><br /> (DM) 지정된 *명령문핸들이* 실행된 상태가 아닙니다. 이 함수는 **SQLExecDirect**, **SQLExecute**또는 카탈로그 함수를 호출하지 않고 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.<br /><br /> (DM) 드라이버는 ODBC *2.x* 드라이버이고 **SQLSetPos는** **SQLFetch가** 호출된 후 *문 핸들을* 호출했습니다.|  
|HY011|특성을 지금 설정할 수 없습니다.|(DM) 드라이버가 ODBC *2.x* 드라이버였습니다. SQL_ATTR_ROW_STATUS_PTR 문 특성이 설정되었습니다. 그런 다음 **SQLSetPos가** **SQLFetch,** **SQLFetch스크롤**또는 **SQLExtendedFetch가** 호출되기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|*작업* 인수가 SQL_UPDATE 데이터 값은 null 포인터이고 열 길이 값은 0, SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NULL_DATA 또는 SQL_LEN_DATA_AT_EXEC_OFFSET 같지 않거나 같지 않았습니다.<br /><br /> *작업* 인수가 SQL_UPDATE. 데이터 값이 null 포인터가 아닙니다. C 데이터 형식이 SQL_C_BINARY 또는 SQL_C_CHAR. 열 길이 값은 0보다 작지만 SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NTS 또는 SQL_NULL_DATA 같지 않거나 SQL_LEN_DATA_AT_EXEC_OFFSET 같지 않습니다.<br /><br /> 길이/표시기 버퍼의 값이 SQL_DATA_AT_EXEC. SQL 형식은 SQL_LONGVARCHAR, SQL_LONGVARBINARY 또는 긴 데이터 원본별 데이터 형식이었습니다. **SQLGetInfo의** SQL_NEED_LONG_DATA_LEN 정보 형식은 "Y"입니다.|  
|HY092|잘못된 특성 식별자|(DM) *작업* 인수에 대해 지정된 값이 잘못되었습니다.<br /><br /> (DM) *LockType* 인수에 대해 지정된 값이 잘못되었습니다.<br /><br /> *작업* 인수가 SQL_UPDATE 또는 SQL_DELETE SQL_ATTR_CONCURRENCY 명령문 특성은 SQL_ATTR_CONCUR_READ_ONLY.|  
|HY107|범위를 벗어난 행 값|*인수 RowNumber에* 대해 지정된 값이 행 집합의 행 수보다 큽합니다.|  
|HY109|잘못된 커서 위치|*StatementHandle와* 연결된 커서는 정방향 전용으로 정의되었기 때문에 커서를 행 집합 내에 배치할 수 없습니다. **SQLSetStmtAttr에서**SQL_ATTR_CURSOR_TYPE 특성에 대한 설명을 참조하십시오.<br /><br /> *작업* 인수가 SQL_UPDATE SQL_DELETE 또는 SQL_REFRESH *및 RowNumber* 인수로 식별된 행이 삭제되었거나 가져오지 않았습니다.<br /><br /> (DM) *RowNumber* 인수가 0이고 *작업* 인수가 SQL_POSITION.<br /><br /> **SQLSetPos는** **SQLBulkOperations가** 호출되고 **SQLFetchScroll** 또는 **SQLFetch가** 호출되기 전에 호출되었습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|드라이버 또는 데이터 원본은 *Operation* 인수 또는 *LockType* 인수에서 요청된 작업을 지원하지 않습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본이 결과 집합을 반환하기 전에 쿼리 시간 시간 만료 기간이 만료되었습니다. 시간 시간 SQL_ATTR_QUERY_TIMEOUT *특성이* 있는 **SQLSetStmtAttr을** 통해 시간 시간 설정됩니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
  
> [!CAUTION]
>  명령문에 대한 자세한 내용은 **SQLSetPos를** 호출할 수 있으며 ODBC *2.x* 응용 프로그램과의 호환성을 위해 수행해야 하는 작업을 [보려면 블록 커서, 스크롤 가능한 커서 및 이전 버전과의 호환성을](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)참조하십시오.  
  
## <a name="rownumber-argument"></a>행 번호 인수  
 *RowNumber* 인수는 *작업* 인수에 의해 지정된 작업을 수행할 행 집합의 행 수를 지정합니다. *RowNumber가* 0이면 행 집합의 모든 행에 작업이 적용됩니다. *RowNumber는* 0부터 행 집합의 행 수까지의 값이어야 합니다.  
  
> [!NOTE]  
>  C 언어에서 배열은 0 기반이고 *RowNumber* 인수는 1 기반입니다. 예를 들어 행 집합의 다섯 번째 행을 업데이트하려면 응용 프로그램이 배열 인덱스 4에서 행 집합 버퍼를 수정하지만 *RowNumber* 5를 지정합니다.  
  
 모든 연산은 RowNumber로 지정된 행에 커서를 *배치합니다.* 다음 작업에는 커서 위치가 필요합니다.  
  
-   위치 업데이트 및 삭제 문입니다.  
  
-   **SQLGetData에**대한 호출 .  
  
-   SQL_DELETE, SQL_REFRESH 및 SQL_UPDATE 옵션을 사용하여 **SQLSetPos를** 호출합니다.  
  
 예를 들어 *rowNumber가* SQL_DELETE *작업이* 있는 **SQLSetPos** 호출에 대해 2인 경우 커서는 행 집합의 두 번째 행에 배치되고 해당 행은 삭제됩니다. 두 번째 행에 대한 구현 행 상태 배열(SQL_ATTR_ROW_STATUS_PTR 문 특성으로 가리키는)의 항목이 SQL_ROW_DELETED 변경됩니다.  
  
 응용 프로그램은 **SQLSetPos를**호출할 때 커서 위치를 지정할 수 있습니다. 일반적으로 위치에 있는 업데이트를 실행하거나 문을 삭제하거나 **SQLGetData를**호출하기 전에 커서를 배치하기 위해 SQL_POSITION 또는 SQL_REFRESH 작업으로 **SQLSetPos를** 호출합니다.  
  
## <a name="operation-argument"></a>작업 인수  
 *작업* 인수는 다음 작업을 지원합니다. 데이터 원본에서 지원되는 옵션을 결정하기 위해 응용 프로그램은 SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 또는 SQL_STATIC_CURSOR_ATTRIBUTES1 정보 유형(커서 유형에 따라 다름)을 사용하여 **SQLGetInfo를** 호출합니다.  
  
|*작업*<br /><br /> 인수|작업(Operation)|  
|------------------------------|---------------|  
|SQL_POSITION|드라이버는 RowNumber로 지정된 행에 커서를 *배치합니다.*<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 문 특성으로 가리키는 행 상태 배열의 내용은 SQL_POSITION *작업에*대해 무시됩니다.|  
|SQL_REFRESH|드라이버는 *RowNumber에* 의해 지정된 행에 커서를 배치하고 해당 행에 대한 행 집합 버퍼의 데이터를 새로 고칩니다. 드라이버가 행 집합 버퍼에서 데이터를 반환하는 방법에 대한 자세한 내용은 **SQLBindCol**에서 행 별 및 열 별 바인딩에 대한 설명을 참조하십시오.<br /><br /> SQL_REFRESH *작업을* 가진 **SQLSetPos는** 현재 가져온 행 집합 내의 행의 상태와 내용을 업데이트합니다. 여기에는 책갈피 새로 고침이 포함됩니다. 버퍼의 데이터는 새로 고쳐지지만 다시 가져오지 않으므로 행 집합의 멤버 자격은 고정됩니다. 이는 SQL_FETCH_RELATIVE *FetchOrientation* 과 *RowNumber0을* 사용하여 **SQLFetchScroll** 호출에서 수행한 새로 고침과 는 다르며, 이는 결과 집합에서 행 집합을 다시 가져오므로 드라이버와 커서에서 해당 작업을 지원하는 경우 삭제된 데이터를 제거할 수 있습니다.<br /><br /> **SQLSetPos를** 사용하면 SQL_ROW_DELETED 행 상태가 변경되지 않습니다. 행 집합 내에서 삭제된 행은 다음 가져오기까지 삭제된 것으로 계속 표시됩니다. 커서가 압축을 지원하는 경우 다음 가져오기에서 행이 사라집니다(후속 **SQLFetch** 또는 **SQLFetchScroll이** 삭제된 행을 반환하지 않음).<br /><br /> **SQLSetPos를** 통해 새로 고침을 수행할 때 추가된 행이 나타나지 않습니다. 이 동작은 *SQL_FETCH_RELATIVE FetchType* 및 *RowNumber0을* 사용하는 **SQLFetchScroll와** 다르며, 현재 행 집합도 새로 고치지만 커서에서 이러한 작업을 지원하는 경우 추가된 레코드 또는 팩 삭제된 레코드가 표시됩니다.<br /><br /> **SQLSetPos를** 사용하여 새로 고침을 성공적으로 하면 행 상태 배열이 있는 경우 SQL_ROW_ADDED SQL_ROW_SUCCESS 행 상태가 변경됩니다.<br /><br /> **SQLSetPos를** 사용하여 새로 고침을 성공적으로 하면 행 상태 배열이 있는 경우 SQL_ROW_UPDATED 행 상태가 행의 새 상태로 변경됩니다.<br /><br /> 행의 **SQLSetPos** 작업에서 오류가 발생하면 행 상태가 SQL_ROW_ERROR 설정됩니다(행 상태 배열이 있는 경우).<br /><br /> SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES SQL_ATTR_CONCURRENCY 문 특성으로 열린 커서의 경우 **SQLSetPos를** 사용하여 새로 고치면 데이터 원본에서 사용되는 낙관적 동시성 값을 업데이트하여 행이 변경되었음을 감지할 수 있습니다. 이 경우 서버에서 행 집합 버퍼를 새로 고칠 때마다 커서 동시성을 보장하는 데 사용되는 행 버전 또는 값이 업데이트됩니다. 새로 고쳐지는 각 행에 대해 이 현상이 발생합니다.<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 문 특성으로 가리키는 행 상태 배열의 내용은 SQL_REFRESH *작업에*대해 무시됩니다.|  
|SQL_UPDATE|드라이버는 *RowNumber에* 의해 지정 된 행에 커서를 배치 하 고 행 버퍼 **(SQLBindCol의** *TargetValuePtr* 인수)에 있는 값으로 데이터의 기본 행을 업데이트 합니다. 길이/표시기 **버퍼(SQLBindCol의** *StrLen_or_IndPtr* 인수)에서 데이터의 길이를 검색합니다. 열의 길이가 SQL_COLUMN_IGNORE 열은 업데이트되지 않습니다. 행을 업데이트한 후 드라이버는 행 상태 배열의 해당 요소를 SQL_ROW_UPDATED 또는 SQL_ROW_SUCCESS_WITH_INFO 변경합니다(행 상태 배열이 있는 경우).<br /><br /> 중복 열이 포함된 커서에서 SQL_UPDATE *작업* 인수를 사용하여 **SQLSetPos가** 호출되는 경우 드라이버 정의됩니다. 드라이버는 드라이버 정의 SQLSTATE를 반환하거나, 결과 집합에 나타나는 첫 번째 열을 업데이트하거나, 다른 드라이버 정의 동작을 수행할 수 있습니다.<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 문 특성이 가리키는 행 작업 배열을 사용하여 대량 업데이트 중에 현재 행 집합의 행을 무시해야 함을 나타낼 수 있습니다. 자세한 내용은 이 함수 참조의 "상태 및 작업 배열"을 참조하십시오.|  
|SQL_DELETE|드라이버는 *RowNumber에* 의해 지정된 행에 커서를 배치하고 데이터의 기본 행을 삭제합니다. 행 상태 배열의 해당 요소를 SQL_ROW_DELETED 변경합니다. 행이 삭제된 후 다음 행에 대해 유효하지 않습니다: 위치 업데이트 및 삭제 문, **SQLGetData에**대한 호출 및 작업을 *사용하여* **SQLSetPos를** 호출하는 작업은 SQL_POSITION 제외한 모든 것으로 설정됩니다. 압축을 지원하는 드라이버의 경우 데이터 원본에서 새 데이터를 검색할 때 행이 커서에서 삭제됩니다.<br /><br /> 행이 표시되는지 여부는 커서 유형에 따라 다릅니다. 예를 들어 삭제된 행은 정적 및 키집합 기반 커서에는 표시되지만 동적 커서에는 표시되지 않습니다.<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 문 특성을 가리키는 행 작업 배열을 사용하여 대량 삭제 중에 현재 행 집합의 행을 무시해야 함을 나타낼 수 있습니다. 자세한 내용은 이 함수 참조의 "상태 및 작업 배열"을 참조하십시오.|  
  
## <a name="locktype-argument"></a>잠금 유형 인수  
 *LockType* 인수는 응용 프로그램이 동시성을 제어하는 방법을 제공합니다. 대부분의 경우 동시성 수준 및 트랜잭션을 지원하는 데이터 원본은 *LockType* 인수의 SQL_LOCK_NO_CHANGE 값만 지원합니다. *LockType* 인수는 일반적으로 파일 기반 지원에만 사용됩니다.  
  
 *LockType* 인수는 **SQLSetPos가** 실행된 후 행의 잠금 상태를 지정합니다. 드라이버가 요청된 작업을 수행하거나 *LockType* 인수를 충족하기 위해 행을 잠글 수 없는 경우 SQL_ERROR 및 SQLSTATE 42000(구문 오류 또는 액세스 위반)을 반환합니다.  
  
 *LockType* 인수는 단일 문에 대해 지정되지만 잠금은 연결의 모든 문에 동일한 권한을 부여합니다. 특히 연결에서 하나의 문으로 획득한 잠금은 동일한 연결의 다른 문으로 잠금을 해제할 수 있습니다.  
  
 **SQLSetPos를** 통해 잠긴 행은 응용 프로그램이 *lockType이* SQL_LOCK_UNLOCK 설정된 행에 대해 **SQLSetPos를** 호출하거나 응용 프로그램이 SQL_CLOSE 옵션을 사용하여 명령문 또는 **SQLFreeStmt에** 대해 **SQLFreeHandle을** 호출할 때까지 잠겨 있습니다. 트랜잭션을 지원하는 드라이버의 경우 응용 프로그램이 **SQLEndTran을** 호출하여 연결을 커밋하거나 롤백할 때 **SQLSetPos를** 통해 잠긴 행이 잠금 해제됩니다(트랜잭션이 커밋되거나 롤백될 때 커서가 닫히거나 롤백될 때 **SQLGetInfo에서**반환되는 SQL_CURSOR_COMMIT_BEHAVIOR SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 유형에 표시된 대로)  
  
 *LockType* 인수는 다음과 같은 유형의 잠금을 지원합니다. 데이터 원본에서 지원되는 잠금을 결정하기 위해 응용 프로그램은 커서 유형에 따라 SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 또는 SQL_STATIC_CURSOR_ATTRIBUTES1 정보 형식을 사용하여 **SQLGetInfo를** 호출합니다.  
  
|*잠금 유형* 인수|잠금 유형|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|드라이버 또는 데이터 원본은 행이 **SQLSetPos가** 호출되기 전과 동일한 잠금 또는 잠금 해제 상태인지 확인합니다. *LockType의* 이 값을 사용하면 명시적 행 수준 잠금을 지원하지 않는 데이터 원본이 현재 동시성 및 트랜잭션 격리 수준에 필요한 모든 잠금을 사용할 수 있습니다.|  
|SQL_LOCK_EXCLUSIVE|드라이버 또는 데이터 원본은 행을 단독으로 잠그습니다. 다른 연결 또는 다른 응용 프로그램의 문은 행의 잠금을 획득하는 데 사용할 수 없습니다.|  
|SQL_LOCK_UNLOCK|드라이버 또는 데이터 원본이 행의 잠금을 해제합니다.|  
  
 드라이버가 SQL_LOCK_EXCLUSIVE 지원하지만 SQL_LOCK_UNLOCK 지원하지 않는 경우 이전 단락에서 설명한 함수 호출 중 하나가 발생할 때까지 잠긴 행은 잠깁니다.  
  
 드라이버가 SQL_LOCK_EXCLUSIVE 지원하지만 SQL_LOCK_UNLOCK 지원하지 않는 경우 응용 프로그램이 명령문또는 SQL_CLOSE 옵션을 사용하닉옵션을 사용할 수 있도록 **SQLFreeHandle** 또는 **SQLFreeStmt를** 호출할 때까지 잠긴 행은 잠긴 상태로 유지됩니다. 드라이버가 트랜잭션을 지원하고 트랜잭션을 커밋하거나 롤백할 때 커서를 닫는 경우 응용 프로그램은 **SQLEndTran을**호출합니다.  
  
 **SQLSetPos의**업데이트 및 삭제 작업의 경우 응용 프로그램은 다음과 같이 *LockType* 인수를 사용합니다.  
  
-   검색 된 후 행이 변경 되지 않습니다 보장 하기 위해 응용 프로그램은 SQL_REFRESH *작업으로* 설정 된 **SQLSetPos** 를 호출 하 고 *LockType* SQL_LOCK_EXCLUSIVE 설정 합니다.  
  
-   응용 프로그램이 *lockType을* SQL_LOCK_NO_CHANGE 설정하면 드라이버는 응용 프로그램이 SQL_ATTR_CONCURRENCY 문 특성에 대해 SQL_CONCUR_LOCK 지정한 경우에만 업데이트 또는 삭제 작업이 성공할 수 있음을 보장합니다.  
  
-   응용 프로그램에서 SQL_ATTR_CONCURRENCY 문 특성에 대한 SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES 지정하는 경우 드라이버는 행 버전 또는 값을 비교하고 응용 프로그램이 행을 가져온 이후 행이 변경된 경우 작업을 거부합니다.  
  
-   응용 프로그램에서 SQL_ATTR_CONCURRENCY 문 특성에 대한 SQL_CONCUR_READ_ONLY 지정하면 드라이버는 업데이트를 거부하거나 작업을 삭제합니다.  
  
 SQL_ATTR_CONCURRENCY 문 특성에 대한 자세한 내용은 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)을 참조하십시오.  
  
## <a name="status-and-operation-arrays"></a>상태 및 작업 배열  
 **SQLSetPos를**호출할 때 다음과 같은 상태 및 작업 배열이 사용됩니다.  
  
-   행 상태 배열(IRD 및 SQL_ATTR_ROW_STATUS_ARRAY 문 특성의 SQL_DESC_ARRAY_STATUS_PTR 필드가 가리키는 대로)에는 행 집합의 각 데이터 행에 대한 상태 값이 포함됩니다. 드라이버는 **SQLFetch,** **SQLFetchScroll,** **SQLBulkOperations**및 **SQLSetPos**에 대한 호출 후이 배열의 상태 값을 설정합니다. 이 배열은 SQL_ATTR_ROW_STATUS_PTR 문 특성을 가리켰습니다.  
  
-   행 작업 배열(ARD 및 SQL_ATTR_ROW_OPERATION_ARRAY 문 특성의 SQL_DESC_ARRAY_STATUS_PTR 필드가 가리키는 대로)에는 대량 작업에 대한 **SQLSetPos** 호출이 무시되거나 수행되는지 여부를 나타내는 행 집합의 각 행에 대한 값이 포함되어 있습니다. 배열의 각 요소는 SQL_ROW_PROCEED(기본값) 또는 SQL_ROW_IGNORE 설정됩니다. 이 배열은 SQL_ATTR_ROW_OPERATION_PTR 문 특성을 가리켰습니다.  
  
 상태 및 작업 배열의 요소 수는 행 집합의 행 수와 같아야 합니다(SQL_ATTR_ROW_ARRAY_SIZE 문 특성에 의해 정의됨).  
  
 행 상태 배열에 대한 자세한 내용은 [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)를 참조하십시오. 행 작업 배열에 대한 자세한 내용은 이 섹션의 뒷부분에서 "대량 작업에서 행 무시"를 참조하십시오.  
  
## <a name="using-sqlsetpos"></a>SQLSetPos 사용  
 응용 프로그램에서 **SQLSetPos를**호출하기 전에 다음 단계 순서를 수행해야 합니다.  
  
1.  응용 프로그램이 SQL_UPDATE *작업* 으로 설정된 **SQLSetPos를** 호출하는 경우 각 열에 대해 **SQLBindCol(또는** **SQLSetDescRec)을**호출하여 해당 데이터 형식을 지정하고 열의 데이터 및 길이에 대한 버퍼를 바인딩합니다.  
  
2.  응용 프로그램이 SQL_DELETE 또는 SQL_UPDATE 설정된 *작업을* 사용하여 **SQLSetPos를** 호출하는 경우 **SQLColAttribute를** 호출하여 삭제하거나 업데이트할 열이 업데이터인지 확인합니다.  
  
3.  **SQLExecDirect,** **SQLExecute**또는 카탈로그 함수를 호출하여 결과 집합을 만듭니다.  
  
4.  데이터를 검색하려면 **SQLFetch** 또는 **SQLFetchScroll를** 호출합니다.  
  
 **SQLSetPos**사용에 대한 자세한 내용은 [SQLSetPos를 사용하여 데이터 업데이트를](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)참조하십시오.  
  
## <a name="deleting-data-using-sqlsetpos"></a>SQLSetPos를 사용하여 데이터 삭제  
 **SQLSetPos를**사용 하 고 데이터를 삭제 하려면 응용 프로그램은 *RowNumber를* 사용 하 고 삭제할 행의 수로 설정 된 **SQLSetPos** 를 호출 하 고 *작업을* SQL_DELETE 설정 합니다.  
  
 데이터가 삭제된 후 드라이버는 적절한 행에 대한 구현 행 상태 배열의 값을 SQL_ROW_DELETED(또는 SQL_ROW_ERROR)으로 변경합니다.  
  
## <a name="updating-data-using-sqlsetpos"></a>SQLSetPos를 사용하여 데이터 업데이트  
 응용 프로그램은 바인딩된 데이터 버퍼또는 하나 이상의 **SQLPutData**에 대한 호출을 사용하여 열에 대한 값을 전달할 수 있습니다. **데이터가 SQLPutData로** 전달되는 열을 *실행 시 데이터* *열이라고 합니다.* 일반적으로 SQL_LONGVARBINARY 및 SQL_LONGVARCHAR 열에 대한 데이터를 전송하는 데 사용되며 다른 열과 혼합될 수 있습니다.  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>SQLSetPos, 응용 프로그램으로 데이터를 업데이트하려면 다음을 수행합니다.  
  
1.  **SQLBindCol으로**바인딩된 데이터 및 길이/표시기 버퍼에 값을 배치합니다.  
  
    -   일반 열의 경우 응용 프로그램은 * \*TargetValuePtr* 버퍼에 새 열 값을 배치하고 * \*해당* 값의 길이를 StrLen_or_IndPtr 버퍼에 배치합니다. 행을 업데이트하지 않으면 응용 프로그램은 행 작업 배열의 해당 행 요소에 SQL_ROW_IGNORE 배치합니다.  
  
    -   실행 시 데이터 열의 경우 응용 프로그램은 * \*TargetValuePtr* 버퍼에 열 번호와 같은 응용 프로그램 정의 값을 배치합니다. 이 값은 나중에 열을 식별하는 데 사용할 수 있습니다.  
  
         응용 프로그램은*SQL_LEN_DATA_AT_EXEC(길이)* 매크로의 결과를 **StrLen_or_IndPtr* 버퍼에 배치합니다. 열의 SQL 데이터 형식이 SQL_LONGVARBINARY, SQL_LONGVARCHAR 또는 긴 데이터 원본별 데이터 형식이고 드라이버가 **SQLGetInfo의**SQL_NEED_LONG_DATA_LEN 정보 형식에 대해 "Y"를 반환하는 경우 *길이는* 매개 변수에 대해 전송할 데이터의 바이트 수입니다. 그렇지 않으면 음수가 아닌 값이어야 하며 무시됩니다.  
  
2.  데이터 *행을* 업데이트하기 위해 SQL_UPDATE 작업 인수를 설정하여 **SQLSetPos를** 호출합니다.  
  
    -   실행 시 데이터 열이 없는 경우 프로세스가 완료됩니다.  
  
    -   실행 시 데이터 열이 있는 경우 함수는 SQL_NEED_DATA 반환하고 3단계로 진행합니다.  
  
3.  **SQLParamData를** 호출하여 처리될 첫 번째 데이터 실행 열에 대한 * \*TargetValuePtr* 버퍼의 주소를 검색합니다. **SQLParamData는** SQL_NEED_DATA 반환합니다. 응용 프로그램은 * \*TargetValuePtr* 버퍼에서 응용 프로그램 정의 값을 검색합니다.  
  
    > [!NOTE]  
    >  실행 시 데이터 매개 변수는 실행 시 데이터 열과 유사하지만 **SQLParamData에서** 반환되는 값은 각각 다릅니다.  
  
    > [!NOTE]  
    >  실행 시 데이터 매개 변수는 SQL 문의 매개 변수로 SQLPutData 로 데이터가 **SQLExecDirect** 또는 **SQLExecute**로 실행될 때 데이터가 **SQLPutData로** 전송됩니다. **SQLBindParameter** 또는 **SQLSetDescRec**. **SQLParamData에서** 반환되는 값은 *ParameterValuePtr* 인수에서 **SQLBindParameter에** 전달된 32비트 값입니다.  
  
    > [!NOTE]  
    >  실행 시 데이터 열은 행이 **SQLSetPos로**업데이트될 때 **데이터가 SQLPutData로** 전송되는 행 집합의 열입니다. **SQLBindCol.** **SQLParamData에서** 반환되는 값은 처리 중인 **TargetValuePtr* 버퍼의 행 주소입니다.  
  
4.  **SQLPutData를** 한 번 이상 호출하여 열에 대한 데이터를 보냅니다. **SQLPutData에**지정된 * \*TargetValuePtr* 버퍼에서 모든 데이터 값을 반환할 수 없는 경우 두 개 이상의 호출이 필요합니다. 동일한 열에 대한 **SQLPutData에** 대한 여러 호출은 문자, 이진 또는 데이터 원본별 데이터 형식이 있는 열에 문자 C 데이터를 보내거나 문자, 이진 또는 데이터 원본별 데이터 형식이 있는 열로 이진 C 데이터를 보낼 때만 허용됩니다.  
  
5.  **SQLParamData를** 다시 호출하여 열에 대한 모든 데이터가 전송되었음을 알릴 수 있습니다.  
  
    -   실행 시 데이터 열이 더 많은 경우 **SQLParamData는** SQL_NEED_DATA 반환하고 다음 실행 시 데이터 열이 처리될 *TargetValuePtr* 버퍼의 주소를 반환합니다. 응용 프로그램은 4 단계와 5단계를 반복합니다.  
  
    -   실행 시 데이터 열이 더 이상 없는 경우 프로세스가 완료됩니다. 명령문이 성공적으로 실행된 경우 **SQLParamData는** SQL_SUCCESS 반환하거나 SQL_SUCCESS_WITH_INFO. 실행이 실패하면 SQL_ERROR 반환합니다. 이 시점에서 **SQLParamData** **SQLSetPos에서**반환할 수 있는 모든 SQLSTATE를 반환할 수 있습니다.  
  
 데이터가 업데이트된 경우 드라이버는 적절한 행이 SQL_ROW_UPDATED 위해 구현 행 상태 배열의 값을 변경합니다.  
  
 작업이 취소되거나 **SQLParamData** 또는 **SQLPutData에서**오류가 발생하는 경우 **SQLSetPos가** SQL_NEED_DATA 반환하고 모든 데이터 실행 시 열에 대해 데이터를 보내기 전에 응용 프로그램은 **SQLCancel**, **SQLGetDiagField , SQLGetDiagOr,** **SQLGetDiagFunctions, SQLGetDiagFunctions, SQLGetFunctionS,** **SQLParamData**또는 **SQLPutData** 를 호출할 수 있습니다. **SQLGetDiagRec** 명령문 또는 문과 연결된 연결에 대한 다른 함수를 호출하는 경우 함수는 SQL_ERROR 및 SQLSTATE HY010(함수 시퀀스 오류)을 반환합니다.  
  
 응용 프로그램에서 **SQLCancel을** 호출하는 동안 드라이버는 여전히 실행 시 데이터 열에 대한 데이터가 필요하면 드라이버는 작업을 취소합니다. 그런 다음 응용 프로그램이 **SQLSetPos를** 다시 호출할 수 있습니다. 취소는 커서 상태 또는 현재 커서 위치에 영향을 주지 않습니다.  
  
 커서와 연결된 쿼리 사양의 SELECT 목록에 동일한 열에 대한 참조가 두 개 이상 포함되어 있으면 오류가 생성되거나 드라이버가 중복된 참조를 무시하고 요청된 작업을 수행하는지 여부가 드라이버 정의됩니다.  
  
## <a name="performing-bulk-operations"></a>대량 작업 수행  
 *RowNumber* 인수가 0이면 드라이버는 SQL_ATTR_ROW_OPERATION_PTR 문 특성으로 가리키는 행 작업 배열의 해당 필드에 SQL_ROW_PROCEED 값이 있는 행 집합의 모든 행에 대해 *작업* 인수에 지정된 작업을 수행합니다. SQL_DELETE, SQL_REFRESH 또는 SQL_UPDATE *작업* 인수에 대 한 *RowNumber* 인수의 유효한 값이지만 SQL_POSITION 아닙니다. SQL_POSITION *및* 행 번호가 0인 **SQLSetPos는** SQLSTATE HY109(잘못된 커서 위치)를 반환합니다. *RowNumber*  
  
 SQLSTATE HYT00(시간 지정 이 만료됨)과 같이 전체 행 집합과 관련된 오류가 발생하면 드라이버는 SQL_ERROR 및 해당 SQLSTATE를 반환합니다. 행 집합 버퍼의 내용은 정의되지 않으며 커서 위치는 변경되지 않습니다.  
  
 단일 행과 관련된 오류가 발생하면 드라이버는 다음과 같은  
  
-   SQL_ATTR_ROW_STATUS_PTR 문 특성이 가리키는 행 상태 배열의 행에 대한 요소를 SQL_ROW_ERROR 설정합니다.  
  
-   오류 큐의 오류에 대해 하나 이상의 추가 SQLSTAT를 게시하고 진단 데이터 구조에서 SQL_DIAG_ROW_NUMBER 필드를 설정합니다.  
  
 오류 또는 경고를 처리한 후 드라이버가 행 집합의 나머지 행에 대한 작업을 완료하면 SQL_SUCCESS_WITH_INFO 반환합니다. 따라서 오류를 반환한 각 행에 대해 오류 큐에 0개 이상의 추가 SQLSTATE가 포함되어 있습니다. 드라이버가 오류 또는 경고를 처리한 후 작업을 중지하면 SQL_ERROR 반환됩니다.  
  
 드라이버가 SQLSTATE 01004(데이터 잘린 데이터)와 같은 경고를 반환하는 경우 특정 행에 적용되는 오류 정보를 반환하기 전에 전체 행 집합 또는 행 집합의 알 수 없는 행에 적용되는 경고를 반환합니다. 해당 행에 대한 다른 오류 정보와 함께 특정 행에 대한 경고를 반환합니다.  
  
 *RowNumber가* 0이고 *작업이* SQL_UPDATE, SQL_REFRESH 또는 SQL_DELETE 경우 **SQLSetPos에서** 작동하는 행 수는 SQL_ATTR_ROWS_FETCHED_PTR 문 특성을 가리켜 야 합니다.  
  
 *RowNumber가* 0이고 *작업이* SQL_DELETE, SQL_REFRESH 또는 SQL_UPDATE 경우 작업 후의 현재 행은 작업 전의 현재 행과 동일합니다.  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>대량 작업에서 행 무시  
 행 작업 배열을 사용하여 현재 행 집합의 행을 **SQLSetPos를**사용 하 여 대량 작업 하는 동안 무시 해야 합니다 나타낼 수 있습니다. 대량 작업 중에 드라이버가 하나 이상의 행을 무시하도록 지시하려면 응용 프로그램이 다음 단계를 수행해야 합니다.  
  
1.  **SQLSetStmtAttr을** 호출하여 SQL_ATTR_ROW_OPERATION_PTR 명령문 특성을 SQLUSMALLINT 배열을 가리키도록 설정합니다. 이 필드는 **SQLSetDescField를** 호출하여 응용 프로그램이 설명자 핸들을 가져와야 하는 ard의 SQL_DESC_ARRAY_STATUS_PTR 헤더 필드를 설정하도록 설정할 수도 있습니다.  
  
2.  행 작업 배열의 각 요소를 다음 두 값 중 하나로 설정합니다.  
  
    -   SQL_ROW_IGNORE 대량 작업에 대해 행이 제외되었음을 나타냅니다.  
  
    -   SQL_ROW_PROCEED 행이 대량 작업에 포함되어 있음을 나타냅니다. True(기본값)임  
  
3.  대량 작업을 수행 하려면 **SQLSetPos를** 호출 합니다.  
  
 다음 규칙은 행 작업 배열에 적용됩니다.  
  
-   SQL_ROW_IGNORE 및 SQL_ROW_PROCEED SQL_DELETE 또는 SQL_UPDATE *작업을* 사용하여 **SQLSetPos를** 사용하여 대량 작업에만 영향을 미칩니다. SQL_REFRESH 또는 SQL_POSITION *작업으로* **SQLSetPos에** 대한 호출에 영향을 주지 않습니다.  
  
-   포인터는 기본적으로 null로 설정됩니다.  
  
-   포인터가 null이면 모든 요소가 SQL_ROW_PROCEED 설정된 것처럼 모든 행이 업데이트됩니다.  
  
-   요소를 SQL_ROW_PROCEED 설정한다고 해서 해당 행에서 작업이 수행된다는 보장은 없습니다. 예를 들어 행 집합의 특정 행에 상태 SQL_ROW_ERROR 지정한 응용 프로그램이 SQL_ROW_PROCEED 여부에 관계없이 해당 행을 업데이트하지 못할 수 있습니다. 응용 프로그램은 항상 행 상태 배열을 확인하여 작업이 성공했는지 확인해야 합니다.  
  
-   SQL_ROW_PROCEED 헤더 파일에서 0으로 정의됩니다. 응용 프로그램은 모든 행을 처리하기 위해 행 작업 배열을 0으로 초기화할 수 있습니다.  
  
-   행 작업 배열의 요소 번호 "n"이 SQL_ROW_IGNORE 설정되어 있고 **SQLSetPos가** 대량 업데이트 또는 삭제 작업을 수행하기 위해 호출되면 **SQLSetPos를**호출한 후에도 행 집합의 n 번째 행은 변경되지 않습니다.  
  
-   응용 프로그램은 읽기 전용 열을 자동으로 설정하여 SQL_ROW_IGNORE 합니다.  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>대량 작업에서 열 무시  
 하나 이상의 읽기 전용 열에 대한 업데이트 시도로 인해 생성된 불필요한 처리 진단을 방지하기 위해 응용 프로그램은 바인딩된 길이/표시기 버퍼의 값을 SQL_COLUMN_IGNORE 설정할 수 있습니다. 자세한 내용은 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)을 참조하십시오.  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서 응용 프로그램은 사용자가 ORDERS 테이블을 찾아보고 주문 상태를 업데이트할 수 있도록 합니다. 커서는 행 집합 크기가 20인 키 집합 기반이며 행 버전을 비교하는 낙관적 동시성 컨트롤을 사용합니다. 각 행 집합을 가져온 후 응용 프로그램은 이를 인쇄하고 사용자가 주문 상태를 선택하고 업데이트할 수 있도록 합니다. 응용 프로그램은 **SQLSetPos를** 사용하여 선택한 행에 커서를 배치하고 행의 위치 업데이트를 수행합니다. (명확성을 위해 오류 처리는 생략됩니다.)  
  
```cpp  
#define ROWS 20  
#define STATUS_LEN 6  
  
SQLCHAR        szStatus[ROWS][STATUS_LEN], szReply[3];  
SQLINTEGER     cbStatus[ROWS], cbOrderID;  
SQLUSMALLINT   rgfRowStatus[ROWS];  
SQLUINTEGER    sOrderID, crow = ROWS, irow;  
SQLHSTMT       hstmtS, hstmtU;  
  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CONCURRENCY, (SQLPOINTER) SQL_CONCUR_ROWVER, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER) SQL_CURSOR_KEYSET_DRIVEN, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER) ROWS, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_STATUS_PTR, (SQLPOINTER) rgfRowStatus, 0);  
SQLSetCursorName(hstmtS, "C1", SQL_NTS);  
SQLExecDirect(hstmtS, "SELECT ORDERID, STATUS FROM ORDERS ", SQL_NTS);  
  
SQLBindCol(hstmtS, 1, SQL_C_ULONG, &sOrderID, 0, &cbOrderID);  
SQLBindCol(hstmtS, 2, SQL_C_CHAR, szStatus, STATUS_LEN, &cbStatus);  
  
while ((retcode == SQLFetchScroll(hstmtS, SQL_FETCH_NEXT, 0)) != SQL_ERROR) {  
   if (retcode == SQL_NO_DATA_FOUND)  
      break;  
   for (irow = 0; irow < crow; irow++) {  
      if (rgfRowStatus[irow] != SQL_ROW_DELETED)  
         printf("%2d %5d %*s\n", irow+1, sOrderID, NAME_LEN-1, szStatus[irow]);  
   }  
   while (TRUE) {  
      printf("\nRow number to update?");  
      gets_s(szReply, 3);  
      irow = atoi(szReply);  
      if (irow > 0 && irow <= crow) {  
         printf("\nNew status?");  
         gets_s(szStatus[irow-1], (ROWS * STATUS_LEN));  
         SQLSetPos(hstmtS, irow, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
         SQLPrepare(hstmtU,  
          "UPDATE ORDERS SET STATUS=? WHERE CURRENT OF C1", SQL_NTS);  
         SQLBindParameter(hstmtU, 1, SQL_PARAM_INPUT,  
            SQL_C_CHAR, SQL_CHAR,  
            STATUS_LEN, 0, szStatus[irow], 0, NULL);  
         SQLExecute(hstmtU);  
      } else if (irow == 0) {  
         break;  
      }  
   }  
}  
```  
  
 자세한 예는 [SQLSetPos를 통해 행 집합의](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md) [위치 업데이트 및 삭제 명령문](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) 및 행 업데이트 를 참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|블록 커서 위치와 관련이 없는 대량 작업 수행|[SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|데이터 블록 가져오기 또는 결과 집합 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|설명자의 단일 필드 얻기|[SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|설명자의 여러 필드 얻기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|설명자의 단일 필드 설정|[SQLSetDesc필드 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|설명자의 여러 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
