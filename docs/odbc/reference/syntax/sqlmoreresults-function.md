---
title: SQLMoreResults 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d156b07358d6430ec52f000ed4bebfe1c5d19d9f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlmoreresults-function"></a>SQLMoreResults 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ODBC  
  
 **요약**  
 **SQLMoreResults** 더 많은 결과에 포함 하는 문을 사용할 수 있는지 확인 **선택**, **업데이트**, **삽입**, 또는  **삭제** 문 및 초기화 그 결과 대 한 처리 그렇다면 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE, 또는 SQL_PARAM_DATA_AVAILABLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLMoreResults** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* sql _HANDLE_STMT 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLMoreResults** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01S02|옵션 값이 변경|일괄 처리로 변경 하는 문 특성의 값 처리 중이 던 합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|40001|Serialization 오류|트랜잭션이 다른 트랜잭션 사용 하 여 리소스 교착 상태로 인해 롤백 되었습니다.|  
|40003|알 수 없는 문 완성|이 함수를 실행 하는 동안 관련된 연결 실패 및 트랜잭션의 상태를 확인할 수 없습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *StatementHandle*합니다. **SQLMoreResults** 함수 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle* . 그런 다음 **SQLMoreResults** 에서 다시 호출 된 함수는 *StatementHandle*합니다.<br /><br /> **SQLMoreResults** 함수 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle*  다중 스레드 응용 프로그램에서 다른 스레드에서 합니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 비동기 함수 계속 실행 될 때는 **SQLMoreResults** 함수를 호출 했습니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>설명  
 **선택** 문은 결과 집합을 반환 합니다. **업데이트**, **삽입**, 및 **삭제** 문의 영향을 받는 행 수를 반환 합니다. 이러한 명령문은 일괄 처리 제출 된 배열 (일괄 처리에 나타나는 순서 대로 매개 변수 오름차순으로 번호가 지정) 하는 매개 변수 또는 프로시저에서 여러 결과 집합을 반환할 수 있습니다 또는 행 수를 계산 합니다. 문의 일괄 처리 및 매개 변수 배열에 대 한 정보를 참조 하십시오. [SQL 문 일괄 처리](../../../odbc/reference/develop-app/batches-of-sql-statements.md) 및 [매개 변수 값의 배열](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)합니다.  
  
 일괄 처리를 실행 한 후 응용 프로그램은 첫 번째 결과 집합에 배치 됩니다. 응용 프로그램에서 호출할 수 **SQLBindCol**, **SQLBulkOperations**, **SQLFetch**, **SQLGetData**, **SQLFetchScroll** , **SQLSetPos**, 및 단일 결과 집합에만 있는 경우와 마찬가지로 정당한 첫 번째 또는 모든 후속 결과 집합에서 모든 메타 데이터 기능을 합니다. 첫 번째 결과 집합으로 완료 된 후 호출 **SQLMoreResults** 다음 결과 집합으로 이동할 수 있습니다. 다른 결과 집합 또는 수를 사용할 수 있으면 **SQLMoreResults** 관계 없이 SQL_SUCCESS를 반환 하 고 결과 집합 또는 추가 처리를 위한 개수를 초기화 합니다. 문 집합 – 생성 될 행 개수 – 생성 문 사이 표시 하는 경우, 호출를 하나씩 실행할 수 있습니다 **SQLMoreResults**합니다. 호출한 후 **SQLMoreResults** 에 대 한 **업데이트**, **삽입**, 또는 **삭제** 문은, 응용 프로그램 를호출할수**SQLRowCount**합니다.  
  
 현재 결과 집합 인출된 행 되었으면 **SQLMoreResults** 해당 결과 집합을 삭제 하 고 다음 결과 집합 또는 사용 가능한 계산을 만듭니다. 모든 결과 처리 경우 **SQLMoreResults** SQL_NO_DATA를 반환 합니다. 일부 드라이버에 대 한 출력 매개 변수 및 반환 값 사용할 수 없는 모든 결과 집합 및 행 개수 처리 될 때까지 합니다. 이러한 드라이버에 대 한 출력 매개 변수 및 반환 값을 사용할 수 있을 때 **SQLMoreResults** SQL_NO_DATA를 반환 합니다.  
  
 여전히 이전 결과 대해 설정 된 모든 바인딩을 계속 유효 합니다. 열 구조가 결과 집합에 대 한 다른 경우 다음 호출 **SQLFetch** 또는 **SQLFetchScroll** 오류 또는 잘림이 발생할 수 있습니다. 이 방지 하려면 응용 프로그램은 호출 **SQLBindCol** 명시적으로 적절 하 게 다시 바인딩 (또는 설정 하면 설명자 필드). 응용 프로그램을 호출할 수 또는 **SQLFreeStmt** 와 *옵션* 의 모든 열 버퍼의 바인딩을 해제 하려면 SQL_UNBIND 합니다.  
  
 호출 하 여 일괄 처리를 통해 응용 프로그램에서 탐색 커서 유형, 커서 동시성, 키 집합 크기, 최대 길이 등 문 특성의 값이 변경 될 수 있습니다 **SQLMoreResults**합니다. 이 경우 **SQLMoreResults** SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01 s 02를 반환 합니다 (옵션 값 변경).  
  
 호출 **SQLCloseCursor**, 또는 **SQLFreeStmt** 와 *옵션* 를 SQL_CLOSE의 모든 결과 집합 및 실행의 결과로 사용할 수 있었던 행 개수 무시 일괄 처리입니다. 문 핸들 할당 또는 준비 된 상태를 반환합니다. 호출 **SQLCancel** 일괄 처리를 실행 하 고 커서가 위치에 실행 된 문 핸들은 또는 비동기 상태로 인해 모든 결과 집합와 행 개수는 비동기적으로 실행 중인 함수를 취소 하려면 취소 호출에 성공 하면 무시 되 고 일괄 처리에 의해 생성 합니다. 그런 다음 문이 준비 또는 할당 된 상태로 반환합니다.  
  
 문 또는 프로시저의 일괄 처리에서 다른 SQL 문을 함께 사용 하는 경우 **선택**, **업데이트**, **삽입**, 및 **삭제** 문 이러한 다른 문의 영향을 주지 않으므로 **SQLMoreResults**합니다.  
  
 자세한 내용은 참조 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)합니다.  
  
 검색 결과 업데이트, 삽입 또는 삭제에 문의 일괄 처리 문의 영향을 주지 않습니다 데이터 소스의 모든 행 **SQLMoreResults** 관계 없이 SQL_SUCCESS를 반환 합니다. 이 검색 결과 업데이트의 경우와에서 다른, insert 또는 delete 문을 통해 실행 되는 **SQLExecDirect**, **SQLExecute**, 또는 **SQLParamData**이며 데이터 소스의 모든 행에 영향을 주지 않는 경우 SQL_NO_DATA를 반환 합니다. 응용 프로그램을 호출 하는 경우 **SQLRowCount** 를 호출한 후 행 수를 검색 하 **SQLMoreResults** 모든 행의 영향을 받지는 **SQLRowCount** SQL_NO_DATA를 반환 합니다.  
  
 결과 처리 함수는 유효한 시퀀싱 하는 방법에 대 한 추가 정보를 참조 하십시오. [부록 b: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)합니다.  
  
 SQL_PARAM_DATA_AVAILABLE 및 스트리밍된 출력 매개 변수에 대 한 자세한 내용은 참조 하십시오. [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)합니다.  
  
## <a name="availability-of-row-counts"></a>행 개수의 가용성  
 여러 연속 된 행 개수 – 생성 문을 포함 하는 일괄 처리, 경우에 이러한 행 개수 한 행 개수도 롤업되는 수 있습니다. 예를 들어 일괄 처리에 포함 된 5 insert 문을, 특정 데이터 소스는 5 개의 개별 행 수를 반환할 수 있습니다. 다른 데이터 원본의 특정 5 개의 개별 행 수 합계를 나타내는 하나의 행만 개수를 반환 합니다.  
  
 결과 집합 – 생성 하 고 행 개수 – 생성 문 조합을 포함 하는 일괄 처리, 행 개수 되었거나 사용 하지 못할 전혀 합니다. 행 개수의 가용성을 기준으로 드라이버의 동작 호출을 통해 사용할 수 있는 SQL_BATCH_ROW_COUNT 정보 유형에 열거 됩니다 **SQLGetInfo**합니다. 예를 들어 일괄 처리에 포함 되어 있는지 한 **선택**와 두 개의 **삽입**s 및 다른 **선택**합니다. 그런 다음 다음과 같은 경우 발생할 수 있습니다.  
  
-   행 개수에 해당 하는 두 **삽입** 문에 전혀 사용할 수 없습니다. 첫 번째 호출 **SQLMoreResults** 두 번째 결과 집합에 배치 **선택** 문.  
  
-   행 개수에 해당 하는 두 **삽입** 개별적으로 사용할 수 있는 문. (에 대 한 호출 **SQLGetInfo** SQL_BATCH_ROW_COUNT 정보 유형에 대해 SQL_BRC_ROLLED_UP 비트를 반환 하지 않습니다.) 첫 번째 호출 **SQLMoreResults** 첫 번째 행 수에 배치 **삽입**, 두 번째 호출 하면 두 번째 행 수에 배치 됩니다 **삽입**합니다. 세 번째 호출은 **SQLMoreResults** 두 번째 결과 집합에 배치 **선택** 문.  
  
-   행 개수에 해당 하는 두 **삽입** 사용할 수 있는 하나의 단일 행 수로 롤업 됩니다. (에 대 한 호출 **SQLGetInfo** SQL_BATCH_ROW_COUNT 정보 종류에 대 한 비트가 SQL_BRC_ROLLED_UP를 반환 합니다.) 첫 번째 호출 **SQLMoreResults** 롤업 행 개수와 두 번째 호출에서 위치 **SQLMoreResults** 두 번째 결과 집합에 배치 **선택**.  
  
 특정 드라이버 명시적 일괄 처리에만 및 저장된 프로시저에 대해 사용 가능한 행 개수를 확인합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|데이터 블록을 인출 또는 스크롤 하는 결과 집합|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|단일 행 이나 앞 으로만 이동 가능한 방향의 데이터 블록을 인출합니다.|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|일부 또는 전체 데이터 열을 인출합니다.|[SQLGetData 함수](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData를 사용하여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
