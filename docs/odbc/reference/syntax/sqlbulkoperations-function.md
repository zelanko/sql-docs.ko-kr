---
title: SQLBulk연운영 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBulkOperations
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBulkOperations
helpviewer_keywords:
- SQLBulkOperations function [ODBC]
ms.assetid: 7029d0da-b0f2-44e6-9114-50bd96f47196
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61f4f294a6d84856bc3065b599a370bb5658e3ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301333"
---
# <a name="sqlbulkoperations-function"></a>SQLBulkOperations 함수
**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ODBC  
  
 **요약**  
 **SQLBulkOperations는** 책갈피별로 업데이트, 삭제 및 가져오기를 포함하여 대량 삽입 및 대량 북마크 작업을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *작업*  
 [입력] 수행할 작업:  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARK SQL_DELETE_BY_BOOKMARK SQL_FETCH_BY_BOOKMARK  
  
 자세한 내용은 '댓글'을 참조하세요.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLBulkOperations** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값 핸들 *SQL_HANDLE_STMT* 핸들 *핸들* *Handle* 핸들을 호출 하 여 **SQLGetDiagRec를** 호출 할 수 있습니다. 다음 표에서는 일반적으로 **SQLBulkOperations에서** 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
 SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR 반환할 수 있는 모든 SQLSTAT(01xxx SQLSTAT)에 대해 하나 이상의 오류가 발생하는 경우 SQL_SUCCESS_WITH_INFO 반환되지만 전부는 아니지만 다중 행 작업의 행이 반환되고 단일 행 작업에서 오류가 발생하면 SQL_ERROR 반환됩니다.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|*작업* 인수가 SQL_FETCH_BY_BOOKMARK 문자열 또는 이진 데이터는 SQL_C_CHAR 또는 SQL_C_BINARY 데이터 형식이 있는 열 또는 열에 대해 반환되어 비NULL 이진 데이터가 잘림되었습니다.|  
|01S01|행의 오류|*작업* 인수가 SQL_ADD 작업을 수행하는 동안 하나 이상의 행에서 오류가 발생했지만 하나 이상의 행이 성공적으로 추가되었습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)<br /><br /> 이 오류는 응용 프로그램이 ODBC 2로 작업하는 경우에만 발생합니다. *x* 드라이버.)|  
|01S07|분수 잘림|*작업* 인수가 SQL_FETCH_BY_BOOKMARK 응용 프로그램 버퍼의 데이터 형식이 SQL_C_CHAR SQL_C_BINARY 않았으며 하나 이상의 열에 대한 응용 프로그램 버퍼에 반환된 데이터가 잘렸습니다. 숫자 C 데이터 형식의 경우 숫자의 소수 부분이 잘렸습니다. 시간 구성 요소를 포함하는 시간, 타임스탬프 및 간격 C 데이터 형식의 경우 시간의 소수 부분이 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07006|제한된 데이터 형식 특성 위반|*작업* 인수가 SQL_FETCH_BY_BOOKMARK 결과 집합의 열의 데이터 값을 **SQLBindCol**호출에서 *TargetType* 인수에 의해 지정된 데이터 유형으로 변환할 수 없습니다.<br /><br /> *작업* 인수가 SQL_UPDATE_BY_BOOKMARK 또는 SQL_ADD 응용 프로그램 버퍼의 데이터 값은 결과 집합에서 열의 데이터 유형으로 변환할 수 없습니다.|  
|07009|잘못된 설명자 인덱스|인수 *작업이* SQL_ADD 열은 결과 집합의 열 수보다 큰 열 번호로 바인딩되었습니다.|  
|21S02|파생 테이블의 정도가 열 목록과 일치하지 않음|인수 *작업은* SQL_UPDATE_BY_BOOKMARK. 모든 열이 언바운드 또는 읽기 전용이거나 바운드 길이/표시기 버퍼의 값이 SQL_COLUMN_IGNORE 때문에 열이 업데이터 처리되지 않았습니다.|  
|22001|문자열 데이터 오른쪽 잘림|결과 집합에서 열에 문자 또는 이진 값을 할당하면 비공백(문자의 경우) 또는 null이 아닌 문자 또는 바이트가 잘림됩니다.|  
|22003|범위를 벗어난 숫자 값|*작업* 인수가 SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK 결과 집합의 열에 숫자 값을 할당하면 숫자의 전체(분수와 반대)가 잘립니다.<br /><br /> 인수 *작업이* SQL_FETCH_BY_BOOKMARK 하나 이상의 바인딩된 열에 대한 숫자 값을 반환하면 상당한 자릿수가 손실됩니다.|  
|22007|잘못된 날짜 시간 형식|*작업* 인수가 SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK 결과 집합의 열에 날짜 또는 타임스탬프 값을 할당하면 연도, 월 또는 일 필드가 범위를 벗어났습니다.<br /><br /> 인수 *작업이* SQL_FETCH_BY_BOOKMARK 하나 이상의 바인딩된 열에 대한 날짜 또는 타임스탬프 값을 반환하면 연도, 월 또는 일 필드가 범위를 벗어났습니다.|  
|22008|날짜/시간 필드 오버플로|*작업* 인수는 SQL_ADD SQL_UPDATE_BY_BOOKMARK 결과 집합의 열로 전송되는 데이터에 대한 datetime 산술 연산의 성능으로 인해 필드의 허용 값 범위를 벗어나거나 날짜 시간에 대한 그레고리오 력의 자연 규칙에 따라 유효하지 않은 결과의 날짜 시간 필드(연도, 월, 일, 시간, 분 또는 두 번째 필드)가 발생했습니다.<br /><br /> *작업* 인수가 SQL_FETCH_BY_BOOKMARK 결과 집합에서 검색되는 데이터에 대한 datetime 산술 연산의 성능으로 인해 필드의 허용 값 범위를 벗어나거나 날짜 시간에 대한 그레고리오력의 자연 규칙에 따라 유효하지 않은 결과의 datetime 필드(연도, 월, 일, 시간, 분 또는 두 번째 필드)가 발생했습니다.|  
|22015|간격 필드 오버플로|*작업* 인수가 SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK 간격 SQL 데이터 형식에 정확한 숫자 또는 간격 C 형식을 할당하면 상당한 숫자가 손실되었습니다.<br /><br /> *작업* 인수가 SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK. 간격 SQL 형식에 할당할 때 INTERVAL SQL 형식에서 C 형식의 값을 표현할 수 없습니다.<br /><br /> *작업* 인수가 SQL_FETCH_BY_BOOKMARK 정확한 숫자 또는 간격 SQL 형식에서 간격 C 형식에 할당하면 선행 필드에서 상당한 자릿수가 손실되었습니다.<br /><br /> *작업* 인수가 SQL_FETCH_BY_BOOKMARK. 간격 C 유형에 할당할 때 간격 C 형식에서 SQL 형식의 값을 표현할 수 없습니다.|  
|22018|캐스트 사양에 대해 잘못된 문자 값|*작업* 인수가 SQL_FETCH_BY_BOOKMARK. C 형식은 정확하거나 대략적인 숫자, 날짜 시간 또는 간격 데이터 형식이었습니다. 열의 SQL 형식은 문자 데이터 형식입니다. 열의 값이 바인딩된 C 형식의 유효한 리터럴이 아닙니다.<br /><br /> 인수 *작업이* SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK. SQL 형식은 정확하거나 대략적인 숫자, 날짜 시간 또는 간격 데이터 형식입니다. C 형은 SQL_C_CHAR. 열의 값이 바인딩된 SQL 형식의 유효한 리터럴이 아닙니다.|  
|23000|무결성 제약 조건 위반|*작업* 인수가 SQL_ADD SQL_DELETE_BY_BOOKMARK 또는 SQL_UPDATE_BY_BOOKMARK 및 무결성 제약 조건을 위반했습니다.<br /><br /> *작업* 인수가 SQL_ADD 바인딩되지 않은 열은 NOT NULL로 정의되며 기본값이 없습니다.<br /><br /> *작업* 인수가 SQL_ADD *바인딩된 StrLen_or_IndPtr* 버퍼에 지정된 길이가 SQL_COLUMN_IGNORE 열에 기본값이 없습니다.|  
|24000|잘못된 커서 상태|*StatementHandle* 실행 된 상태에 있었지만 결과 *집합은 StatementHandle*.|  
|40001|직렬화 실패|다른 트랜잭션의 리소스 교착 상태 때문에 트랜잭션이 롤백되었습니다.|  
|40003|명령문 완료를 알 수 없음|이 함수를 실행하는 동안 연결된 연결이 실패했으며 트랜잭션 상태를 확인할 수 없습니다.|  
|42000|구문 오류 또는 액세스 위반|*작업* 인수에서 요청된 작업을 수행하기 위해 필요에 따라 드라이버를 잠글 수 없습니다.|  
|44000|WITH CHECK OPTION 위반|*작업* 인수는 SQL_ADD SQL_UPDATE_BY_BOOKMARK 및 삽입 또는 업데이트는 **WITH CHECK OPTION을**지정하여 만든 조회된 테이블(또는 본 테이블에서 파생된 테이블)에서 수행되었으며, 삽입 또는 업데이트의 영향을 받는 하나 이상의 행이 더 이상 본 테이블에 존재하지 않습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *명령문 핸들*에서 호출되었습니다. 그런 다음 *함수가 StatementHandle*에서 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 **SQLBulkOperations** 함수가 호출될 때 계속 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 지정된 *명령문핸들이* 실행된 상태가 아닙니다. 이 함수는 **SQLExecDirect**, **SQLExecute**또는 카탈로그 함수를 호출하지 않고 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLSetPos는** *명령문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.<br /><br /> (DM) 드라이버는 ODBC 2였습니다. *x* 드라이버 및 **SQLBulkOperations는** **SQLFetchScroll** 또는 **SQLFetch가** 호출되기 전에 *문 핸들을* 호출했습니다.<br /><br /> (DM) **SQLBulkOperations는** **SQLExtendedFetch가** *명령문 핸들에서*호출된 후에 호출되었습니다.|  
|HY011|특성을 지금 설정할 수 없습니다.|(DM) 드라이버는 ODBC 2였습니다. *x* 드라이버 및 SQL_ATTR_ROW_STATUS_PTR 문 특성은 **SQLFetch** 또는 **SQLFetchScroll** 및 **SQLBulkOperations**에 대한 호출 간에 설정되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|*작업* 인수가 SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK. 데이터 값이 null 포인터가 아닙니다. C 데이터 형식이 SQL_C_BINARY 또는 SQL_C_CHAR. 열 길이 값은 0보다 작지만 SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NTS 또는 SQL_NULL_DATA 같지 않거나 SQL_LEN_DATA_AT_EXEC_OFFSET 같지 않습니다.<br /><br /> 길이/표시기 버퍼의 값이 SQL_DATA_AT_EXEC. SQL 형식은 SQL_LONGVARCHAR, SQL_LONGVARBINARY 또는 긴 데이터 원본별 데이터 형식이었습니다. **SQLGetInfo의** SQL_NEED_LONG_DATA_LEN 정보 형식은 "Y"입니다.<br /><br /> *작업* 인수가 SQL_ADD SQL_ATTR_USE_BOOKMARK 문 특성이 SQL_UB_VARIABLE 설정되었으며 열 0이 이 결과 집합의 책갈피의 최대 길이와 같지 않은 버퍼에 바인딩되었습니다. 이 길이는 IRD의 SQL_DESC_OCTET_LENGTH 필드에서 사용할 수 있으며 **SQLDescribeCol,** **SQLColAttribute**또는 **SQLGetDescField를**호출하여 얻을 수 있습니다.|  
|HY092|잘못된 특성 식별자|(DM) *작업* 인수에 대해 지정된 값이 잘못되었습니다.<br /><br /> *작업* 인수가 SQL_ADD SQL_UPDATE_BY_BOOKMARK 또는 SQL_DELETE_BY_BOOKMARK SQL_ATTR_CONCURRENCY 명령문 특성이 SQL_CONCUR_READ_ONLY 설정되었습니다.<br /><br /> *작업* 인수가 SQL_DELETE_BY_BOOKMARK, SQL_FETCH_BY_BOOKMARK 또는 SQL_UPDATE_BY_BOOKMARK 및 책갈피 열이 바인딩되지 않았거나 SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_OFF 설정되었습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|드라이버 또는 데이터 원본은 *작업* 인수에서 요청된 작업을 지원하지 않습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본이 결과 집합을 반환하기 전에 쿼리 시간 시간 만료 기간이 만료되었습니다. 시간 시간 설정 기간은 SQL_ATTR_QUERY_TIMEOUT *특성* 인수를 가진 **SQLSetStmtAttr을** 통해 설정됩니다.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
  
> [!CAUTION]  
>  **SQLBulkOperations를** 호출할 수 있는 명령문 과 ODBC 2와의 호환성을 위해 수행해야 하는 작업에 대한 자세한 내용을 참조하십시오. *x* 응용 프로그램은 부록 G: 이전 버전과의 호환성을 위한 드라이버 지침의 [블록 커서, 스크롤 가능한 커서 및 이전 버전과의 호환성](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 섹션을 참조하십시오.  
  
 응용 프로그램은 **SQLBulkOperations를** 사용하여 현재 쿼리에 해당하는 기본 테이블 또는 뷰에서 다음 작업을 수행합니다.  
  
-   새 행을 추가합니다.  
  
-   책갈피로 각 행을 식별하는 행 집합을 업데이트합니다.  
  
-   각 행이 책갈피로 식별되는 행 집합을 삭제합니다.  
  
-   각 행이 책갈피로 식별되는 행 집합을 가져옵니다.  
  
 **SQLBulkOperations를**호출한 후 블록 커서 위치가 정의되지 않습니다. 응용 프로그램은 커서 위치를 설정하려면 **SQLFetchScroll를** 호출해야 합니다. 응용 프로그램은 SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE 또는 SQL_FETCH_BOOKMARK *대한 FetchOrientation* 인수를 사용하여 **SQLFetchScroll를** 호출해야 합니다. 응용 프로그램에서 SQL_FETCH_PRIOR, SQL_FETCH_NEXT 또는 SQL_FETCH_RELATIVE *대한 FetchOrientation* 인수를 사용하여 **SQLFetch** 또는 **SQLFetchScroll를** 호출하는 경우 커서 위치가 정의되지 않습니다.  
  
 **SQLBindCol에**대한 호출에 지정된 열 길이/표시기 버퍼를 설정하여 **SQLBulkOperations** 호출에 의해 수행되는 대량 작업에서 열을 무시할 수 SQL_COLUMN_IGNORE.  
  
 이 함수를 사용하여 대량 작업을 수행할 때 행을 무시할 수 없기 때문에 응용 프로그램에서 SQL_ATTR_ROW_OPERATION_PTR 문 특성을 **SQLBulkOperations를** 호출할 때 설정할 필요가 없습니다.  
  
 SQL_ATTR_ROWS_FETCHED_PTR 문 특성으로 가리키는 버퍼에는 **SQLBulkOperations**에 대한 호출의 영향을 받는 행 수가 포함됩니다.  
  
 *작업* 인수가 SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK 커서와 연결된 쿼리 사양의 선택 목록에 동일한 열에 대한 두 개 이상의 참조가 포함된 경우 드라이버가 생성되는지 또는 드라이버가 중복된 참조를 무시하고 요청된 작업을 수행하는지에 대해 드라이버 정의됩니다.  
  
 **SQLBulkOperations를**사용하는 방법에 대한 자세한 내용은 [SQLBulkOperations를 사용하여 데이터 업데이트를](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)참조하십시오.  
  
## <a name="performing-bulk-inserts"></a>벌크 인서삽입 수행  
 **SQLBulkOperations를**사용하여 데이터를 삽입하려면 응용 프로그램은 다음 단계 순서를 수행합니다.  
  
1.  결과 집합을 반환 하는 쿼리를 실행 합니다.  
  
2.  SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 삽입할 행 수로 설정합니다.  
  
3.  **SQLBindCol을** 호출하여 삽입하려는 데이터를 바인딩합니다. 데이터는 SQL_ATTR_ROW_ARRAY_SIZE 값과 같은 크기의 배열에 바인딩됩니다.  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 문 특성이 가리키는 배열의 크기는 SQL_ATTR_ROW_ARRAY_SIZE 같아야 하거나 SQL_ATTR_ROW_STATUS_PTR null 포인터여야 합니다.  
  
4.  삽입을 수행 하려면 **SQLBulkOperations***(명령문 핸들,* SQL_ADD)를 호출 합니다.  
  
5.  응용 프로그램에서 SQL_ATTR_ROW_STATUS_PTR 문 특성을 설정한 경우 이 배열을 검사하여 작업 결과를 확인할 수 있습니다.  
  
 응용 프로그램이 SQL_ADD *작업* 인수를 사용 하 고 **SQLBulkOperations를** 호출 하기 전에 열 0을 바인딩하는 경우 드라이버는 새로 삽입 된 행에 대 한 책갈피 값으로 바인딩된 열 0 버퍼를 업데이트 합니다. 이렇게 하려면 응용 프로그램이 문을 실행하기 전에 SQL_ATTR_USE_BOOKMARKS 문 특성을 SQL_UB_VARIABLE 설정해야 합니다. ODBC 2에서는 작동하지 않습니다. *x* 드라이버.)  
  
 SQLBulkOperations에 의해 부분적으로 긴 데이터를 추가할 수 있습니다., SQLParamData 및 SQLPutData에 대 한 호출을 사용 하 여. 자세한 내용은 이 함수 참조의 왼쪽 에 있는 "대량 삽입 및 업데이트에 대한 긴 데이터 제공"을 참조하십시오.  
  
 응용 프로그램이 **SQLBulkOperations를** 호출하기 전에 **SQLFetch** 또는 **SQLFetchScroll을** 호출할 필요는 없습니다(ODBC 2에 대해 가는 경우 제외).* x* 드라이버; 이전 [버전 과의 호환성 및 표준 준수](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)를 참조하십시오.  
  
 SQL_ADD *작업* 인수가 있는 **SQLBulkOperations가**중복 열이 포함된 커서에서 호출되는 경우 이 동작은 드라이버 정의됩니다. 드라이버는 드라이버 정의 SQLSTATE를 반환하거나, 결과 집합에 나타나는 첫 번째 열에 데이터를 추가하거나, 다른 드라이버 정의 동작을 수행할 수 있습니다.  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>북마크를 사용하여 대량 업데이트 수행  
 **SQLBulkOperations를**사용하여 책갈피를 사용하여 대량 업데이트를 수행하려면 응용 프로그램이 순서대로 다음 단계를 수행합니다.  
  
1.  SQL_ATTR_USE_BOOKMARKS 명령문 특성을 SQL_UB_VARIABLE 설정합니다.  
  
2.  결과 집합을 반환 하는 쿼리를 실행 합니다.  
  
3.  SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 업데이트하려는 행 수로 설정합니다.  
  
4.  **SQLBindCol을** 호출하여 업데이트하려는 데이터를 바인딩합니다. 데이터는 SQL_ATTR_ROW_ARRAY_SIZE 값과 같은 크기의 배열에 바인딩됩니다. 또한 **SQLBindCol을** 호출하여 열 0(책갈피 열)을 바인딩합니다.  
  
5.  열 0에 바인딩된 배열로 업데이트하려는 행에 대한 책갈피를 복사합니다.  
  
6.  바인딩된 버퍼의 데이터를 업데이트합니다.  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 문 특성이 가리키는 배열의 크기는 SQL_ATTR_ROW_ARRAY_SIZE SQL_ATTR_ROW_STATUS_PTR 같아야 합니다.  
  
7.  SQLBulkOperations *(명령문 핸들,* SQL_UPDATE_BY_BOOKMARK)를 **호출합니다.**  
  
    > [!NOTE]  
    >  응용 프로그램에서 SQL_ATTR_ROW_STATUS_PTR 문 특성을 설정한 경우 이 배열을 검사하여 작업 결과를 확인할 수 있습니다.  
  
8.  선택적으로 **SQLBulkOperations***(문 핸들*, SQL_FETCH_BY_BOOKMARK)를 호출하여 바인딩된 응용 프로그램 버퍼로 데이터를 가져와 업데이트가 발생했는지 확인합니다.  
  
9. 데이터가 업데이트된 경우 드라이버는 해당 행이 SQL_ROW_UPDATED 위해 행 상태 배열의 값을 변경합니다.  
  
 **SQLBulkOperations에서** 수행하는 대량 업데이트에는 **SQLParamData** 및 **SQLPutData**에 대한 호출을 사용하여 긴 데이터가 포함될 수 있습니다. 자세한 내용은 이 함수 참조의 왼쪽 에 있는 "대량 삽입 및 업데이트에 대한 긴 데이터 제공"을 참조하십시오.  
  
 책갈피커에서 책갈피가 지속되는 경우 책갈피를 사용하여 업데이트하기 전에 응용 프로그램에서 **SQLFetch** 또는 **SQLFetchScroll를** 호출할 필요가 없습니다. 이전 커서에서 저장한 책갈피를 사용할 수 있습니다. 책갈피커 간에 책갈피가 유지되지 않으면 응용 프로그램은 **SQLFetch** 또는 **SQLFetchScroll를** 호출하여 책갈피를 검색해야 합니다.  
  
 이 동작은 SQL_UPDATE_BY_BOOKMARK *작업* 인수인 **SQLBulkOperations가**중복 열을 포함하는 커서에서 호출되는 경우 드라이버 정의됩니다. 드라이버는 드라이버 정의 SQLSTATE를 반환하거나, 결과 집합에 나타나는 첫 번째 열을 업데이트하거나, 다른 드라이버 정의 동작을 수행할 수 있습니다.  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>책갈피를 사용하여 대량 가져오기 수행  
 **SQLBulkOperations를**사용하여 책갈피를 사용하여 대량 인출을 수행하려면 응용 프로그램이 순서대로 다음 단계를 수행합니다.  
  
1.  SQL_ATTR_USE_BOOKMARKS 명령문 특성을 SQL_UB_VARIABLE 설정합니다.  
  
2.  결과 집합을 반환 하는 쿼리를 실행 합니다.  
  
3.  SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 가져올 행 수로 설정합니다.  
  
4.  **SQLBindCol을** 호출하여 가져오려는 데이터를 바인딩합니다. 데이터는 SQL_ATTR_ROW_ARRAY_SIZE 값과 같은 크기의 배열에 바인딩됩니다. 또한 **SQLBindCol을** 호출하여 열 0(책갈피 열)을 바인딩합니다.  
  
5.  열 0에 바인딩된 배열로 가져오는 데 관심이 있는 행에 대한 책갈피를 복사합니다. (응용 프로그램이 이미 책갈피를 별도로 얻었다고 가정합니다.)  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 문 특성이 가리키는 배열의 크기는 SQL_ATTR_ROW_ARRAY_SIZE SQL_ATTR_ROW_STATUS_PTR 같아야 합니다.  
  
6.  SQLBulkOperations *(명령문 핸들,* SQL_FETCH_BY_BOOKMARK)를 **호출합니다.**  
  
7.  응용 프로그램에서 SQL_ATTR_ROW_STATUS_PTR 문 특성을 설정한 경우 이 배열을 검사하여 작업 결과를 확인할 수 있습니다.  
  
 책갈피커에서 책갈피를 유지하는 경우 응용 프로그램은 책갈피를 사용하여 가져오기 전에 **SQLFetch** 또는 **SQLFetchScroll을** 호출할 필요가 없습니다. 이전 커서에서 저장한 책갈피를 사용할 수 있습니다. 책갈피커 간에 책갈피가 유지되지 않으면 응용 프로그램은 **SQLFetch** 또는 **SQLFetchScroll를** 한 번 호출하여 책갈피를 검색해야 합니다.  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>책갈피를 사용하여 대량 삭제 수행  
 **SQLBulkOperations를**사용하여 책갈피를 사용하여 대량 삭제를 수행하려면 응용 프로그램이 순서대로 다음 단계를 수행합니다.  
  
1.  SQL_ATTR_USE_BOOKMARKS 명령문 특성을 SQL_UB_VARIABLE 설정합니다.  
  
2.  결과 집합을 반환 하는 쿼리를 실행 합니다.  
  
3.  SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 삭제하려는 행 수로 설정합니다.  
  
4.  **SQLBindCol을** 호출하여 열 0(책갈피 열)을 바인딩합니다.  
  
5.  열 0에 바인딩된 배열로 삭제하려는 행에 대한 책갈피를 복사합니다.  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 문 특성이 가리키는 배열의 크기는 SQL_ATTR_ROW_ARRAY_SIZE SQL_ATTR_ROW_STATUS_PTR 같아야 합니다.  
  
6.  SQLBulkOperations *(명령문 핸들,* SQL_DELETE_BY_BOOKMARK)를 **호출합니다.**  
  
7.  응용 프로그램에서 SQL_ATTR_ROW_STATUS_PTR 문 특성을 설정한 경우 이 배열을 검사하여 작업 결과를 확인할 수 있습니다.  
  
 책갈피커에서 책갈피가 지속되는 경우 응용 프로그램은 책갈피를 사용하여 삭제하기 전에 **SQLFetch** 또는 **SQLFetchScroll을** 호출할 필요가 없습니다. 이전 커서에서 저장한 책갈피를 사용할 수 있습니다. 책갈피커 간에 책갈피가 유지되지 않으면 응용 프로그램은 **SQLFetch** 또는 **SQLFetchScroll를** 한 번 호출하여 책갈피를 검색해야 합니다.  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>대량 삽입 및 업데이트를 위한 긴 데이터 제공  
 **SQLBulkOperations**에 대한 호출에 의해 수행되는 대량 삽입 및 업데이트에 대해 긴 데이터를 제공할 수 있습니다. 긴 데이터를 삽입하거나 업데이트하기 위해 응용 프로그램은 이 항목의 앞에서 "대량 삽입 수행" 및 "책갈피를 사용하여 대량 업데이트 수행" 섹션에 설명된 단계 외에도 다음 단계를 수행합니다.  
  
1.  **SQLBindCol을**사용하여 데이터를 바인딩할 때 응용 프로그램은 실행 시 데이터 열에 대한 * \*TargetValuePtr* 버퍼에 열 번호와 같은 응용 프로그램 정의 값을 배치합니다. 이 값은 나중에 열을 식별하는 데 사용할 수 있습니다.  
  
     응용 프로그램은*SQL_LEN_DATA_AT_EXEC(길이)* 매크로의 결과를 * \*StrLen_or_IndPtr* 버퍼에 배치합니다. 열의 SQL 데이터 형식이 SQL_LONGVARBINARY, SQL_LONGVARCHAR 또는 긴 데이터 원본별 데이터 형식이고 드라이버가 **SQLGetInfo의**SQL_NEED_LONG_DATA_LEN 정보 형식에 대해 "Y"를 반환하는 경우 *길이는* 매개 변수에 대해 전송할 데이터의 바이트 수입니다. 그렇지 않으면 음수값이 아닌 값이어야 하며 무시됩니다.  
  
2.  **SQLBulkOperations가** 호출될 때 실행 시 데이터 열이 있는 경우 함수는 SQL_NEED_DATA 반환하고 다음 단계 3단계로 진행됩니다. (실행 시 데이터 열이 없는 경우 프로세스가 완료됩니다.)  
  
3.  응용 프로그램은 **SQLParamData를** 호출하여 처리될 첫 번째 데이터 실행 열에 대한 * \*TargetValuePtr* 버퍼의 주소를 검색합니다. **SQLParamData는** SQL_NEED_DATA 반환합니다. 응용 프로그램은 * \*TargetValuePtr* 버퍼에서 응용 프로그램 정의 값을 검색합니다.  
  
    > [!NOTE]  
    >  실행 시 데이터 매개 변수는 실행 시 데이터 열과 유사하지만 **SQLParamData에서** 반환하는 값은 각각 다릅니다.  
  
     실행 시 데이터 열은 행이 **SQLBulkOperations**로 업데이트되거나 삽입될 때 **데이터가 SQLPutData로** 전송되는 행 집합의 열입니다. **SQLBindCol.** **SQLParamData에서** 반환되는 값은 처리 중인 **TargetValuePtr* 버퍼의 행 주소입니다.  
  
4.  응용 프로그램은 **SQLPutData를** 열에 대한 데이터를 보내기 위해 하나 이상 호출합니다. **SQLPutData에**지정된 * \*TargetValuePtr* 버퍼에서 모든 데이터 값을 반환할 수 없는 경우 두 개 이상의 호출이 필요합니다. 동일한 열에 대한 **SQLPutData에** 대한 여러 호출은 문자, 이진 또는 데이터 원본별 데이터 형식이 있는 열에 문자 C 데이터를 보내거나 문자, 이진 또는 데이터 원본별 데이터 형식이 있는 열로 이진 C 데이터를 보낼 때만 허용됩니다.  
  
5.  응용 프로그램은 **SQLParamData를** 다시 호출하여 열에 대해 모든 데이터가 전송되었음을 알릴 수 있습니다.  
  
    -   실행 시 데이터 열이 더 많은 경우 **SQLParamData는** SQL_NEED_DATA 반환하고 다음 실행 시 데이터 열이 처리될 *TargetValuePtr* 버퍼의 주소를 반환합니다. 응용 프로그램은 4 단계와 5단계를 반복합니다.  
  
    -   실행 시 데이터 열이 더 이상 없는 경우 프로세스가 완료됩니다. 명령문이 성공적으로 실행된 경우 **SQLParamData는** SQL_SUCCESS 반환하거나 SQL_SUCCESS_WITH_INFO. 실행이 실패하면 SQL_ERROR 반환합니다. 이 시점에서 **SQLParamData** **SQLBulkOperations**.  
  
 작업이 취소 되거나 **SQLBulkOperations** SQL_NEED_DATA 반환 하 고 모든 데이터 실행 열에 대 한 데이터를 전송 하기 전에 **SQLParaData** 또는 **SQLPutData에서** 오류가 발생 하는 경우 응용 프로그램은 **SQLCancel**, **SQLGetDiagField, SQLGetDiagOr,** **SQLGetDiagFunctions, SQLGetFunctions,** **SQLParamData,** 또는 **SQLPutData** 문과 관련 된 연결에 대 한 호출할 수 있습니다. **SQLGetDiagRec** 명령문 또는 문과 연결된 연결에 대한 다른 함수를 호출하는 경우 함수는 SQL_ERROR 및 SQLSTATE HY010(함수 시퀀스 오류)을 반환합니다.  
  
 응용 프로그램에서 **SQLCancel을** 호출하는 동안 드라이버는 여전히 실행 시 데이터 열에 대한 데이터가 필요하면 드라이버는 작업을 취소합니다. 그런 다음 응용 프로그램은 **SQLBulkOperations를** 다시 호출할 수 있습니다. 취소는 커서 상태 또는 현재 커서 위치에 영향을 주지 않습니다.  
  
## <a name="row-status-array"></a>행 상태 배열  
 행 상태 배열에는 **SQLBulkOperations**를 호출한 후 행 집합의 각 데이터 행에 대한 상태 값이 포함되어 있습니다. 드라이버는 **SQLFetch,** **SQLFetchScroll,** **SQLSetPos**또는 **SQLBulkOperations를**호출한 후 이 배열의 상태 값을 설정합니다. 이 배열은 **SQLBulkOperations** 전에 **SQLFetch** 또는 **SQLFetchScroll가** 호출되지 않은 경우 **SQLBulkOperations에**대한 호출로 처음 채워집니다. 이 배열은 SQL_ATTR_ROW_STATUS_PTR 문 특성을 가리켰습니다. 행 상태 배열의 요소 수는 행 집합의 행 수와 같아야 합니다(SQL_ATTR_ROW_ARRAY_SIZE 문 특성에 의해 정의됨). 이 행 상태 배열에 대한 자세한 내용은 [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)를 참조하십시오.  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서는 Customers 테이블에서 한 번에 10개의 데이터 행을 가져옵니다. 그런 다음 사용자에게 수행하라는 메시지를 표시합니다. 네트워크 트래픽을 줄이기 위해 예제 버퍼는 바운드 배열에서 로컬로 업데이트, 삭제 및 삽입하지만 행 집합 데이터를 지나오프셋에서 업데이트됩니다. 사용자가 데이터 원본에 업데이트, 삭제 및 삽입을 전송하도록 선택하면 코드는 바인딩 오프셋을 적절하게 설정하고 **SQLBulkOperations**를 호출합니다. 간단히 하기 위해 사용자는 10개 이상의 업데이트, 삭제 또는 삽입을 버퍼링할 수 없습니다.  
  
```cpp  
// SQLBulkOperations_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include "stdio.h"  
  
#define UPDATE_ROW 100  
#define DELETE_ROW 101  
#define ADD_ROW 102  
#define SEND_TO_DATA_SOURCE 103  
#define UPDATE_OFFSET 10  
#define INSERT_OFFSET 20  
#define DELETE_OFFSET 30  
  
// Define structure for customer data (assume 10 byte maximum bookmark size).  
typedef struct tagCustStruct {  
   SQLCHAR Bookmark[10];  
   SQLINTEGER BookmarkLen;  
   SQLUINTEGER CustomerID;  
   SQLINTEGER CustIDInd;  
   SQLCHAR CompanyName[51];  
   SQLINTEGER NameLenOrInd;  
   SQLCHAR Address[51];  
   SQLINTEGER AddressLenOrInd;  
   SQLCHAR Phone[11];  
   SQLINTEGER PhoneLenOrInd;  
} CustStruct;  
  
// Allocate 40 of these structures. Elements 0-9 are for the current rowset,  
// elements 10-19 are for the buffered updates, elements 20-29 are for  
// the buffered inserts, and elements 30-39 are for the buffered deletes.  
CustStruct CustArray[40];  
SQLUSMALLINT RowStatusArray[10], Action, RowNum, NumUpdates = 0, NumInserts = 0,  
NumDeletes = 0;  
SQLLEN BindOffset = 0;  
SQLRETURN retcode;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLHSTMT hstmt = NULL;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Set the following statement attributes:  
   // SQL_ATTR_CURSOR_TYPE:           Keyset-driven  
   // SQL_ATTR_ROW_BIND_TYPE:         Row-wise  
   // SQL_ATTR_ROW_ARRAY_SIZE:        10  
   // SQL_ATTR_USE_BOOKMARKS:         Use variable-length bookmarks  
   // SQL_ATTR_ROW_STATUS_PTR:        Points to RowStatusArray  
   // SQL_ATTR_ROW_BIND_OFFSET_PTR:   Points to BindOffset  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER)SQL_CURSOR_KEYSET_DRIVEN, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER)sizeof(CustStruct), 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_USE_BOOKMARKS, (SQLPOINTER)SQL_UB_VARIABLE, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_OFFSET_PTR, &BindOffset, 0);  
  
   // Bind arrays to the bookmark, CustomerID, CompanyName, Address, and Phone columns.  
   retcode = SQLBindCol(hstmt, 0, SQL_C_VARBOOKMARK, CustArray[0].Bookmark, sizeof(CustArray[0].Bookmark), &CustArray[0].BookmarkLen);  
   retcode = SQLBindCol(hstmt, 1, SQL_C_ULONG, &CustArray[0].CustomerID, 0, &CustArray[0].CustIDInd);  
   retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, CustArray[0].CompanyName, sizeof(CustArray[0].CompanyName), &CustArray[0].NameLenOrInd);  
   retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, CustArray[0].Address, sizeof(CustArray[0].Address), &CustArray[0].AddressLenOrInd);  
   retcode = SQLBindCol(hstmt, 4, SQL_C_CHAR, CustArray[0].Phone, sizeof(CustArray[0].Phone), &CustArray[0].PhoneLenOrInd);  
  
   // Execute a statement to retrieve rows from the Customers table.  
   retcode = SQLExecDirect(hstmt, (SQLCHAR*)"SELECT CustomerID, CompanyName, Address, Phone FROM Customers", SQL_NTS);  
  
   // Fetch and display the first 10 rows.  
   retcode = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
   // DisplayCustData(CustArray, 10);  
  
   // Call GetAction to get an action and a row number from the user.  
   // while (GetAction(&Action, &RowNum)) {  
   Action = SQL_FETCH_NEXT;  
   RowNum = 2;  
   switch (Action) {  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmt, Action, RowNum);  
         // DisplayCustData(CustArray, 10);  
         break;  
  
      case UPDATE_ROW:  
         // Check if we have reached the maximum number of buffered updates.  
         if (NumUpdates < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered updates section of CustArray, copy the bookmark of the row  
            // being updated to the same element, and increment the update counter.  
            // Checking to see we have not already buffered an update for this  
            // row not shown.  
            // GetNewCustData(CustArray, UPDATE_OFFSET + NumUpdates);  
            memcpy(CustArray[UPDATE_OFFSET + NumUpdates].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
            CustArray[UPDATE_OFFSET + NumUpdates].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
            NumUpdates++;  
         } else {  
            printf("Buffers full. Send buffered changes to the data source.");  
         }  
         break;  
      case DELETE_ROW:  
         // Check if we have reached the maximum number of buffered deletes.  
         if (NumDeletes < 10) {  
            // Copy the bookmark of the row being deleted to the next available element  
            // of the buffered deletes section of CustArray and increment the delete  
            // counter. Checking to see we have not already buffered an update for  
            // this row not shown.  
            memcpy(CustArray[DELETE_OFFSET + NumDeletes].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
  
            CustArray[DELETE_OFFSET + NumDeletes].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
  
            NumDeletes++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case ADD_ROW:  
         // reached maximum number of buffered inserts?  
         if (NumInserts < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered inserts section of CustArray and increment insert counter.  
            // GetNewCustData(CustArray, INSERT_OFFSET + NumInserts);  
            NumInserts++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case SEND_TO_DATA_SOURCE:  
         // If there are any buffered updates, inserts, or deletes, set the array size  
         // to that number, set the binding offset to use the data in the buffered  
         // update, insert, or delete part of CustArray, and call SQLBulkOperations to  
         // do the updates, inserts, or deletes. Because we will never have more than  
         // 10 updates, inserts, or deletes, we can use the same row status array.  
         if (NumUpdates) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumUpdates, 0);  
            BindOffset = UPDATE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_UPDATE_BY_BOOKMARK);  
            NumUpdates = 0;  
         }  
  
         if (NumInserts) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumInserts, 0);  
            BindOffset = INSERT_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_ADD);  
            NumInserts = 0;  
         }  
  
         if (NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumDeletes, 0);  
            BindOffset = DELETE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_DELETE_BY_BOOKMARK);  
            NumDeletes = 0;  
         }  
  
         // If there were any updates, inserts, or deletes, reset the binding offset  
         // and array size to their original values.  
         if (NumUpdates || NumInserts || NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
            BindOffset = 0;  
         }  
         break;  
   }  
   // }  
  
   // Close the cursor.  
   SQLFreeStmt(hstmt, SQL_CLOSE);  
}  
```  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|데이터 블록 가져오기 또는 결과 집합 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|설명자의 단일 필드 얻기|[SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|설명자의 여러 필드 얻기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|설명자의 단일 필드 설정|[SQLSetDesc필드 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|설명자의 여러 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|커서 위치 지정, 행 집합의 데이터 새로 고침 또는 행 집합의 데이터 업데이트 또는 삭제|[SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
