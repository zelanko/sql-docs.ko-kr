---
title: 비동기 실행 (폴링 방법) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- asynchronous execution [ODBC]
ms.assetid: 8cd21734-ef8e-4066-afd5-1f340e213f9c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a188c607c499e16652e314c67c37914f6cc9b85f
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87362771"
---
# <a name="asynchronous-execution-polling-method"></a>비동기 실행(폴링 메서드)
ODBC 3.8 및 Windows 7 SDK 이전에는 문 함수 에서만 비동기 작업을 수행할 수 있었습니다. 자세한 내용은이 항목의 뒷부분에 나오는 **문 작업을 비동기적으로 실행**을 참조 하세요.  
  
 Windows 7 SDK의 ODBC 3.8에는 연결 관련 작업에 대 한 비동기 실행이 도입 되었습니다. 자세한 내용은이 항목의 뒷부분에 나오는 **비동기 연결 작업 실행** 섹션을 참조 하십시오.  
  
 Windows 7 SDK에서 비동기 문 또는 연결 작업의 경우 응용 프로그램은 폴링 메서드를 사용 하 여 비동기 작업이 완료 되었음을 확인 합니다. Windows 8 SDK부터 알림 방법을 사용 하 여 비동기 작업이 완료 되었는지 확인할 수 있습니다. 자세한 내용은 [비동기 실행 (알림 방법)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)을 참조 하세요.  
  
 기본적으로 드라이버는 ODBC 함수를 동기적으로 실행 합니다. 즉, 응용 프로그램은 함수를 호출 하 고 드라이버는 함수 실행을 완료할 때까지 응용 프로그램에 제어를 반환 하지 않습니다. 그러나 일부 함수는 비동기적으로 실행할 수 있습니다. 즉, 응용 프로그램은 함수를 호출 하 고, 드라이버는 최소한의 처리 후에 컨트롤을 응용 프로그램에 반환 합니다. 그러면 응용 프로그램은 첫 번째 함수가 실행 되는 동안 다른 함수를 호출할 수 있습니다.  
  
 비동기 실행은 연결을 설정 하 고, SQL 문을 준비 및 실행 하 고, 메타 데이터를 검색 하 고, 데이터를 인출 하 고, 트랜잭션을 커밋하는 함수와 같이 데이터 원본에서 주로 실행 되는 대부분의 함수에 대해 지원 됩니다. 데이터 원본에 대해 실행 되는 작업에 긴 시간이 소요 되는 경우 (예: 로그인 프로세스 또는 큰 데이터베이스에 대 한 복잡 한 쿼리) 가장 유용 합니다.  
  
 응용 프로그램이 비동기 처리를 사용 하도록 설정 된 문이나 연결을 사용 하 여 함수를 실행 하는 경우 드라이버는 최소한의 처리를 수행 하 고 (예: 오류에 대 한 인수 확인) 데이터 소스를 처리 하 고 SQL_STILL_EXECUTING 반환 코드를 사용 하 여 응용 프로그램에 제어를 반환 합니다. 그러면 응용 프로그램에서 다른 작업을 수행 합니다. 비동기 함수가 완료 된 시기를 확인 하기 위해 응용 프로그램은 원래 사용 했던 것과 동일한 인수를 사용 하 여 함수를 호출 하 여 일정 한 간격으로 드라이버를 폴링합니다. 함수가 계속 실행 중인 경우에는 SQL_STILL_EXECUTING를 반환 합니다. 실행이 완료 되 면 반환 되는 코드 (예: SQL_SUCCESS, SQL_ERROR 또는 SQL_NEED_DATA)를 동기적으로 실행 했을 때 반환 합니다.  
  
 함수가 동기적으로 실행 되는지 또는 비동기적으로 실행 되는지는 드라이버 마다 다릅니다. 예를 들어 결과 집합 메타 데이터가 드라이버에 캐시 되어 있다고 가정 합니다. 이 경우 **SQLDescribeCol** 를 실행 하는 데 시간이 거의 걸리지 않으며 드라이버는 인위적 지연 실행이 아니라 단순히 함수를 실행 해야 합니다. 반면에 드라이버가 데이터 원본에서 메타 데이터를 검색 해야 하는 경우에는이 작업을 수행 하는 동안 응용 프로그램에 제어를 반환 해야 합니다. 따라서 응용 프로그램은 처음에 함수를 비동기적으로 실행할 때 SQL_STILL_EXECUTING 아닌 반환 코드를 처리할 수 있어야 합니다.  
  
## <a name="executing-statement-operations-asynchronously"></a>비동기 문 작업 실행  
 다음 문 함수는 데이터 원본에 대해 작동 하 고 비동기적으로 실행 될 수 있습니다.  

:::row:::
    :::column:::
        [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)  
        [SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)  
        [SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)  
        [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)  
        [SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)  
        [SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)  
        [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)  
        [SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)  
        [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)  
    :::column-end:::
    :::column:::
        [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)  
        [SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)  
        [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)  
        [SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
        [SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)  
        [SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)  
        [SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)  
        [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)  
        [SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)  
    :::column-end:::
    :::column:::
        [SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)  
        [SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)  
        [SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)  
        [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)  
        [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)  
        [SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)  
        [SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)  
        [SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)  
        [SQLTables](../../../odbc/reference/syntax/sqltables-function.md)  
    :::column-end:::
:::row-end:::

 비동기 문 실행은 데이터 원본에 따라 문이나 연결 단위 별로 제어 됩니다. 즉, 응용 프로그램은 특정 함수가 비동기적으로 실행 되는 것이 아니라 특정 문에서 실행 되는 모든 함수가 비동기적으로 실행 되도록 지정 합니다. 지원 되는 항목을 찾기 위해 응용 프로그램은 SQL_ASYNC_MODE 옵션으로 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 를 호출 합니다. 문 핸들에 대 한 연결 수준 비동기 실행이 지원 되는 경우 SQL_AM_CONNECTION 반환 됩니다. 문 수준 비동기 실행이 지원 되는지 여부를 SQL_AM_STATEMENT 합니다.  
  
 특정 문으로 실행 되는 함수가 비동기적으로 실행 되도록 지정 하기 위해 응용 프로그램은 SQL_ATTR_ASYNC_ENABLE 특성을 사용 하 여 **SQLSetStmtAttr** 를 호출 하 고 SQL_ASYNC_ENABLE_ON로 설정 합니다. 연결 수준 비동기 처리가 지원 되는 경우 SQL_ATTR_ASYNC_ENABLE statement 특성은 읽기 전용 이며 해당 값은 문이 할당 된 연결의 연결 특성과 같습니다. 문 특성의 값이 문 할당 시간 이상에서 설정 되었는지 여부에 관계 없이 드라이버 마다 다릅니다. 설정 하려고 하면 SQL_ERROR 및 SQLSTATE HYC00 (선택적 기능이 구현 되지 않음)가 반환 됩니다.  
  
 특정 연결을 사용 하 여 실행 되는 함수가 비동기적으로 실행 되도록 지정 하려면 응용 프로그램이 SQL_ATTR_ASYNC_ENABLE 특성을 사용 하 여 **SQLSetConnectAttr** 를 호출 하 고 SQL_ASYNC_ENABLE_ON로 설정 합니다. 연결에 할당 된 이후의 모든 문 핸들은 비동기 실행에 사용할 수 있습니다. 이 작업으로 기존 문 핸들을 사용할 수 있는지 여부를 드라이버에서 정의 합니다. SQL_ATTR_ASYNC_ENABLE을 SQL_ASYNC_ENABLE_OFF로 설정 하면 연결의 모든 문이 동기 모드에 있습니다. 연결에 활성 문이 있는 상태에서 비동기 실행을 사용 하는 경우 오류가 반환 됩니다.  
  
 지정 된 연결에서 드라이버가 지원할 수 있는 비동기 모드의 최대 활성 동시 문 수를 확인 하기 위해 응용 프로그램은 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS 옵션으로 **SQLGetInfo** 를 호출 합니다.  
  
 다음 코드에서는 폴링 모델의 작동 방식을 보여 줍니다.  
  
```  
SQLHSTMT  hstmt1;  
SQLRETURN rc;  
  
// Specify that the statement is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute a SELECT statement asynchronously.  
while ((rc=SQLExecDirect(hstmt1,"SELECT * FROM Orders",SQL_NTS))==SQL_STILL_EXECUTING) {  
   // While the statement is still executing, do something else.  
   // Do not use hstmt1, because it is being used asynchronously.  
}  
  
// When the statement has finished executing, retrieve the results.  
```  
  
 함수가 비동기적으로 실행 되는 동안 응용 프로그램은 다른 문에서 함수를 호출할 수 있습니다. 응용 프로그램은 비동기 문과 연결 된 것을 제외 하 고 모든 연결에서 함수를 호출할 수도 있습니다. 그러나 문 작업에서 SQL_STILL_EXECUTING 반환 된 후에는 응용 프로그램에서 원래 함수를 호출 하 고 문 핸들이 나 연결 된 연결, 환경 핸들을 사용 하 여 다음 함수를 호출할 수 있습니다.  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [Sqlcancelhandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) (문 핸들)  
  
-   [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
 응용 프로그램에서 비동기 문이나 해당 문과 연결 된 연결을 사용 하 여 다른 함수를 호출 하는 경우이 함수는 SQLSTATE HY010 (함수 시퀀스 오류)를 반환 합니다 (예:).  
  
```  
SQLHDBC       hdbc1, hdbc2;  
SQLHSTMT      hstmt1, hstmt2, hstmt3;  
SQLCHAR *     SQLStatement = "SELECT * FROM Orders";  
SQLUINTEGER   InfoValue;  
SQLRETURN     rc;  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt2);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc2, &hstmt3);  
  
// Specify that hstmt1 is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute hstmt1 asynchronously.  
while ((rc = SQLExecDirect(hstmt1, SQLStatement, SQL_NTS)) == SQL_STILL_EXECUTING) {  
   // The following calls return HY010 because the previous call to  
   // SQLExecDirect is still executing asynchronously on hstmt1. The  
   // first call uses hstmt1 and the second call uses hdbc1, on which  
   // hstmt1 is allocated.  
   SQLExecDirect(hstmt1, SQLStatement, SQL_NTS);   // Error!  
   SQLGetInfo(hdbc1, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // Error!  
  
   // The following calls do not return errors. They use a statement  
   // handle other than hstmt1 or a connection handle other than hdbc1.  
   SQLExecDirect(hstmt2, SQLStatement, SQL_NTS);   // OK  
   SQLTables(hstmt3, NULL, 0, NULL, 0, NULL, 0, NULL, 0);   // OK  
   SQLGetInfo(hdbc2, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // OK  
}  
```  
  
 응용 프로그램이 함수를 호출 하 여 비동기적으로 실행 중인지 여부를 확인 하는 경우 원래 문 핸들을 사용 해야 합니다. 이는 비동기 실행이 문 별로 추적 되기 때문입니다. 또한 응용 프로그램은 다른 인수에 대 한 유효한 값을 제공 해야 합니다. 원래 인수는 드라이버 관리자에서 오류 검사를 이전 하는 데 필요 합니다. 그러나 드라이버가 문 핸들을 확인 하 고 문이 비동기식으로 실행 되 고 있음을 확인 한 후에는 다른 모든 인수를 무시 합니다.  
  
 함수가 비동기 방식으로 실행 되는 동안 즉, SQL_STILL_EXECUTING 반환 된 후 다른 코드를 반환 하기 전에 응용 프로그램은 동일한 문 핸들을 사용 하 여 **sqlcancel** 또는 **sqlcancelhandle** 을 호출 하 여 코드를 취소할 수 있습니다. 이는 함수 실행을 취소 하는 것이 보장 되지 않습니다. 예를 들어 함수가 이미 완료 되었을 수 있습니다. 또한 **sqlcancel** 또는 **sqlcancelhandle** 에 의해 반환 되는 코드는 함수를 실제로 취소 했는지 여부에 관계 없이 함수를 취소 하려는 시도가 성공 했는지 여부를 나타냅니다. 함수가 취소 되었는지 여부를 확인 하기 위해 응용 프로그램은 함수를 다시 호출 합니다. 함수가 취소 된 경우 SQL_ERROR 및 SQLSTATE HY008 (작업 취소 됨)를 반환 합니다. 함수가 취소 되지 않은 경우에는 다른 코드 (예: SQL_SUCCESS, SQL_STILL_EXECUTING 또는 다른 SQLSTATE를 사용 하는 SQL_ERROR)를 반환 합니다.  
  
 드라이버가 문 수준 비동기 처리를 지 원하는 경우 특정 문의 비동기 실행을 사용 하지 않도록 설정 하기 위해 응용 프로그램은 SQL_ATTR_ASYNC_ENABLE 특성을 사용 하 여 **SQLSetStmtAttr** 를 호출 하 고 SQL_ASYNC_ENABLE_OFF로 설정 합니다. 드라이버가 연결 수준 비동기 처리를 지 원하는 경우 응용 프로그램은 **SQLSetConnectAttr** 를 호출 하 여 연결에서 모든 문의 비동기 실행을 사용 하지 않도록 설정 하는 SQL_ATTR_ASYNC_ENABLE를 SQL_ASYNC_ENABLE_OFF로 설정 합니다.  
  
 응용 프로그램은 원래 함수의 반복 루프에서 진단 레코드를 처리 해야 합니다. 비동기 함수가 실행 중일 때 **SQLGetDiagField** 또는 **SQLGetDiagRec** 가 호출 되 면 현재 진단 레코드 목록이 반환 됩니다. 원래 함수 호출이 반복 될 때마다 이전 진단 레코드를 지웁니다.  
  
## <a name="executing-connection-operations-asynchronously"></a>비동기적으로 연결 작업 실행  
 ODBC 3.8 이전에는 준비, 실행 및 페치와 같은 문 관련 작업 뿐만 아니라 카탈로그 메타 데이터 작업에 대해 비동기 실행이 허용 되었습니다. ODBC 3.8 부터는 연결, 연결 끊기, 커밋, 롤백 등의 연결 관련 작업에도 비동기 실행이 가능 합니다.  
  
 ODBC 3.8에 대 한 자세한 내용은 [odbc 3.8의 새로운 기능](../../../odbc/reference/what-s-new-in-odbc-3-8.md)을 참조 하십시오.  
  
 연결 작업을 비동기적으로 실행 하는 것은 다음 시나리오에서 유용 합니다.  
  
-   적은 수의 스레드가 매우 높은 데이터 요금으로 많은 장치를 관리 하는 경우 응답성 및 확장성을 최대화 하려면 모든 작업을 비동기적으로 수행 하는 것이 좋습니다.  
  
-   경과 된 전송 시간을 줄이기 위해 여러 연결에 대 한 데이터베이스 작업을 겹치게 합니다.  
  
-   효율적인 비동기 ODBC 호출 및 연결 작업을 취소 하는 기능을 통해 응용 프로그램은 사용자가 시간 초과를 기다리지 않고 속도가 느려지는 작업을 취소할 수 있습니다.  
  
 이제 연결 핸들에 대해 작동 하는 다음 함수를 비동기적으로 실행할 수 있습니다.  

:::row:::
    :::column:::
        [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)  
        [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)  
    :::column-end:::
    :::column:::
        [SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)  
        [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
    :::column-end:::
    :::column:::
        [SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)  
        [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)  
    :::column-end:::
:::row-end:::

 드라이버가 이러한 함수에 대해 비동기 작업을 지원 하는지 여부를 확인 하기 위해 응용 프로그램은 SQL_ASYNC_DBC_FUNCTIONS를 사용 하 여 **SQLGetInfo** 를 호출 합니다. 비동기 작업이 지원 되는 경우 SQL_ASYNC_DBC_CAPABLE 반환 됩니다. 비동기 작업이 지원 되지 않는 경우 SQL_ASYNC_DBC_NOT_CAPABLE 반환 됩니다.  
  
 특정 연결을 사용 하 여 실행 되는 함수가 비동기적으로 실행 되도록 지정 하려면 응용 프로그램은 **SQLSetConnectAttr** 를 호출 하 고 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 특성을 SQL_ASYNC_DBC_ENABLE_ON로 설정 합니다. 연결을 설정 하기 전에 연결 특성을 설정 하는 것은 항상 동기적으로 실행 됩니다. 또한 **SQLSetConnectAttr** 를 사용 하 여 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 연결 특성을 설정 하는 작업은 항상 동기적으로 실행 됩니다.  
  
 응용 프로그램은 연결을 만들기 전에 비동기 작업을 사용 하도록 설정할 수 있습니다. 드라이버 관리자는 연결을 설정 하기 전에 사용할 드라이버를 결정할 수 없기 때문에 드라이버 관리자는 항상 **SQLSetConnectAttr**에서 성공을 반환 합니다. 그러나 ODBC 드라이버가 비동기 작업을 지원 하지 않는 경우 연결에 실패할 수 있습니다.  
  
 일반적으로 특정 연결 핸들이 나 문 핸들과 연결 된 비동기적으로 실행 되는 함수는 최대 하나만 있을 수 있습니다. 그러나 연결 핸들에는 두 개 이상의 연결 된 문 핸들이 있을 수 있습니다. 연결 핸들에서 실행 중인 비동기 작업이 없으면 연결 된 문 핸들이 비동기 작업을 실행할 수 있습니다. 마찬가지로, 연결 된 문 핸들에 대해 진행 중인 비동기 작업이 없는 경우 연결 핸들에 대해 비동기 작업을 수행할 수 있습니다. 현재 비동기 작업을 실행 하는 핸들을 사용 하 여 비동기 작업을 실행 하려는 시도는 HY010, "함수 시퀀스 오류"를 반환 합니다.  
  
 연결 작업에서 SQL_STILL_EXECUTING 반환 하는 경우 응용 프로그램은 원래 함수를 호출할 수 있으며 해당 연결 핸들에 대해 다음 함수만 호출할 수 있습니다.  
  
-   **Sqlcancelhandle** (연결 핸들)  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle** (ENV/DBC 할당)  
  
-   **SQLAllocHandleStd** (ENV/DBC 할당)  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLDataSources**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 응용 프로그램은 원래 함수의 반복 루프에서 진단 레코드를 처리 해야 합니다. 비동기 함수가 실행 중일 때 SQLGetDiagField 또는 SQLGetDiagRec가 호출 되 면 현재 진단 레코드 목록이 반환 됩니다. 원래 함수 호출이 반복 될 때마다 이전 진단 레코드를 지웁니다.  
  
 연결이 비동기적으로 열리거나 닫힐 때 응용 프로그램이 SQL_SUCCESS를 받거나 원래 함수 호출에서 SQL_SUCCESS_WITH_INFO 때 작업이 완료 됩니다.  
  
 새 함수가 ODBC 3.8, **Sqlcancelhandle**에 추가 되었습니다. 이 함수는 6 개의 연결 함수 (**SQLBrowseConnect**, **SQLConnect**, **sqldisconnect**, **SQLDriverConnect**, **sqlendtran**및 **SQLSetConnectAttr**)를 취소 합니다. 응용 프로그램은 **SQLGetFunctions** 를 호출 하 여 드라이버가 **sqlcancelhandle**을 지원 하는지 확인 해야 합니다. **Sqlcancel**을 사용 하는 것 처럼 **sqlcancelhandle** 이 success를 반환 하는 경우 작업이 취소 된 것을 의미 하지는 않습니다. 응용 프로그램은 원래 함수를 다시 호출 하 여 작업이 취소 되었는지 여부를 확인 해야 합니다. **Sqlcancelhandle** 을 사용 하면 연결 핸들이 나 문 핸들에 대 한 비동기 작업을 취소할 수 있습니다. **Sqlcancelhandle** 을 사용 하 여 문 핸들에 대 한 작업을 취소 하는 것은 **sqlcancel**을 호출 하는 것과 같습니다.  
  
 **Sqlcancelhandle** 과 비동기 연결 작업을 동시에 지원할 필요는 없습니다. 드라이버는 비동기 연결 작업을 지원할 수 있지만 **Sqlcancelhandle**은 지원할 수 없으며 그 반대의 경우도 마찬가지입니다.  
  
 Odbc 3.8 드라이버 및 odbc 3.8 드라이버 관리자를 사용 하 여 ODBC 2.x 및 odbc 2.x 응용 프로그램에서 비동기 연결 작업 및 **Sqlcancelhandle** 을 사용할 수도 있습니다. 이전 응용 프로그램에서 이후 ODBC 버전의 새 기능을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [호환성 매트릭스](../../../odbc/reference/develop-app/compatibility-matrix.md)를 참조 하세요.  
  
### <a name="connection-pooling"></a>연결 풀링  
 연결 풀링을 사용 하도록 설정할 때마다 비동기 작업은 **SQLConnect** 및 **SQLDriverConnect**를 사용 하 여 연결을 설정 하 고 **sqldisconnect**를 사용 하 여 연결을 닫을 때만 최소한으로 지원 됩니다. 하지만 응용 프로그램은 **SQLConnect**, **SQLDriverConnect**및 **sqldisconnect**의 SQL_STILL_EXECUTING 반환 값을 처리할 수 있어야 합니다.  
  
 연결 풀링을 사용 하도록 설정 하면 **Sqlendtran** 및 **SQLSetConnectAttr** 이 비동기 작업에 대해 지원 됩니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>설명  
 다음 예제에서는 **SQLSetConnectAttr** 를 사용 하 여 연결 관련 함수에 대해 비동기 실행을 사용 하도록 설정 하는 방법을 보여 줍니다.  
  
### <a name="code"></a>코드  
  
```  
BOOL AsyncConnect (SQLHANDLE hdbc)   
{  
   SQLRETURN r;  
   SQLHANDLE hdbc;  
  
   // Enable asynchronous execution of connection functions.  
   // This must be executed synchronously, that is r != SQL_STILL_EXECUTING  
   r = SQLSetConnectAttr(  
         hdbc,   
         SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE,  
         reinterpret_cast<SQLPOINTER> (SQL_ASYNC_DBC_ENABLE_ON),  
         0);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   TCHAR szConnStrIn[256] = _T("DSN=AsyncDemo");  
  
   r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
  
   if (r == SQL_ERROR)   
   {  
      // Use SQLGetDiagRec to process the error.  
      // If SQLState is HY114, the driver does not support asynchronous execution.  
      return FALSE;  
   }  
  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion, with the same set of arguments.  
      r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   return TRUE;  
}  
  
```  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>설명  
 이 예제에서는 비동기 커밋 작업을 보여 줍니다. 이러한 방식으로 롤백 작업을 수행할 수도 있습니다.  
  
### <a name="code"></a>코드  
  
```  
BOOL AsyncCommit ()   
{  
   SQLRETURN r;   
  
   // Assume that SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE is SQL_ASYNC_DBC_ENABLE_ON.  
  
   r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion with the same set of arguments.  
      r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [문 실행 ODBC](../../../odbc/reference/develop-app/executing-statements-odbc.md)
