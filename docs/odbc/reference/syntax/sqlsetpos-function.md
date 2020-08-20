---
description: SQLSetPos 함수
title: SQLSetPos 함수 | Microsoft Docs
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
ms.openlocfilehash: 55741fba1dca898e087f4a992dfd7affbf3bcfcb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491233"
---
# <a name="sqlsetpos-function"></a>SQLSetPos 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **SQLSetPos** 는 행 집합에서 커서 위치를 설정 하 고 응용 프로그램에서 행 집합의 데이터를 새로 고치거 나 결과 집합의 데이터를 업데이트 하거나 삭제할 수 있도록 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLSetPos(  
      SQLHSTMT        StatementHandle,  
      SQLSETPOSIROW   RowNumber,  
      SQLUSMALLINT    Operation,  
      SQLUSMALLINT    LockType);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *RowNumber*  
 입력 *작업* 인수를 사용 하 여 지정 된 작업을 수행할 행 집합의 행 위치입니다. *RowNumber* 가 0 이면 행 집합의 모든 행에 작업이 적용 됩니다.  
  
 자세한 내용은 "설명"을 참조 하십시오.  
  
 *연산*  
 입력 수행할 작업:  
  
 SQL_POSITION SQL_REFRESH SQL_UPDATE SQL_DELETE  
  
> [!NOTE]
>  *작업* 인수의 SQL_ADD 값 *은 ODBC 3.x*에서 사용 되지 않습니다. ODBC *3.x* 드라이버는 이전 버전과의 호환성을 위해 SQL_ADD를 지원 해야 합니다. 이 기능은 SQL_ADD *작업* 을 사용 하 여 **SQLBulkOperations** 에 대 한 호출로 대체 되었습니다. ODBC *2.x 응용 프로그램이 odbc 2.x* *드라이버를* 사용 하 여 작동 하는 경우 드라이버 관리자는 SQL_ADD *작업* 으로 **SQLBulkOperations** 에 대 한 호출을 SQL_ADD *작업* 을 사용 하 여 **SQLSetPos** 에 매핑합니다.  
  
 자세한 내용은 "설명"을 참조 하십시오.  
  
 *LockType*  
 입력 *작업* 인수에 지정 된 작업을 수행한 후 행을 잠그는 방법을 지정 합니다.  
  
 SQL_LOCK_NO_CHANGE SQL_LOCK_EXCLUSIVE SQL_LOCK_UNLOCK  
  
 자세한 내용은 "설명"을 참조 하십시오.  
  
## <a name="returns"></a>반환  
  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLSetPos** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환할 때 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLSetPos** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
 SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR (01xxx SQLSTATEs 제외)를 반환할 수 있는 모든 SQLSTATEs의 경우 하나 이상의 행 작업에서 오류가 발생 하는 경우 SQL_SUCCESS_WITH_INFO가 반환 되 고 단일 행 작업에서 오류가 발생 하면 SQL_ERROR 반환 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01001|커서 작업 충돌|*작업* 인수가 SQL_DELETE 또는 SQL_UPDATE 되었으며 행 또는 둘 이상의 행이 삭제 되거나 업데이트 되지 않았습니다. 하나 이상의 행에 대 한 업데이트에 대 한 자세한 내용은 **SQLSetStmtAttr**의 SQL_ATTR_SIMULATE_CURSOR *특성* 에 대 한 설명을 참조 하십시오. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.<br /><br /> *작업* 인수가 SQL_DELETE 또는 SQL_UPDATE 되었으며 낙관적 동시성 때문에 작업이 실패 했습니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터 오른쪽 잘림|*작업* 인수가 SQL_REFRESH 되었거나 데이터 형식이 SQL_C_CHAR 또는 SQL_C_BINARY 인 열에 대해 반환 된 문자열 또는 이진 데이터가 비어 있지 않은 문자 또는 NULL이 아닌 이진 데이터를 잘렸습니다.|  
|01S01|행에 오류가 있습니다.|*RowNumber* 인수가 0이 고 *작업* 인수를 사용 하 여 지정 된 작업을 수행 하는 동안 하나 이상의 행에서 오류가 발생 했습니다.<br /><br /> 하나 이상의 행 작업에서 오류가 발생 하는 경우 SQL_SUCCESS_WITH_INFO가 반환 되 고, 단일 행 작업에서 오류가 발생 하는 경우 SQL_ERROR 반환 됩니다.<br /><br /> 이 SQLSTATE는 *드라이버가 ODBC 2.x* 드라이버이 고 커서 라이브러리가 사용 되지 않는 경우 **sqlextendedfetch**후 **SQLSetPos** 가 호출 되는 경우에만 반환 됩니다.|  
|01S07|소수 잘림|*작업* 인수가 SQL_REFRESH 되었으며 응용 프로그램 버퍼의 데이터 형식이 SQL_C_CHAR 되지 않았거나 SQL_C_BINARY 하나 이상의 열에 대해 응용 프로그램 버퍼에 반환 된 데이터가 잘렸습니다. 숫자 데이터 형식의 경우 숫자의 소수 부분이 잘렸습니다. 시간 구성 요소를 포함 하는 time, timestamp 및 interval 데이터 형식의 경우 시간의 소수 부분이 잘렸습니다.<br /><br /> 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|07006|제한 된 데이터 형식 특성 위반|결과 집합에 있는 열의 데이터 값을 **SQLBindCol**에 대 한 호출의 *TargetType* 에 지정 된 데이터 형식으로 변환할 수 없습니다.|  
|07009|잘못 된 설명자 인덱스|인수 *연산이* SQL_REFRESH 되었거나 SQL_UPDATE 열이 결과 집합의 열 수보다 많은 열 번호를 사용 하 여 바인딩 되었습니다.|  
|21S02|파생 테이블의 수준이 열 목록과 일치 하지 않습니다.|인수 *작업이* SQL_UPDATE 되었으며 모든 열이 바인딩 해제 되었거나 읽기 전용 이거나 바인딩된 길이/지표 버퍼의 값이 SQL_COLUMN_IGNORE 되었으므로 열을 업데이트할 수 없습니다.|  
|22001|문자열 데이터, 오른쪽 잘림|*작업* 인수가 SQL_UPDATE 되었으며, 열에 문자 또는 이진 값을 할당 하 여 비어 있지 않은 문자 (문자) 또는 null이 아닌 문자 또는 바이트를 잘렸습니다.|  
|22003|숫자 값이 범위를 벗어났습니다.|인수 *연산이* SQL_UPDATE 되었으며 결과 집합의 열에 숫자 값을 할당 하 여 소수 부분에 대 한 전체 값이 잘릴 수 있습니다.<br /><br /> 인수 *연산이* SQL_REFRESH 되었으며 하나 이상의 바인딩된 열에 대해 숫자 값을 반환 하면 유효 자릿수가 손실 될 수 있습니다.|  
|22007|날짜/시간 형식이 잘못 되었습니다.|인수 *연산이* SQL_UPDATE 되었으며 결과 집합의 열에 날짜 또는 타임 스탬프 값을 할당 하 여 year, month 또는 day 필드가 범위를 벗어났습니다.<br /><br /> 인수 *연산이* SQL_REFRESH 되었으며 하나 이상의 바인딩된 열에 대해 날짜 또는 타임 스탬프 값을 반환 하면 year, month 또는 day 필드가 범위를 벗어납니다.|  
|22008|날짜/시간 필드 오버플로입니다.|*작업* 인수가 SQL_UPDATE 되었으며 결과 집합의 열로 전송 되는 데이터에 대 한 datetime 값이 필드에 대 한 허용 범위를 벗어났거나 날짜/시간에 대 한 양력의 자연 규칙에 따라 유효 하지 않은 날짜/시간 필드 (연도, 월, 일, 시, 분 또는 초 필드)가 발생 했습니다.<br /><br /> *작업* 인수가 SQL_REFRESH 되었으며 결과 집합에서 검색 되는 데이터에 대 한 datetime 값이 필드에 대 한 허용 범위를 벗어났거나 날짜/시간에 대 한 양력의 자연 규칙에 따라 유효 하지 않은 날짜/시간 필드 (연도, 월, 일, 시, 분 또는 초 필드)가 발생 했습니다.|  
|22015|간격 필드 오버플로입니다.|*작업* 인수가 SQL_UPDATE 되었으며 정확한 숫자 또는 간격 C 유형을 interval SQL 데이터 형식으로 할당 하면 유효 자릿수가 손실 됩니다.<br /><br /> *작업* 인수가 SQL_UPDATE 되었습니다. interval SQL 형식에 할당할 때 interval SQL 형식에 C 형식의 값이 표시 되지 않았습니다.<br /><br /> *작업* 인수가 SQL_REFRESH 되었으며 정확한 숫자 또는 간격 SQL 형식에서 interval C 형식으로 할당 하면 선행 필드에 유효 자릿수가 손실 됩니다.<br /><br /> *작업* 인수가 SQL_ 새로 고침입니다. 간격 C 유형에 할당할 때 간격 C 유형에 서 SQL 유형의 값을 표시 하지 않았습니다.|  
|22018|캐스트 사양에 대 한 문자 값이 잘못 되었습니다.|*작업* 인수가 SQL_REFRESH 되었습니다. C 형식은 정확한 수치 또는 근사치, datetime 또는 interval 데이터 형식입니다. 열의 SQL 형식이 문자 데이터 형식입니다. 열에 있는 값이 바인딩된 C 형식의 올바른 리터럴이 아닙니다.<br /><br /> 인수 *작업이* SQL_UPDATE 되었습니다. SQL 형식은 정확한 수치 또는 근사치, datetime 또는 interval 데이터 형식입니다. C 형식이 SQL_C_CHAR 되었습니다. 열 값이 바인딩된 SQL 형식의 올바른 리터럴이 아닙니다.|  
|23000|무결성 제약 조건 위반|인수 *작업이* SQL_DELETE 또는 SQL_UPDATE 되었으며 무결성 제약 조건을 위반 했습니다.|  
|24000|잘못된 커서 상태|*StatementHandle* 가 실행 된 상태 이지만 *StatementHandle*과 연결 된 결과 집합이 없습니다.<br /><br /> (DM) *StatementHandle*에서 커서가 열려 있지만 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하지 않았습니다.<br /><br /> *StatementHandle*에서 커서를 열 었으 며 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 했지만 결과 집합의 시작 앞 이나 결과 집합의 끝 뒤에 커서가 배치 되었습니다.<br /><br /> 인수 *작업이* SQL_DELETE, SQL_REFRESH 또는 SQL_UPDATE 되었으며 커서가 결과 집합의 시작 위치 앞 이나 결과 집합의 끝 위치 앞에 있습니다.|  
|40001|Serialization 오류|다른 트랜잭션과의 리소스 교착 상태 때문에 트랜잭션이 롤백 되었습니다.|  
|40003|문 완료를 알 수 없음|이 함수를 실행 하는 동안 연결 된 연결에 실패 하 여 트랜잭션의 상태를 확인할 수 없습니다.|  
|42000|구문 오류 또는 액세스 위반|드라이버가 인수 *작업*에서 요청 된 작업을 수행 하는 데 필요한 행을 잠글 수 없습니다.<br /><br /> 드라이버가 *LockType*인수에서 요청 된 행을 잠글 수 없습니다.|  
|44000|WITH CHECK OPTION 위반|*작업* 인수가 SQL_UPDATE 되었으며 **WITH CHECK OPTION**을 지정 하 여 만든 표시 된 테이블에서 파생 된 테이블이 나 표시 된 테이블에 대 한 업데이트가 수행 되었습니다 .이 경우 업데이트의 영향을 받는 하나 이상의 행이 표시 된 테이블에 더 이상 표시 되지 않습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. * \* MessageText* 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 *StatementHandle*에서 **Sqlcancel** 또는 **Sqlcancelhandle** 이 호출 되 고 *StatementHandle*에서 함수가 다시 호출 되었습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. SQLSetPos 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) 지정한 *StatementHandle* 가 실행 된 상태가 아닙니다. 함수가 먼저 **Sqlexecdirect**, **sqlexecute**또는 catalog 함수를 호출 하지 않고 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.<br /><br /> (DM) 드라이버 *는 ODBC 2.x* 드라이버 이며 **sqlfetch** 를 호출한 후에 *StatementHandle* 에 대 한 **SQLSetPos** 가 호출 되었습니다.|  
|HY011|특성을 지금 설정할 수 없습니다.|(DM) 드라이버는 ODBC 2.x 드라이버 *입니다.* SQL_ATTR_ROW_STATUS_PTR statement 특성이 설정 되었습니다. 그런 다음, **Sqlfetch**, **sqlfetchscroll**또는 **sqlextendedfetch** 가 호출 되기 전에 **SQLSetPos** 가 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|*작업* 인수가 SQL_UPDATE, 데이터 값이 null 포인터이 고 열 길이 값이 0, SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NULL_DATA 또는 SQL_LEN_DATA_AT_EXEC_OFFSET 보다 작거나 같습니다.<br /><br /> *작업* 인수가 SQL_UPDATE 되었습니다. 데이터 값이 null 포인터가 아닙니다. C 데이터 형식이 SQL_C_BINARY 되었거나 SQL_C_CHAR. 열 길이 값이 0 보다 작지만 SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NTS, SQL_NULL_DATA 또는 SQL_LEN_DATA_AT_EXEC_OFFSET 보다 작거나 같습니다.<br /><br /> 길이/표시기 버퍼의 값이 SQL_DATA_AT_EXEC 되었습니다. SQL 형식이 SQL_LONGVARCHAR, SQL_LONGVARBINARY 또는 long 데이터 원본에 해당 하는 데이터 형식입니다. **SQLGetInfo** 의 SQL_NEED_LONG_DATA_LEN 정보 형식은 "Y" 였습니다.|  
|HY092|특성 식별자가 잘못 되었습니다.|(DM) *작업* 인수에 지정 된 값이 잘못 되었습니다.<br /><br /> (DM) *LockType* 인수에 지정 된 값이 잘못 되었습니다.<br /><br /> *작업* 인수가 SQL_UPDATE 또는 SQL_DELETE 되었으며 SQL_ATTR_CONCURRENCY 문 특성이 SQL_ATTR_CONCUR_READ_ONLY 되었습니다.|  
|HY107|행 값이 범위를 벗어났습니다.|*RowNumber* 인수에 지정 된 값이 행 집합의 행 수보다 큽니다.|  
|HY109|커서 위치가 잘못 되었습니다.|*StatementHandle* 연결 된 커서는 앞 으로만 정의 되었으므로 행 집합 내에 커서를 배치할 수 없습니다. **SQLSetStmtAttr**의 SQL_ATTR_CURSOR_TYPE 특성에 대 한 설명을 참조 하세요.<br /><br /> *작업* 인수가 SQL_UPDATE, SQL_DELETE 또는 SQL_REFRESH 되었으며 *RowNumber* 인수로 식별 된 행이 삭제 되었거나 인출 되지 않았습니다.<br /><br /> (DM) *RowNumber* 인수가 0이 고 *작업* 인수가 SQL_POSITION 되었습니다.<br /><br /> **SQLBulkOperations** 를 호출한 후 **Sqlfetchscroll** 또는 **sqlfetch** 를 호출 하기 전에 **SQLSetPos** 가 호출 되었습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|드라이버 또는 데이터 원본이 *작업* 인수 또는 *LockType* 인수에서 요청 된 작업을 지원 하지 않습니다.|  
|HYT00|제한 시간이 만료되었습니다.|데이터 원본에서 결과 집합을 반환 하기 전에 쿼리 제한 시간이 만료 되었습니다. 제한 시간은 SQL_ATTR_QUERY_TIMEOUT *특성* 을 사용 하 여 **SQLSetStmtAttr** 를 통해 설정 됩니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
  
> [!CAUTION]
>  문에 대 한 자세한 내용은에서 **SQLSetPos** 를 호출 하 *고 ODBC 2.x* 응용 프로그램과의 호환성을 위해 수행 해야 하는 작업을 참조 하세요. [블록 커서, 스크롤 가능 커서 및 이전 버전과의 호환성](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)을 참조 하세요.  
  
## <a name="rownumber-argument"></a>RowNumber 인수  
 *RowNumber* 인수는 *작업* 인수에 지정 된 작업을 수행할 행 집합의 행 번호를 지정 합니다. *RowNumber* 가 0 이면 행 집합의 모든 행에 작업이 적용 됩니다. *RowNumber* 는 0에서 행 집합에 있는 행 수 사이의 값 이어야 합니다.  
  
> [!NOTE]  
>  C 언어에서 배열은 0부터 사용 되며 *RowNumber* 인수는 1부터 사용 됩니다. 예를 들어 행 집합의 다섯 번째 행을 업데이트 하기 위해 응용 프로그램은 배열 인덱스 4에서 행 집합 버퍼를 수정 하지만 *RowNumber* 를 5로 지정 합니다.  
  
 모든 작업은 *RowNumber*로 지정 된 행에 커서를 놓습니다. 다음 작업에는 커서 위치가 필요 합니다.  
  
-   위치 지정 update 및 delete 문  
  
-   **SQLGetData**를 호출 합니다.  
  
-   SQL_DELETE, SQL_REFRESH 및 SQL_UPDATE 옵션을 사용 하 여 **SQLSetPos** 를 호출 합니다.  
  
 예를 들어 SQL_DELETE *작업* 을 사용 하 여 **SQLSetPos** 를 호출 하기 위해 *RowNumber* 가 2 인 경우 커서는 행 집합의 두 번째 행에 배치 되 고 해당 행은 삭제 됩니다. 두 번째 행에 대 한 구현 행 상태 배열 (SQL_ATTR_ROW_STATUS_PTR statement 특성에 의해 가리키는 항목)이 SQL_ROW_DELETED으로 변경 됩니다.  
  
 응용 프로그램은 **SQLSetPos**를 호출할 때 커서 위치를 지정할 수 있습니다. 일반적으로 SQL_POSITION 또는 SQL_REFRESH 작업을 사용 하 여 **SQLSetPos** 를 호출 하 여 위치 지정 update 또는 delete 문을 실행 하거나 **SQLGetData**를 호출 하기 전에 커서를 배치 합니다.  
  
## <a name="operation-argument"></a>Operation 인수  
 *작업* 인수는 다음 작업을 지원 합니다. 데이터 원본에서 지원 되는 옵션을 확인 하기 위해 응용 프로그램은 커서의 형식에 따라 SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 또는 SQL_STATIC_CURSOR_ATTRIBUTES1 정보 형식으로 **SQLGetInfo** 를 호출 합니다.  
  
|*연산*<br /><br /> 인수|작업|  
|------------------------------|---------------|  
|SQL_POSITION|드라이버는 *RowNumber*에서 지정 된 행에 커서를 놓습니다.<br /><br /> SQL_ATTR_ROW_OPERATION_PTR statement 특성이 가리키는 행 상태 배열의 내용은 SQL_POSITION *작업*에서 무시 됩니다.|  
|SQL_REFRESH|드라이버는 *RowNumber* 에서 지정 된 행에 커서를 놓고 해당 행에 대 한 행 집합 버퍼의 데이터를 새로 고칩니다. 드라이버가 행 집합 버퍼의 데이터를 반환 하는 방법에 대 한 자세한 내용은 **SQLBindCol**의 행 단위 및 열 단위 바인딩에 대 한 설명을 참조 하세요.<br /><br /> SQL_REFRESH *작업* 을 사용 하 여 **SQLSetPos** 는 현재 인출 된 행 집합 내에서 행의 상태와 내용을 업데이트 합니다. 여기에는 책갈피를 새로 고치는 작업이 포함 됩니다. 버퍼의 데이터는 새로 고쳐지고 refetched (사방)은 새로 고쳐지지 않으므로 행 집합의 멤버 자격은 고정 되어 있습니다. 이는 SQL_FETCH_RELATIVE의 *Fetch방향이* 포함 된 **sqlfetchscroll** 에 대 한 호출에 의해 수행 되는 새로 고침과는 다르며, *RowNumber* 는 0과 같으며,이는 결과 집합에서 행 집합을 refetches 하 여 해당 작업이 드라이버 및 커서에서 지원 되는 경우 삭제 된 데이터를 표시 하 고 삭제 된 데이터를 제거할 수 있습니다.<br /><br /> **SQLSetPos** 를 성공적으로 새로 고치면 SQL_ROW_DELETED의 행 상태가 변경 되지 않습니다. 행 집합에서 삭제 된 행은 다음 인출까지 삭제 된 것으로 계속 표시 됩니다. 커서에서 압축을 지 원하는 경우 (후속 **Sqlfetch** 또는 **sqlfetchscroll** 에서 삭제 된 행을 반환 하지 않는) 다음 인출 시 행이 사라집니다.<br /><br /> **SQLSetPos** 로 새로 고침을 수행 하면 추가 된 행이 표시 되지 않습니다. 이 동작은 현재 행 *집합을 새로* 고치는 **Sqlfetchscroll scroll** 및 0과 동일한 *RowNumber* 와는 달리, 이러한 작업이 커서에서 지원 되는 경우 추가 된 레코드 또는 팩 삭제 된 레코드를 표시 합니다.<br /><br /> **SQLSetPos** 를 성공적으로 새로 고치면 SQL_ROW_ADDED의 행 상태가 SQL_ROW_SUCCESS (행 상태 배열이 있는 경우)로 변경 됩니다.<br /><br /> **SQLSetPos** 를 사용 하 여 새로 고치면 SQL_ROW_UPDATED의 행 상태가 행의 새 상태 (행 상태 배열이 있는 경우)로 변경 됩니다.<br /><br /> 행의 **SQLSetPos** 작업에서 오류가 발생 하는 경우 행 상태 배열이 있으면 행 상태가 SQL_ROW_ERROR로 설정 됩니다.<br /><br /> SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES의 SQL_ATTR_CONCURRENCY statement 특성을 사용 하 여 열린 커서의 경우 **SQLSetPos** 를 사용 하 여 새로 고치면 행이 변경 되었음을 감지 하기 위해 데이터 원본에서 사용 하는 낙관적 동시성 값을 업데이트할 수 있습니다. 이 경우 행 집합 버퍼를 서버에서 새로 고칠 때마다 커서 동시성을 보장 하는 데 사용 되는 행 버전 또는 값이 업데이트 됩니다. 이는 새로 고쳐지는 각 행에 대해 발생 합니다.<br /><br /> SQL_ATTR_ROW_OPERATION_PTR statement 특성이 가리키는 행 상태 배열의 내용은 SQL_REFRESH *작업*에서 무시 됩니다.|  
|SQL_UPDATE|드라이버는 *RowNumber* 에서 지정한 행에 커서를 놓고 데이터의 기본 행을 행 집합 버퍼 ( **SQLBindCol**의 *targetvalueptr* 인수)의 값으로 업데이트 합니다. 길이/표시기 버퍼 ( **SQLBindCol**의 *StrLen_or_IndPtr* 인수)에서 데이터 길이를 검색 합니다. 열의 길이가 SQL_COLUMN_IGNORE 면 열이 업데이트 되지 않습니다. 행을 업데이트 한 후 드라이버는 행 상태 배열의 해당 요소를 SQL_ROW_UPDATED 또는 SQL_ROW_SUCCESS_WITH_INFO (행 상태 배열이 있는 경우)로 변경 합니다.<br /><br /> 중복 된 열을 포함 하는 커서에서 SQL_UPDATE의 *작업* 인수를 사용 하 여 **SQLSetPos** 를 호출 하는 경우의 동작을 드라이버에서 정의 합니다. 드라이버는 드라이버 정의 SQLSTATE를 반환 하거나, 결과 집합에 표시 되는 첫 번째 열을 업데이트 하거나, 다른 드라이버 정의 동작을 수행할 수 있습니다.<br /><br /> SQL_ATTR_ROW_OPERATION_PTR statement 특성에서 가리키는 행 작업 배열은 대량 업데이트를 수행 하는 동안 현재 행 집합의 행을 무시 하도록 지정 하는 데 사용할 수 있습니다. 자세한 내용은이 함수 참조의 뒷부분에 나오는 "상태 및 작업 배열"을 참조 하세요.|  
|SQL_DELETE|드라이버는 *RowNumber* 에서 지정 된 행에 커서를 놓고 데이터의 기본 행을 삭제 합니다. 행 상태 배열의 해당 요소를 SQL_ROW_DELETED로 변경 합니다. 행이 삭제 된 후에는 다음이 행에 대해 유효 하지 않습니다. 위치 지정 update 및 delete 문, **SQLGetData**호출 및 *작업* 을 사용 하 여 **SQLSetPos** 에 대 한 호출을 SQL_POSITION를 제외한 모든 항목으로 설정 합니다. 압축을 지 원하는 드라이버의 경우 데이터 원본에서 새 데이터를 검색 하면 커서에서 행이 삭제 됩니다.<br /><br /> 행이 계속 표시 되는지 여부는 커서 유형에 따라 달라 집니다. 예를 들어 삭제 된 행은 정적 및 키 집합 커서에 표시 되지만 동적 커서에는 표시 되지 않습니다.<br /><br /> SQL_ATTR_ROW_OPERATION_PTR statement 특성에서 가리키는 행 작업 배열은 대량 삭제 중에 현재 행 집합의 행을 무시 해야 함을 나타내는 데 사용할 수 있습니다. 자세한 내용은이 함수 참조의 뒷부분에 나오는 "상태 및 작업 배열"을 참조 하세요.|  
  
## <a name="locktype-argument"></a>LockType 인수  
 *LockType* 인수는 응용 프로그램에서 동시성을 제어 하는 방법을 제공 합니다. 대부분의 경우 동시성 수준 및 트랜잭션을 지 원하는 데이터 원본을 사용할 경우 *LockType* 인수의 SQL_LOCK_NO_CHANGE 값만 지원 됩니다. *LockType* 인수는 일반적으로 파일 기반 지원에만 사용 됩니다.  
  
 *LockType* 인수는 **SQLSetPos** 가 실행 된 후 행의 잠금 상태를 지정 합니다. 드라이버에서 요청 된 작업을 수행 하거나 *LockType* 인수를 충족 하기 위해 행을 잠글 수 없는 경우 SQL_ERROR 및 SQLSTATE 42000 (구문 오류 또는 액세스 위반)을 반환 합니다.  
  
 *LockType* 인수는 단일 문에 대해 지정 되지만 잠금은 연결의 모든 문에 대해 동일한 권한을 accords 합니다. 특히 연결에서 한 문에 의해 획득 되는 잠금은 동일한 연결에서 다른 문으로 잠금을 해제할 수 있습니다.  
  
 **Sqlsetpos** 를 통해 잠긴 행은 응용 프로그램이 *LockType* 를 SQL_LOCK_UNLOCK로 설정 하거나 응용 프로그램이 SQL_CLOSE 옵션을 사용 하 여 문이나 **SQLFreeStmt** 에 대해 **sqlfreehandle** **을 호출할 때** 까지 잠긴 상태로 유지 됩니다. 트랜잭션을 지 원하는 드라이버의 경우 응용 프로그램에서 **Sqlendtran** 을 호출 하 여 연결에서 트랜잭션을 커밋하거나 롤백하려고 할 때 **SQLSetPos** 를 통해 잠긴 행의 잠금이 해제 됩니다. 예를 들어 **SQLGetInfo**에서 반환 하는 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 형식에 따라 트랜잭션이 커밋되거나 롤백될 때 커서가 닫히는 경우.  
  
 *LockType* 인수는 다음과 같은 형식의 잠금을 지원 합니다. 데이터 원본에서 지 원하는 잠금을 확인 하기 위해 응용 프로그램은 커서의 형식에 따라 SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 또는 SQL_STATIC_CURSOR_ATTRIBUTES1 정보 형식으로 **SQLGetInfo** 를 호출 합니다.  
  
|*LockType* 인수|잠금 유형|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|드라이버 또는 데이터 원본은 **SQLSetPos** 가 호출 되기 전과 동일한 잠금 또는 잠금 해제 상태를 유지 합니다. 이 *LockType* 값은 명시적 행 수준 잠금을 지원 하지 않는 데이터 원본에서 현재 동시성 및 트랜잭션 격리 수준에 필요한 모든 잠금을 사용 하도록 허용 합니다.|  
|SQL_LOCK_EXCLUSIVE|드라이버 또는 데이터 원본에서 행을 독점적으로 잠급니다. 다른 연결 또는 다른 응용 프로그램의 문을 사용 하 여 행에 대 한 잠금을 획득할 수 없습니다.|  
|SQL_LOCK_UNLOCK|드라이버 또는 데이터 원본에서 행의 잠금을 해제 합니다.|  
  
 드라이버가 SQL_LOCK_EXCLUSIVE을 지원 하지만 SQL_LOCK_UNLOCK를 지원 하지 않는 경우에는 이전 단락에서 설명한 함수 호출 중 하나가 발생할 때까지 잠긴 행이 잠깁니다.  
  
 드라이버가 SQL_LOCK_EXCLUSIVE을 지원 하지만 SQL_LOCK_UNLOCK를 지원 하지 않는 경우 잠긴 행은 응용 프로그램이 문에 대해 **Sqlfreehandle** 을 호출 하거나 SQL_CLOSE 옵션을 사용 하 여 **SQLFreeStmt** 때까지 잠긴 상태로 유지 됩니다. 드라이버가 트랜잭션을 지원 하 고 트랜잭션을 커밋하거나 롤백하여 커서를 닫으면 응용 프로그램은 **Sqlendtran**을 호출 합니다.  
  
 **SQLSetPos**의 업데이트 및 삭제 작업의 경우 응용 프로그램은 다음과 같이 *LockType* 인수를 사용 합니다.  
  
-   행이 검색 된 후 변경 되지 않도록 하기 위해 응용 프로그램은 *작업* 을 SQL_REFRESH로 설정 하 고 *LockType* 를 SQL_LOCK_EXCLUSIVE으로 설정 하 여 **SQLSetPos** 를 호출 합니다.  
  
-   응용 프로그램이 SQL_LOCK_NO_CHANGE에 대해 *LockType* 를 설정 하는 경우 드라이버는 응용 프로그램이 SQL_ATTR_CONCURRENCY statement 특성에 대해 SQL_CONCUR_LOCK 지정 된 경우에만 업데이트 또는 삭제 작업이 성공 하도록 보장 합니다.  
  
-   응용 프로그램에서 SQL_ATTR_CONCURRENCY 문 특성에 대해 SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES를 지정 하는 경우 드라이버는 행 버전 또는 값을 비교 하 고 응용 프로그램이 행을 가져온 이후 행이 변경 된 경우 작업을 거부 합니다.  
  
-   응용 프로그램이 SQL_ATTR_CONCURRENCY statement 특성에 대 한 SQL_CONCUR_READ_ONLY를 지정 하는 경우 드라이버는 업데이트 또는 삭제 작업을 거부 합니다.  
  
 SQL_ATTR_CONCURRENCY statement 특성에 대 한 자세한 내용은 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)를 참조 하세요.  
  
## <a name="status-and-operation-arrays"></a>상태 및 작업 배열  
 **SQLSetPos**를 호출할 때 다음 상태 및 작업 배열이 사용 됩니다.  
  
-   IRD 및 SQL_ATTR_ROW_STATUS_ARRAY statement 특성의 SQL_DESC_ARRAY_STATUS_PTR 필드가 가리키는 행 상태 배열에는 행 집합의 각 데이터 행에 대 한 상태 값이 포함 됩니다. 이 드라이버는 **Sqlfetch**, **sqlfetchscroll**, **SQLBulkOperations**또는 **SQLSetPos**를 호출한 후이 배열의 상태 값을 설정 합니다. 이 배열은 SQL_ATTR_ROW_STATUS_PTR statement 특성에 의해 가리킵니다.  
  
-   행 작업 배열 (이 하 및 SQL_ATTR_ROW_OPERATION_ARRAY 문 특성의 SQL_DESC_ARRAY_STATUS_PTR 필드가 가리키는 행 작업 배열)에는 행 집합의 각 행에 대 한 값이 포함 되어 있으므로 대량 작업에 대 한 **SQLSetPos** 호출을 무시 하거나 수행할지 여부를 나타냅니다. 배열의 각 요소는 SQL_ROW_PROCEED (기본값) 또는 SQL_ROW_IGNORE로 설정 됩니다. 이 배열은 SQL_ATTR_ROW_OPERATION_PTR statement 특성에 의해 가리킵니다.  
  
 상태 및 작업 배열의 요소 수는 행 집합의 행 수와 같아야 합니다 (SQL_ATTR_ROW_ARRAY_SIZE statement 특성에 정의 됨).  
  
 행 상태 배열에 대 한 자세한 내용은 [Sqlfetch](../../../odbc/reference/syntax/sqlfetch-function.md)를 참조 하세요. Row 작업 배열에 대 한 자세한 내용은이 섹션의 뒷부분에 나오는 "대량 작업에서 행 무시"를 참조 하십시오.  
  
## <a name="using-sqlsetpos"></a>SQLSetPos 사용  
 응용 프로그램이 **SQLSetPos**를 호출 하기 전에 다음과 같은 일련의 단계를 수행 해야 합니다.  
  
1.  응용 프로그램에서 *작업이* SQL_UPDATE로 설정 된 **SQLSetPos** 를 호출 하는 경우 각 열에 대해 **SQLBindCol** (또는 **SQLSetDescRec**)를 호출 하 여 해당 데이터 형식을 지정 하 고 열 데이터 및 길이에 대 한 버퍼를 바인딩합니다.  
  
2.  응용 프로그램에서 *작업이* SQL_DELETE 또는 SQL_UPDATE로 설정 된 **SQLSetPos** 를 호출 하는 경우 **sqlcolattribute** 를 호출 하 여 삭제 하거나 업데이트할 열을 업데이트할 수 있는지 확인 합니다.  
  
3.  **Sqlexecdirect**, **sqlexecute**또는 catalog 함수를 호출 하 여 결과 집합을 만듭니다.  
  
4.  **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하 여 데이터를 검색 합니다.  
  
 **Sqlsetpos**를 사용 하는 방법에 대 한 자세한 내용은 sqlsetpos를 사용 하 [여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)를 참조 하세요.  
  
## <a name="deleting-data-using-sqlsetpos"></a>SQLSetPos를 사용 하 여 데이터 삭제  
 **Sqlsetpos**를 사용 하 여 데이터를 삭제 하기 위해 응용 프로그램은 *RowNumber* 가 삭제할 행 수로 설정 된 **Sqlsetpos** 를 호출 하 고 *작업* 을 SQL_DELETE로 설정 합니다.  
  
 데이터를 삭제 한 후 드라이버는 해당 행에 대 한 구현 행 상태 배열의 값을 SQL_ROW_DELETED 또는 SQL_ROW_ERROR로 변경 합니다.  
  
## <a name="updating-data-using-sqlsetpos"></a>SQLSetPos를 사용 하 여 데이터 업데이트  
 응용 프로그램은 바인딩된 데이터 버퍼에 있거나 **Sqlputdata**에 대 한 하나 이상의 호출로 열의 값을 전달할 수 있습니다. **Sqlputdata** 를 사용 하 여 데이터를 전달 하는 열을 *실행 시 데이터* *열*이라고 합니다. 이러한 데이터는 일반적으로 SQL_LONGVARBINARY 및 SQL_LONGVARCHAR 열의 데이터를 전송 하는 데 사용 되며 다른 열과 혼합할 수 있습니다.  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>SQLSetPos를 사용 하 여 데이터를 업데이트 하려면 응용 프로그램:  
  
1.  **SQLBindCol**를 사용 하 여 바인딩된 데이터 및 길이/표시기 버퍼에 값을 배치 합니다.  
  
    -   표준 열의 경우 응용 프로그램이 * \* targetvalueptr* 버퍼에 새 열 값을, * \* StrLen_or_IndPtr* 버퍼에 해당 값의 길이를 배치 합니다. 행을 업데이트 하지 않아야 하는 경우 응용 프로그램은 행 작업 배열의 해당 행 요소에 SQL_ROW_IGNORE을 배치 합니다.  
  
    -   실행 시 데이터 열의 경우 응용 프로그램에서 열 번호와 같은 응용 프로그램 정의 값을 * \* targetvalueptr* 버퍼에 배치 합니다. 나중에이 값을 사용 하 여 열을 식별할 수 있습니다.  
  
         응용 프로그램은 SQL_LEN_DATA_AT_EXEC (*길이*) 매크로의 결과를 **StrLen_or_IndPtr* 버퍼에 저장 합니다. 열의 SQL 데이터 형식이 SQL_LONGVARBINARY, SQL_LONGVARCHAR 또는 long 데이터 원본 관련 데이터 형식이 고 드라이버에서 **SQLGetInfo**의 SQL_NEED_LONG_DATA_LEN 정보 형식에 대해 "Y"를 반환 하는 경우 *길이* 는 매개 변수에 대해 전송 되는 데이터 바이트 수입니다. 그렇지 않으면 음수가 아닌 값 이어야 하며 무시 됩니다.  
  
2.  *작업* 인수가 SQL_UPDATE로 설정 된 **SQLSetPos** 를 호출 하 여 데이터 행을 업데이트 합니다.  
  
    -   실행 시 데이터 열이 없으면 프로세스가 완료 된 것입니다.  
  
    -   실행 시 데이터 열이 있는 경우 함수는 SQL_NEED_DATA을 반환 하 고 3 단계로 진행 합니다.  
  
3.  **Sqlparamdata** 를 호출 하 여 처리할 첫 번째 실행 시 데이터 열에 대 한 * \* targetvalueptr* 버퍼의 주소를 검색 합니다. **Sqlparamdata** 는 SQL_NEED_DATA를 반환 합니다. 응용 프로그램이 * \* targetvalueptr* 버퍼에서 응용 프로그램 정의 값을 검색 합니다.  
  
    > [!NOTE]  
    >  실행 시 데이터 매개 변수는 실행 시 데이터 열과 유사 하지만 **Sqlparamdata** 에서 반환 되는 값은 서로 다릅니다.  
  
    > [!NOTE]  
    >  실행 시 데이터 매개 변수는 문이 **Sqlputdata** 또는 **sqlexecute**를 사용 하 여 실행 될 때 **sqlputdata** 를 사용 하 여 데이터를 전송 하는 SQL 문의 매개 변수입니다. **SQLBindParameter** 를 사용 하거나 설명자를 **SQLSetDescRec**로 설정 하 여 바인딩합니다. **Sqlparamdata** 에서 반환 되는 값은 *ParameterSQLBindParameter Eptr* 인수에서 **SQLBindParameter** 로 전달 되는 32 비트 값입니다.  
  
    > [!NOTE]  
    >  실행 시 데이터 열은 **SQLSetPos**로 행을 업데이트할 때 **sqlputdata** 를 사용 하 여 데이터를 전송 하는 행 집합의 열입니다. **SQLBindCol**와 바인딩됩니다. **Sqlparamdata** 에서 반환 되는 값은 처리 중인 **Targetvalueptr* 버퍼의 행 주소입니다.  
  
4.  **Sqlputdata** 를 한 번 이상 호출 하 여 열에 대 한 데이터를 보냅니다. **Sqlputdata**에 지정 된 * \* targetvalueptr* 버퍼에 모든 데이터 값을 반환할 수 없는 경우 두 번 이상 호출 해야 합니다. 문자, 이진 또는 데이터 원본 관련 데이터 형식이 있는 열에 문자 c 데이터를 전송 하거나 문자, 이진 또는 데이터 원본 관련 데이터 형식이 있는 열에 이진 c 데이터를 보내는 경우에만 동일한 열에 대 한 **sqlputdata** 를 여러 번 호출할 수 있습니다.  
  
5.  **Sqlparamdata** 를 다시 호출 하 여 열에 대해 모든 데이터가 전송 되었음을 알립니다.  
  
    -   실행 시 데이터 열이 더 있는 경우 **Sqlparamdata** 는 처리할 다음 실행 시 데이터 열에 대 한 *Targetvalueptr* 버퍼의 주소 및 SQL_NEED_DATA 반환 합니다. 응용 프로그램은 4 단계와 5 단계를 반복 합니다.  
  
    -   실행 시 데이터 열이 더 이상 없으면 프로세스가 완료 된 것입니다. 문이 성공적으로 실행 된 경우 **Sqlparamdata** 는 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO을 반환 합니다. 실행에 실패 하면 SQL_ERROR 반환 됩니다. 이 시점에서 **Sqlparamdata** 는 **SQLSetPos**에서 반환 될 수 있는 모든 SQLSTATE를 반환할 수 있습니다.  
  
 데이터가 업데이트 된 경우 드라이버는 해당 행의 구현 행 상태 배열에서 값을 SQL_ROW_UPDATED로 변경 합니다.  
  
 작업이 취소 되거나 **Sqlparamdata** 또는 **sqlparamdata**에서 오류가 발생 하는 경우 **SQLSetPos** 가 SQL_NEED_DATA를 반환한 후 모든 실행 시 데이터 열에 대해 데이터를 전송 하기 전에 응용 프로그램은 **sqlcancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **sqlparamdata**또는 문에 연결 된 연결 또는 문에 대해 **sqlparamdata** 만 호출할 수 있습니다. 문 또는 문과 연결 된 연결에 대 한 다른 함수를 호출 하는 경우이 함수는 SQL_ERROR 및 SQLSTATE HY010 (함수 시퀀스 오류)를 반환 합니다.  
  
 드라이버가 실행 시 데이터 열에 대 한 데이터를 필요로 하는 동안 **Sqlcancel** 을 호출 하면 드라이버에서 작업을 취소 합니다. 그러면 응용 프로그램이 **SQLSetPos** 를 다시 호출할 수 있습니다. 취소 해도 커서 상태나 현재 커서 위치에는 영향을 주지 않습니다.  
  
 커서와 연결 된 쿼리 사양의 선택 목록에 같은 열에 대 한 참조가 두 개 이상 포함 되어 있는 경우 오류가 발생 하는지, 아니면 드라이버가 중복 된 참조를 무시 하 고 요청 된 작업을 수행 합니다.  
  
## <a name="performing-bulk-operations"></a>대량 작업 수행  
 *RowNumber* 인수가 0 이면 드라이버는 행 집합의 각 행에 대해 *작업* 인수에 지정 된 작업을 수행 합니다 .이 작업은 행 작업 배열의 해당 필드에 SQL_ROW_PROCEED 값을 포함 하 SQL_ATTR_ROW_OPERATION_PTR statement 특성을 가리킵니다. 이 값은 SQL_DELETE, SQL_REFRESH 또는 SQL_UPDATE의 *작업* 인수에 대 한 *RowNumber* 인수의 유효한 값 이지만 SQL_POSITION 되지 않습니다. SQL_POSITION의 *작업* 및 *RowNumber* 가 0 인 **SQLSetPos** 는 SQLSTATE HY109 (잘못 된 커서 위치)를 반환 합니다.  
  
 SQLSTATE HYT00 (Timeout 만료 됨)와 같이 전체 행 집합에 관련 된 오류가 발생 하는 경우 드라이버는 SQL_ERROR 및 적절 한 SQLSTATE를 반환 합니다. 행 집합 버퍼의 내용은 정의 되지 않으며 커서 위치는 변경 되지 않습니다.  
  
 단일 행과 관련 된 오류가 발생 하는 경우 드라이버는 다음과 같습니다.  
  
-   SQL_ATTR_ROW_STATUS_PTR statement 특성이 가리키는 행 상태 배열의 행에 대 한 요소를 SQL_ROW_ERROR로 설정 합니다.  
  
-   오류 큐에서 오류에 대 한 하나 이상의 추가 SQLSTATEs를 게시 하 고 진단 데이터 구조의 SQL_DIAG_ROW_NUMBER 필드를 설정 합니다.  
  
 오류 또는 경고를 처리 한 후 드라이버에서 행 집합의 나머지 행에 대 한 작업을 완료 하면 SQL_SUCCESS_WITH_INFO 반환 됩니다. 따라서 오류가 반환 된 각 행에 대해 오류 큐에 0 개 이상의 추가 SQLSTATEs가 포함 됩니다. 오류 또는 경고를 처리 한 후 드라이버에서 작업을 중지 하면 SQL_ERROR 반환 됩니다.  
  
 SQLSTATE 01004 (데이터 잘림)와 같은 경고를 반환 하는 경우 특정 행에 적용 되는 오류 정보를 반환 하기 전에 전체 행 집합 또는 행 집합의 알 수 없는 행에 적용 되는 경고를 반환 합니다. 이러한 행에 대 한 다른 오류 정보와 함께 특정 행에 대 한 경고를 반환 합니다.  
  
 *RowNumber* 가 0이 고 *작업이* SQL_UPDATE, SQL_REFRESH 또는 SQL_DELETE 인 경우 **SQLSetPos** 가 작동 하는 행 수는 SQL_ATTR_ROWS_FETCHED_PTR statement 특성에 의해 가리킵니다.  
  
 *RowNumber* 가 0이 고 *연산이* SQL_DELETE, SQL_REFRESH 또는 SQL_UPDATE 이면 작업 후 현재 행이 작업 전의 현재 행과 동일 합니다.  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>대량 작업에서 행 무시  
 행 작업 배열은 **SQLSetPos**를 사용 하 여 대량 작업을 수행 하는 동안 현재 행 집합의 행을 무시 하도록 지정 하는 데 사용할 수 있습니다. 대량 작업 중에 드라이버에서 하나 이상의 행을 무시 하도록 지시 하려면 응용 프로그램에서 다음 단계를 수행 해야 합니다.  
  
1.  **SQLSetStmtAttr** 를 호출 하 여 SQLUSMALLINTs의 배열을 가리키도록 SQL_ATTR_ROW_OPERATION_PTR statement 특성을 설정 합니다. **SQLSetDescField** 를 호출 하 여이 필드를 설정 하 여 응용 프로그램에서 설명자 핸들을 가져와야 하는 사용의 SQL_DESC_ARRAY_STATUS_PTR 헤더 필드를 설정할 수도 있습니다.  
  
2.  Row 작업 배열의 각 요소를 두 값 중 하나로 설정 합니다.  
  
    -   SQL_ROW_IGNORE-대량 작업에 대해 행이 제외 됨을 표시 합니다.  
  
    -   행이 대량 작업에 포함 되어 있음을 나타내려면를 SQL_ROW_PROCEED 합니다. True(기본값)임  
  
3.  **SQLSetPos** 를 호출 하 여 대량 작업을 수행 합니다.  
  
 Row 작업 배열에 적용 되는 규칙은 다음과 같습니다.  
  
-   SQL_ROW_IGNORE 및 SQL_ROW_PROCEED는 SQL_DELETE 또는 SQL_UPDATE *작업* 에 **SQLSetPos** 를 사용 하는 대량 작업에만 영향을 줍니다. SQL_REFRESH 또는 SQL_POSITION의 *작업* 을 사용 하 여 **SQLSetPos** 호출에는 영향을 주지 않습니다.  
  
-   포인터는 기본적으로 null로 설정 됩니다.  
  
-   포인터가 null 이면 모든 행이 SQL_ROW_PROCEED로 설정 된 것 처럼 모든 행이 업데이트 됩니다.  
  
-   SQL_ROW_PROCEED로 요소를 설정 해도 해당 특정 행에서 작업이 발생 하는 것을 보장 하지는 않습니다. 예를 들어 행 집합의 특정 행에 상태가 SQL_ROW_ERROR 이면 응용 프로그램에서 SQL_ROW_PROCEED 지정 했는지 여부에 관계 없이 드라이버가 해당 행을 업데이트 하지 못할 수 있습니다. 응용 프로그램은 작업의 성공 여부를 확인 하려면 항상 행 상태 배열을 확인 해야 합니다.  
  
-   SQL_ROW_PROCEED 헤더 파일에서 0으로 정의 됩니다. 응용 프로그램은 모든 행을 처리 하기 위해 행 작업 배열을 0으로 초기화할 수 있습니다.  
  
-   Row 작업 배열의 요소 번호 "n"이 SQL_ROW_IGNORE로 설정 되 고, **sqlsetpos** 를 호출 하 여 대량 업데이트 또는 삭제 작업을 수행 하면 **sqlsetpos**를 호출한 후 행 집합의 n 번째 행이 변경 되지 않은 상태로 유지 됩니다.  
  
-   응용 프로그램은 SQL_ROW_IGNORE 읽기 전용 열을 자동으로 설정 해야 합니다.  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>대량 작업에서 열 무시  
 하나 이상의 읽기 전용 열에 대 한 업데이트를 시도 하 여 발생 하는 불필요 한 처리 진단을 방지 하기 위해 응용 프로그램은 바인딩된 길이/표시기 버퍼의 값을 SQL_COLUMN_IGNORE로 설정할 수 있습니다. 자세한 내용은 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)를 참조 하세요.  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서 응용 프로그램을 사용 하면 사용자가 ORDERS 테이블을 검색 하 고 주문 상태를 업데이트할 수 있습니다. 커서는 행 집합 크기가 20 인 키 집합을 기반으로 하며 행 버전을 비교 하는 낙관적 동시성 제어를 사용 합니다. 각 행 집합을 인출 하면 응용 프로그램에서 해당 행 집합을 출력 하 고 사용자가 주문 상태를 선택 하 고 업데이트할 수 있습니다. 응용 프로그램은 **SQLSetPos** 를 사용 하 여 커서를 선택한 행에 배치 하 고 해당 행의 위치 업데이트를 수행 합니다. 명확 하 게 하기 위해 오류 처리는 생략 됩니다.  
  
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
  
 더 많은 예제는 [위치 지정 Update 및 Delete 문](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) 및 [SQLSetPos를 사용 하 여 행 집합의 행 업데이트](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)를 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|블록 커서 위치와 관련이 없는 대량 작업 수행|[SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|데이터 블록 가져오기 또는 결과 집합을 통한 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|설명자의 단일 필드 가져오기|[SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|설명자의 여러 필드 가져오기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|설명자의 단일 필드 설정|[SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|설명자의 여러 필드 설정|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
