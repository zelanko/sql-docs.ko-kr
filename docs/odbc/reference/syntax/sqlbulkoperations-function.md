---
title: SQLBulkOperations 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBulkOperations
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBulkOperations
helpviewer_keywords:
- SQLBulkOperations function [ODBC]
ms.assetid: 7029d0da-b0f2-44e6-9114-50bd96f47196
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 496148e51e56ebbeea239101660b37e45cfa7eba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036173"
---
# <a name="sqlbulkoperations-function"></a>SQLBulkOperations 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ODBC  
  
 **요약**  
 **SQLBulkOperations** 대량 책갈피 및 대량 삽입 수행 업데이트 등과 같은 작업을 삭제 및 책갈피에서 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *연산*  
 [입력] 수행할 연산입니다.  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARK SQL_DELETE_BY_BOOKMARK SQL_FETCH_BY_BOOKMARK  
  
 자세한 내용은 "설명입니다."을 참조 하세요.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLBulkOperations** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* 의 호출 및 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLBulkOperations** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 앞 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 . 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
 다중 행 작업의 하나 또는 더 많은 전부는 아니지만, 행에 오류가 발생 하 고에서 오류가 발생할 경우 SQL_ERROR가 반환 하는 경우 모든 해당 SQLSTATEs SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR (제외 01xxx SQLSTATEs) 반환할 수 있는, sql_success_with_info가 반환 됩니다는 단일 행 작업입니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|합니다 *작업* 인수가 SQL_FETCH_BY_BOOKMARK, 및의 공백이 아닌 문자 또는 NULL이 아닌 이진 데이터 잘림이 발생 하는 문자열 또는 이진 데이터를 SQL_C_CHAR 또는 SQL_C_BINARY 데이터 형식의 열 또는 열에 대해 반환 합니다.|  
|01S01|행에 오류가 있습니다.|합니다 *작업* 인수 SQL_ADD, 및 작업을 수행 하는 동안 하나 이상의 행에 오류가 발생 했지만 하나 이상의 행에 추가 되었습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)<br /><br /> (이 오류는 ODBC 2를 사용 하 여 응용 프로그램 작동 하는 경우에 발생 됩니다. *x* 드라이버입니다.)|  
|01S07|소수 잘림|합니다 *작업* 인수가 SQL_FETCH_BY_BOOKMARK, 응용 프로그램 버퍼의 데이터 형식을 SQL_C_CHAR 또는 SQL_C_BINARY 없습니다 및 하나 이상의 열에 대 한 응용 프로그램 버퍼에 반환 된 데이터가 잘렸습니다. (숫자 C 데이터 형식에 대 한 수의 소수 부분이 잘렸습니다. 시간, 타임 스탬프 및 시간 구성 요소를 포함 하는 간격 C 데이터 형식에 대 한 시간의 소수 부분을 잘렸습니다.)<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07006|제한 된 데이터 형식 특성을 위반 했습니다.|합니다 *작업이* 인수가 SQL_FETCH_BY_BOOKMARK, 및에서 지정한 데이터 형식으로 결과 집합에 있는 열의 데이터 값을 변환할 수 없습니다는 *TargetType* 에대한호출에서인수**SQLBindCol**합니다.<br /><br /> 합니다 *작업* 인수 SQL_UPDATE_BY_BOOKMARK 되었거나 SQL_ADD, 및 결과 집합의 열 데이터 형식으로 응용 프로그램 버퍼에 데이터 값을 변환할 수 없습니다.|  
|07009|잘못 된 설명자 인덱스입니다.|인수 *작업* SQL_ADD, 되어 결과 집합의 열 수보다 큰 열 번호를 사용 하 여 열 바인딩 되었습니다.|  
|21S02|파생된 테이블의 단계가 열 목록과 일치 하지 않습니다.|인수 *작업* SQL_UPDATE_BY_BOOKMARK; 되었으며 모든 열이 바인딩되지 않은 또는 읽기 전용 된 또는 바인딩된 길이/표시기 버퍼의 값이 SQL_COLUMN_IGNORE 때문에 열을 업데이트할 수 있는 되었습니다.|  
|22001|문자열 데이터 오른쪽 잘림|(문자)에 대 한 비어 있지 않은 값 또는 null이 아닌 (이진)에 대 한 문자 또는 바이트 잘리는 문자 또는 이진 값을 결과 집합의 열에에서 할당이 했습니다.|  
|22003|숫자 값 범위를 벗어났습니다.|합니다 *작업* 인수 SQL_ADD 되었거나 SQL_UPDATE_BY_BOOKMARK, 및 결과 집합의 열에에서 숫자 값으로 할당 (소수) 대신 전체 부분 잘릴 수 수를 발생 합니다.<br /><br /> 인수 *작업* SQL_FETCH_BY_BOOKMARK, 되었으며 하나 이상의 바인딩된 열에 대 한 숫자 값이 반환 되 었어야 하지만 유효 자릿수 손실입니다.|  
|22007|잘못 된 날짜/시간 형식|합니다 *작업* 인수 SQL_ADD 되었거나 SQL_UPDATE_BY_BOOKMARK, 및 연도, 월 또는 일 필드 범위를 벗어났거나 인해 발생 하는 결과 집합의 열에 날짜 또는 타임 스탬프 값을 할당 합니다.<br /><br /> 인수 *작업* SQL_FETCH_BY_BOOKMARK, 되었으며 하나 이상의 바인딩된 열에 대 한 날짜 또는 타임 스탬프 값이 반환 되 었어야 하지만 연도, 월 또는 일 필드를 범위를 벗어났습니다.|  
|22008|날짜/시간 필드 오버플로가|합니다 *작업* 인수 SQL_ADD 되었거나 SQL_UPDATE_BY_BOOKMARK, 및 (연도, 월, 일, 시간, 분 또는 초를 날짜/시간 필드에서 발생 한 날짜/시간 산술 연산을 결과 집합의 열으로 전송 되는 데이터의 성능 필드에 대 한 대체 값의 범위에 속하지 않습니다 또는 잘못 된 일반 달력의 날짜/시간에 대 한 자연 스러운 규칙을 기준으로 결과의 필드).<br /><br /> 합니다 *작업* 인수가 SQL_FETCH_BY_BOOKMARK, 및의 datetime 필드 (연도, 월, 일, 시간, 분, 또는 두 번째 필드)에서 발생 한 날짜/시간 산술 연산을 결과 집합에서 검색 중인 데이터의 성능을 합니다 결과 필드에 대 한 대체 값의 범위에 속하지 않습니다 또는 잘못 된 일반 달력의 날짜/시간에 대 한 자연 스러운 규칙 기반으로 합니다.|  
|22015|간격 필드 오버플로|합니다 *작업* 인수 SQL_ADD 되었거나 SQL_UPDATE_BY_BOOKMARK, 및 했기 때문에 유효 자릿수의 손실 된 정확한 숫자의 할당 또는 SQL 데이터 형식 설정 된 간격 C 간격 유형입니다.<br /><br /> 합니다 *작업* 인수 SQL_ADD 되었거나 SQL_UPDATE_BY_BOOKMARK; 간격 SQL 형식에 할당할 때 간격 SQL 형식 C 형식 값의 표현이 없는 했습니다.<br /><br /> 합니다 *작업* 인수가 SQL_FETCH_BY_BOOKMARK, 및 선행 필드에 유효 자릿수의 손실 발생 한 정확한 수치 또는 간격 SQL 형식에서 C 간격 유형을 할당 합니다.<br /><br /> 합니다 *작업* 인수가 SQL_FETCH_BY_BOOKMARK; 간격 C 형식에 할당할 때 C 간격 유형으로 SQL 형식의 값 표현 방식이 없기 했습니다.|  
|22018|캐스트 사양의 문자 값|합니다 *작업* 인수가 SQL_FETCH_BY_BOOKMARK; C 형식은 정확 하거나 대략적인 숫자, datetime, 또는 간격 데이터 형식; 열의 SQL 형식이 된 문자 데이터 형식으로 되어 열에 값을 잘못 되었습니다. 바인딩된 C 형식의 리터럴입니다.<br /><br /> 인수 *작업* SQL_ADD 되었거나 SQL_UPDATE_BY_BOOKMARK;는 정확 하거나 대략적인 숫자, datetime, 또는 간격 데이터 형식이 SQL 유형은; C 형식 SQL_C_CHAR; 되어 열의 값이 유효한 리터럴 합니다 바인딩된 SQL 형식입니다.|  
|23000|무결성 제약 조건 위반|합니다 *작업* 인수가 SQL_ADD, SQL_DELETE_BY_BOOKMARK, 또는 SQL_UPDATE_BY_BOOKMARK, 및는 무결성 제약 조건을 위반 했습니다.<br /><br /> 합니다 *작업* 인수가 SQL_ADD, 및 열을 찾을 수 없습니다. 기본값이 없는 NOT NULL로 정의 됩니다.<br /><br /> 합니다 *작업이* SQL_ADD, 경계에서 지정 된 길이 인수가 *StrLen_or_IndPtr* 버퍼가 SQL_COLUMN_IGNORE, 및 열에 기본값이 없는 합니다.|  
|24000|잘못된 커서 상태|합니다 *StatementHandle* 실행 상태가 되었지만 결과 집합이 연관 된 합니다 *StatementHandle*합니다.|  
|40001|Serialization 오류|트랜잭션은 다른 트랜잭션과 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 하지 못했으며 트랜잭션의 상태를 확인할 수 없습니다.|  
|42000|구문 오류 또는 액세스 위반|드라이버에서 요청 된 작업을 수행 하는 데 필요한 대로 행을 잠글 수 없습니다. 합니다 *작업* 인수입니다.|  
|44000|WITH CHECK OPTION 위반|합니다 *작업이* 인수가 SQL_ADD 있고 SQL_UPDATE_BY_BOOKMARK, 삽입 또는 업데이트가 표시 테이블에서 수행 된 (또는 본된 테이블에서 파생 된 테이블)을 지정 하 여 만들어진 **WITH CHECK OPTION**에 삽입 영향을 받는 하나 이상의 행 또는 업데이트를 볼된 테이블에 더 이상 하는 방식입니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*합니다. 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 가 호출 된 *StatementHandle*합니다. 함수에서 다시 호출 된 다음 합니다 *StatementHandle*합니다.<br /><br /> 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLBulkOperations** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) 지정 된 *StatementHandle* 실행 상태가 없습니다. 이 함수가 먼저 호출 하지 않고 호출 **SQLExecDirect**를 **SQLExecute**, 또는 카탈로그 함수입니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLSetPos** 에 대해 호출 된 합니다 *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.<br /><br /> (DM) 드라이버는 ODBC 2 되었습니다. *x* 드라이버와 **SQLBulkOperations** 에 대해 호출 된를 *StatementHandle* 전에 **SQLFetchScroll** 또는 **SQLFetch**  호출 되었습니다.<br /><br /> (DM) **SQLBulkOperations** 후 호출 되었습니다 **SQLExtendedFetch** 가 호출 된 *StatementHandle*합니다.|  
|HY011|특성을 지금 설정할 수 없습니다.|(DM) 드라이버는 ODBC 2 되었습니다. *x* 드라이버 및 SQL_ATTR_ROW_STATUS_PTR 문 특성에 대 한 호출 사이 설정 된 **SQLFetch** 하거나 **SQLFetchScroll** 고 **SQLBulkOperations** .|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|합니다 *작업* 인수 SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK; 데이터 값이 null 포인터; C 데이터 형식 SQL_C_BINARY 되었거나 SQL_C_CHAR; 되어 열 길이 값이 0 보다 작거나 되었지만 SQL_DATA_AT_EXEC 다음과 같지 않은 경우 SQL_COLUMN_IGNORE, SQL_NTS, SQL_NULL_DATA, 또는 SQL_LEN_DATA_AT_EXEC_OFFSET 작거나 합니다.<br /><br /> 길이/표시기 버퍼의 값이 SQL_DATA_AT_EXEC; SQL 형식 되었거나 SQL_LONGVARCHAR, SQL_LONGVARBINARY에는 긴 데이터 소스 특정 데이터 형식 SQL_NEED_LONG_DATA_LEN 정보 입력 **SQLGetInfo** "Y" 되었습니다.<br /><br /> 합니다 *작업* 인수가 SQL_ADD, SQL_ATTR_USE_BOOKMARK 문 특성이 SQL_UB_VARIABLE로 설정 된 및 0 열이 결과 집합에 대 한 책갈피에 대 한 최대 길이 같은 길이가 없습니다. 버퍼에 바인딩 되었습니다. (이 길이 IRD의 SQL_DESC_OCTET_LENGTH 필드 수 및 호출 하 여 가져올 수 있습니다 **SQLDescribeCol**하십시오 **SQLColAttribute**, 또는 **SQLGetDescField**.)|  
|HY092|잘못 된 특성 식별자|(DM)에 대 한 지정 된 값을 *작업* 인수가 잘못 되었습니다.<br /><br /> 합니다 *작업* 인수가 SQL_ADD, SQL_UPDATE_BY_BOOKMARK, 또는 SQL_DELETE_BY_BOOKMARK, 및 문 특성 SQL_ATTR_CONCURRENCY를 SQL_CONCUR_READ_ONLY로 설정 합니다.<br /><br /> 합니다 *작업* 인수가 SQL_DELETE_BY_BOOKMARK, SQL_FETCH_BY_BOOKMARK, 또는 SQL_UPDATE_BY_BOOKMARK, 및 책갈피 열이 바인딩되지 않았습니다 또는 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_OFF로 설정 되었습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|드라이버 또는 데이터 원본에서 요청 된 작업을 지원 하지 않습니다 합니다 *작업* 인수입니다.|  
|HYT00|제한 시간이 만료되었습니다.|쿼리 제한 시간에는 데이터 원본의 결과 집합을 반환 하기 전에 만료 되었습니다. 시간 제한 기간을 통해 설정 됩니다 **SQLSetStmtAttr** 사용 하 여는 *특성* SQL_ATTR_QUERY_TIMEOUT의 인수입니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
  
> [!CAUTION]  
>  문에 상태에 대 한 자세한 **SQLBulkOperations** 호출할 수 있습니다 ODBC 2를 사용 하 여 호환성을 위해 필요한 작업 및. *x* 응용 프로그램을 표시 합니다 [블록 커서, 스크롤 가능 커서 및 이전 버전과 호환성](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 섹션의 부록 g: 이전 버전과 호환성에 대 한 드라이버 지침입니다.  
  
 응용 프로그램에서 사용 **SQLBulkOperations** 기본 테이블 또는 현재 쿼리에 해당 하는 보기에서 다음 작업을 수행 합니다.  
  
-   새 행을 추가 합니다.  
  
-   각 행 책갈피도 식별 되는 행 집합을 업데이트 합니다.  
  
-   각 행 책갈피도 식별 되는 행 집합을 삭제 합니다.  
  
-   각 행 책갈피도 식별 되는 행 집합을 가져옵니다.  
  
 호출한 후 **SQLBulkOperations**를 블록 커서 위치가 정의 되지 않습니다. 응용 프로그램은 호출 **SQLFetchScroll** 커서 위치를 설정 합니다. 응용 프로그램에서 호출 해야 **SQLFetchScroll** 만 *FetchOrientation* SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE, 또는에서는 SQL_FETCH_BOOKMARK의 인수입니다. 응용 프로그램을 호출 하는 경우에 커서 위치가 정의 되지 않습니다 **SQLFetch** 하거나 **SQLFetchScroll** 사용 하 여는 *FetchOrientation* SQL_FETCH_PRIOR SQL_FETCH_NEXT, 인수 또는 SQL_FETCH_RELATIVE 합니다.  
  
 호출 하 여 수행 되는 대량 작업에서 열을 무시할 수 있습니다 **SQLBulkOperations** 에 대 한 호출에 지정 된 열 길이/표시기 버퍼를 설정 하 여 **SQLBindCol**, SQL_COLUMN_IGNORE 하 합니다.  
  
 호출할 때 SQL_ATTR_ROW_OPERATION_PTR 문 특성을 설정 하려면 응용 프로그램에 대 한 필요는 없습니다 **SQLBulkOperations** 있으므로이 함수를 사용 하 여 대량 작업을 수행 하는 경우 행을 무시할 수 없습니다.  
  
 SQL_ATTR_ROWS_FETCHED_PTR 문 특성에서 가리키는 버퍼를 호출 하 여 영향을 받는 행의 개수가 **SQLBulkOperations**합니다.  
  
 경우는 *작업* 인수가 SQL_ADD 이거나 SQL_UPDATE_BY_BOOKMARK 및 커서와 연결 된 쿼리 사양의 선택 목록에 동일한 열 참조가 둘 이상의 드라이버-정의 된 오류가 있는지 여부를 생성 또는 드라이버 중복 된 참조를 무시 하 고 요청 된 작업을 수행 합니다.  
  
 사용 하는 방법에 대 한 자세한 **SQLBulkOperations**를 참조 하십시오 [SQLBulkOperations 사용 하 여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)합니다.  
  
## <a name="performing-bulk-inserts"></a>대량 삽입을 수행  
 사용 하 여 데이터를 삽입할 **SQLBulkOperations**, 응용 프로그램에 다음 일련의 단계를 수행 합니다.  
  
1.  결과 집합을 반환 하는 쿼리를 실행 합니다.  
  
2.  삽입 하고자 하는 행의 수 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 설정 합니다.  
  
3.  호출 **SQLBindCol** 삽입 하고자 하는 데이터를 바인딩합니다. 데이터 크기와 동일한 SQL_ATTR_ROW_ARRAY_SIZE의 값을 가진 배열에 바인딩됩니다.  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_ARRAY_SIZE 같거나 SQL_ATTR_ROW_STATUS_PTR null 포인터 여야 합니다 SQL_ATTR_ROW_STATUS_PTR 문 특성에서 가리키는 배열 크기 여야 합니다.  
  
4.  호출 **SQLBulkOperations**(*StatementHandle,* SQL_ADD) 삽입 하는 데 있습니다.  
  
5.  응용 프로그램 SQL_ATTR_ROW_STATUS_PTR 문 특성에 설정한 경우 작업의 결과를 보려면이 배열을 검사할 수 있습니다.  
  
 응용 프로그램 호출 하기 전에 0 열을 바인딩하는 경우 **SQLBulkOperations** 사용 하 여는 *작업* SQL_ADD의 인수를 드라이버에 대 한 책갈피 값을 사용 하 여 0의 바인딩된 열 버퍼를 업데이트 합니다는 새로 행을 삽입 합니다. 이 위해서는 응용 프로그램 해야 SQL_ATTR_USE_BOOKMARKS 문 특성을 설정할 SQL_UB_VARIABLE 문을 실행 하기 전에. (이 작동 하지 않습니다는 ODBC 2. *x* 드라이버입니다.)  
  
 Long 데이터 여 추가할 수 있습니다 지역의 SQLBulkOperations를 호출 SQLParamData 및 SQLPutData를 사용 하 여 합니다. 자세한 내용은 뒷부분에서는이 함수 참조 "를 제공 하 긴 데이터에 대 한 대량 삽입 및 업데이트"를 참조 하세요.  
  
 호출 응용 프로그램에 대 한 필요는 없습니다 **SQLFetch** 하거나 **SQLFetchScroll** 호출 하기 전에 **SQLBulkOperations** (는 ODBC 2에 대 한 경우를 제외 하 고. *x* 드라이버; 참조 [이전 버전과 호환성 및 표준 준수](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)).  
  
 동작은 드라이버에서 정의 된 경우 **SQLBulkOperations**를 사용 하 여는 *작업* SQL_ADD, 인수의 중복 열을 포함 하는 커서에 대해 호출 됩니다. 드라이버를 드라이버에서 정의 된 SQLSTATE를 반환, 추가 결과에 표시 되는 첫 번째 열에 데이터 집합 또는 다른 드라이버에서 정의 된 동작을 수행할 수 있습니다.  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>책갈피를 사용 하 여 대량 업데이트를 수행 합니다.  
 사용 하 여 책갈피를 사용 하 여 대량 업데이트를 수행할 **SQLBulkOperations**, 시퀀스에서 다음 단계를 수행 하는 응용 프로그램:  
  
1.  SQL_UB_VARIABLE를 SQL_ATTR_USE_BOOKMARKS 문 특성을 설정합니다.  
  
2.  결과 집합을 반환 하는 쿼리를 실행 합니다.  
  
3.  업데이트 하고자 하는 행의 수 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 설정 합니다.  
  
4.  호출 **SQLBindCol** 업데이트 하고자 하는 데이터를 바인딩합니다. 데이터 크기와 동일한 SQL_ATTR_ROW_ARRAY_SIZE의 값을 가진 배열에 바인딩됩니다. 또한 호출 **SQLBindCol** 0 (책갈피 열) 열을 바인딩합니다.  
  
5.  복사는 관심 있는 배열에 업데이트 된 행에 대 한 책갈피 0 열에 바인딩됩니다.  
  
6.  바인딩된 버퍼에 데이터를 업데이트합니다.  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 문 특성에서 가리키는 배열 크기는 SQL_ATTR_ROW_ARRAY_SIZE 같거나 SQL_ATTR_ROW_STATUS_PTR에 대 한 null 포인터가 되어야 합니다. 이어야 합니다.  
  
7.  호출 **SQLBulkOperations**(*StatementHandle,* SQL_UPDATE_BY_BOOKMARK).  
  
    > [!NOTE]  
    >  응용 프로그램 SQL_ATTR_ROW_STATUS_PTR 문 특성에 설정한 경우 작업의 결과를 보려면이 배열을 검사할 수 있습니다.  
  
8.  필요에 따라 호출 **SQLBulkOperations**(*StatementHandle*, SQL_FETCH_BY_BOOKMARK) 업데이트 되었음을 확인 하려면 바인딩된 응용 프로그램 버퍼에 데이터를 인출 합니다.  
  
9. 데이터 업데이트 된 드라이버 SQL_ROW_UPDATED를 적절 한 행에 대 한 행 상태 배열 값을 변경 합니다.  
  
 대량 업데이트를 수행한 **SQLBulkOperations** 호출을 사용 하 여 긴 데이터를 포함할 수 있습니다 **SQLParamData** 하 고 **SQLPutData**합니다. 자세한 내용은 뒷부분에서는이 함수 참조 "를 제공 하 긴 데이터에 대 한 대량 삽입 및 업데이트"를 참조 하세요.  
  
 응용 프로그램을 호출 하지 않아도 책갈피 커서에서 지속 되 면 **SQLFetch** 하거나 **SQLFetchScroll** 책갈피를 업데이트 하기 전에 합니다. 이전 커서에서 저장 된 책갈피 사용할 수 있습니다. 호출 응용 프로그램은 책갈피 커서 간에 지속 되지 않습니다, 경우 **SQLFetch** 또는 **SQLFetchScroll** 에 책갈피를 검색 합니다.  
  
 동작은 드라이버에서 정의 된 경우 **SQLBulkOperations**를 사용 하 여는 *작업* SQL_UPDATE_BY_BOOKMARK, 인수의 중복 열을 포함 하는 커서에 대해 호출 됩니다. 드라이버를 드라이버에서 정의 된 SQLSTATE를 반환, 결과 집합에 표시 되는 첫 번째 열을 업데이트 하거나 다른 드라이버에서 정의 된 동작을 수행할 수 있습니다.  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>책갈피를 사용 하 여 인출 수행  
 사용 하 여 책갈피를 사용 하 여 대량 인출 하는 데 **SQLBulkOperations**, 응용 프로그램 시퀀스에서 다음 단계를 수행 합니다.  
  
1.  SQL_UB_VARIABLE를 SQL_ATTR_USE_BOOKMARKS 문 특성을 설정합니다.  
  
2.  결과 집합을 반환 하는 쿼리를 실행 합니다.  
  
3.  인출 하려는 행의 수 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 설정 합니다.  
  
4.  호출 **SQLBindCol** 인출 하고자 하는 데이터를 바인딩할 합니다. 데이터 크기와 동일한 SQL_ATTR_ROW_ARRAY_SIZE의 값을 가진 배열에 바인딩됩니다. 또한 호출 **SQLBindCol** 0 (책갈피 열) 열을 바인딩합니다.  
  
5.  복사는 관심 있는 배열로 가져오는 행에 대 한 책갈피 0 열에 바인딩됩니다. (이 가정 하는 응용 프로그램을 이미 받은 책갈피 별도로.)  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 문 특성에서 가리키는 배열 크기는 SQL_ATTR_ROW_ARRAY_SIZE 같거나 SQL_ATTR_ROW_STATUS_PTR에 대 한 null 포인터가 되어야 합니다. 이어야 합니다.  
  
6.  호출 **SQLBulkOperations**(*StatementHandle,* SQL_FETCH_BY_BOOKMARK).  
  
7.  응용 프로그램 SQL_ATTR_ROW_STATUS_PTR 문 특성에 설정한 경우 작업의 결과를 보려면이 배열을 검사할 수 있습니다.  
  
 응용 프로그램을 호출 하지 않아도 책갈피 커서에서 지속 되 면 **SQLFetch** 하거나 **SQLFetchScroll** 책갈피에서 페치 하기 전에 합니다. 이전 커서에서 저장 된 책갈피 사용할 수 있습니다. 호출 응용 프로그램은 책갈피 커서 간에 지속 되지 않는, 하는 경우 **SQLFetch** 하거나 **SQLFetchScroll** 책갈피를 검색 하는 한 번입니다.  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>책갈피를 사용 하 여 삭제 수행  
 사용 하 여 책갈피를 사용 하 여 대량 삭제 하는 데 **SQLBulkOperations**, 시퀀스에서 다음 단계를 수행 하는 응용 프로그램:  
  
1.  SQL_UB_VARIABLE를 SQL_ATTR_USE_BOOKMARKS 문 특성을 설정합니다.  
  
2.  결과 집합을 반환 하는 쿼리를 실행 합니다.  
  
3.  삭제 하려는 행의 수 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 설정 합니다.  
  
4.  호출 **SQLBindCol** 0 (책갈피 열) 열을 바인딩합니다.  
  
5.  복사는 관심 있는 배열로 삭제 된 행에 대 한 책갈피 0 열에 바인딩됩니다.  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 문 특성에서 가리키는 배열 크기는 SQL_ATTR_ROW_ARRAY_SIZE 같거나 SQL_ATTR_ROW_STATUS_PTR에 대 한 null 포인터가 되어야 합니다. 이어야 합니다.  
  
6.  호출 **SQLBulkOperations**(*StatementHandle,* SQL_DELETE_BY_BOOKMARK).  
  
7.  응용 프로그램 SQL_ATTR_ROW_STATUS_PTR 문 특성에 설정한 경우 작업의 결과를 보려면이 배열을 검사할 수 있습니다.  
  
 응용 프로그램 호출 되지 않은 책갈피 커서에서 지속 되 면 **SQLFetch** 하거나 **SQLFetchScroll** 책갈피를 삭제 하기 전에 합니다. 이전 커서에서 저장 된 책갈피 사용할 수 있습니다. 호출 응용 프로그램은 책갈피 커서 간에 지속 되지 않는, 하는 경우 **SQLFetch** 하거나 **SQLFetchScroll** 책갈피를 검색 하는 한 번입니다.  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>대량 삽입 및 업데이트에 대 한 Long 데이터를 제공합니다.  
 대량 삽입 및 업데이트에 대 한 호출을 수행한에 대 한 long 데이터를 제공할 수 있습니다 **SQLBulkOperations**합니다. 를 삽입 하거나 긴 데이터를 업데이트 하려면 응용 프로그램에는이 항목의 앞부분에 나오는 "대량 삽입 수행" 및 "수행 대량 업데이트를 사용 하 여 책갈피" 섹션에 설명 된 단계 외에 다음 단계를 수행 합니다.  
  
1.  때 사용 하 여 데이터를 바인딩되기 **SQLBindCol**, 응용 프로그램에서 열 번호와 같은 응용 프로그램 정의 값을 배치 합니다  *\*TargetValuePtr* 실행 시 데이터에 대 한 버퍼 열입니다. 열을 식별 하는 값을 나중에 사용할 수 있습니다.  
  
     응용 프로그램을 SQL_LEN_DATA_AT_EXEC의 결과 배치 (*길이*)에서 매크로  *\*StrLen_or_IndPtr* 버퍼입니다. SQL 데이터 형식의 열 SQL_LONGVARBINARY, SQL_LONGVARCHAR 또는 long 데이터 소스 관련 데이터 형식이 고 드라이버 "Y" SQL_NEED_LONG_DATA_LEN 정보 유형에 대해에서 반환 **SQLGetInfo**, *길이*  ; 매개 변수에 대해 보낼 데이터의 바이트 수이 고, 그렇지 음수가 아닌 값 이어야 하 고 무시 됩니다.  
  
2.  때 **SQLBulkOperations** 실행 시 데이터 열, 함수는 SQL_NEED_DATA 반환 및 3 단계를 따라 진행 하는 경우 호출 됩니다. (실행 시 데이터 열이 없는 경우 프로세스 완료 되었습니다.)  
  
3.  응용 프로그램 호출 **SQLParamData** 의 주소를 검색 합니다  *\*TargetValuePtr* 처리할 첫 번째 실행 시 데이터 열에 대 한 버퍼입니다. **SQLParamData** SQL_NEED_DATA를 반환 합니다. 응용 프로그램에서 응용 프로그램 정의 값을 검색 하는  *\*TargetValuePtr* 버퍼입니다.  
  
    > [!NOTE]  
    >  반환 되는 값 이지만 실행 시 데이터 매개 변수가 실행 시 데이터 열과 비슷한 **SQLParamData** 마다 다릅니다.  
  
     실행 시 데이터 열이 있는 데이터를 보낼 사용 하 여 행 집합의 열 **SQLPutData** 행을 업데이트 하거나 삽입 하는 경우 **SQLBulkOperations**합니다. 사용 하 여 바인딩된 **SQLBindCol**합니다. 반환한 값 **SQLParamData** 행의 주소는 **TargetValuePtr* 처리 중인 버퍼입니다.  
  
4.  응용 프로그램 호출 **SQLPutData** 한 번 이상 열에 대 한 데이터를 보내도록 합니다. 번 이상 호출 하는 경우 모든 데이터 값 반환 될 수 없습니다는  *\*TargetValuePtr* 에 지정 된 버퍼 **SQLPutData**;에 대 한 여러 호출은 **SQLPutData** 문자, 이진 또는 데이터 소스 특정 데이터 형식의 열에 문자 데이터를 전송 하는 경우에 또는 문자를 이진 열에 이진 C 데이터를 보낼 때 동일한 열 수 또는 데이터 소스 특정 데이터 형식에 대 한 합니다.  
  
5.  응용 프로그램 호출 **SQLParamData** 열에 대 한 모든 데이터를 보냈는지는 신호를 다시 합니다.  
  
    -   더 많은 실행 시 데이터 열이 없으면 **SQLParamData** SQL_NEED_DATA 및 주소를 반환 합니다 *TargetValuePtr* 처리할 다음 실행 시 데이터 열에 대 한 버퍼입니다. 응용 프로그램 4, 5 단계를 반복합니다.  
  
    -   더 이상 실행 시 데이터 열이 있는 경우에 프로세스가 완료 되었습니다. 문이 성공적으로 실행 된 경우 **SQLParamData** SQL_SUCCESS 또는; SQL_SUCCESS_WITH_INFO를 반환 합니다. 실행 하지 못했습니다 SQL_ERROR를 반환 합니다. 이때 **SQLParamData** 에서 반환 될 수 있는 모든 SQLSTATE를 반환할 수 있습니다 **SQLBulkOperations**합니다.  
  
 작업이 취소 되었습니다. 또는 오류가 발생 하는 경우 **SQLParamData** 또는 **SQLPutData** 후 **SQLBulkOperations** SQL_NEED_DATA를 반환 합니다. 모든 데이터를 보내기 전에 및 실행 시 데이터 열을 응용 프로그램 에서만 호출할 수 있습니다 **SQLCancel**를 **SQLGetDiagField**하십시오 **SQLGetDiagRec**, **SQLGetFunctions** , **SQLParamData**, 또는 **SQLPutData** 문이나 문과 사용 하 여 관련 연결에 대 한 합니다. 함수는 SQL_ERROR 및 SQLSTATE HY010 반환 문이나 문과 사용 하 여 관련 연결에 대 한 다른 함수를 호출 하는 경우 (함수 시퀀스 오류).  
  
 응용 프로그램을 호출 하는 경우 **SQLCancel** 드라이버 실행 시 데이터 열에 대 한 데이터를 필요로 하, 동안 드라이버 작업을 취소 합니다. 응용 프로그램을 호출할 수 있습니다 **SQLBulkOperations** 다시 취소 영향을 주지 않습니다 커서 상태 또는 현재 커서 위치입니다.  
  
## <a name="row-status-array"></a>행 상태 배열  
 호출한 후 각 행 집합의 데이터 행에 대 한 상태 값을 포함 하는 행 상태 배열이 **SQLBulkOperations**합니다. 드라이버를 호출한 후이 배열에 상태 값을 설정 해도 **SQLFetch**, **SQLFetchScroll**합니다 **SQLSetPos**, 또는 **SQLBulkOperations** . 호출 하 여이 배열의 처음 채워집니다 **SQLBulkOperations** 하는 경우 **SQLFetch** 하거나 **SQLFetchScroll** 하기 전에 호출 되지 않았습니다 **SQLBulkOperations** . 이 배열 SQL_ATTR_ROW_STATUS_PTR 문 특성에 의해 가리킵니다. 행 상태 배열에 있는 요소의 수 (SQL_ATTR_ROW_ARRAY_SIZE 문 특성에 의해 정의 됨)으로 행 집합의 행 수와 같아야 합니다. 이 행 상태 배열에 대 한 정보를 참조 하세요 [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)합니다.  
  
## <a name="code-example"></a>코드 예  
 다음 예에서는 Customers 테이블에서 한 번에 10 개의 데이터 행을 인출합니다. 그런 다음 사용자가 취해야 할 작업에 대 한 메시지가 나타납니다. 네트워크 사용량을 줄이기 위해 예제에서는 버퍼 업데이트, 삭제 및 바인딩된 배열의 하지만 이전의 행 집합 데이터 오프셋 로컬 삽입 합니다. 사용자 업데이트, 삭제를 보내도록 선택 하 고 데이터 원본에 삽입 하는 경우 코드 오프셋을 적절 하 게 바인딩을 설정 하 고 호출 **SQLBulkOperations**합니다. 간단히 하기 위해 10 개 업데이트, 삭제 또는 삽입 사용자 버퍼 수 없습니다.  
  
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
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|데이터 블록을 인출 또는 결과 통해 스크롤 설정|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|설명자의 단일 필드 가져오기|[SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|설명자의 여러 필드 가져오기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|설명자의 단일 필드를 설정합니다.|[SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|설명자의 여러 필드를 설정합니다.|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|커서를 놓고, 행 집합에서 데이터 새로 고침, 업데이트 또는 행 집합의 데이터 삭제|[SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
