---
title: SQLBulkOperations 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 60bcb6851adeba08105dabd6fb0800d2e969a04e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343177"
---
# <a name="sqlbulkoperations-function"></a>SQLBulkOperations 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수: ODBC  
  
 **요약**  
 **SQLBulkOperations** 는 update, delete 및 fetch by 책갈피를 비롯 한 대량 삽입 및 대량 책갈피 작업을 수행 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *연산*  
 입력 수행할 작업:  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARK SQL_DELETE_BY_BOOKMARK SQL_FETCH_BY_BOOKMARK  
  
 자세한 내용은 "설명"을 참조 하십시오.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLBulkOperations** 에서 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 *HandleType의 SQL_HANDLE_STMT* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. . 다음 표에서는 일반적으로 **SQLBulkOperations** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR입니다.  
  
 SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR (01xxx SQLSTATEs 제외)를 반환할 수 있는 모든 SQLSTATEs의 경우에는 한 개 이상의 행 작업에 오류가 발생 하는 경우 SQL_SUCCESS_WITH_INFO가 반환 되 고, 다음에 오류가 발생 하면 SQL_ERROR가 반환 됩니다. 단일 행 작업  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터 오른쪽 잘림|*작업* 인수는 SQL_FETCH_BY_BOOKMARK이 고 데이터 형식이 SQL_C_CHAR 또는 SQL_C_BINARY 인 열에 대해 반환 된 문자열 또는 이진 데이터는 비어 있지 않은 문자 또는 NULL이 아닌 이진 데이터를 잘렸습니다.|  
|01S01|행에 오류가 있습니다.|작업 *인수는* SQL_ADD 작업을 수행 하는 동안 하나 이상의 행에 오류가 발생 했지만 하나 이상의 행이 성공적으로 추가 되었습니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.<br /><br /> 이 오류는 응용 프로그램에서 ODBC 2를 사용 하는 경우에만 발생 합니다. *x* 드라이버)|  
|01S07|소수 잘림|*작업* 인수가 SQL_FETCH_BY_BOOKMARK 이거나, 응용 프로그램 버퍼의 데이터 형식이 SQL_C_CHAR 또는 SQL_C_BINARY이 아니거나, 하나 이상의 열에 대 한 응용 프로그램 버퍼에 반환 된 데이터가 잘렸습니다. 숫자 C 데이터 형식의 경우 숫자의 소수 부분이 잘렸습니다. 시간 구성 요소를 포함 하는 time, timestamp 및 interval C 데이터 형식의 경우 시간의 소수 부분이 잘렸습니다.<br /><br /> 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|07006|제한 된 데이터 형식 특성 위반|*작업* 인수는 SQL_FETCH_BY_BOOKMARK이 고 결과 집합에 있는 열의 데이터 값을 **SQLBindCol**에 대 한 호출의 *TargetType* 인수에 지정 된 데이터 형식으로 변환할 수 없습니다.<br /><br /> *작업* 인수가 SQL_UPDATE_BY_BOOKMARK 또는 SQL_ADD이 고 응용 프로그램 버퍼의 데이터 값을 결과 집합에 있는 열의 데이터 형식으로 변환할 수 없습니다.|  
|07009|잘못 된 설명자 인덱스|인수 *연산이* SQL_ADD 열이 결과 집합의 열 수보다 많은 열 번호와 바인딩 되었습니다.|  
|21S02|파생 테이블의 수준이 열 목록과 일치 하지 않습니다.|인수 *작업* 은 SQL_UPDATE_BY_BOOKMARK입니다. 모든 열이 언바운드 또는 읽기 전용 이거나 바인딩된 길이/지표 버퍼의 값이 SQL_COLUMN_IGNORE 때문에 업데이트할 열이 없습니다.|  
|22001|문자열 데이터 오른쪽 잘림|결과 집합의 열에 문자 또는 이진 값을 할당 하 여 비어 있지 않은 문자 (문자) 또는 null이 아닌 문자 또는 바이트를 잘렸습니다.|  
|22003|숫자 값이 범위를 벗어났습니다.|*작업* 인수는 SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK이 고, 결과 집합의 열에 숫자 값을 할당 하는 경우에는 소수 자릿수와는 반대로 소수 부분이 잘립니다.<br /><br /> 인수 *연산이* SQL_FETCH_BY_BOOKMARK 하나 이상의 바인딩된 열에 대해 숫자 값을 반환 하면 유효 자릿수가 손실 될 수 있습니다.|  
|22007|날짜/시간 형식이 잘못 되었습니다.|*작업* 인수가 SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK이 고 결과 집합의 열에 날짜 또는 타임 스탬프 값을 할당 하 여 year, month 또는 day 필드가 범위를 벗어났습니다.<br /><br /> 인수 *연산이* SQL_FETCH_BY_BOOKMARK, 하나 이상의 바인딩된 열에 대해 날짜 또는 타임 스탬프 값을 반환 하면 year, month 또는 day 필드가 범위를 벗어납니다.|  
|22008|날짜/시간 필드 오버플로입니다.|*작업* 인수는 SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK이 고, 결과 집합의 열로 전송 되는 데이터에 대 한 datetime 산술 연산은 결과의 날짜/시간 필드 (연도, 월, 일, 시, 분 또는 초 필드)로 나타났습니다. 날짜/시간에 대 한 양력의 자연 규칙에 따라 필드의 허용 되는 값 범위를 벗어났거나 유효 하지 않습니다.<br /><br /> *작업* 인수는 SQL_FETCH_BY_BOOKMARK이 고 결과 집합에서 검색 되는 데이터에 대 한 datetime 산술 연산으로 인해 결과의 datetime 필드 (연도, 월, 일, 시, 분 또는 초 필드)가 날짜/시간에 대 한 양력의 자연 규칙에 따라 필드의 허용 되는 범위 또는 유효 하지 않은 값의 범위입니다.|  
|22015|간격 필드 오버플로입니다.|*작업* 인수는 SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK이 고, 정확한 숫자 또는 간격 C 유형을 interval SQL 데이터 형식에 할당 하면 유효 자릿수가 손실 됩니다.<br /><br /> *작업* 인수가 SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK입니다. interval SQL 형식에 할당할 때 interval SQL 형식에 C 형식의 값이 표시 되지 않았습니다.<br /><br /> *작업* 인수는 SQL_FETCH_BY_BOOKMARK이 고 정확한 숫자 또는 간격 SQL 형식에서 interval C 형식으로 할당 하면 선행 필드에 유효 자릿수가 손실 됩니다.<br /><br /> *작업* 인수가 SQL_FETCH_BY_BOOKMARK입니다. 간격 C 유형에 할당할 때 간격 C 유형에 서 SQL 유형의 값을 표시 하지 않았습니다.|  
|22018|캐스트 사양에 대 한 문자 값이 잘못 되었습니다.|*작업* 인수가 SQL_FETCH_BY_BOOKMARK입니다. C 형식은 정확한 수치 또는 근사치, datetime 또는 interval 데이터 형식입니다. 열의 SQL 형식이 문자 데이터 형식입니다. 열에 있는 값이 바인딩된 C 형식의 올바른 리터럴이 아닙니다.<br /><br /> 인수 *작업* 은 SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK입니다. SQL 형식은 정확한 수치 또는 근사치, datetime 또는 interval 데이터 형식입니다. C 형식은 SQL_C_CHAR입니다. 열 값이 바인딩된 SQL 형식의 올바른 리터럴이 아닙니다.|  
|23000|무결성 제약 조건 위반|*작업* 인수가 SQL_ADD, SQL_DELETE_BY_BOOKMARK 또는 SQL_UPDATE_BY_BOOKMARK이 고 무결성 제약 조건을 위반 했습니다.<br /><br /> *작업* 인수는 SQL_ADD이 고 바인딩되지 않은 열은 not NULL로 정의 되며 기본값은 없습니다.<br /><br /> *작업* 인수가 SQL_ADD이 고, 바인딩된 *StrLen_or_IndPtr* buffer에 지정 된 길이가 SQL_COLUMN_IGNORE 되었고, 열에 기본값이 없습니다.|  
|24000|잘못된 커서 상태|*StatementHandle* 가 실행 된 상태 이지만 *StatementHandle*과 연결 된 결과 집합이 없습니다.|  
|40001|Serialization 오류|다른 트랜잭션과의 리소스 교착 상태가 발생 하 여 트랜잭션이 롤백 되었습니다.|  
|40003|문 완료를 알 수 없음|이 함수를 실행 하는 동안 연결 된 연결에 실패 하 여 트랜잭션의 상태를 확인할 수 없습니다.|  
|42000|구문 오류 또는 액세스 위반|드라이버에서 *작업* 인수에 요청 된 작업을 수행 하는 데 필요한 행을 잠글 수 없습니다.|  
|44000|WITH CHECK OPTION 위반|*작업* 인수는 SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK이 고, 삽입 또는 업데이트는 **WITH CHECK OPTION**을 지정 하 여 만든 표시 된 테이블 (또는 표시 된 테이블에서 파생 된 테이블)에서 수행 된 것으로, 하나 이상의 행에 대해 수행 되었습니다. 삽입 또는 업데이트의 영향을 받는는 더 이상 표시 되는 테이블에 표시 되지 않습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec에** 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.  *\**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소 됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 **sqlcancel** 또는 **Sqlcancelhandle** 이 *StatementHandle*에 대해 호출 되었습니다. 그런 다음 *StatementHandle*에서 함수를 다시 호출 했습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLBulkOperations** 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE이 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) 지정한 *StatementHandle* 가 실행 된 상태가 아닙니다. 함수가 먼저 **Sqlexecdirect**, **sqlexecute**또는 catalog 함수를 호출 하지 않고 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA이 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.<br /><br /> (DM) 드라이버가 ODBC 2 였습니다. **Sqlfetchscroll** 또는 **sqlfetch** 가 호출 되기 *전에 StatementHandle* 에 대 한 *x* 드라이버 및 **SQLBulkOperations** 가 호출 되었습니다.<br /><br /> (DM) **SQLBulkOperations** 가 *StatementHandle*에서 **sqlextendedfetch** 를 호출한 후에 호출 되었습니다.|  
|HY011|특성을 지금 설정할 수 없습니다.|(DM) 드라이버가 ODBC 2 였습니다. *x* 드라이버 및 SQL_ATTR_ROW_STATUS_PTR Statement 특성이 **Sqlfetch** 또는 **sqlfetchscroll** 및 **SQLBulkOperations**호출 사이에서 설정 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|*작업* 인수가 SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK입니다. 데이터 값이 null 포인터가 아닙니다. C 데이터 형식은 SQL_C_BINARY 또는 SQL_C_CHAR입니다. 열 길이 값이 0 보다 작지만 SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NTS 또는 SQL_NULL_DATA와 같지 않거나 SQL_LEN_DATA_AT_EXEC_OFFSET 보다 작거나 같습니다.<br /><br /> 길이/표시기 버퍼의 값이 SQL_DATA_AT_EXEC 되었습니다. SQL 형식은 SQL_LONGVARCHAR, SQL_LONGVARBINARY 또는 long 데이터 원본에 특정 한 데이터 형식입니다. **SQLGetInfo** 의 SQL_NEED_LONG_DATA_LEN information 형식은 "Y" 였습니다.<br /><br /> *작업* 인수는 SQL_ADD이 고 SQL_ATTR_USE_BOOKMARK statement 특성은 SQL_UB_VARIABLE로 설정 되었으며 열 0은 길이가이 결과 집합에 대 한 책갈피의 최대 길이와 같지 않은 버퍼에 바인딩되어 있습니다. 이 길이는 IRD의 SQL_DESC_OCTET_LENGTH 필드에서 사용할 수 있으며 **SQLDescribeCol**, **sqlcolattribute**또는 **SQLGetDescField**를 호출 하 여 가져올 수 있습니다.|  
|HY092|특성 식별자가 잘못 되었습니다.|(DM) *작업* 인수에 지정 된 값이 잘못 되었습니다.<br /><br /> *작업* 인수는 SQL_ADD, SQL_UPDATE_BY_BOOKMARK 또는 SQL_DELETE_BY_BOOKMARK이 고 SQL_ATTR_CONCURRENCY statement 특성은 SQL_CONCUR_READ_ONLY로 설정 되었습니다.<br /><br /> *작업* 인수가 SQL_DELETE_BY_BOOKMARK, SQL_FETCH_BY_BOOKMARK 또는 SQL_UPDATE_BY_BOOKMARK이 고 책갈피 열이 바인딩되지 않았거나 SQL_ATTR_USE_BOOKMARKS STATEMENT 특성이 SQL_UB_OFF로 설정 되었습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|드라이버 또는 데이터 원본이 *작업* 인수에서 요청 된 작업을 지원 하지 않습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에서 결과 집합을 반환 하기 전에 쿼리 제한 시간이 만료 되었습니다. 제한 시간은 SQL_ATTR_QUERY_TIMEOUT의 *특성* 인수를 사용 하 여 **SQLSetStmtAttr** 를 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출에서 SQL_STILL_EXECUTING를 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
  
> [!CAUTION]  
>  에서 **SQLBulkOperations** 을 호출할 수 있는 문 및 ODBC 2와의 호환성을 위해 수행 해야 하는 작업에 대 한 자세한 내용은을 (를) 확인 하십시오. *x* 응용 프로그램에 대 [](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 한 자세한 내용은 부록 G: 이전 버전과의 호환성을 위한 드라이버 지침  
  
 응용 프로그램은 **SQLBulkOperations** 를 사용 하 여 현재 쿼리에 해당 하는 기본 테이블 또는 뷰에서 다음 작업을 수행 합니다.  
  
-   새 행을 추가 합니다.  
  
-   각 행이 책갈피에 의해 식별 되는 행 집합을 업데이트 합니다.  
  
-   각 행이 책갈피에 의해 식별 되는 행 집합을 삭제 합니다.  
  
-   각 행이 책갈피에 의해 식별 되는 행 집합을 인출 합니다.  
  
 **SQLBulkOperations**를 호출한 후에는 블록 커서 위치가 정의 되지 않습니다. 응용 프로그램은 **Sqlfetchscroll** 을 호출 하 여 커서 위치를 설정 해야 합니다. 응용 프로그램은 SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE 또는 SQL_FETCH_BOOKMARK의 *Fetchorientation* 인수를 사용 하 여 **sqlfetchscroll** 만 호출 해야 합니다. 응용 프로그램에서 SQL_FETCH_PRIOR, SQL_FETCH_NEXT 또는 SQL_FETCH_RELATIVE의 *Fetchorientation* 인수를 사용 하 여 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하면 커서 위치가 정의 되지 않습니다.  
  
 **SQLBindCol**에 대 한 호출에 지정 된 열 길이/표시 버퍼를 SQL_COLUMN_IGNORE로 설정 하 여 **SQLBulkOperations** 를 호출 하 여 수행 된 대량 작업에서 열을 무시할 수 있습니다.  
  
 이 함수를 사용 하 여 대량 작업을 수행 하는 경우에는 행을 무시할 수 없기 때문에 응용 프로그램에서 **SQLBulkOperations** 를 호출할 때 SQL_ATTR_ROW_OPERATION_PTR statement 특성을 설정할 필요가 없습니다.  
  
 SQL_ATTR_ROWS_FETCHED_PTR statement 특성에 의해 가리키는 버퍼에는 **SQLBulkOperations**에 대 한 호출의 영향을 받는 행 수가 포함 되어 있습니다.  
  
 *작업* 인수가 SQL_ADD 또는 SQL_UPDATE_BY_BOOKMARK이 고 커서와 연결 된 쿼리 사양의 선택 목록에 동일한 열에 대 한 참조가 두 개 이상 포함 되어 있는 경우 오류가 생성 되었는지 여부에 관계 없이 드라이버가 정의 됩니다. 드라이버가 중복 된 참조를 무시 하 고 요청 된 작업을 수행 합니다.  
  
 **SQLBulkOperations**를 사용 하는 방법에 대 한 자세한 내용은 SQLBulkOperations를 사용 하 [여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)를 참조 하세요.  
  
## <a name="performing-bulk-inserts"></a>대량 삽입 수행  
 **SQLBulkOperations**를 사용 하 여 데이터를 삽입 하기 위해 응용 프로그램은 다음과 같은 일련의 단계를 수행 합니다.  
  
1.  결과 집합을 반환 하는 쿼리를 실행 합니다.  
  
2.  SQL_ATTR_ROW_ARRAY_SIZE statement 특성을 삽입 하려는 행 수로 설정 합니다.  
  
3.  **SQLBindCol** 를 호출 하 여 삽입 하려는 데이터를 바인딩합니다. 데이터는 크기가 SQL_ATTR_ROW_ARRAY_SIZE의 값과 같은 배열에 바인딩됩니다.  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR statement 특성이 가리키는 배열의 크기는 SQL_ATTR_ROW_ARRAY_SIZE 또는 SQL_ATTR_ROW_STATUS_PTR가 null 포인터 여야 합니다.  
  
4.  **SQLBulkOperations**(*StatementHandle,* SQL_ADD)를 호출 하 여 삽입을 수행 합니다.  
  
5.  응용 프로그램에서 SQL_ATTR_ROW_STATUS_PTR statement 특성을 설정한 경우이 배열을 검사 하 여 작업 결과를 볼 수 있습니다.  
  
 응용 프로그램이 SQL_ADD의 *작업* 인수를 사용 하 여 **SQLBulkOperations** 를 호출 하기 전에 열 0을 바인딩하는 경우 드라이버는 새로 삽입 된 행의 책갈피 값으로 바인딩된 열 0 버퍼를 업데이트 합니다. 이를 위해서는 응용 프로그램이 문을 실행 하기 전에 SQL_ATTR_USE_BOOKMARKS statement 특성을 SQL_UB_VARIABLE로 설정 해야 합니다. ODBC 2에서는 작동 하지 않습니다. *x* 드라이버)  
  
 SQLParamData 및 Sqlparamdata에 대 한 호출을 사용 하 여 SQLBulkOperations에 의해 긴 데이터를 추가할 수 있습니다. 자세한 내용은이 함수 참조의 뒷부분에 나오는 "대량 삽입 및 업데이트를 위한 긴 데이터 제공"을 참조 하세요.  
  
 응용 프로그램에서 SQLBulkOperations를 호출 하기 전에 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하는  것은 필요 하지 않습니다 (ODBC 2로 이동 하는 경우 제외). *x* 드라이버 [이전 버전과의 호환성 및 표준 준수를](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)참조 하세요.)  
  
 SQL_ADD의 *작업* 인수를 사용 하 여 **SQLBulkOperations**가 중복 된 열이 포함 된 커서에 대해 호출 되는 경우이 동작은 드라이버에 정의 됩니다. 드라이버는 드라이버 정의 SQLSTATE를 반환 하거나, 결과 집합에 표시 되는 첫 번째 열에 데이터를 추가 하거나, 다른 드라이버 정의 동작을 수행할 수 있습니다.  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>책갈피를 사용 하 여 대량 업데이트 수행  
 **SQLBulkOperations**와 함께 책갈피를 사용 하 여 대량 업데이트를 수행 하기 위해 응용 프로그램에서는 다음 단계를 순서 대로 수행 합니다.  
  
1.  SQL_ATTR_USE_BOOKMARKS statement 특성을 SQL_UB_VARIABLE로 설정 합니다.  
  
2.  결과 집합을 반환 하는 쿼리를 실행 합니다.  
  
3.  SQL_ATTR_ROW_ARRAY_SIZE statement 특성을 업데이트 하려는 행 수로 설정 합니다.  
  
4.  **SQLBindCol** 를 호출 하 여 업데이트 하려는 데이터를 바인딩합니다. 데이터는 크기가 SQL_ATTR_ROW_ARRAY_SIZE의 값과 같은 배열에 바인딩됩니다. 또한 **SQLBindCol** 를 호출 하 여 열 0 (책갈피 열)을 바인딩합니다.  
  
5.  업데이트 하려는 행의 책갈피를 열 0에 바인딩된 배열에 복사 합니다.  
  
6.  바인딩된 버퍼의 데이터를 업데이트 합니다.  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR statement 특성이 가리키는 배열의 크기는 SQL_ATTR_ROW_ARRAY_SIZE 또는 SQL_ATTR_ROW_STATUS_PTR가 null 포인터 여야 합니다.  
  
7.  **SQLBulkOperations**(*StatementHandle,* SQL_UPDATE_BY_BOOKMARK)를 호출 합니다.  
  
    > [!NOTE]  
    >  응용 프로그램에서 SQL_ATTR_ROW_STATUS_PTR statement 특성을 설정한 경우이 배열을 검사 하 여 작업 결과를 볼 수 있습니다.  
  
8.  필요에 따라 **SQLBulkOperations**(*StatementHandle*, SQL_FETCH_BY_BOOKMARK)를 호출 하 여 바인딩된 응용 프로그램 버퍼로 데이터를 인출 하 여 업데이트가 발생 했는지 확인 합니다.  
  
9. 데이터가 업데이트 된 경우 드라이버는 해당 행에 대 한 행 상태 배열의 값을 SQL_ROW_UPDATED로 변경 합니다.  
  
 **SQLBulkOperations** 에서 수행 하는 대량 업데이트는 **sqlparamdata** 및 **sqlparamdata**에 대 한 호출을 사용 하 여 긴 데이터를 포함할 수 있습니다. 자세한 내용은이 함수 참조의 뒷부분에 나오는 "대량 삽입 및 업데이트를 위한 긴 데이터 제공"을 참조 하세요.  
  
 책갈피가 커서 사이에서 지속 되는 경우 응용 프로그램은 책갈피로 업데이트 하기 전에 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출할 필요가 없습니다. 이전 커서에서 저장 한 책갈피를 사용할 수 있습니다. 책갈피를 커서 간에 유지 하지 않는 경우 응용 프로그램에서 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하 여 책갈피를 검색 해야 합니다.  
  
 SQL_UPDATE_BY_BOOKMARK의 *작업* 인수를 사용 하 여 **SQLBulkOperations**가 중복 된 열이 포함 된 커서에 대해 호출 되는 경우이 동작은 드라이버에 정의 됩니다. 드라이버는 드라이버 정의 SQLSTATE를 반환 하거나, 결과 집합에 표시 되는 첫 번째 열을 업데이트 하거나, 기타 드라이버 정의 동작을 수행할 수 있습니다.  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>책갈피를 사용 하 여 대량 페치 수행  
 **SQLBulkOperations**에서 책갈피를 사용 하 여 대량 페치를 수행 하기 위해 응용 프로그램에서는 다음 단계를 순서 대로 수행 합니다.  
  
1.  SQL_ATTR_USE_BOOKMARKS statement 특성을 SQL_UB_VARIABLE로 설정 합니다.  
  
2.  결과 집합을 반환 하는 쿼리를 실행 합니다.  
  
3.  SQL_ATTR_ROW_ARRAY_SIZE statement 특성을 페치할 행 수로 설정 합니다.  
  
4.  **SQLBindCol** 를 호출 하 여 인출 하려는 데이터를 바인딩합니다. 데이터는 크기가 SQL_ATTR_ROW_ARRAY_SIZE의 값과 같은 배열에 바인딩됩니다. 또한 **SQLBindCol** 를 호출 하 여 열 0 (책갈피 열)을 바인딩합니다.  
  
5.  열 0에 바인딩된 배열에 인출 하려는 행의 책갈피를 복사 합니다. 이 경우 응용 프로그램에서 책갈피를 별도로 이미 가져온 것으로 가정 합니다.  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR statement 특성이 가리키는 배열의 크기는 SQL_ATTR_ROW_ARRAY_SIZE 또는 SQL_ATTR_ROW_STATUS_PTR가 null 포인터 여야 합니다.  
  
6.  **SQLBulkOperations**(*StatementHandle,* SQL_FETCH_BY_BOOKMARK)를 호출 합니다.  
  
7.  응용 프로그램에서 SQL_ATTR_ROW_STATUS_PTR statement 특성을 설정한 경우이 배열을 검사 하 여 작업 결과를 볼 수 있습니다.  
  
 책갈피가 커서 사이에서 지속 되는 경우 응용 프로그램은 책갈피를 인출 하기 전에 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출할 필요가 없습니다. 이전 커서에서 저장 한 책갈피를 사용할 수 있습니다. 책갈피를 커서 간에 유지 하지 않는 경우 응용 프로그램은 한 번만 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하 여 책갈피를 검색 합니다.  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>책갈피를 사용 하 여 대량 삭제 수행  
 **SQLBulkOperations**와 함께 책갈피를 사용 하 여 대량 삭제를 수행 하기 위해 응용 프로그램에서는 다음 단계를 순서 대로 수행 합니다.  
  
1.  SQL_ATTR_USE_BOOKMARKS statement 특성을 SQL_UB_VARIABLE로 설정 합니다.  
  
2.  결과 집합을 반환 하는 쿼리를 실행 합니다.  
  
3.  SQL_ATTR_ROW_ARRAY_SIZE statement 특성을 삭제 하려는 행 수로 설정 합니다.  
  
4.  **SQLBindCol** 을 호출 하 여 열 0 (책갈피 열)을 바인딩합니다.  
  
5.  삭제 하려는 행의 책갈피를 열 0에 바인딩된 배열에 복사 합니다.  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR statement 특성이 가리키는 배열의 크기는 SQL_ATTR_ROW_ARRAY_SIZE 또는 SQL_ATTR_ROW_STATUS_PTR가 null 포인터 여야 합니다.  
  
6.  **SQLBulkOperations**(*StatementHandle,* SQL_DELETE_BY_BOOKMARK)를 호출 합니다.  
  
7.  응용 프로그램에서 SQL_ATTR_ROW_STATUS_PTR statement 특성을 설정한 경우이 배열을 검사 하 여 작업 결과를 볼 수 있습니다.  
  
 책갈피가 커서 사이에서 지속 되는 경우 책갈피를 삭제 하기 전에 응용 프로그램에서 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출할 필요가 없습니다. 이전 커서에서 저장 한 책갈피를 사용할 수 있습니다. 책갈피를 커서 간에 유지 하지 않는 경우 응용 프로그램은 한 번만 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하 여 책갈피를 검색 합니다.  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>대량 삽입 및 업데이트를 위한 긴 데이터 제공  
 **SQLBulkOperations**에 대 한 호출에 의해 수행 되는 대량 삽입 및 업데이트에 대해 Long 데이터를 제공할 수 있습니다. 긴 데이터를 삽입 하거나 업데이트 하기 위해 응용 프로그램은이 항목의 앞부분에 나오는 "대량 삽입 수행" 및 "책갈피를 사용 하 여 대량 업데이트 수행" 섹션에 설명 된 단계 외에 다음 단계를 수행 합니다.  
  
1.  **SQLBindCol**를 사용 하 여 데이터를 바인딩할 때 응용 프로그램은 실행 시 데이터 열에 대 한  *\*targetvalueptr* 버퍼에 열 번호와 같은 응용 프로그램 정의 값을 배치 합니다. 나중에이 값을 사용 하 여 열을 식별할 수 있습니다.  
  
     응용 프로그램은 SQL_LEN_DATA_AT_EXEC (*길이*) 매크로의 결과를  *\*StrLen_or_IndPtr* 버퍼에 저장 합니다. 열의 SQL 데이터 형식이 SQL_LONGVARBINARY, SQL_LONGVARCHAR 또는 long 데이터 원본 관련 데이터 형식이 고 드라이버에서 **SQLGetInfo**의 SQL_NEED_LONG_DATA_LEN 정보 형식에 대해 "Y"를 반환 하는 경우 *길이* 는 데이터의 바이트 수입니다. 매개 변수에 대해 전송 됩니다. 그렇지 않으면 음수가 아닌 값 이어야 하며 무시 됩니다.  
  
2.  **SQLBulkOperations** 가 호출 될 때 실행 시 데이터 열이 있는 경우 함수는 SQL_NEED_DATA를 반환 하 고 다음에 나오는 3 단계로 진행 합니다. 실행 시 데이터 열이 없으면 프로세스가 완료 된 것입니다.  
  
3.  응용 프로그램은 **sqlparamdata** 를 호출 하 여 처리할 첫 번째 실행 시 데이터 열에 대 한  *\*targetvalueptr* 버퍼의 주소를 검색 합니다. **Sqlparamdata** 는 SQL_NEED_DATA을 반환 합니다. 응용 프로그램이  *\*targetvalueptr* 버퍼에서 응용 프로그램 정의 값을 검색 합니다.  
  
    > [!NOTE]  
    >  실행 시 데이터 매개 변수는 실행 시 데이터 열과 비슷하지만 **Sqlparamdata** 에서 반환 되는 값은 서로 다릅니다.  
  
     실행 시 데이터 열은 **SQLBulkOperations**를 사용 하 여 행을 업데이트 하거나 삽입할 때 **sqlputdata** 를 사용 하 여 데이터를 전송 하는 행 집합의 열입니다. **SQLBindCol**와 바인딩됩니다. **Sqlparamdata** 에서 반환 되는 값은 처리 중인 **Targetvalueptr* 버퍼의 행 주소입니다.  
  
4.  응용 프로그램은 **Sqlputdata** 를 한 번 이상 호출 하 여 열에 대 한 데이터를 보냅니다. **Sqlputdata**에 지정 된  *\*targetvalueptr* 버퍼에 모든 데이터 값을 반환할 수 없는 경우 두 개 이상의 호출이 필요 합니다. 동일한 열에 대 한 **sqlputdata** 에 대 한 여러 호출은 문자 C 데이터를 보내는 경우에만 허용 됩니다. 문자, 이진 또는 데이터 원본 관련 데이터 형식이 있는 열 또는 이진 C 데이터를 문자, 이진 또는 데이터 원본 관련 데이터 형식의 열로 보내는 경우  
  
5.  응용 프로그램은 **Sqlparamdata** 를 다시 호출 하 여 열에 대해 모든 데이터가 전송 되었음을 알립니다.  
  
    -   실행 시 데이터 열이 더 있는 경우 **Sqlparamdata** 는 다음에 처리할 실행 시 데이터 열에 대해 SQL_NEED_DATA 및 *Targetvalueptr* 버퍼의 주소를 반환 합니다. 응용 프로그램은 4 단계와 5 단계를 반복 합니다.  
  
    -   실행 시 데이터 열이 더 이상 없으면 프로세스가 완료 된 것입니다. 문이 성공적으로 실행 된 경우 **Sqlparamdata** 는 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO을 반환 합니다. 실행에 실패 한 경우 SQL_ERROR를 반환 합니다. 이 시점에서 **Sqlparamdata** 는 **SQLBulkOperations**에서 반환 될 수 있는 모든 SQLSTATE를 반환할 수 있습니다.  
  
 **SQLBulkOperations** 이 SQL_NEED_DATA를 반환 하 고 모든 실행 시 데이터 열에 대해 데이터가 전송 되기 전에 작업이 취소 되거나 sqlparamdata 또는 **sqlparamdata** **에서 오류가** 발생 하는 경우 응용 프로그램은 sqlcancel만 호출할 수 있습니다. , **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **Sqlparamdata**또는 문에 대 한 **sqlparamdata** 또는 문과 연결 된 연결입니다. 문에 대 한 다른 함수 또는 문과 연결 된 연결을 호출 하는 경우 함수는 SQL_ERROR 및 SQLSTATE HY010 (함수 시퀀스 오류)를 반환 합니다.  
  
 드라이버가 실행 시 데이터 열에 대 한 데이터를 필요로 하는 동안 **Sqlcancel** 을 호출 하면 드라이버에서 작업을 취소 합니다. 그러면 응용 프로그램은 **SQLBulkOperations** 를 다시 호출할 수 있습니다. 취소 해도 커서 상태나 현재 커서 위치에는 영향을 주지 않습니다.  
  
## <a name="row-status-array"></a>행 상태 배열  
 행 상태 배열에는 **SQLBulkOperations**를 호출한 후 행 집합의 각 데이터 행에 대 한 상태 값이 포함 됩니다. 이 드라이버는 **Sqlfetch**, **sqlfetchscroll**, **SQLSetPos**또는 **SQLBulkOperations**를 호출한 후이 배열의 상태 값을 설정 합니다. **SQLBulkOperations**전에 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하지 않은 경우이 배열은 처음에 **SQLBulkOperations** 에 대 한 호출로 채워집니다. 이 배열은 SQL_ATTR_ROW_STATUS_PTR statement 특성에 의해 가리킵니다. 행 상태 배열의 요소 수는 SQL_ATTR_ROW_ARRAY_SIZE statement 특성에 정의 된 행 집합의 행 수와 같아야 합니다. 이 행 상태 배열에 대 한 자세한 내용은 [Sqlfetch](../../../odbc/reference/syntax/sqlfetch-function.md)를 참조 하십시오.  
  
## <a name="code-example"></a>코드 예  
 다음 예에서는 Customers 테이블에서 한 번에 10 개의 데이터 행을 인출 합니다. 그런 다음 사용자에 게 수행할 작업을 묻는 메시지를 표시 합니다. 네트워크 트래픽을 줄이기 위해 예제 버퍼는 바인딩된 배열에서 로컬로 업데이트, 삭제 및 삽입 하지만 행 집합 데이터를 지난 오프셋에서 삽입 합니다. 사용자가 업데이트, 삭제 및 데이터 소스에 삽입을 전송 하도록 선택 하면 코드에서 바인딩 오프셋을 적절 하 게 설정 하 고 **SQLBulkOperations**를 호출 합니다. 편의상 사용자는 10 개 이상의 업데이트, 삭제 또는 삽입을 버퍼링 할 수 없습니다.  
  
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
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|데이터 블록 가져오기 또는 결과 집합을 통한 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|설명자의 단일 필드 가져오기|[SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|설명자의 여러 필드 가져오기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|설명자의 단일 필드 설정|[SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|설명자의 여러 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|커서 위치 지정, 행 집합의 데이터 새로 고침 또는 행 집합의 데이터 업데이트 또는 삭제|[SQLSetPos 함수](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
