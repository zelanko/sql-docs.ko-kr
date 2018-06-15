---
title: 비동기 실행 (폴링 방법) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- asynchronous execution [ODBC]
ms.assetid: 8cd21734-ef8e-4066-afd5-1f340e213f9c
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d64874a4633e7bede14051d882925f633dadc36c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913828"
---
# <a name="asynchronous-execution-polling-method"></a>비동기 실행 (폴링 방법)
ODBC 3.8 및 Windows 7 SDK 하기 전에 비동기 작업 문 함수에 대해서만 허용 합니다. 자세한 내용은 참조는 **문 작업 비동기적으로 실행**이 항목의 뒷부분에 나오는 합니다.  
  
 Windows 7 SDK에서 ODBC 3.8 연결 관련 작업에 비동기 실행을 도입 합니다. 자세한 내용은 참조는 **연결 작업이 비동기적으로 실행** 이 항목의 뒷부분에 나오는 섹션.  
  
 Windows 7 SDK 비동기 문이나 연결 작업에 대 한 응용 프로그램 비동기 작업이 폴링 메서드를 사용 하 여 완료 되었음을 확인 했습니다. Windows 8 SDK부터, 비동기 작업이 알림 방법을 사용 하 여 완료 되었음을 확인할 수 있습니다. 자세한 내용은 참조 [비동기 실행 (알림 방법)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)합니다.  
  
 드라이버 기본적으로 ODBC 함수, 실행 즉, 한 함수를 호출 하는 응용 프로그램 있으며 드라이버 반환 하지 않는 제어 응용 프로그램에 함수 실행이 완료 될 때까지 합니다. 하지만 일부 함수를 비동기적으로 실행할 수 있습니다 즉, 응용 프로그램에는 해당 함수를 호출 고 드라이버를 최소한의 처리를 수행한 컨트롤을 반환 응용 프로그램입니다. 그런 다음 응용 프로그램 수 첫 번째 함수는 여전히 실행 하는 동안 다른 함수를 호출 해야 합니다.  
  
 비동기 실행은 주로 데이터 원본에서 실행 되는 대부분의 함수에 대 한 지원, 연결을 설정, 준비 하 고 SQL 문을 실행 하는 함수 메타 데이터를 검색 하는 경우와 같은 데이터를 인출 하 고 트랜잭션을 커밋합니다. 데이터 원본에 대해 실행 중인 작업 로그인 프로세스 등 큰 데이터베이스에 대 한 복잡 한 쿼리 시간이 오래 걸리는 경우에 가장 유용 합니다.  
  
 문 또는 비동기 처리를 사용 하는 연결을 사용 하는 함수를 실행 하는 응용 프로그램이 드라이버 수행 최소한 처리 (예: 오류에 대 한 인수)의 데이터 원본에 대 한 처리를 전달 하 고, 반환 반환 코드를 SQL_STILL_EXECUTING으로 응용 프로그램을 제어 합니다. 그러면 응용 프로그램이 다른 작업을 수행합니다. 비동기 함수 완료 되 면를 확인 하려면 응용 프로그램 인수가 드라이버 원래 사용한 것과 동일한 인수를 사용 하 여 함수를 호출 하 여 정기적으로 폴링합니다. 함수가 아직 실행 되 고, SQL_STILL_EXECUTING; 반환 실행 완료 될 경우 그가 동기적으로 실행 SQL_SUCCESS, SQL_ERROR 또는 sql_need_data가 같은 반환는 코드를 반환 합니다.  
  
 함수는 동기적 또는 비동기적인지를 실행 하는 여부는 특정입니다. 예를 들어, 드라이버에서 결과 집합 메타 데이터 캐시 됩니다. 이 경우 실행 시간이 거의 걸리는 **SQLDescribeCol** 드라이버 인위적으로 실행이 지연 하지 않고 단순히 함수를 실행 해야 합니다. 반면에 드라이버를 데이터 원본에서 메타 데이터를 검색 하는 경우이 수행 하는 동안 응용 프로그램에 컨트롤을 반환 해야 것 합니다. 따라서 응용 프로그램을 처음 실행할 때 함수 비동기적으로 SQL_STILL_EXECUTING 이외의 반환 코드를 처리할 수 있어야 합니다.  
  
## <a name="executing-statement-operations-asynchronously"></a>문 작업을 비동기적으로 실행  
 다음 문 함수는 데이터 원본에 작동 하 고 비동기적으로 실행할 수 있습니다.  
  
||||  
|-|-|-|  
|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
  
 비동기 문 실행 당 문 또는 데이터 원본에 따라 연결 단위로에서 제어 됩니다. 즉, 응용 프로그램 특정 기능 비동기적으로 실행 될 이지만 특정 문을 실행 하는 함수를 비동기적으로 실행 사용 하도록 하지 지정 합니다. 찾을 출력을 사용할 수 있는 하나, 응용 프로그램이 호출 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) SQL_ASYNC_MODE의 옵션을 사용 합니다. SQL_AM_CONNECTION 연결 수준의 비동기 실행 (문 핸들)에 대 한 지원 되 면 반환 됩니다. SQL_AM_STATEMENT 문 수준의 비동기 실행을 지원 되는 경우.  
  
 함수는 특정 문을 사용 하 여 실행 될 것인지를 지정 하려면 비동기적으로 실행, 응용 프로그램 호출 **SQLSetStmtAttr** 여 SQL_ATTR_ASYNC_ENABLE 특성은 및 SQL_ASYNC_ENABLE_ON으로 설정 합니다. 연결 수준 비동기 처리는 지원 SQL_ATTR_ASYNC_ENABLE 문 특성은 읽기 전용 및 해당 값은 문이 할당 된 연결의 연결 특성으로 동일 합니다. 문 특성의 값은 설정한 문 할당 시 또는 나중에 드라이버 관련 됩니다. 설정 하려고은 결과 반환 하면 SQL_ERROR SQLSTATE HYC00 (선택적 기능이 구현 되지 않음).  
  
 함수는 특정 연결을 사용 하 여 실행 될 것인지를 지정 하려면 비동기적으로 실행, 응용 프로그램 호출 **SQLSetConnectAttr** 여 SQL_ATTR_ASYNC_ENABLE 특성은 및 SQL_ASYNC_ENABLE_ON으로 설정 합니다. 비동기 실행을 위해 연결에 할당 된 모든 이후 문 핸들을 설정할 드라이버 정의 된 기존 문 핸들은이 동작에서 사용할 수 있는지 여부 SQL_ATTR_ASYNC_ENABLE SQL_ASYNC_ENABLE_OFF로 설정 된 경우 연결에 대 한 모든 문을 동기 모드입니다. 비동기 실행 중이면 연결에서 활성 문을 사용 하는 경우 오류가 반환 됩니다.  
  
 드라이버는 지정된 된 연결을 지원할 수 있는 비동기 모드의 동시 활성 문의 최대 수를 확인 하려면 응용 프로그램 호출 **SQLGetInfo** SQL_MAX_ASYNC_CONCURRENT_STATEMENTS 옵션을 사용 합니다.  
  
 다음 코드는 폴링 모델 사용 예를 보여 줍니다.  
  
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
  
 함수는 비동기적으로 실행 하는 동안 응용 프로그램에서 다른 문 함수를 호출 합니다. 응용 프로그램 비동기 문과 연결 된 노드를 제외한 모든 연결에서 함수를 호출할 수도 있습니다. 하지만 응용 프로그램 수만 호출 원래 기능과 다음 함수 (문 핸들 또는 해당 관련된 연결 환경 핸들) 문 작업을 수행한 후 SQL_STILL_EXECUTING을 반환:  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) (문 핸들)에서  
  
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
  
 해당 문과 연관 된 연결 또는 비동기 문을 사용 하 여 다른 함수를 호출 하는 응용 프로그램, 함수 반환 SQLSTATE HY010 (함수 시퀀스 오류입니다.), 예를 들어 있습니다.  
  
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
  
 응용 프로그램이 있는지 여부를 실행 하는 비동기적으로 확인 하는 함수를 호출할 때 원래 문 핸들을 사용 해야 합니다. 즉, 비동기 실행 문 별 별로 추적 됩니다. 응용 프로그램에는 다른 인수에 대 한 유효한 값도 제공 해야 — 원래 인수 처리 해-오류 드라이버 관리자에서 검사를 통과 하도록 합니다. 그러나, 드라이버 문 핸들을 확인 하 고 문이 비동기적으로 실행 됨을 확인 한 후 다른 인수는 모두 무시 합니다.  
  
 함수는 비동기적으로 실행 하는 동안-즉, SQL_STILL_EXECUTING을 반환 했습니다 후 및 하기 전에 반환 코드를 다른-응용 프로그램 호출 하 여 취소할 수 **SQLCancel** 또는 **SQLCancelHandle** 동일한 문 핸들을 포함 합니다. 함수 실행을 취소 하는 보장 되지 않습니다. 예를 들어 함수를 이미 완료 된 될 수 있습니다. 코드에서 반환 된 또한 **SQLCancel** 또는 **SQLCancelHandle** 만 함수를 취소할 수 성공 여부를 나타냅니다, 함수를 실제로 취소 여부를 하지 않습니다. 을 함수 취소 되었는지 여부를 확인 하려면 응용 프로그램 다시 함수를 호출 합니다. SQL_ERROR 및 SQLSTATE HY008 반환 함수가 취소 된 경우 (작업이 취소 됨). 함수는 취소 되지 않은 경우 SQL_SUCCESS, SQL_STILL_EXECUTING, 또는 다른 sqlstate SQL_ERROR와 같은 다른 코드를 반환 합니다.  
  
 드라이버에서 문 수준의 비동기 처리에는 응용 프로그램 호출을 지 원하는 경우 특정 문에의 비동기 실행을 해제 하려면 **SQLSetStmtAttr** SQL_ 설정 하 여 SQL_ATTR_ASYNC_ENABLE 특성은 ASYNC_ENABLE_OFF 합니다. 드라이버가 연결 수준의 비동기 처리를 지 원하는 경우 응용 프로그램 호출 **SQLSetConnectAttr** SQL_ASYNC_ENABLE_OFF에 모든 문의 비동기 실행을 사용 하지 않도록 설정 하려면 SQL_ATTR_ASYNC_ENABLE을 설정 하 고 연결입니다.  
  
 응용 프로그램 진단 레코드 원래 함수의 반복 루프에서 처리 해야 합니다. 경우 **SQLGetDiagField** 또는 **SQLGetDiagRec** 비동기 함수를 실행할 때 라고 진단 레코드의 현재 목록을 반환 합니다. 원래 함수 호출을 반복 될 때마다 이전 진단 레코드를 지웁니다.  
  
## <a name="executing-connection-operations-asynchronously"></a>연결 작업을 비동기적으로 실행  
 ODBC 3.8 하기 전에 문을 관련 작업 등 준비에 대 한 비동기 실행 허용, 실행 및도 카탈로그 메타 데이터 작업의 경우와 인출 합니다. ODBC 3.8 년부터 비동기 실행도 가능 연결, 분리 같은 연결 관련 작업, commit 및 rollback에 대 한 합니다.  
  
 ODBC 3.8에 대 한 자세한 내용은 참조 하십시오. [What's New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)합니다.  
  
 연결 작업을 비동기적으로 실행 하는 다음과 같은 시나리오에서 유용 합니다.  
  
-   경우 적은 수의 스레드 수가 많은 매우 높은 데이터 속도 사용 하 여 장치를 관리 합니다. 응답 속도 및 확장성을 최대화 하기 위해 비동기 되도록 모든 작업에 대해 좋습니다.  
  
-   경과 된 전송 시간을 줄이기 위한 여러 연결을 통해 데이터베이스 작업을 하려는 경우.  
  
-   효율적인 비동기 ODBC 호출 및 연결 작업을 취소 하 고 사용자가 시간 초과 될 때까지 기다릴 필요 없이 느린 모든 작업을 취소를 허용 하도록 응용 프로그램을 사용 하도록 설정 합니다.  
  
 이제 연결 핸들에서 작동 하는 다음 함수를 비동기적으로 실행 수 있습니다.  
  
||||  
|-|-|-|  
|[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
 응용 프로그램이 드라이버를 이러한 함수에 대 한 비동기 작업을 지원 하는지 확인, 호출 **SQLGetInfo** SQL_ASYNC_DBC_FUNCTIONS 사용 합니다. 지원 되는 비동기 작업 SQL_ASYNC_DBC_CAPABLE 반환 됩니다. 비동기 작업이 지원 되지 않는 경우 SQL_ASYNC_DBC_NOT_CAPABLE 반환 됩니다.  
  
 함수는 특정 연결을 사용 하 여 실행 될 것인지를 지정 하려면 비동기적으로 실행, 응용 프로그램 호출 **SQLSetConnectAttr** SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 특성 SQL_ASYNC_DBC_ENABLE을 설정 하 고 _ON 합니다. 동기적으로 실행 항상 연결을 설정 하기 전에 연결 특성을 설정 합니다. 또한 연결을 설정 하 고 작업 특성으로 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE **SQLSetConnectAttr** 항상 동기적으로 실행 합니다.  
  
 응용 프로그램에 연결 하기 전에 비동기 작업 사용 하도록 설정할 수 있습니다. 드라이버 관리자는 성공적으로 항상 반환 드라이버 관리자 연결 하기 전에 사용 하는 드라이버를 확인할 수 없으므로, **SQLSetConnectAttr**합니다. 그러나이 ODBC 드라이버는 비동기 작업을 지원 하지 않는 경우 연결 하는 데 실패할 수 있습니다.  
  
 일반적으로 있을 수 있습니다 최대 특정 연결 핸들 또는 문 핸들에 연결 되어 비동기적으로 함수를 실행 합니다. 그러나 연결 핸들 둘 이상의 연결 된 문 핸들을 가질 수 있습니다. 연결 핸들에서 실행 되는 비동기 작업이 없는 경우 관련 된 문 핸들을 비동기 작업을 실행할 수 있습니다. 마찬가지로, 모든 관련된 문 핸들에서 진행 중인 비동기 작업이 없으며 경우 연결 핸들에는 비동기 작업을 사용할 수 있습니다. 현재 비동기 작업을 실행 하는 핸들을 사용 하 여 비동기 작업을 실행 하려고 HY010, "함수 시퀀스 오류"를 반환 합니다.  
  
 연결 작업 SQL_STILL_EXECUTING을 반환 하는 경우 응용 프로그램만 호출할 수 있습니다 원래 기능과 다음 기능 해당 연결 핸들에 대 한:  
  
-   **SQLCancelHandle** (연결 핸들)에  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle** (ENV/dbc입니다 할당)  
  
-   **SQLAllocHandleStd** (ENV/dbc입니다 할당)  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLDataSources**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 응용 프로그램 진단 레코드 원래 함수의 반복 루프에서 처리 해야 합니다. SQLGetDiagRec 나 SQLGetDiagField를 호출 하 여 비동기 함수를 실행할 때, 진단 레코드의 현재 목록을 반환 합니다. 원래 함수 호출을 반복 될 때마다 이전 진단 레코드를 지웁니다.  
  
 연결 되는 경우 응용 프로그램이 원래 함수 호출에 관계 없이 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 받으면 작업을 완료 열거나 비동기적으로 종료 합니다.  
  
 ODBC 3.8에 추가 된 새 함수 **SQLCancelHandle**합니다. 이 함수는 6 개의 연결 함수 취소 (**SQLBrowseConnect**, **SQLConnect**, **SQLDisconnect**, **SQLDriverConnect**, **SQLEndTran**, 및 **SQLSetConnectAttr**). 응용 프로그램 호출 해야 **SQLGetFunctions** 드라이버에서 지원 하는지 확인할 **SQLCancelHandle**합니다. 와 마찬가지로 **SQLCancel**경우 **SQLCancelHandle** 성공을 반환 작업 취소를 의미 하지 않습니다. 응용 프로그램 작업이 취소 된 경우 확인을 다시 원래 함수를 호출 해야 합니다. **SQLCancelHandle** 연결 핸들 또는 문 핸들에 대 한 비동기 작업을 취소할 수 있습니다. 사용 하 여 **SQLCancelHandle** 핸들은이 문에서 작업을 취소할 **SQLCancel**합니다.  
  
 둘 다 지 원하는 데 필요 없는 **SQLCancelHandle** 및 동시에 비동기 연결 작업입니다. 드라이버는 비동기 연결 작업을 지원할 수 있지만 **SQLCancelHandle**, 또는 그 반대로 합니다.  
  
 비동기 연결 작업 및 **SQLCancelHandle** ODBC에서 사용할 수도 있습니다 3.x 및 ODBC 3.8 드라이버 및 ODBC 3.8 드라이버 관리자와 ODBC 2.x 응용 프로그램입니다. 에 대 한 이후 ODBC 버전의 새로운 기능을 사용 하도록 이전 응용 프로그램을 사용 하도록 설정 하는 방법에 대 한 정보를 참조 하십시오. [호환성 매트릭스](../../../odbc/reference/develop-app/compatibility-matrix.md)합니다.  
  
### <a name="connection-pooling"></a>연결 풀링  
 때마다 연결 풀링을 사용 하는 비동기 작업에 대 한 연결 설정 최소한 으로만 지원 됩니다 (으로 **SQLConnect** 및 **SQLDriverConnect**) 및와 연결을 닫기 **SQLDisconnect**합니다. 응용 프로그램이 여전히 SQL_STILL_EXECUTING 반환 값에서 처리할 수 있어야 하지만 **SQLConnect**, **SQLDriverConnect**, 및 **SQLDisconnect**합니다.  
  
 연결 풀링을 사용 하는 경우 **SQLEndTran** 및 **SQLSetConnectAttr** 비동기 작업에 대해 지원 됩니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>Description  
 다음 예제에서는 사용 하는 방법을 보여 줍니다. **SQLSetConnectAttr** 연결 관련 함수에 대 한 비동기 실행을 사용 하도록 합니다.  
  
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
  
### <a name="description"></a>Description  
 이 예제에서는 비동기 커밋 작업을 보여 줍니다. 롤백 작업 이런 방식이으로 수행할 수도 있습니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [문 실행 ODBC](../../../odbc/reference/develop-app/executing-statements-odbc.md)
