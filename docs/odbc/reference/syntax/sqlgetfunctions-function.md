---
title: SQLGetFunctions 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetFunctions
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLGetFunctions
helpviewer_keywords:
- SQLGetFunctions function [ODBC]
ms.assetid: 0451d2f9-0f4f-46ba-b252-670956a52183
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 15537b28ff2bae8a4fcd3e7be82426eb53aa83a8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285333"
---
# <a name="sqlgetfunctions-function"></a>SQLGetFunctions 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLGetFunctions는** 드라이버가 특정 ODBC 함수를 지원하는지 여부에 대한 정보를 반환합니다. 이 함수는 드라이버 관리자에서 구현됩니다. 드라이버에서도 구현할 수 있습니다. 드라이버가 **SQLGetFunctions를**구현하는 경우 드라이버 관리자는 드라이버의 함수를 호출합니다. 그렇지 않으면 함수 자체를 실행합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLGetFunctions(  
     SQLHDBC           ConnectionHandle,  
     SQLUSMALLINT      FunctionId,  
     SQLUSMALLINT *    SupportedPtr);  
```  
  
## <a name="arguments"></a>인수  
 *연결 핸들*  
 [Input] 연결 핸들입니다.  
  
 *Functionid*  
 [입력] 관심 있는 ODBC 함수를 식별하는 **#define** 값입니다. **SQL_API_ODBC3_ALL_FUNCTIONS orSQL_API_ALL_FUNCTIONS**. **SQL_API_ODBC3_ALL_FUNCTIONS** ODBC 3 *.x* 응용 프로그램에서 ODBC 3 *.x* 및 이전 함수의 지원을 확인하는 데 사용됩니다. **SQL_API_ALL_FUNCTIONS** ODBC 2 *.x* 응용 프로그램에서 ODBC 2 *.x* 및 이전 함수의 지원을 확인하는 데 사용됩니다.  
  
 ODBC 함수를 식별하는 **#define** 값 목록은 "주석"의 표를 참조하십시오.  
  
 *지원되는 Ptr*  
 [출력]  *FunctionId가* 단일 ODBC 함수를 식별하는 경우 *지원Ptr은* 지정된 함수가 드라이버에서 지원되는 경우 SQL_TRUE 단일 SQLUSMALLINT 값을 가리키며 지원되지 않는 경우 SQL_FALSE.  
  
 *FunctionId가* SQL_API_ODBC3_ALL_FUNCTIONS 경우 *지원Ptr은* SQL_API_ODBC3_ALL_FUNCTIONS_SIZE 같은 여러 요소가 있는 SQLSMALLINT 배열을 가리킵니다. 이 배열은 드라이버 관리자에 의해 ODBC 3 *.x* 또는 이전 함수가 지원되는지 여부를 확인하는 데 사용할 수 있는 4,000비트 비트맵으로 처리됩니다. SQL_FUNC_EXISTS 매크로는 함수 지원을 결정하기 위해 호출됩니다. ("댓글"참조)) ODBC 3 .x 응용 프로그램은 ODBC 3 *.x* 또는 ODBC*2.x* 드라이버에 대해 SQL_API_ODBC3_ALL_FUNCTIONS **SQLGetFunctions를** 호출할 수 있습니다.*.x*  
  
 *FunctionId가* SQL_API_ALL_FUNCTIONS 경우 *지원Ptr은* 100개 요소의 SQLUSMALLINT 배열을 가리킵니다. 배열은 *FunctionId에서* 각 ODBC 함수를 식별하는 데 사용되는 **#define** 값으로 인덱싱됩니다. 배열의 일부 요소는 사용되지 않으며 나중에 사용할 수 있습니다. 요소는 드라이버에서 지원하는 ODBC 2 *.x* 또는 이전 함수를 식별하는 경우 SQL_TRUE. 드라이버에서 지원되지 않는 ODBC 함수를 식별하거나 ODBC 함수를 식별하지 않는 경우 SQL_FALSE.  
  
 **지원되는 Ptr에서* 반환된 배열은 0기반 인덱싱을 사용합니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetFunctions** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값 핸들 *SQL_HANDLE_DBC 핸들* 핸들 SQL_HANDLE_DBC 및 *연결 핸들* *핸들을* **호출** 하 여 가져올 수 있습니다. 다음 표에서는 **SQLGetFunctions에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------|-----|-----------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) **SQLGetFunctions는** **SQLConnect,** **SQLBrowseConnect**또는 **SQLDriverConnect**전에 호출되었습니다.<br /><br /> (DM) **SQLBrowseConnect는** *연결 핸들에* 대 한 호출 하 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 **SQLBrowseConnect가** SQL_SUCCESS_WITH_INFO 또는 SQL_SUCCESS 반환하기 전에 호출되었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *연결 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY095|범위를 벗어난 함수 유형|(DM) 잘못된 *FunctionId* 값을 지정했습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
  
## <a name="comments"></a>주석  
 **SQLGetFunctions는** 항상 **SQLGetFunctions,** **SQLDataSource**및 **SQL드라이버가** 지원되는 것을 반환합니다. 이러한 함수는 드라이버 관리자에서 구현되기 때문에 이 작업을 수행합니다. 드라이버 관리자는 유니코드 함수가 있는 경우 ANSI 함수를 해당 유니코드 함수에 매핑하고 ANSI 함수가 있는 경우 유니코드 함수를 해당 ANSI 함수에 매핑합니다. 응용 프로그램에서 **SQLGetFunctions를**사용하는 방법에 대한 자세한 내용은 [인터페이스 적합성 수준을](../../../odbc/reference/develop-app/interface-conformance-levels.md)참조하십시오.  
  
 다음은 ISO 92 표준 준수 수준을 준수하는 함수에 대한 *FunctionId에* 대한 유효한 값 목록입니다.  
  
|함수ID 값|함수ID 값|  
|----------|----------|  
|SQL_API_SQLALLOCHANDLE|SQL_API_SQLGETDESCFIELD|  
|SQL_API_SQLBINDCOL|SQL_API_SQLGETDESCREC|  
|SQL_API_SQLCANCEL|SQL_API_SQLGETDIAGFIELD|  
|SQL_API_SQLCLOSECURSOR|SQL_API_SQLGETDIAGREC|  
|SQL_API_SQLCOLATTRIBUTE|SQL_API_SQLGETENVATTR|  
|SQL_API_SQLCONNECT|SQL_API_SQLGETFUNCTIONS|  
|SQL_API_SQLCOPYDESC|SQL_API_SQLGETINFO|  
|SQL_API_SQLDATASOURCES|SQL_API_SQLGETSTMTATTR|  
|SQL_API_SQLDESCRIBECOL|SQL_API_SQLGETTYPEINFO|  
|SQL_API_SQLDISCONNECT|SQL_API_SQLNUMRESULTCOLS|  
|SQL_API_SQLDRIVERS|SQL_API_SQLPARAMDATA|  
|SQL_API_SQLENDTRAN|SQL_API_SQLPREPARE|  
|SQL_API_SQLEXECDIRECT|SQL_API_SQLPUTDATA|  
|SQL_API_SQLEXECUTE|SQL_API_SQLROWCOUNT|  
|SQL_API_SQLFETCH|SQL_API_SQLSETCONNECTATTR|  
|SQL_API_SQLFETCHSCROLL|SQL_API_SQLSETCURSORNAME|  
|SQL_API_SQLFREEHANDLE|SQL_API_SQLSETDESCFIELD|  
|SQL_API_SQLFREESTMT|SQL_API_SQLSETDESCREC|  
|SQL_API_SQLGETCONNECTATTR|SQL_API_SQLSETENVATTR|  
|SQL_API_SQLGETCURSORNAME|SQL_API_SQLSETSTMTATTR|  
|SQL_API_SQLGETDATA| |  
  
 다음은 Open Group 표준 준수 수준을 준수하는 함수에 대한 *FunctionId에* 대한 유효한 값 목록입니다.  
  
|함수ID 값|함수ID 값|  
|-|-|  
|SQL_API_SQLCOLUMNS|SQL_API_SQLSTATISTICS|  
|SQL_API_SQLSPECIALCOLUMNS|SQL_API_SQLTABLES|  
  
 다음은 ODBC 표준 준수 수준을 준수하는 함수에 대한 *FunctionId에* 대한 유효한 값 목록입니다.  
  
|함수ID 값|함수ID 값|  
|-|-|  
|SQL_API_SQLBINDPARAMETER|SQL_API_SQLNATIVESQL|  
|SQL_API_SQLBROWSECONNECT|SQL_API_SQLNUMPARAMS|  
|SQL_API_SQLBULKOPERATIONS[1]|SQL_API_SQLPRIMARYKEYS|  
|SQL_API_SQLCOLUMNPRIVILEGES|SQL_API_SQLPROCEDURECOLUMNS|  
|SQL_API_SQLDESCRIBEPARAM|SQL_API_SQLPROCEDURES|  
|SQL_API_SQLDRIVERCONNECT|SQL_API_SQLSETPOS|  
|SQL_API_SQLFOREIGNKEYS|SQL_API_SQLTABLEPRIVILEGES|  
|SQL_API_SQLMORERESULTS| |  
  
 [1] ODBC 2 *.x* 드라이버로 작업하는 **경우, SQLBulkOperations는** 다음 두 가지 모두 true인 경우에만 지원되는 것으로 반환됩니다: ODBC 2 *.x* 드라이버는 **SQLSetPos를**지원하고 정보 형식 SQL_POS_OPERATIONS SQL_POS_ADD 비트를 집합으로 반환합니다.  
  
 다음은 ODBC 3.8 이상에 도입된 함수에 대한 *FunctionId에* 대한 유효한 값 목록입니다.  
  
|함수ID 값|  
|-|  
|SQL_API_SQLCANCELHANDLE [2]|  
  
 [2] **SQLCancelHandle** 드라이버는 **SQLCancel** 및 **SQLCancelHandle**을 모두 지원하는 경우에만 지원되는 대로 반환됩니다. **SQLCancel이** 지원되지만 **SQLCancelHandle이** 없는 경우 응용 프로그램은 **SQLCancel**에 매핑되므로 문 핸들에서 **SQLCancelHandle을** 호출할 수 있습니다.  
  
## <a name="sql_func_exists-macro"></a>SQL_FUNC_EXISTS 매크로  
 *SQL_FUNC_EXISTS(지원Ptr*, *FunctionID)* 매크로는 **SQLGetFunctions가** SQL_API_ODBC3_ALL_FUNCTIONS *FunctionId* 인수로 호출된 후 ODBC*3.x* 또는 이전 함수의 지원을 확인하는 데 사용됩니다. 응용 프로그램은 SQL_FUNC_EXISTS *지원되는 Ptr* 인수가 *SQLGetFunctions에서*전달된 *지원되는 Ptr로* 설정되고 *FunctionID* 인수가 함수의 **#define** 집합된 경우를 호출합니다. SQL_FUNC_EXISTS 함수가 지원되는 경우 SQL_TRUE 반환하고 그렇지 않으면 SQL_FALSE.  
  
> [!NOTE]
>  ODBC 2 *.x* 드라이버로 **SQLFreeConnect**작업할 때, ODBC **SQLAllocConnect** **SQLAllocStmt***3.x* 드라이버 관리자는 **SQLAllocHandle** 및 **SQLFreeHandle에** **SQLAllocEnv**대한 SQL_TRUE **SQLFreeHandle** **SQLFreeEnv** **SQLFreeStmt** **반환합니다.** 그러나 SQL_HANDLE_DESC *핸들 타이* 인수를 가진 **SQLAllocHandle** 또는 **SQLFreeHandle은** 이 경우에 매핑할 ODBC 2 *.x* 함수가 없기 때문에 함수에 대해 반환되는 경우에도 SQL_TRUE 지원되지 않습니다.  
  
## <a name="code-example"></a>코드 예  
 다음 세 가지 예제에서는 응용 프로그램에서 **SQLGetFunctions를** 사용하여 드라이버가 **SQLTables, SQLColumns**및 **SQLStatistics**를 지원하는지 확인하는 방법을 보여 주며 있습니다. **SQLColumns** 드라이버가 이러한 기능을 지원하지 않으면 응용 프로그램이 드라이버에서 연결을 끊습니다. 첫 번째 예제는 각 함수에 대해 **SQLGetFunctions를** 한 번 호출합니다.  
  
```cpp  
SQLUSMALLINT TablesExists, ColumnsExists, StatisticsExists;  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
  
retcodeTables = SQLGetFunctions(hdbc, SQL_API_SQLTABLES, &TablesExists);  
retcodeColumns = SQLGetFunctions(hdbc, SQL_API_SQLCOLUMNS, &ColumnsExists);  
retcodeStatistics = SQLGetFunctions(hdbc, SQL_API_SQLSTATISTICS, &StatisticsExists);  
  
// SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver.  
if (retcodeTables == SQL_SUCCESS && TablesExists == SQL_TRUE &&   
retcodeColumns == SQL_SUCCESS && ColumnsExists == SQL_TRUE &&   
retcodeStatistics == SQL_SUCCESS && StatisticsExists == SQL_TRUE)   
{  
  
   // Continue with application  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
 두 번째 예에서 ODBC 3.x 응용 프로그램은 **SQLGetFunctions를** 호출하고 **SQLGetFunctions가** 모든 ODBC 3.x 및 이전 함수에 대한 정보를 반환하는 배열을 전달합니다.  
  
```cpp  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
SQLUSMALLINT fExists[SQL_API_ODBC3_ALL_FUNCTIONS_SIZE];  
  
retcode = SQLGetFunctions(hdbc, SQL_API_ODBC3_ALL_FUNCTIONS, fExists);  
  
// SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver.  
if (reccode == SQL_SUCCESS &&   
SQL_FUNC_EXISTS(fExists, SQL_API_SQLTABLES) == SQL_TRUE &&  
   SQL_FUNC_EXISTS(fExists, SQL_API_SQLCOLUMNS) == SQL_TRUE &&  
   SQL_FUNC_EXISTS(fExists, SQL_API_SQLSTATISTICS) == SQL_TRUE)   
{  
  
   // Continue with application  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
 세 번째 예는 ODBC 2.x 응용 프로그램이 **SQLGetFunctions를** 호출하고 **SQLGetFunctions가** 모든 ODBC 2.x 및 이전 함수에 대한 정보를 반환하는 100개 요소의 배열을 전달하는 것입니다.  
  
```cpp  
#define FUNCTIONS 100  
  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
SQLUSMALLINT fExists[FUNCTIONS];  
  
retcode = SQLGetFunctions(hdbc, SQL_API_ALL_FUNCTIONS, fExists);  
  
/* SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver. */  
if (retcode == SQL_SUCCESS &&   
fExists[SQL_API_SQLTABLES] == SQL_TRUE &&  
   fExists[SQL_API_SQLCOLUMNS] == SQL_TRUE &&  
   fExists[SQL_API_SQLSTATISTICS] == SQL_TRUE)   
{  
  
   /* Continue with application */  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|연결 특성의 설정 반환|[SQLGetConnectAttr 함수(SQLGetConnectAttr Function)](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|드라이버 또는 데이터 원본에 대한 정보 반환|[SQLGetInfo 함수](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|문 특성의 설정 반환|[SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
