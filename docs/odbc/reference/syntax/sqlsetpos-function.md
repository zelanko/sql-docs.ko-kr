---
title: "SQLSetPos 함수 | Microsoft Docs"
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
- SQLSetPos
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetPos
helpviewer_keywords:
- SQLSetPos function [ODBC]
ms.assetid: 80190ee7-ae3b-45e5-92a9-693eb558f322
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6140625da489bcb573b3beb4ca2be0838805f8d5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetpos-function"></a>SQLSetPos 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **SQLSetPos** 행 집합에서 커서 위치를 설정 하 고 행 집합의 데이터를 새로 고치려면 또는 업데이트 하거나 결과 집합의 데이터를 삭제 하는 응용 프로그램을 허용 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLSetPos(  
      SQLHSTMT        StatementHandle,  
      SQLSETPOSIROW   RowNumber,  
      SQLUSMALLINT    Operation,  
      SQLUSMALLINT    LockType);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *RowNumber*  
 [입력] 에 지정 된 작업을 수행 하는 행 집합에서 행의 위치는 *작업* 인수입니다. 경우 *RowNumber* 가 0 이면 행 집합의 모든 행에 작업 적용 됩니다.  
  
 자세한 내용은 "설명"을 참조 하십시오.  
  
 *연산*  
 [입력] 수행할 연산입니다.  
  
 SQL_POSITION SQL_REFRESH SQL_UPDATE SQL_DELETE  
  
> [!NOTE]  
>  에 대 한 SQL_ADD 값은 *작업* ODBC 3에 대 한 인수를 더 이상 사용 되지*.x*합니다. ODBC 3입니다. *x* 드라이버 SQL_ADD 이전 버전과 호환성에 대 한 지원 해야 합니다. 이 기능에 대 한 호출으로 대체 되었습니다 **SQLBulkOperations** 와 *작업* SQL_ADD입니다. 때 ODBC 3. *x* 응용 프로그램이 작동 ODBC 2. *x* 드라이버를 드라이버 관리자에 대 한 호출 매핑합니다 **SQLBulkOperations** 와 *작업* 에 SQL_ADD의 **SQLSetPos** 와  *작업* SQL_ADD입니다.  
  
 자세한 내용은 "설명"을 참조 하십시오.  
  
 *LockType*  
 [입력] 에 지정 된 작업을 수행한 후 행을 잠그는 방법을 지정는 *작업* 인수입니다.  
  
 SQL_LOCK_NO_CHANGE SQL_LOCK_EXCLUSIVE SQL_LOCK_UNLOCK  
  
 자세한 내용은 "설명"을 참조 하십시오.  
  
 **반환**  
  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLSetPos** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* SQL_의 HANDLE_STMT 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLSetPos** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
 다중 행 작업의 하나 또는 더 전부가 아닌 행에 오류가 발생 하 고에서 오류가 발생할 경우 SQL_ERROR가 반환 되는 경우 모든 해당 SQLSTATEs SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR (제외 01xxx SQLSTATEs) 반환할 수 있는, sql_success_with_info가 반환 됩니다는 단일 행 작업입니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01001|커서 작업이 충돌 합니다.|*작업* 인수 SQL_DELETE 되었거나 SQL_UPDATE, 및 둘 이상의 행 또는 행이 없는 된 삭제 하거나 업데이트 합니다. (둘 이상의 행에 대 한 업데이트에 대 한 자세한 내용은 참조는 SQL_ATTR_SIMULATE_CURSOR에 대 한 설명을 *특성* 에 **SQLSetStmtAttr**.) (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)<br /><br /> *작업* 인수 SQL_DELETE 되었거나 SQL_UPDATE, 및 낙관적 동시성으로 인해 작업이 실패 했습니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|*작업* SQL_REFRESH에 인수가 며 문자열이 나 이진 데이터 열 또는 열을 SQL_C_CHAR 또는 SQL_C_BINARY 데이터 형식에 대해 반환 된 공백이 아닌 문자 또는 NULL이 아닌 이진 데이터 잘림.|  
|01S01|행 하는 동안 오류가 발생 했습니다.|*RowNumber* 되었습니다. 0, 인수 및 지정 된 작업을 수행 하는 동안 하나 이상의 행에 오류가 발생는 *작업* 인수입니다.<br /><br /> (Sql_success_with_info가 반환 됩니다 다중 행 작업의 하나 또는 더 전부가 아닌 행에 오류가 발생 하 고 단일 행 작업에서 오류가 발생할 경우 SQL_ERROR가 반환 됩니다.)<br /><br /> (이 SQLSTATE는 경우에만 반환 됩니다 **SQLSetPos** 이후에 호출 **SQLExtendedFetch**경우 드라이버는 ODBC 2. *x* 드라이버 및 커서 라이브러리 사용 되지 않습니다.)|  
|01S07|일부가 잘렸습니다.|*작업* SQL_REFRESH 되었습니다, 응용 프로그램 버퍼의 데이터 형식이 되지 않았거나 SQL_C_CHAR SQL_C_BINARY 및 하나 이상의 열에 대 한 응용 프로그램 버퍼를 반환 합니다. 데이터가 잘렸습니다. 숫자 데이터 형식에 대 한 수의 소수 부분이 잘렸습니다. 시간, 타임 스탬프 및 interval 데이터 형식을 시간 구성 요소가 포함 된 경우 시간의 소수 부분이 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07006|제한 된 데이터 형식 특성 위반|지정한 데이터 형식으로 결과 집합에 있는 열의 데이터 값을 변환할 수 없습니다 *TargetType* 에 대 한 호출에서 **SQLBindCol**합니다.|  
|07009|잘못 된 설명자 인덱스입니다.|인수 *작업* SQL_REFRESH 되었거나 SQL_UPDATE, 및 열 번호가 결과 집합의 열 개수 보다 큰 열 바인딩 되었습니다.|  
|21S02|파생된 테이블의 수준이 열 목록과 일치 하지 않습니다.|인수 *작업* SQL_UPDATE, 였으며 바인딩된 길이/표시기 버퍼의 값이 SQL_COLUMN_IGNORE 또는 모든 열 중 하나 언바운드, 읽기 전용 되어 열이 없으면 된 업데이트할 수 있습니다.|  
|22001|문자열 데이터, 오른쪽이 잘렸습니다.|*작업* 인수 SQL_UPDATE, 였으며는 문자 또는 이진 열 값을 할당 (문자 수)에 대 한 비어 있지 않은 값 또는 null이 아닌 (이진)에 대 한 문자 또는 바이트 잘림이 발생 했습니다.|  
|22003|숫자 값 범위를 벗어났습니다.|인수 *작업* SQL_UPDATE, 였으며 결과 집합의 열에 숫자 값의 할당 (소수) 대비 전체 잘릴 숫자 부분과 발생 합니다.<br /><br /> 인수 *작업* SQL_REFRESH, 되었으며 하나 이상의 바인딩된 열에 대 한 숫자 값 반환 발생 유효 자릿수의 손실입니다.|  
|22007|잘못 된 날짜/시간 형식|인수 *작업* SQL_UPDATE, 였으며 연도, 월 또는 일 필드 범위를 벗어났거나를 결과 집합의 열에 날짜 또는 타임 스탬프 값이 할당 발생 합니다.<br /><br /> 인수 *작업* SQL_REFRESH, 되었으며 하나 이상의 바인딩된 열에 대 한 날짜 또는 타임 스탬프 값을 반환 발생 연도, 월 또는 일 필드가 포함 범위를 벗어났습니다. 되도록 합니다.|  
|22008|날짜/시간 필드 오버플로|*작업* SQL_UPDATE에 인수가 며 날짜/시간 산술 연산을 결과 집합의 열으로 전송 되는 데이터의 성능이 되는 결과의 날짜/시간 필드 (연도, 월, 일, 시간, 분, 또는 두 번째 필드) 외부의 필드 또는 잘못 된 값의 허용 범위 datetime에 대 한 일반 달력의 자연 규칙에 따라.<br /><br /> *작업* SQL_REFRESH에 인수가 며 날짜/시간 산술 연산을 결과 집합에서 검색 중인 데이터의 성능이 되는 결과의 날짜/시간 필드 (연도, 월, 일, 시간, 분, 또는 두 번째 필드) 외부의 필드 또는 잘못 된 값의 허용 범위 datetime에 대 한 일반 달력의 자연 규칙에 따라.|  
|22015|간격 필드 오버플로|*작업* 인수 SQL_UPDATE, 였으며 했기 때문에 유효 자릿수의 손실 배정 정확한 숫자 또는 SQL 데이터 형식 설정 된 간격 C 간격 유형입니다.<br /><br /> *작업* 인수는 SQL_UPDATE; 간격 SQL 형식에 할당할 때는 간격 SQL 형식에서에서 C 형식의 값의 표시가 없을 했습니다.<br /><br /> *작업* 인수 SQL_REFRESH, 였으며 선행 필드에 유효 자릿수의 손실 발생 한 정확한 숫자 또는 간격 SQL 형식에서 C 간격 유형으로 할당 합니다.<br /><br /> *작업* 인수는 SQL_ 새로 고침; C 간격 유형을 할당할 때는 간격 C 형식에서 SQL 형식의 값으로 표시 되지 했습니다.|  
|22018|캐스트 사양의 문자 값|*작업* SQL_REFRESH에 인수가; 정확한 수 또는 대략적인 숫자, datetime, 또는 간격 데이터 형식이 C 유형은; 열의 SQL 형식을 문자 데이터 형식 되어 열에 값이 올바른 리터럴은 바인딩된 C 형식입니다.<br /><br /> 인수 *작업* SQL_UPDATE 되었습니다; 그리고 SQL 형식 정확한 수 또는 대략적인 숫자, datetime, 또는 간격 데이터 형식;가 SQL_C_CHAR; C 유형은 되어 값 열에 바인딩된 SQL 형식의 올바른 리터럴 수 없습니다.|  
|23000|무결성 제약 조건 위반|인수 *작업* SQL_DELETE 되었거나 SQL_UPDATE, 및는 무결성 제약 조건을 위반 했습니다.|  
|24000|잘못된 커서 상태|*StatementHandle* 된 실행된 상태에 있지만 결과 집합이 연관 된는 *StatementHandle*합니다.<br /><br /> (DM)에서 커서가 열린는 *StatementHandle*, 하지만 **SQLFetch** 또는 **SQLFetchScroll** 마치 호출 합니다.<br /><br /> 에 커서가 열린는 *StatementHandle*, 및 **SQLFetch** 또는 **SQLFetchScroll** 마치 호출 된 후 또는 결과 집합의 시작 되기 전에 커서가 있었기 하지만 결과 집합의 끝입니다.<br /><br /> 인수 *작업* SQL_DELETE, SQL_REFRESH, 또는 SQL_UPDATE, 및 커서 시작 이후 또는 결과 집합의 끝 이후에 결과 집합의 앞에 배치 되었습니다.|  
|40001|Serialization 오류|트랜잭션이 다른 트랜잭션 사용 하 여 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 실패 및 트랜잭션의 상태를 확인할 수 없습니다.|  
|42000|구문 오류 또는 액세스 위반|인수에 요청한 작업을 수행 하는 데 필요한 만큼의 행을 잠글 수 없습니다 *작업*합니다.<br /><br /> 인수에 대 한 요청에 따라 행을 잠글 수 없습니다 *LockType*합니다.|  
|44000|WITH CHECK OPTION 위반|*작업* 인수 SQL_UPDATE, 및 본된 테이블에서 수행 된 업데이트 되었거나 지정 하 여 생성 된 표시 테이블에서 파생 된 테이블 **WITH CHECK OPTION**하는 하나 이상의 행 영향을 받는 업데이트가 더 이상 표시 테이블에 표시 됩니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *StatementHandle*합니다. 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle*, 함수가 호출 후 및 다시는 *StatementHandle*합니다.<br /><br /> 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle* 의 서로 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. SQLSetPos 함수를 호출할 때이 비동기 함수 계속 실행 합니다.<br /><br /> (DM) 지정 된 *StatementHandle* 가 실행 된 상태가 아닙니다. 함수가 먼저 호출 하지 않고 호출 된 **SQLExecDirect**, **SQLExecute**, 또는 카탈로그 함수입니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.<br /><br /> DM ()는 드라이버에서 ODBC 2. *x* 드라이버 및 **SQLSetPos** 에 대해 호출 되었습니다는 *StatementHandle* 후 **SQLFetch** 호출 되었습니다.|  
|HY011|특성을 지금 설정할 수 없습니다.|DM ()는 드라이버에서 ODBC 2. *x* 드라이버; SQL_ATTR_ROW_STATUS_PTR을는 문 특성 설정 되었으면 다음 **SQLSetPos** 하기 전에 호출 된 **SQLFetch**, **SQLFetchScroll**, 또는 **SQLExtendedFetch** 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|*작업* SQL_UPDATE 되었습니다, 데이터 값이 null 포인터, 및 열 길이 값이 SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NULL_DATA, 0 또는 SQL_LEN_DATA_AT_EXEC_OFFSET 합니다.<br /><br /> *작업* 인수 SQL_UPDATE 않으면 데이터 값이 null 포인터; C 데이터 형식 SQL_C_BINARY 되었거나 SQL_C_CHAR; 되어 열 길이 값이 0 보다 작은 되었지만 SQL_DATA_AT_EXEC로 SQL_COLUMN_IGNORE 같지 않음 SQL_NTS 또는 SQL_NULL_DATA, 또는 SQL_LEN_DATA_AT_EXEC_OFFSET 합니다.<br /><br /> 길이/표시기 버퍼의 값이 SQL_DATA_AT_EXEC; SQL 형식이 SQL_LONGVARCHAR, SQL_LONGVARBINARY, 또는 long 데이터 원본에 따른 특정 데이터 형식 및에서 SQL_NEED_LONG_DATA_LEN 정보 유형을 **SQLGetInfo** "Y"가 있습니다.|  
|HY092|잘못 된 특성 식별자|(DM)에 대 한 지정 된 값은 *작업* 인수가 잘못 되었습니다.<br /><br /> (DM)에 대 한 지정 된 값은 *LockType* 인수가 잘못 되었습니다.<br /><br /> *작업* 인수 SQL_UPDATE 또는 SQL_DELETE, 한 문 특성 SQL_ATTR_CONCURRENCY SQL_ATTR_CONCUR_READ_ONLY 였습니다.|  
|HY107|행 값 범위를 벗어났습니다.|인수에 대해 지정 된 값 *RowNumber* 행 집합의 행 개수 보다 큽니다.|  
|HY109|잘못 된 커서 위치|연관 된 커서는 *StatementHandle* 행 집합 내에서 커서를 배치 될 수 있으므로 정방향 전용으로 정의 되었습니다. SQL_ATTR_CURSOR_TYPE 특성에 대 한 설명을 참조 **SQLSetStmtAttr**합니다.<br /><br /> *작업* 인수 SQL_UPDATE, SQL_DELETE, 또는 SQL_REFRESH, 였으며 행으로 식별는 *RowNumber* 인수를 삭제 한 또는 페치 하지 했습니다.<br /><br /> DM ()는 *RowNumber* 되었습니다. 0, 인수 및 *작업* SQL_POSITION 되었습니다.<br /><br /> **SQLSetPos** 후 호출 된 **SQLBulkOperations** 호출 하기 전에 **SQLFetchScroll** 또는 **SQLFetch** 호출 되었습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|드라이버 또는 데이터 원본에 요청 된 작업을 지원 하지 않습니다는 *작업* 인수 또는 *LockType* 인수입니다.|  
|HYT00|제한 시간이 만료되었습니다.|쿼리 제한 시간에는 데이터 원본의 결과 집합을 반환 하기 전에 만료 되었습니다. 제한 시간을 통해 설정 됩니다 **SQLSetStmtAttr** 와 *특성* SQL_ATTR_QUERY_TIMEOUT입니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>설명  
  
> [!CAUTION]  
>  없다는 문에 대 한 정보에 대 한 **SQLSetPos** 에서 호출할 수 있습니다 및 ODBC 2와 호환성을 위해 수행 하는 데*.x* 응용 프로그램 참조 [블록 커서, 스크롤 가능 커서 및 이전 버전과 호환성](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)합니다.  
  
## <a name="rownumber-argument"></a>RowNumber 인수  
 *RowNumber* 로 지정 된 작업을 수행할 행 집합의 행 수를 지정 하는 인수는 *작업* 인수입니다. 경우 *RowNumber* 가 0 이면 행 집합의 모든 행에 작업 적용 됩니다. *RowNumber* 행 집합의 행 수를 0 사이의 값 이어야 합니다.  
  
> [!NOTE]  
>  C 언어의 배열은 0부터 시작 및 *RowNumber* 인수는 1부터 시작 합니다. 예를 들어 행 집합의 5 번째 행을 업데이트 하려면 응용 프로그램 수정 4 배열 인덱스에서 행 집합 버퍼 하지만 지정 된 *RowNumber* 5입니다.  
  
 모든 작업에서 지정한 행에 커서를 배치 *RowNumber*합니다. 다음 작업 커서 위치에 필요 합니다.  
  
-   배치 update 및 delete 문입니다.  
  
-   에 대 한 호출이 **SQLGetData**합니다.  
  
-   에 대 한 호출이 **SQLSetPos** SQL_DELETE, SQL_REFRESH, 및 SQL_UPDATE 옵션을 사용 합니다.  
  
 예를 들어 경우 *RowNumber* 2에 대 한 호출에 대 한 **SQLSetPos** 와 *작업* SQL_DELETE의 커서 행 집합의 두 번째 행에 위치 하 고 해당 행이 삭제 됩니다. 구현 행 상태 배열 (SQL_ATTR_ROW_STATUS_PTR 문 특성에서 가리키는)에 두 번째 행의 항목은 SQL_ROW_DELETED로 변경 됩니다.  
  
 응용 프로그램를 호출할 때 커서 위치를 지정할 수 **SQLSetPos**합니다. 일반적으로 호출 **SQLSetPos** SQL_POSITION 또는 SQL_REFRESH 작업 배치를 실행 하기 전에 커서의 위치를 업데이트 또는 delete 문 또는 호출 **SQLGetData**합니다.  
  
## <a name="operation-argument"></a>Operation 인수  
 *작업* 인수는 다음 작업을 지원 합니다. 데이터 소스에서 옵션을 지 원하는 확인 하려면 응용 프로그램이 호출 **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1, 또는 SQL_STATIC_ (커서 유형)에 따라 다름 CURSOR_ATTRIBUTES1 정보 유형입니다.  
  
|*연산*<br /><br /> 인수(argument)|연산|  
|------------------------------|---------------|  
|SQL_POSITION|드라이버에서 지정한 행에 커서를 놓습니다 *RowNumber*합니다.<br /><br /> SQL_POSITION에 대 한 행 상태 배열이 SQL_ATTR_ROW_OPERATION_PTR 문 특성에서 가리키는의 내용이 무시 됩니다 *작업*합니다.|  
|SQL_REFRESH|드라이버에서 지정한 행에 커서를 놓습니다 *RowNumber* 하 고 해당 행에 대 한 행 집합 버퍼의에서 데이터를 새로 고칩니다. 드라이버는 행 집합 버퍼의 데이터를 반환 하는 방법에 대 한 자세한 내용은 열 단위 및 행 단위 바인딩의 설명을 참조 **SQLBindCol**합니다.<br /><br /> **SQLSetPos** 와 *작업* SQL_REFRESH의 상태 및 현재 인출 된 행 집합 내에서 행의 내용을 업데이트 합니다. 책갈피를 새로 고쳐 포함 됩니다. 버퍼의 데이터는 새로 고쳐지지만 하지에 따라 다시 인출, 때문에 행 집합의 멤버 자격이 고정 되어 있습니다. 이 새로 고침에 대 한 호출을 수행한 다릅니다 **SQLFetchScroll** 와 *FetchOrientation* SQL_FETCH_RELATIVE의 및 *RowNumber* 다시 0 이러한 작업은 드라이버 및 커서에 의해 지원 되는 경우 추가 된 데이터를 표시 하 고 제거할 수 있도록 설정 하는 결과에서 행 집합 데이터를 삭제 했습니다.<br /><br /> 성공적인 새로 **SQLSetPos** 행 상태의 sql_row_deleted가 변경 되지 것입니다. 행 집합 내에서 삭제 된 행은 다음 인출 될 때까지 삭제 된 것으로 표시 되어야 계속 됩니다. 행이 커서에서 압축을 지 원하는 경우 다음 인출에서 사라집니다 (에 후속 **SQLFetch** 또는 **SQLFetchScroll** 삭제 된 행을 반환 하지 않습니다).<br /><br /> 행 나타나지에서 새로 추가 **SQLSetPos** 수행 됩니다. 이 동작은 다른 **SQLFetchScroll** 와 *FetchType* SQL_FETCH_RELATIVE의 및 *RowNumber* 0도 있지만 현재 행 집합을 새로 고칩니다. 이러한 작업은 커서에서 지원 되는 경우 삭제 된 레코드를 팩 전이나 추가 된 레코드를 표시 합니다.<br /><br /> 성공적인 새로 **SQLSetPos** (행 상태 배열이 있는 경우) 행 상태의 SQL_ROW_ADDED SQL_ROW_SUCCESS를 변경 합니다.<br /><br /> 성공적인 새로 **SQLSetPos** (행 상태 배열이 있는 경우) SQL_ROW_UPDATED 행 상태의 행의 새 상태로 변경 됩니다.<br /><br /> 오류가 발생 하는 경우는 **SQLSetPos** 행에 대 한 작업을 행 상태 설정은 SQL_ROW_ERROR (행 상태 배열이 있는 경우).<br /><br /> SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES에서 새로 문 특성 SQL_ATTR_CONCURRENCY 사용 하 여 열린 커서의 경우 **SQLSetPos** 점을 감지할 데이터 소스에서 사용 하는 낙관적 동시성 값을 업데이트 해야 할 수는 행이 변경 됩니다. 이 경우 행 버전이 나 커서 동시성 확인에 사용 되는 값 행 집합 버퍼는 서버에서 새로 고칠 때마다 업데이트 됩니다. 이 새로 고쳐지는 각 행에 대해 발생 합니다.<br /><br /> SQL_REFRESH에 대 한 행 상태 배열이 SQL_ATTR_ROW_OPERATION_PTR 문 특성에서 가리키는의 내용이 무시 됩니다 *작업*합니다.|  
|SQL_UPDATE|드라이버에서 지정한 행에 커서를 놓습니다 *RowNumber* 행 집합 버퍼에 값을 사용 하 여 데이터의 기본 행 업데이트 (고 *TargetValuePtr* 인수  **SQLBindCol**). 길이/표시기 버퍼에서 데이터의 길이 검색 (의 *StrLen_or_IndPtr* 인수 **SQLBindCol**). 열 길이가 SQL_COLUMN_IGNORE 열 업데이트 되지 않습니다. 행을 업데이트 한 다음 드라이버 (행 상태 배열이 있는 경우) SQL_ROW_UPDATED 또는 SQL_ROW_SUCCESS_WITH_INFO 행 상태 배열이의 해당 요소를 변경 합니다.<br /><br /> 드라이버에서 정의 된 것은 동작 하는 경우 **SQLSetPos** 와 *작업* SQL_UPDATE의 인수는 중복 된 열을 포함 하는 커서에 대해 호출 됩니다. 드라이버는 드라이버에서 정의 된 SQLSTATE를 반환할 수 있습니다, 그리고 결과 집합에 나타나는 첫 번째 열을 업데이트 하거나 다른 드라이버에서 정의 된 동작을 수행할 수 있습니다.<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 문 특성에서 가리키는 행 작업 배열은 현재 행 집합의 행에 대해 대량 업데이트 중 무시 되어야 함을 나타내는 데 사용할 수 있습니다. 자세한 내용은이 함수 참조의 뒷부분에 나오는 "상태 및 작업 배열"를 참조 합니다.|  
|SQL_DELETE|드라이버에서 지정한 행에 커서를 놓습니다 *RowNumber* 데이터의 기본 행을 삭제 합니다. 행 상태 배열이의 해당 요소 sql_row_deleted가 변경 됩니다. 해당 행이 삭제 된 후 다음 행에 유효 하지 않습니다: 배치 update 및 delete 문에 대 한 호출 **SQLGetData**에 대 한 **SQLSetPos** 와 *작업* SQL_POSITION 제외 하 고 값으로 설정 합니다. 압축 지원 드라이버, 데이터 원본에서 새 데이터를 검색할 때 커서에서 행이 삭제 합니다.<br /><br /> 행 설명이 표시 되는 커서 유형에 따라 달라 집니다. 예를 들어, 삭제 된 행이 정적 및 키 집합 커서에 표시 되기는 하지만 동적 커서에 표시 됩니다.<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 문 특성에서 가리키는 행 작업 배열은 현재 행 집합의 행 대량 삭제 중 무시 해야 함을 나타내는 데 사용할 수 있습니다. 자세한 내용은이 함수 참조의 뒷부분에 나오는 "상태 및 작업 배열"를 참조 합니다.|  
  
## <a name="locktype-argument"></a>LockType 인수  
 *LockType* 인수 응용 프로그램의 동시성 제어 하는 방법을 제공 합니다. 대부분의 경우에서 동시성 수준 및 트랜잭션을 지 원하는 데이터 원본만 SQL_LOCK_NO_CHANGE 값을 지원 합니다는 *LockType* 인수입니다. *LockType* 인수는 일반적으로 파일 기반 지원에만 사용 됩니다.  
  
 *LockType* 후 행 잠금 상태를 지정 하는 인수 **SQLSetPos** 실행 된 합니다. 드라이버를 요청한 작업을 수행 하거나 충족 하기 위해 행을 잠글 수 없는 경우는 *LockType* SQL_ERROR 및 SQLSTATE 42000 (구문 오류 또는 액세스 위반) 반환 인수입니다.  
  
 하지만 *LockType* 잠금을 accords 연결에서 모든 문에 동일한 권한, 단일 문에 대 한 인수를 지정 합니다. 특히, 한 획득 된 잠금에 대 한 연결에 하나의 문에서 동일한 연결에서 다른 문의 잠금을 해제할 수 있습니다.  
  
 통해 행 잠금 **SQLSetPos** 응용 프로그램 호출 될 때까지 잠금이 유지 **SQLSetPos** 인 행에 대 한 *LockType* SQL_LOCK_UNLOCK, 또는 응용 프로그램까지 설정 호출 **SQLFreeHandle** 문에 대 한 또는 **SQLFreeStmt** SQL_CLOSE 옵션을 사용 합니다. 트랜잭션을 지 원하는 드라이버를 통해 행 잠금 **SQLSetPos** 잠겨 있지는 응용 프로그램 호출 때 **SQLEndTran** 커밋하거나 롤백하는 연결에서 (커서를 닫을 경우 트랜잭션이 커밋 또는 롤백된 경우 반환한 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 유형에 의해 표시 된 대로 **SQLGetInfo**).  
  
 *LockType* 인수는 다음과 같은 유형의 잠금을 지원 합니다. 데이터 소스에서는 잠금을 지 원하는 확인 하려면 응용 프로그램이 호출 **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1, 또는 SQL_STATIC_ (커서 유형)에 따라 다름 CURSOR_ATTRIBUTES1 정보 유형입니다.  
  
|*LockType* 인수|잠금 유형|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|드라이버 또는 데이터 원본 되기 전의 행 동일한 잠금 또는 잠금 해제 된 상태 인지 확인 **SQLSetPos** 호출 되었습니다. 이 값의 *LockType* 명시적 행 수준 잠금을 현재 동시성 및 트랜잭션 격리 수준에서 필요한 모든 잠금을 사용 하도록 지원 하지 않는 데이터 소스를 허용 합니다.|  
|SQL_LOCK_EXCLUSIVE|드라이버 또는 데이터 원본에서 행을 단독으로 잠깁니다. 행에 대 한 모든 잠금을 얻으려고 문 다른 연결에서 또는 다른 응용 프로그램에서을 사용할 수 없습니다.|  
|SQL_LOCK_UNLOCK|드라이버 또는 데이터 원본에는 행 잠금을 해제합니다.|  
  
 드라이버 SQL_LOCK_EXCLUSIVE를 지원 하지만 SQL_LOCK_UNLOCK를 지원 하지 않습니다, 경우 이전 단락에서 설명한 함수 호출 중 하나가 발생할 때까지 잠긴 행은 잠긴 상태로 유지 됩니다.  
  
 드라이버 SQL_LOCK_EXCLUSIVE를 지원 하지만 SQL_LOCK_UNLOCK를 지원 하지 않습니다, 잠긴 행 잠긴 상태가 유지 되며 응용 프로그램 호출할 때까지 **SQLFreeHandle** 문에 대 한 또는 **SQLFreeStmt** 와 SQL_CLOSE 옵션입니다. 드라이버에서 트랜잭션을 지원 하 고 커밋 또는 응용 프로그램 호출 하 여 트랜잭션 롤백 시 커서를 닫습니다 경우 **SQLEndTran**합니다.  
  
 업데이트 및 삭제 작업을 위해 **SQLSetPos**, 응용 프로그램에서 사용 하 여는 *LockType* 다음과 같이 인수:  
  
-   응용 프로그램이 검색 된 후 행 변경 되지 않습니다을 보장 하기 위해 호출 **SQLSetPos** 와 *작업* SQL_REFRESH로 설정 하 고 *LockType* SQL_LOCK_로 설정 단독 잠금.  
  
-   응용 프로그램을 설정 하는 경우 *LockType* 드라이버 SQL_LOCK_NO_CHANGE에 업데이트 또는 삭제 작업이 응용 프로그램 SQL_ATTR_CONCURRENCY 문 특성에 대 한 sql_concur_lock으로 지정한 경우에 성공할 지을 보장 합니다.  
  
-   SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES SQL_ATTR_CONCURRENCY 문 특성을 지정 하는 응용 프로그램, 드라이버와 행 버전이 나 값을 비교 행을 인출 하는 응용 프로그램이 이후 변경 된 행이 경우 작업을 거부 합니다.  
  
-   문 특성 SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY를 지정 하는 응용 프로그램, 하는 경우 드라이버가 모든 업데이트 또는 삭제.  
  
 문 특성 SQL_ATTR_CONCURRENCY에 대 한 자세한 내용은 참조 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)합니다.  
  
## <a name="status-and-operation-arrays"></a>상태 및 작업 배열  
 호출할 때 사용 되는 다음과 같은 상태 및 작업 배열을 **SQLSetPos**:  
  
-   행 상태 배열이 (IRD 및 SQL_ATTR_ROW_STATUS_ARRAY 문 특성에서 SQL_DESC_ARRAY_STATUS_PTR 필드에서 가리키는)으로 행 집합의 데이터의 각 행에 대 한 상태 값을 포함 합니다. 드라이버를 호출한 후 상태 값이이 배열에 설정 **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, 또는 **SQLSetPos** . 이 배열은 SQL_ATTR_ROW_STATUS_PTR 문 특성 가리키는입니다.  
  
-   행 작업 배열을 (SQL_DESC_ARRAY_STATUS_PTR 필드는 카드가 및 SQL_ATTR_ROW_OPERATION_ARRAY 문 특성에서 가리키는) 대로 나타내는 행 집합의 각 행에 대 한 값이 포함 여부에 대 한 호출 **SQLSetPos**대량 작업을 무시 하거나 수행 됩니다. 배열의 각 요소는 SQL_ROW_PROCEED (기본값) 또는 SQL_ROW_IGNORE로 설정 됩니다. 이 배열은 SQL_ATTR_ROW_OPERATION_PTR 문 특성 가리키는입니다.  
  
 상태 및 작업 배열의 요소 수 (SQL_ATTR_ROW_ARRAY_SIZE 문 특성에 정의 된) 하는 대로 행 집합의 행 수와 같아야 합니다.  
  
 행 상태 배열이 대 한 정보를 참조 하십시오. [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)합니다. 행 작업 배열에 대 한 내용은 "무시 하 고는 행에는 대량 작업을"이이 섹션의 뒷부분에 나오는 참조 하십시오.  
  
## <a name="using-sqlsetpos"></a>SQLSetPos를 사용 하 여  
 응용 프로그램이 호출 되기 전에 **SQLSetPos**, 다음과 같은 일련의 단계를 수행 해야 합니다.  
  
1.  응용 프로그램에서 호출할 경우 **SQLSetPos** 와 *작업* SQL_UPDATE, 호출으로 설정 **SQLBindCol** (또는 **SQLSetDescRec**) 각각에 대해 열의 데이터 및 길이 대 한 버퍼를 바인딩하고 해당 데이터 형식을 지정 하는 열입니다.  
  
2.  응용 프로그램에서 호출할 경우 **SQLSetPos** 와 *작업* SQL_DELETE 또는 SQL_UPDATE, 호출으로 설정 **SQLColAttribute** 고유 하도록 열을 삭제 하거나 업데이트할 수 업데이트할 수 없습니다.  
  
3.  호출 **SQLExecDirect**, **SQLExecute**, 또는 카탈로그 함수 결과 집합을 만듭니다.  
  
4.  호출 **SQLFetch** 또는 **SQLFetchScroll** 데이터를 검색 합니다.  
  
 사용에 대 한 자세한 내용은 **SQLSetPos**, 참조 [SQLSetPos 사용 하 여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)합니다.  
  
## <a name="deleting-data-using-sqlsetpos"></a>SQLSetPos를 사용 하 여 데이터를 삭제 합니다.  
 사용 하 여 데이터를 삭제 하려면 **SQLSetPos**, 응용 프로그램이 호출 **SQLSetPos** 와 *RowNumber* 삭제 하는 행의 수로 설정 하 고 *작업*SQL_DELETE로 설정 합니다.  
  
 데이터를 삭제 한 다음 드라이버는 sql_row_deleted가 (또는 SQL_ROW_ERROR) 적절 한 행에 대 한 구현 행 상태 배열이에 값을 변경 합니다.  
  
## <a name="updating-data-using-sqlsetpos"></a>SQLSetPos를 사용 하 여 데이터를 업데이트 합니다.  
 응용 프로그램이 바인딩된 데이터 버퍼 또는 하나 이상의 호출을 통해 열에 대 한 값을 전달할 수 **SQLPutData**합니다. 데이터와 함께 전달 되는 열 **SQLPutData** 라고 *실행 시 데이터* *열*합니다. 이러한 SQL_LONGVARBINARY 및 SQL_LONGVARCHAR 열에 대 한 데이터를 보내는 데 일반적으로 사용 하 고 다른 열과 함께 사용할 수 있습니다.  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>SQLSetPos, 응용 프로그램 데이터를 업데이트 하려면:  
  
1.  데이터 및 길이/표시기 버퍼에 환경 값과 바인딩된 **SQLBindCol**:  
  
    -   일반 열에 대 한 응용 프로그램에 새 열 값이 배치는  *\*TargetValuePtr* 버퍼와 해당 값의 길이  *\*StrLen_or_IndPtr* 버퍼입니다. 행을 업데이트 되지 않아야 하는 경우 응용 프로그램 SQL_ROW_IGNORE 행 작업 배열의 해당 행의 요소에 배치 합니다.  
  
    -   실행 시 데이터 열에 대 한 응용 프로그램에는 열 번호와 같은 응용 프로그램 정의 값을 배치는  *\*TargetValuePtr* 버퍼입니다. 열을 식별 하는 값을 나중에 사용할 수 있습니다.  
  
         응용 프로그램은 SQL_LEN_DATA_AT_EXEC의 결과 배치 (*길이*)에서 매크로 **StrLen_or_IndPtr* 버퍼입니다. SQL 데이터 형식의 열은 SQL_LONGVARBINARY, SQL_LONGVARCHAR 또는 long 데이터 원본에 따른 특정 데이터 형식이 고 드라이버 반환 "Y" SQL_NEED_LONG_DATA_LEN 정보 유형에 대해에서 **SQLGetInfo**, *길이*  ; 매개 변수에 대해 전달할 데이터의 바이트 수, 음수가 아닌 값 이어야 하 고는 무시 됩니다.  
  
2.  호출 **SQLSetPos** 와 *작업* 인수는 데이터의 행을 업데이트 하려면 SQL_UPDATE로 설정 합니다.  
  
    -   실행 시 데이터 열이 없는 경우 프로세스 완료 되었습니다.  
  
    -   모든 실행 시 데이터 열이 있는 경우 함수 sql_need_data가 반환 하 고 3 단계로 진행 됩니다.  
  
3.  호출 **SQLParamData** 의 주소를 검색 하는  *\*TargetValuePtr* 처리할 첫 번째 실행 시 데이터 열에 대 한 버퍼입니다. **SQLParamData** SQL_NEED_DATA를 반환 합니다. 응용 프로그램 정의 값을 검색 하는 응용 프로그램의  *\*TargetValuePtr* 버퍼입니다.  
  
    > [!NOTE]  
    >  반환 된 값 실행 시 데이터 매개 변수가 실행 시 데이터 열과 비슷한 이기는 하지만 **SQLParamData** 을에 따라 다릅니다.  
  
    > [!NOTE]  
    >  실행 시 데이터 매개 변수를 데이터 전송 하는 SQL 문의 매개 변수에 **SQLPutData** 와 문이 실행 되는 경우 **SQLExecDirect** 또는 **SQLExecute**. 연결 된 **SQLBindParameter** 또는 설명자를 설정 하 여 **SQLSetDescRec**합니다. 반환한 값 **SQLParamData** 에 전달 되는 32 비트 값은 **SQLBindParameter** 에 *ParameterValuePtr* 인수입니다.  
  
    > [!NOTE]  
    >  실행 시 데이터 열을 데이터 전송 하는 행 집합의 열은 **SQLPutData** 행으로 업데이트 될 때 **SQLSetPos**합니다. 연결 된 **SQLBindCol**합니다. 반환한 값 **SQLParamData** 는에 있는 행의 주소는 **TargetValuePtr* 처리 중인 버퍼입니다.  
  
4.  호출 **SQLPutData** 한 번 이상 열에 대 한 데이터를 보내려고 합니다. 한 번 이상 호출 하는 경우 모든 데이터 값으로 반환할 수 없습니다는  *\*TargetValuePtr* 에 지정 된 버퍼 **SQLPutData**;를 여러 번 호출 **SQLPutData** 데이터 원본에 따른 특정 데이터 형식 또는 같은 열은 문자, 이진, 지정 된 열에 이진 C 데이터를 보낼 때 또는는 문자, 이진, 또는 데이터 원본에 따른 특정 데이터 형식과 열에 문자 데이터를 보낼 때만 허용 됩니다.  
  
5.  호출 **SQLParamData** 모든 데이터 열에 대 한 보냈음을 알리는 돌아갑니다.  
  
    -   더 많은 실행 시 데이터 열이 있는 경우 **SQLParamData** SQL_NEED_DATA를 반환 하는의 주소는 *TargetValuePtr* 처리할 다음 실행 시 데이터 열에 대 한 버퍼입니다. 응용 프로그램 4, 5 단계를 반복합니다.  
  
    -   더 이상 실행 시 데이터 열이 있는 경우에 프로세스가 완료 됩니다. 문이 성공적으로 실행 한 경우 **SQLParamData** SQL_SUCCESS 또는; SQL_SUCCESS_WITH_INFO를 반환 합니다. 실행이 실패 SQL_ERROR를 반환 합니다. 이 시점에서 **SQLParamData** 에서 반환 될 수 있는 모든 SQLSTATE를 반환할 수 **SQLSetPos**합니다.  
  
 데이터 업데이트 되었으면 드라이버 SQL_ROW_UPDATED에 적절 한 행에 대 한 구현 행 상태 배열이에 값을 변경 합니다.  
  
 작업이 취소 되는 경우 또는에서 오류가 발생 **SQLParamData** 또는 **SQLPutData**이후에 **SQLSetPos** SQL_NEED_DATA를 반환 합니다. 모든 데이터를 보내기 전에 및 실행 시 데이터 열을 응용 프로그램 에서만 호출할 수 **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions** , **SQLParamData**, 또는 **SQLPutData** 문이나 문과 연결 된 연결에 대 한 합니다. 함수 반환 SQL_ERROR 및 SQLSTATE HY010 문이나 문과 연결 된 연결에 대 한 다른 어떤 기능을 호출 하면 (함수 시퀀스 오류).  
  
 응용 프로그램을 호출 하는 경우 **SQLCancel** 드라이버 작업을 취소 하는 동안 드라이버 실행 시 데이터 열에 대 한 데이터를 여전히 필요 합니다. 응용 프로그램이 호출할 수 **SQLSetPos** 다시; 취소 영향을 주지 않습니다 커서 상태 또는 현재 커서 위치입니다.  
  
 오류가 발생 하거나 중복 된 참조를 무시 하 고 요청 된 작업을 수행 하는 드라이버 커서와 관련 된 쿼리 사양 중 선택 목록에서 같은 열에 대 한 참조를 여러 개를 포함 하는 경우는 드라이버 정의입니다.  
  
## <a name="performing-bulk-operations"></a>대량 작업 수행  
 경우는 *RowNumber* 인수는 0에 지정 된 작업을 수행 하는 드라이버는 *작업* 행 작업에서 해당 필드에서 SQL_ROW_PROCEED의 값을 갖도록 하는 행 집합의 모든 행에 대 한 인수 문 특성 SQL_ATTR_ROW_OPERATION_PTR 가리키는 배열입니다. 유효한 값은이 *RowNumber* 에 대 한 인수는 *작업* SQL_DELETE, SQL_REFRESH, 또는 SQL_UPDATE, 있지만 하지 SQL_POSITION의 인수입니다. **SQLSetPos** 와 *작업* SQL_POSITION의 및 *RowNumber* 0 같음 SQLSTATE HY109 반환 됩니다 (잘못 된 커서 위치).  
  
 SQLSTATE HYT00 등 전체 행 집합에 관련 된 오류가 발생 하는 경우 (제한 시간 만료 됨), 드라이버 SQL_ERROR와 적절 한 SQLSTATE를 반환 합니다. 행 집합 버퍼의 내용을 정의 되지 않으며 커서 위치는 변경 되지 않습니다.  
  
 오류가 발생 하는 경우 관련 된 단일 행에는 드라이버:  
  
-   SQL_ATTR_ROW_STATUS_PTR 문 특성 SQL_ROW_ERROR 가리키는 행 상태 배열이의 행에 대 한 요소를 설정 합니다.  
  
-   오류에 대 한 하나 이상의 추가 SQLSTATEs 오류 큐에 게시 하 고 진단 데이터 구조에서 SQL_DIAG_ROW_NUMBER 필드를 설정 합니다.  
  
 드라이버는 행 집합의 나머지 행에 대 한 작업을 완료 하는 경우 오류나 경고를 처리, 후 SQL_SUCCESS_WITH_INFO를 반환 합니다. 따라서 오류 큐에서 오류를 반환 하는 각 행에 대해 0 개 이상의 추가 Sqlstate를 포함 합니다. 오류 또는 경고 처리 후 작업을 중지 하는 드라이버, SQL_ERROR를 반환 합니다.  
  
 모든 경고, SQLSTATE 01004 같은 (데이터 잘림)를 반환 하는 드라이버 특정 행에 적용 되는 오류 정보를 반환 하기 전에 전체 행 집합 또는 알 수 없는 행에에서 적용 되는 경고를 반환 합니다. 이러한 행에 대 한 다른 오류 정보가 특정 행에 대 한 경고를 반환합니다.  
  
 경우 *RowNumber* 가 0 및 *작업* SQL_UPDATE, SQL_REFRESH, 또는 SQL_DELETE, 하는 행의 수 **SQLSetPos** 작동에 2를 가리키고는 SQL_ATTR_ROWS _FETCHED_PTR 문 특성입니다.  
  
 경우 *RowNumber* 가 0 및 *작업* SQL_DELETE, SQL_REFRESH, 또는 SQL_UPDATE, 현재 행 후 작업을 작업 앞에 있는 현재 행과 같습니다.  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>대량 작업에서 행을 무시합니다.  
 행 작업 배열을 현재 행 집합의 행을 사용 하 여 대량 작업 중 무시 되어야 함을 나타내는 데 사용할 수 있습니다 **SQLSetPos**합니다. 응용 프로그램에 대량 작업 중 하나 이상의 행이 무시 되도록 드라이버를 지시 하는 경우, 다음 단계를 수행 해야:  
  
1.  호출 **SQLSetStmtAttr** SQLUSMALLINTs 배열을를 가리키도록 SQL_ATTR_ROW_OPERATION_PTR 문 특성을 설정 합니다. 이 필드를 호출 하 여 설정할 수도 있습니다 **SQLSetDescField** 응용 프로그램에서는 설명자 핸들 하 가져옵니다 엔드가 카드가의 SQL_DESC_ARRAY_STATUS_PTR 헤더 필드를 설정할 수 있습니다.  
  
2.  행 작업 배열의 각 요소 두 값 중 하나로 설정 합니다.  
  
    -   SQL_ROW_IGNORE 대량 작업에 대 한 행 제외 되었음을 나타냅니다.  
  
    -   SQL_ROW_PROCEED 행 대량 작업에 포함 되어 있는지를 나타냅니다. True(기본값)임  
  
3.  호출 **SQLSetPos** 대량 작업을 수행할 수 있습니다.  
  
 행 작업 배열을 다음 규칙이 적용 됩니다.  
  
-   SQL_ROW_IGNORE 및 SQL_ROW_PROCEED 사용 하 여 대량 작업에만 영향을 미칩니다 **SQLSetPos** 와 *작업* SQL_DELETE 또는 SQL_UPDATE 합니다. 에 대 한 호출에 영향을 주지 **SQLSetPos** 와 *작업* SQL_REFRESH 또는 SQL_POSITION 합니다.  
  
-   포인터가 설정 되어 기본적으로 null로 합니다.  
  
-   포인터가 null 이면 모든 행은 모든 요소 SQL_ROW_PROCEED 하도록 설정 된 경우에 따라 업데이트 됩니다.  
  
-   SQL_ROW_PROCEED에 요소를 설정 하는 작업이 해당 특정 행에 수행 되는지 보장 하지 않습니다. 예를 들어 행 집합의 특정 행에 있는 상태 SQL_ROW_ERROR 경우 드라이버 수 있습니다 응용 프로그램의 SQL_ROW_PROCEED 지정 여부에 관계 없이 해당 행을 업데이트할 수 없습니다. 응용 프로그램 작업이 성공 했는지 확인 하려면 행 상태 배열이 항상 확인 해야 합니다.  
  
-   SQL_ROW_PROCEED 헤더 파일에는 0으로 정의 됩니다. 응용 프로그램에 모든 행을 처리 하기 위해 0으로 행 작업 배열을 초기화할 수 있습니다.  
  
-   행 작업 배열의 요소 수 "n" SQL_ROW_IGNORE로 설정 되어 있으면 및 **SQLSetPos** 대량 업데이트를 수행 하거나 작업을 호출한 후 변경 되지 않은 행 집합은 n 번째 행을 삭제 하기 위해 호출 **SQLSetPos**.  
  
-   자동으로 응용 프로그램 SQL_ROW_IGNORE에 읽기 전용 열을 설정 해야 합니다.  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>대량 작업에서 열을 무시합니다.  
 시도 된 하나 이상의 읽기 전용 열이 업데이트에 의해 생성 된 불필요 한 처리 진단을 방지 하려면 응용 프로그램 SQL_COLUMN_IGNORE 바인딩된 길이/표시기 버퍼의 값을 설정할 수 있습니다. 자세한 내용은 참조 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)합니다.  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서는 응용 프로그램에 ORDERS 테이블을 찾아 주문 상태를 업데이트 한 사용자 수 있습니다. 커서 행 집합 크기를 20으로 키 집합 기반 하며 행 버전을 비교 하는 낙관적 동시성 제어를 사용 합니다. 각 행 집합은 인출 된 후 응용 프로그램에 출력 하 고 선택 하 고 주문 상태를 업데이트할 수 있습니다. 응용 프로그램이 사용 **SQLSetPos** 선택 된 행에 커서를 배치 하 고 행의 위치 지정된 업데이트를 수행 합니다. (오류 처리는 명확한 설명을 위해 생략 됨).  
  
```  
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
  
 더 많은 예제를 참조 하십시오. [배치 Update 및 Delete 문이](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) 및 [SQLSetPos이 있는 행 집합의 행 업데이트](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|블록 커서 위치와 관련이 없으며 대량 작업 수행|[SQLBulkOperations 함수](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|데이터 블록을 인출 또는 스크롤 하는 결과 집합|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|설명자의 단일 필드 가져오기|[SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|설명자의 여러 필드 가져오기|[SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|설명자의 단일 필드를 설정합니다.|[SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|설명자의 여러 필드를 설정합니다.|[SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

