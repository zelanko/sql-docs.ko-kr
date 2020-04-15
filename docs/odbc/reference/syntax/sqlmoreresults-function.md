---
title: SQLMoreResults 기능 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304744"
---
# <a name="sqlmoreresults-function"></a>SQLMoreResults 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ODBC  
  
 **요약**  
 **SQLMoreResults** **SELECT,** **UPDATE**, **INSERT**또는 **DELETE** 문을 포함하는 명령문에서 더 많은 결과를 사용할 수 있는지 여부를 결정하고, 그렇다면 해당 결과에 대한 처리를 초기화합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE, OR SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLMoreResults** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 SQL_HANDLE_STMT 핸들 핸들* *핸들*핸들을 사용하는 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. *Handle* 다음 표에서는 **SQLMoreResults에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01S02|옵션 값이 변경되었습니다.|일괄 처리가 처리될 때 문 특성의 값이 변경되었습니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|40001|직렬화 실패|다른 트랜잭션이 있는 리소스 교착 상태로 인해 트랜잭션이 롤백되었습니다.|  
|40003|명령문 완료를 알 수 없음|이 함수를 실행하는 동안 연결된 연결이 실패했으며 트랜잭션 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. **SQLMoreResults** 함수가 호출되었으며 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *명령문 핸들*에서 호출되었습니다. 그런 다음 **SQLMoreResults** 함수는 *문 핸들에*다시 호출되었습니다.<br /><br /> **SQLMoreResults** 함수가 호출되었으며 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *문 핸들에서* 호출되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 **SQLMoreResults** 함수가 호출될 때 계속 실행중이었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SELECT** 문은 결과 집합을 반환합니다. **UPDATE**, **INSERT**및 **DELETE** 문은 영향을 받는 행의 수를 반환합니다. 이러한 명령문 중 어느 것이든 매개 변수 배열(매개 변수 순서증가, 일괄 처리에 나타나는 순서대로 번호 매기기) 또는 프로시저로 제출된 경우 여러 결과 집합 또는 행 수를 반환할 수 있습니다. 명령문 일괄 처리 및 매개 변수 배열에 대한 자세한 내용은 [SQL 문 일괄 처리](../../../odbc/reference/develop-app/batches-of-sql-statements.md) 및 매개 변수 값 [배열을](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)참조하십시오.  
  
 일괄 처리를 실행한 후 응용 프로그램은 첫 번째 결과 집합에 배치됩니다. 응용 프로그램은 **SQLBindCol,** **SQLBulkOperations**, **SQLFetchData**, **SQLGetData**, **SQLFetchScroll**, **SQLSetPos**및 모든 메타데이터 함수를 첫 번째 또는 후속 결과 집합에서 호출할 수 있습니다. 첫 번째 결과 집합이 완료되면 응용 프로그램은 **SQLMoreResults를** 호출하여 다음 결과 집합으로 이동합니다. 다른 결과 집합 또는 개수를 사용할 수 있는 경우 **SQLMoreResults** SQL_SUCCESS 반환 하 고 결과 집합 또는 추가 처리에 대 한 수를 초기화 합니다. 결과 집합 생성 문 사이에 행 개수 생성 문이 나타나면 **SQLMoreResults**를 호출하여 단계별로 사용할 수 있습니다. **업데이트,** **INSERT**및 **DELETE** 문을 위해 **SQLMoreResults를** 호출한 후 응용 프로그램은 **SQLRowCount**를 호출할 수 있습니다.  
  
 페치되지 않은 행이 있는 현재 결과 집합이 있는 경우 **SQLMoreResults는** 해당 결과 집합을 삭제하고 다음 결과 집합 또는 개수를 사용할 수 있도록 합니다. 모든 결과가 처리된 경우 **SQLMoreResults는** SQL_NO_DATA 반환합니다. 일부 드라이버의 경우 모든 결과 집합 및 행 수가 처리될 때까지 출력 매개 변수 및 반환 값을 사용할 수 없습니다. 이러한 드라이버의 경우 **SQLMoreResults가** SQL_NO_DATA 반환할 때 출력 매개 변수 및 반환 값을 사용할 수 있습니다.  
  
 이전 결과 집합에 대해 설정된 모든 바인딩은 여전히 유효합니다. 이 결과 집합에 대해 열 구조가 다른 경우 **SQLFetch** 또는 **SQLFetchScroll를** 호출하면 오류 나 잘림이 발생할 수 있습니다. 이를 방지하기 위해 응용 프로그램은 **SQLBindCol을** 호출하여 적절하게 명시적으로 다시 바인딩하거나 설명자 필드를 설정하여 바인딩해야 합니다. 또는 응용 프로그램은 모든 열 버퍼를 바인딩 해제하는 SQL_UNBIND *옵션으로* **SQLFreeStmt를** 호출할 수 있습니다.  
  
 응용 프로그램이 **SQLMoreResults**를 호출하여 일괄 처리를 탐색할 때 커서 유형, 커서 동시성, 키 집합 크기 또는 최대 길이와 같은 문 특성의 값은 변경될 수 있습니다. 이 경우 **SQLMoreResults는** SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01S02(옵션 값이 변경되었습니다)를 반환합니다.  
  
 **SQLCloseCursor**또는 SQL_CLOSE *옵션을* 사용 하 여 **SQLFreeStmt를** 호출 하면 일괄 처리 실행의 결과로 사용할 수 있는 모든 결과 집합 및 행 수를 삭제 합니다. 명령문 핸들은 할당되거나 준비된 상태로 돌아갑니다. **SQLCancel을** 호출하여 일괄 처리가 실행되고 명령문 핸들이 실행, 커서 위치 지정 또는 비동기 상태에 있을 때 비동기 실행 함수를 취소하면 취소 호출이 성공한 경우 일괄 처리에서 생성된 모든 결과 집합 및 행 수가 삭제됩니다. 그런 다음 명령문은 준비된 상태로 돌아갑니다.  
  
 명령문 또는 프로시저의 일괄 처리가 **SELECT ,** **UPDATE**, **INSERT**및 **DELETE** 문과 다른 SQL 문을 혼합하는 경우 이러한 다른 문은 **SQLMoreResults**에 영향을 주지 않습니다.  
  
 자세한 내용은 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)를 참조하십시오.  
  
 검색된 업데이트, 삽입 또는 문 일괄 처리에 문을 삭제해도 데이터 원본의 행에 영향을 주지 않는 경우 **SQLMoreResults는** SQL_SUCCESS 반환합니다. 이는 데이터 원본의 행에 영향을 주지 않는 경우 SQL_NO_DATA 반환하는 **SQLExecDirect**, **SQLExecute**또는 **SQLParamData를**통해 실행되는 검색된 업데이트, 삽입 또는 삭제 문의 경우와 다릅니다. 응용 프로그램에서 **SQLRowCount를** 호출하여 **SQLMoreResults** 호출 후 행 수를 검색하면 **SQLRowCount가** SQL_NO_DATA 반환합니다.  
  
 결과 처리 함수의 유효한 순서에 대한 자세한 내용은 [부록 B: ODBC 상태 전환 테이블을](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)참조하십시오.  
  
 SQL_PARAM_DATA_AVAILABLE 및 스트리밍된 출력 매개 변수에 대한 자세한 내용은 [SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)를 사용하여 출력 매개 변수 검색을 참조하십시오.  
  
## <a name="availability-of-row-counts"></a>행 수의 가용성  
 일괄 처리에 여러 개의 연속행 개수 생성 문이 포함되어 있는 경우 이러한 행 수가 하나의 행 개수로 롤업될 수 있습니다. 예를 들어 일괄 처리에 5개의 삽입 문이 있는 경우 특정 데이터 원본은 5개의 개별 행 수를 반환할 수 있습니다. 다른 특정 데이터 원본은 5개의 개별 행 개수의 합계를 나타내는 하나의 행 개수만 반환합니다.  
  
 일괄 처리에 결과 집합 생성 및 행 개수 생성 문의 조합이 포함된 경우 행 수를 전혀 사용할 수 없거나 사용하지 못할 수 있습니다. 행 수의 가용성에 대한 드라이버의 동작은 **SQLGetInfo**에 대한 호출을 통해 사용할 수 있는 SQL_BATCH_ROW_COUNT 정보 유형에서 열거됩니다. 예를 들어 일괄 처리에 **SELECT가**포함되어 있고 그 다음에 두 개의 **INSERT**s와 다른 **SELECT가**포함되어 있다고 가정합니다. 그런 다음 다음과 같은 경우가 가능합니다.  
  
-   두 **INSERT** 문에 해당하는 행 개수는 전혀 사용할 수 없습니다. **SQLMoreResults에** 대한 첫 번째 호출은 두 번째 **SELECT** 문의 결과 집합에 배치됩니다.  
  
-   두 **INSERT** 문에 해당하는 행 개수는 개별적으로 사용할 수 있습니다. **SQLGetInfo에** 대한 호출은 SQL_BATCH_ROW_COUNT 정보 유형에 대한 SQL_BRC_ROLLED_UP 비트를 반환하지 않습니다. **SQLMoreResults에** 대한 첫 번째 호출은 첫 번째 **INSERT의**행 수에 배치되고 두 번째 호출은 두 번째 **INSERT의**행 수에 배치됩니다. **SQLMoreResults에** 대한 세 번째 호출은 두 번째 **SELECT** 문의 결과 집합에 배치됩니다.  
  
-   두 **INSERT에** 해당하는 행 수는 사용 가능한 하나의 행 카운트로 롤업됩니다. **SQLGetInfo에** 대한 호출은 SQL_BATCH_ROW_COUNT 정보 유형에 대한 SQL_BRC_ROLLED_UP 비트를 반환합니다. **SQLMoreResults에** 대한 첫 번째 호출은 롤업 행 수에 배치되고 **SQLMoreResults에** 대한 두 번째 호출은 두 번째 **SELECT의**결과 집합에 배치됩니다.  
  
 특정 드라이버는 저장 프로시저가 아닌 명시적 일괄 처리에 대해서만 행 수를 사용할 수 있도록 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|데이터 블록 가져오기 또는 결과 집합 스크롤|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|정방향 전용 방향으로 단일 행 또는 데이터 블록 가져오기|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 열의 일부 또는 전체 가져오기|[SQLGetData 함수(SQLGetData Function)](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData를 사용하여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
