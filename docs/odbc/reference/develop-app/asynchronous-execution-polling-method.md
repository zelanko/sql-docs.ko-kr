---
title: 비동기 실행(폴링 방법) | 마이크로 소프트 문서
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
ms.openlocfilehash: ca7b3d5fa16be44bf4c2ef8f8df8953ae081235d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293403"
---
# <a name="asynchronous-execution-polling-method"></a>비동기 실행(폴링 메서드)
ODBC 3.8 및 Windows 7 SDK 이전에는 명령문 함수에서만 비동기 작업이 허용되었습니다. 자세한 내용은 이 항목의 후반부에서 **비동기적으로 실행 명령문 작업을**참조하십시오.  
  
 Windows 7 SDK의 ODBC 3.8은 연결 관련 작업에 비동기 실행을 도입했습니다. 자세한 내용은 이 항목의 후반부의 **비동기 연결 작업 실행** 섹션을 참조하십시오.  
  
 Windows 7 SDK에서 비동기 문 또는 연결 작업의 경우 응용 프로그램이 폴링 방법을 사용하여 비동기 작업이 완료되었다고 확인했습니다. Windows 8 SDK에서 시작하여 알림 방법을 사용하여 비동기 작업이 완료되었는지 확인할 수 있습니다. 자세한 내용은 [비동기 실행(알림 메서드)을](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)참조하십시오.  
  
 기본적으로 드라이버는 ODBC 함수를 동기적으로 실행합니다. 즉, 응용 프로그램은 함수를 호출하고 드라이버는 함수 실행이 완료될 때까지 응용 프로그램에 대한 제어를 반환하지 않습니다. 그러나 일부 함수는 비동기적으로 실행될 수 있습니다. 즉, 응용 프로그램은 함수를 호출하고 드라이버는 최소한의 처리 후 응용 프로그램에 대한 제어를 반환합니다. 그런 다음 첫 번째 함수가 계속 실행되는 동안 응용 프로그램이 다른 함수를 호출할 수 있습니다.  
  
 비동기 실행은 연결을 설정하고, SQL 문을 준비하고 실행하고, 메타데이터를 검색하고, 데이터를 가져오고, 트랜잭션을 커밋하는 함수와 같이 데이터 원본에서 주로 실행되는 대부분의 함수에 대해 지원됩니다. 데이터 원본에서 실행되는 작업이 로그인 프로세스 나 대규모 데이터베이스에 대한 복잡한 쿼리와 같이 시간이 오래 걸리는 경우에 가장 유용합니다.  
  
 응용 프로그램이 비동기 처리에 사용하도록 설정된 문 또는 연결이 있는 함수를 실행하면 드라이버는 최소한의 처리(예: 오류 인수 확인), 데이터 원본에 대한 핸즈 프로세싱 및 SQL_STILL_EXECUTING 반환 코드를 사용하여 응용 프로그램에 대한 제어를 반환합니다. 그런 다음 응용 프로그램이 다른 작업을 수행합니다. 비동기 함수가 완료된 시기를 확인하기 위해 응용 프로그램은 원래 사용된 것과 동일한 인수를 사용하여 함수를 호출하여 드라이버를 정기적으로 폴링합니다. 함수가 계속 실행 중이면 SQL_STILL_EXECUTING 반환합니다. 실행이 완료되면 SQL_SUCCESS, SQL_ERROR 또는 SQL_NEED_DATA 같은 동기적으로 실행된 경우 반환한 코드를 반환합니다.  
  
 함수가 동기적으로 실행되는지 또는 비동기적으로 실행되는지 여부는 드라이버에 따라 다릅니다. 예를 들어 결과 집합 메타데이터가 드라이버에 캐시되어 있다고 가정합니다. 이 경우 **SQLDescribeCol을** 실행하는 데 거의 시간이 걸리지 않으며 드라이버는 인위적으로 실행을 지연시키는 대신 함수를 실행해야 합니다. 반면에 드라이버가 데이터 원본에서 메타데이터를 검색해야 하는 경우 이 작업을 수행하는 동안 응용 프로그램에 컨트롤을 반환해야 합니다. 따라서 응용 프로그램은 함수를 비동기적으로 처음 실행할 때 SQL_STILL_EXECUTING 이외의 반환 코드를 처리할 수 있어야 합니다.  
  
## <a name="executing-statement-operations-asynchronously"></a>비동기적으로 명령문 작업 실행  
 다음 문 함수는 데이터 원본에서 작동하며 비동기적으로 실행할 수 있습니다.  
  
||||  
|-|-|-|  
|[SQLBulk운영](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
  
 비동기 문 실행은 데이터 원본에 따라 문별 또는 연결단위로 제어됩니다. 즉, 응용 프로그램은 특정 함수를 비동기적으로 실행하도록 지정하지 않지만 특정 명령문에서 실행되는 모든 함수는 비동기적으로 실행되도록 지정합니다. 지원되는 응용 프로그램을 찾으려면 응용 프로그램에서 [sqlGetInfo를](../../../odbc/reference/syntax/sqlgetinfo-function.md) 호출하여 SQL_ASYNC_MODE. 연결 수준 비동기 실행(문 핸들의 경우)이 지원되는 경우 SQL_AM_CONNECTION 반환됩니다. 문 수준 비동기 실행이 지원되는지 SQL_AM_STATEMENT.  
  
 특정 문으로 실행되는 함수를 비동기적으로 실행하도록 지정하기 위해 응용 프로그램은 SQL_ATTR_ASYNC_ENABLE 특성을 사용하여 **SQLSetStmtAttr을** 호출하고 SQL_ASYNC_ENABLE_ON 설정합니다. 연결 수준 비동기 처리가 지원되는 경우 SQL_ATTR_ASYNC_ENABLE 문 특성은 읽기 전용이며 해당 값은 문이 할당된 연결의 연결 특성과 동일합니다. 명령문 특성의 값이 문 할당 시간 또는 이후 시간에 설정되어 있는지 여부에 관계없이 드라이버에 따라 다릅니다. SQL_ERROR 및 SQLSTATE HYC00(선택적 기능이 구현되지 않음)을 설정하려고 하면 반환됩니다.  
  
 특정 연결로 실행되는 함수를 비동기적으로 실행하도록 지정하기 위해 응용 프로그램은 **sqlSetConnectAttr을** SQL_ATTR_ASYNC_ENABLE 특성으로 호출하고 SQL_ASYNC_ENABLE_ON 설정합니다. 연결에 할당된 모든 향후 문 핸들은 비동기 실행을 위해 활성화됩니다. 이 작업에 의해 기존 명령문 핸들을 사용할지 여부를 드라이버 정의합니다. SQL_ATTR_ASYNC_ENABLE SQL_ASYNC_ENABLE_OFF 설정하면 연결의 모든 문이 동기 모드에 있습니다. 연결에 활성 문이 있는 동안 비동기 실행이 활성화된 경우 오류가 반환됩니다.  
  
 드라이버가 지정된 연결에서 지원할 수 있는 비동기 모드에서 활성 동시 문의 최대 수를 결정하기 위해 응용 프로그램은 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS 옵션으로 **SQLGetInfo를** 호출합니다.  
  
 다음 코드는 폴링 모델의 작동 방식을 보여 줍니다.  
  
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
  
 함수가 비동기적으로 실행되는 동안 응용 프로그램은 다른 문에서 함수를 호출할 수 있습니다. 응용 프로그램은 비동기 문과 연결된 연결을 제외한 모든 연결에서 함수를 호출할 수도 있습니다. 그러나 응용 프로그램은 문 작업이 SQL_STILL_EXECUTING 반환한 후에 원래 함수와 다음 함수(문 핸들 또는 관련 연결, 환경 핸들)만 호출할 수 있습니다.  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle(명령문](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 핸들)  
  
-   [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLAlloc핸들](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLDataSource](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
 응용 프로그램이 비동기 문또는 해당 명령문과 연결된 연결이 있는 다른 함수를 호출하는 경우 함수는 SQLSTATE HY010(함수 시퀀스 오류)을 반환합니다.  
  
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
  
 응용 프로그램이 여전히 비동기적으로 실행되고 있는지 여부를 확인하기 위해 함수를 호출하는 경우 원래 문 핸들을 사용해야 합니다. 비동기 실행은 문단위로 추적하기 때문입니다. 또한 응용 프로그램은 드라이버 관리자에서 과거 오류 검사를 받으려면 원래 인수가 수행하는 다른 인수에 대해 유효한 값을 제공해야 합니다. 그러나 드라이버가 문 핸들을 확인하고 명령문이 비동기적으로 실행되고 있음을 확인한 후 다른 모든 인수를 무시합니다.  
  
 함수가 비동기적으로 실행되는 동안( 즉, SQL_STILL_EXECUTING 반환된 후 다른 코드를 반환하기 전에 응용 프로그램은 동일한 문 핸들을 사용하는 **SQLCancel** 또는 **SQLCancelHandle을** 호출하여 이를 취소할 수 있습니다. 이는 함수 실행을 취소하는 것을 보장하지 않습니다. 예를 들어 함수가 이미 완료되었을 수 있습니다. 또한 **SQLCancel** 또는 **SQLCancelHandle에서** 반환되는 코드는 함수를 실제로 취소했는지 여부가 아니라 함수를 취소하려는 시도가 성공했는지 여부만 나타냅니다. 함수가 취소되었는지 여부를 확인하기 위해 응용 프로그램은 함수를 다시 호출합니다. 함수가 취소된 경우 SQL_ERROR 및 SQLSTATE HY008(작업 취소)을 반환합니다. 함수가 취소되지 않은 경우 SQL_SUCCESS, SQL_STILL_EXECUTING 또는 다른 SQLSTATE를 가진 SQL_ERROR 같은 다른 코드를 반환합니다.  
  
 드라이버가 문 수준 비동기 처리를 지원할 때 특정 문의 비동기 실행을 사용하지 않도록 설정하려면 응용 프로그램은 SQL_ATTR_ASYNC_ENABLE 특성을 사용하여 **SQLSetStmtAttr을** 호출하고 SQL_ASYNC_ENABLE_OFF 설정합니다. 드라이버가 연결 수준 비동기 처리를 지원하는 경우 응용 프로그램은 **SQLSetConnectAttr을** 호출하여 SQL_ASYNC_ENABLE_OFF SQL_ATTR_ASYNC_ENABLE 설정하여 연결의 모든 명령문의 비동기 실행을 비활성화합니다.  
  
 응용 프로그램은 원래 함수의 반복 루프에서 진단 레코드를 처리해야 합니다. 비동기 함수가 실행 될 때 **SQLGetDiagField** 또는 **SQLGetDiagRec가** 호출되는 경우 현재 진단 레코드 목록을 반환합니다. 원래 함수 호출이 반복될 때마다 이전 진단 레코드가 지워지습니다.  
  
## <a name="executing-connection-operations-asynchronously"></a>연결 작업을 비동기적으로 실행  
 ODBC 3.8 이전에는 카탈로그 메타데이터 작업뿐만 아니라 준비, 실행 및 가져오기와 같은 문 관련 작업에 비동기 실행이 허용되었습니다. ODBC 3.8부터는 연결, 연결 끊기, 커밋 및 롤백과 같은 연결 관련 작업에대해비동기 실행도 가능합니다.  
  
 ODBC 3.8에 대한 자세한 내용은 [ODBC 3.8의 새로운 내용을](../../../odbc/reference/what-s-new-in-odbc-3-8.md)참조하십시오.  
  
 연결 작업을 비동기적으로 실행하는 것은 다음 시나리오에서 유용합니다.  
  
-   소수의 스레드가 매우 높은 데이터 속도를 가진 많은 수의 장치를 관리하는 경우. 응답성과 확장성을 최대화하려면 모든 작업이 비동기가 되는 것이 바람직합니다.  
  
-   여러 연결에 걸쳐 데이터베이스 작업을 겹쳐서 전송 시간을 줄이려는 경우  
  
-   효율적인 비동기 ODBC 호출과 연결 작업을 취소하는 기능을 통해 응용 프로그램은 사용자가 시간 시간을 기다릴 필요 없이 느린 작업을 취소할 수 있습니다.  
  
 이제 연결 핸들에서 작동하는 다음 함수를 비동기적으로 실행할 수 있습니다.  
  
||||  
|-|-|-|  
|[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|[SQL분리](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
 드라이버가 이러한 함수에서 비동기 작업을 지원하는지 여부를 확인하려면 응용 프로그램에서 **sqlGetInfo를** SQL_ASYNC_DBC_FUNCTIONS 호출합니다. 비동기 작업이 지원되는 경우 SQL_ASYNC_DBC_CAPABLE 반환됩니다. 비동기 작업이 지원되지 않으면 SQL_ASYNC_DBC_NOT_CAPABLE 반환됩니다.  
  
 특정 연결로 실행되는 함수를 비동기적으로 실행하도록 지정하기 위해 응용 프로그램은 **SQLSetConnectAttr을** 호출하고 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 특성을 SQL_ASYNC_DBC_ENABLE_ON 설정합니다. 연결을 설정하기 전에 연결 특성을 설정하면 항상 동기적으로 실행됩니다. 또한 **SQLSetConnectAttr을** SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 연결 특성을 설정하는 작업은 항상 동기적으로 실행됩니다.  
  
 응용 프로그램은 연결을 하기 전에 비동기 작업을 활성화할 수 있습니다. 드라이버 관리자는 연결을 하기 전에 사용할 드라이버를 결정할 수 없으므로 드라이버 관리자는 항상 **SQLSetConnectAttr**에서 성공을 반환합니다. 그러나 ODBC 드라이버가 비동기 작업을 지원하지 않으면 연결되지 않을 수 있습니다.  
  
 일반적으로 특정 연결 핸들 또는 문 핸들과 연결된 비동기적으로 실행되는 함수가 하나일 수 있습니다. 그러나 연결 핸들에는 두 개 이상의 연결된 문 핸들이 있을 수 있습니다. 연결 핸들에서 비동기 작업이 실행되지 않으면 연결된 문 핸들이 비동기 작업을 실행할 수 있습니다. 마찬가지로 연결된 문 핸들에서 진행 중인 비동기 작업이 없는 경우 연결 핸들에서 비동기 작업을 수행할 수 있습니다. 현재 비동기 작업을 실행 중인 핸들을 사용하여 비동기 작업을 실행하려는 시도는 HY010, "함수 시퀀스 오류"를 반환합니다.  
  
 연결 작업이 SQL_STILL_EXECUTING 반환하는 경우 응용 프로그램은 해당 연결 핸들에 대한 원래 함수와 다음 함수만 호출할 수 있습니다.  
  
-   **SQLCancelHandle(연결** 핸들)  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle** (ENV / DBC 할당)  
  
-   **SQLAlloc핸들스트드(ENV/DBC** 할당)  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLDataSource**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 응용 프로그램은 원래 함수의 반복 루프에서 진단 레코드를 처리해야 합니다. 비동기 함수가 실행 될 때 SQLGetDiagField 또는 SQLGetDiagRec가 호출되는 경우 현재 진단 레코드 목록을 반환합니다. 원래 함수 호출이 반복될 때마다 이전 진단 레코드가 지워지습니다.  
  
 연결이 비동기적으로 열리거나 닫히는 경우 응용 프로그램이 원래 함수 호출에서 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 받을 때 작업이 완료됩니다.  
  
 새로운 함수가 ODBC 3.8, **SQLCancelHandle에**추가되었습니다. 이 함수는 6개의 연결**함수(SQLBrowseConnect,** **SQLConnect,** **SQLDisconnect,** **SQLDriverConnect,** **SQLEndTran**및 **SQLSetConnectAttr)를**취소합니다. 응용 프로그램은 **SQLGetFunctions를** 호출하여 드라이버가 **SQLCancelHandle**을 지원하는지 확인해야 합니다. **SQLCancel에서와**마찬가지로 **SQLCancelHandle이** 성공을 반환한다고 해서 작업이 취소된 것은 아닙니다. 응용 프로그램은 원래 함수를 다시 호출하여 작업이 취소되었는지 확인해야 합니다. **SQLCancelHandle을** 사용하면 연결 핸들 또는 명령문 핸들에서 비동기 작업을 취소할 수 있습니다. **SQLCancelHandle을** 사용하여 문 핸들에서 작업을 취소하는 것은 **SQLCancel**.  
  
 **SQLCancelHandle** 및 비동기 연결 작업을 동시에 지원할 필요는 없습니다. 드라이버는 비동기 연결 작업을 지원할 수 있지만 **SQLCancelHandle은**지원하지 않으며 그 반대의 경우도 마찬가지입니다.  
  
 비동기 연결 작업 및 **SQLCancelHandleODBC** 3.8 드라이버 및 ODBC 3.8 드라이버 관리자와 ODBC 3.8 드라이버 관리자와 ODBC 3.x 응용 프로그램에서 사용할 수 있습니다. 이전 응용 프로그램이 이후 ODBC 버전에서 새 기능을 사용하도록 설정하는 방법에 대한 자세한 내용은 [호환성 매트릭스](../../../odbc/reference/develop-app/compatibility-matrix.md)를 참조하십시오.  
  
### <a name="connection-pooling"></a>연결 풀링  
 연결 풀링을 사용할 때마다 **SQLConnect** 및 **SQLDriverConnect**를 사용 하 고 **SQLDisconnect와의**연결을 닫기 위해 비동기 작업만 최소한의 지원 됩니다. 그러나 응용 프로그램은 **여전히 SQLConnect,** **SQLDriverConnect**및 **SQLDisconnect에서**반환 값을 SQL_STILL_EXECUTING 처리 할 수 있어야합니다.  
  
 연결 풀링을 사용하도록 설정하면 **SQLEndTran** 및 **SQLSetConnectAttr이** 비동기 작업에 지원됩니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>설명  
 다음 예제에서는 **SQLSetConnectAttr을** 사용하여 연결 관련 함수에 대한 비동기 실행을 활성화하는 방법을 보여 주며 있습니다.  
  
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
 이 예제에서는 비동기 커밋 작업을 보여 주며 롤백 작업도 이 방법으로 수행할 수 있습니다.  
  
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
 [실행 명령 문 ODBC](../../../odbc/reference/develop-app/executing-statements-odbc.md)
