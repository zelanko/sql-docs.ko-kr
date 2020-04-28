---
title: SQLMoreResults 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLMoreResults
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLMoreResults
helpviewer_keywords:
- SQLMoreResults function [ODBC]
ms.assetid: bf169ed5-4d55-412c-b184-12065a726e89
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78bbb277e4b783eb46c79f59939a1080feae2b60
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304744"
---
# <a name="sqlmoreresults-function"></a>SQLMoreResults 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **SQLMoreResults** 는 **select**, **UPDATE**, **INSERT**또는 **DELETE** 문이 포함 된 문에서 더 많은 결과를 사용할 수 있는지 여부를 확인 하 고, 그럴 경우 해당 결과에 대 한 처리를 초기화 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_PARAM_DATA_AVAILABLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLMoreResults** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLMoreResults** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01 S 02|옵션 값이 변경 되었습니다.|일괄 처리를 처리 하는 중에 문 특성의 값이 변경 되었습니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|40001|Serialization 오류|다른 트랜잭션과의 리소스 교착 상태 때문에 트랜잭션이 롤백 되었습니다.|  
|40003|문 완료를 알 수 없음|이 함수를 실행 하는 동안 연결 된 연결에 실패 하 여 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. **SQLMoreResults** 함수를 호출 했지만 실행이 완료 되기 전에 **Sqlcancel** 또는 **sqlcancelhandle** 이 *StatementHandle*에 대해 호출 되었습니다. 그런 다음 *StatementHandle*에서 **SQLMoreResults** 함수를 다시 호출 했습니다.<br /><br /> **SQLMoreResults** 함수를 호출 했지만 실행이 완료 되기 전에 **Sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 에 대해 호출 되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLMoreResults** 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SELECT** 문은 결과 집합을 반환 합니다. **UPDATE**, **INSERT**및 **DELETE** 문은 영향을 받는 행의 수를 반환 합니다. 이러한 문이 일괄 처리 되는 경우 매개 변수 배열 (일괄 처리에 표시 되는 순서 대로 매개 변수 순서에 따라 번호가 매겨져 있음) 또는 프로시저에서 여러 개의 결과 집합이 나 행 개수를 반환할 수 있습니다. 문 및 매개 변수 배열의 일괄 처리에 대 한 자세한 내용은 [SQL 문 일괄 처리](../../../odbc/reference/develop-app/batches-of-sql-statements.md) 및 [매개 변수 값 배열](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)을 참조 하세요.  
  
 일괄 처리를 실행 한 후 응용 프로그램은 첫 번째 결과 집합에 배치 됩니다. 응용 프로그램은 단일 결과 집합이 있는 경우와 마찬가지로 첫 번째 또는 그 이후의 결과 집합에서 **SQLBindCol**, **SQLBulkOperations**, **sqlfetch**, **SQLGetData**, **sqlfetchscroll**, **SQLSetPos**및 모든 메타 데이터 함수를 호출할 수 있습니다. 첫 번째 결과 집합으로 완료 되 면 응용 프로그램은 **SQLMoreResults** 를 호출 하 여 다음 결과 집합으로 이동 합니다. 다른 결과 집합 또는 수를 사용할 수 있는 경우 **SQLMoreResults** 는 SQL_SUCCESS을 반환 하 고 추가 처리를 위해 결과 집합 또는 개수를 초기화 합니다. 행 개수 생성 문이 결과 집합 생성 문 사이에 표시 되는 경우 **SQLMoreResults**를 호출 하 여 단계별로 실행할 수 있습니다. **UPDATE**, **INSERT**또는 **DELETE** 문에 대해 **SQLMoreResults** 를 호출한 후 응용 프로그램에서 **sqlrowcount**를 호출할 수 있습니다.  
  
 인출 되지 않은 rows를 포함 하는 현재 결과 집합이 있는 경우 **SQLMoreResults** 은 해당 결과 집합을 삭제 하 고 다음 결과 집합 또는 개수를 사용할 수 있도록 합니다. 모든 결과가 처리 된 경우 **SQLMoreResults** 는 SQL_NO_DATA을 반환 합니다. 일부 드라이버의 경우 모든 결과 집합과 행 개수가 처리 될 때까지 출력 매개 변수와 반환 값을 사용할 수 없습니다. 이러한 드라이버의 경우 **SQLMoreResults** 가 SQL_NO_DATA를 반환할 때 출력 매개 변수 및 반환 값을 사용할 수 있습니다.  
  
 이전 결과 집합에 대해 설정 된 모든 바인딩은 계속 유효한 상태로 유지 됩니다. 이 결과 집합에 대해 열 구조가 다른 경우 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하면 오류 또는 잘림이 발생할 수 있습니다. 이를 방지 하기 위해 응용 프로그램은 **SQLBindCol** 를 호출 하 여 적절 하 게 명시적으로 다시 바인딩해야 합니다 (또는 설명자 필드를 설정 하 여). 또는 SQL_UNBIND *옵션* 으로 **SQLFreeStmt** 를 호출 하 여 모든 열 버퍼의 바인딩을 해제할 수 있습니다.  
  
 응용 프로그램에서 **SQLMoreResults**를 호출 하 여 일괄 처리를 탐색할 때 커서 유형, 커서 동시성, 키 집합 크기 또는 최대 길이와 같은 statement 특성의 값이 변경 될 수 있습니다. 이 경우 **SQLMoreResults** 는 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01 S 02 (옵션 값이 변경 됨)를 반환 합니다.  
  
 SQL_CLOSE *옵션* 을 사용 하 여 **SQLCloseCursor**또는 **SQLFreeStmt** 를 호출 하면 일괄 처리 실행의 결과로 사용 가능한 모든 결과 집합과 행 수가 무시 됩니다. 문 핸들은 할당 된 또는 준비 된 상태로 돌아갑니다. 일괄 처리를 실행 했을 때 비동기 실행 함수를 취소 하기 위해 **Sqlcancel** 을 호출 하 고, 문 핸들이 실행 중이 고, 커서 위치 지정 또는 비동기 상태 이면 취소 호출에 성공한 경우 일괄 처리에 의해 생성 된 모든 결과 집합 및 행 개수가 삭제 됩니다. 그런 다음 문은 준비 됨 또는 할당 됨 상태로 돌아갑니다.  
  
 문 또는 프로시저 일괄 처리에서 **SELECT**, **UPDATE**, **INSERT**및 **DELETE** 문을 사용 하 여 다른 SQL 문을 혼합 하는 경우 이러한 다른 문은 **SQLMoreResults**에 영향을 주지 않습니다.  
  
 자세한 내용은 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)를 참조 하세요.  
  
 문 일괄 처리에서 검색 된 update, insert 또는 delete 문이 데이터 원본의 어떤 행에도 영향을 주지 않으면 **SQLMoreResults** 는 SQL_SUCCESS을 반환 합니다. 이는 **Sqlexecdirect**, **Sqlexecute**또는 **sqlexecdirect**를 통해 실행 되는 검색 된 update, insert 또는 delete 문의 경우와는 다릅니다 .이는 데이터 원본의 행에 영향을 주지 않는 경우 SQL_NO_DATA를 반환 합니다. **SQLMoreResults** 에 대 한 호출로 인해 응용 프로그램에서 **sqlrowcount** 를 호출 하 여 행 개수를 검색 하는 경우 **sqlrowcount** 는 SQL_NO_DATA을 반환 합니다.  
  
 유효한 결과 처리 함수 시퀀싱에 대 한 자세한 내용은 [부록 B: ODBC 상태 전환 표](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)를 참조 하세요.  
  
 SQL_PARAM_DATA_AVAILABLE 및 스트리밍된 출력 매개 변수에 대 한 자세한 내용은 [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)을 참조 하세요.  
  
## <a name="availability-of-row-counts"></a>행 개수 사용 가능  
 일괄 처리에 연속 행 개수 생성 문이 여러 개 있는 경우 이러한 행 개수가 하나의 행 개수로 롤업되는 것이 가능 합니다. 예를 들어 일괄 처리에 5 개의 insert 문이 있는 경우 특정 데이터 원본은 5 개의 개별 행 개수를 반환할 수 있습니다. 다른 특정 데이터 원본은 5 개의 개별 행 수의 합계를 나타내는 행 수를 하나만 반환 합니다.  
  
 일괄 처리에 결과 집합 생성 및 행 개수 생성 문의 조합이 포함 되어 있으면 행 개수는 전혀 사용 하지 못할 수도 있습니다. 행 개수의 가용성과 관련 된 드라이버 동작은 **SQLGetInfo**를 호출 하 여 사용할 수 있는 SQL_BATCH_ROW_COUNT 정보 형식으로 열거 됩니다. 예를 들어 일괄 처리에 **select**와 두 개의 **INSERT**와 다른 **select**가 포함 되어 있다고 가정 합니다. 그러면 다음과 같은 경우가 발생할 수 있습니다.  
  
-   두 **INSERT** 문에 해당 하는 행 개수는 사용할 수 없습니다. **SQLMoreResults** 에 대 한 첫 번째 호출에서는 두 번째 **SELECT** 문의 결과 집합을 배치 합니다.  
  
-   두 **INSERT** 문에 해당 하는 행 개수는 개별적으로 사용할 수 있습니다. **SQLGetInfo** 를 호출 하면 SQL_BATCH_ROW_COUNT 된 정보 형식에 대 한 SQL_BRC_ROLLED_UP 비트가 반환 되지 않습니다. **SQLMoreResults** 에 대 한 첫 번째 호출에서 첫 번째 **삽입**의 행 수를 표시 하 고 두 번째 호출은 두 번째 **삽입**의 행 수에 따라 배치 됩니다. **SQLMoreResults** 에 대 한 세 번째 호출에서는 두 번째 **SELECT** 문의 결과 집합을 배치 합니다.  
  
-   두 **삽입** 에 해당 하는 행 개수는 사용할 수 있는 하나의 단일 행 개수로 롤업 됩니다. **SQLGetInfo** 를 호출 하면 SQL_BATCH_ROW_COUNT 된 정보 형식에 대 한 SQL_BRC_ROLLED_UP 비트가 반환 됩니다. **SQLMoreResults** 에 대 한 첫 번째 호출에서는 롤업 된 행 수를 표시 하 고, **SQLMoreResults** 에 대 한 두 번째 호출에서는 두 번째 **SELECT**의 결과 집합을 배치 합니다.  
  
 특정 드라이버는 행 수를 명시적 일괄 처리에 대해서만 사용할 수 있으며 저장 프로시저에 대해서는 사용할 수 없습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|데이터 블록 가져오기 또는 결과 집합을 통한 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|정방향 전용 방향으로 단일 행 또는 데이터 블록 페치|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 열의 일부 또는 전체를 가져오는 중|[SQLGetData 함수(SQLGetData Function)](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData를 사용하여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
