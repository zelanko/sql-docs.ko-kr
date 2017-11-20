---
title: "SQLGetFunctions 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLGetFunctions
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetFunctions
helpviewer_keywords:
- SQLGetFunctions function [ODBC]
ms.assetid: 0451d2f9-0f4f-46ba-b252-670956a52183
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e7359f5e652c2db21a991845accc15aaea5710e7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetfunctions-function"></a>SQLGetFunctions 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetFunctions** 는 드라이버 특정 ODBC 함수를 지원 하는지 여부에 대 한 정보를 반환 합니다. 이 함수는 드라이버 관리자; 구현 드라이버에서 구현할 수도 있습니다. 드라이버를 구현 하는 경우 **SQLGetFunctions**, 드라이버 관리자 드라이버에서 함수를 호출 합니다. 그렇지 않으면 함수 자체를 실행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLGetFunctions(  
     SQLHDBC           ConnectionHandle,  
     SQLUSMALLINT      FunctionId,  
     SQLUSMALLINT *    SupportedPtr);  
```  
  
## <a name="arguments"></a>인수  
 *ConnectionHandle*  
 [입력] 연결 핸들입니다.  
  
 *FunctionId*  
 [입력] A **#define** 관심; ODBC 함수를 식별 하는 값 **SQL_API_ODBC3_ALL_FUNCTIONS orSQL_API_ALL_FUNCTIONS**합니다. **SQL_API_ODBC3_ALL_FUNCTIONS** ODBC 3에서 사용 하는*.x* 응용 프로그램을 ODBC 3의 지원을 확인*.x* 및 이전 함수입니다. **SQL_API_ALL_FUNCTIONS** 는 ODBC 2에서 사용 하는*.x* 응용 프로그램을 ODBC 2의 지원을 확인*.x* 및 이전 함수입니다.  
  
 목록은 **#define** ODBC 함수를 식별 하는 값 "설명" 표를 참조 하십시오.  
  
 *SupportedPtr*  
 [출력]  경우 *FunctionId* 단일 ODBC 함수를 식별 *SupportedPtr* 단일 지점을 SQLUSMALLINT 값 즉 SQL_TRUE 없는 경우 지정된 된 함수, 드라이버 및 SQL_FALSE에서 지원 되는 경우 지원 됩니다.  
  
 경우 *FunctionId* SQL_API_ODBC3_ALL_FUNCTIONS은 *SupportedPtr* SQL_API_ODBC3_ALL_FUNCTIONS_SIZE 같은 요소의 수가 있는 SQLSMALLINT 배열을 가리킵니다. 이 배열은 ODBC 3 지 여부를 결정 하는 데 사용할 수 있는 4, 000 비트 비트맵으로 드라이버 관리자에서 처리는*.x* 또는 이전 함수는 지원 합니다. SQL_FUNC_EXISTS 매크로 기능 지원을 확인 하기 위해 호출 됩니다. ("주석" 참조) ODBC 3*.x* 응용 프로그램에서 호출할 수 **SQLGetFunctions** 중 하나는 ODBC 3에 대해 SQL_API_ODBC3_ALL_FUNCTIONS와*.x* 또는 ODBC 2*.x* 드라이버입니다.  
  
 경우 *FunctionId* SQL_API_ALL_FUNCTIONS은 *SupportedPtr* 100 요소의 SQLUSMALLINT 배열을 가리킵니다. 배열의 기준으로 인덱싱되어 있으면 **#define** 사용 하는 값 *FunctionId* 각 ODBC 함수를 식별 하는 배열의 일부 요소는 사용 되지 않고 나중에 사용할 목적으로 예약 된 합니다. ODBC 2를 식별 하는 경우 요소 이면 SQL_TRUE*.x* 또는 드라이버에서 지원 되는 이전 함수입니다. 드라이버에서 지원 되지 않습니다는 ODBC 함수를 식별 하거나 ODBC 함수를 식별 하지 못할 경우 SQL_FALSE를은 합니다.  
  
 반환 된 배열이 **SupportedPtr* 0부터 시작 하는 인덱스를 사용 합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetFunctions** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* 의 Sql_handle_dbc 라는 및 *처리* 의 *ConnectionHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLGetFunctions** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------|-----|-----------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) **SQLGetFunctions** 하기 전에 호출 된 **SQLConnect**, **SQLBrowseConnect**, 또는 **SQLDriverConnect**합니다.<br /><br /> (DM) **SQLBrowseConnect** 에 대 한 호출 된는 *ConnectionHandle* SQL_NEED_DATA를 반환 합니다. 이 함수를 호출 **SQLBrowseConnect** SQL_SUCCESS_WITH_INFO 또는 관계 없이 SQL_SUCCESS를 반환 합니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대 한 호출 된는 *ConnectionHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY095|함수 유형 범위를 벗어났습니다|(DM) 잘못 된 *FunctionId* 값이 지정 되었습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
  
## <a name="comments"></a>설명  
 **SQLGetFunctions** 항상 반환 하는 **SQLGetFunctions**, **SQLDataSources**, 및 **SQLDrivers** 지원 됩니다. 이러한 함수는 드라이버 관리자는 구현 않기 때문에이 없습니다. 드라이버 관리자는 ANSI 함수에 매핑됩니다 해당 유니코드 함수에서는 Unicode 함수가 존재 하 고 ANSI 함수가 있는 경우 유니코드 함수는 해당 ANSI 함수에 매핑합니다. 응용 프로그램 사용 하는 방법에 대 한 내용은 **SQLGetFunctions**, 참조 [인터페이스 받는 규칙 수준](../../../odbc/reference/develop-app/interface-conformance-levels.md)합니다.  
  
 다음은에 대 한 유효한 값 목록이 *FunctionId* ISO 92 표준-준수 수준을를 준수 하는 함수:  
  
|FunctionId 값|FunctionId 값|  
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
  
 다음은에 대 한 유효한 값 목록이 *FunctionId* Open Group 표준-준수 수준을를 준수 하는 함수에 대 한:  
  
|FunctionId 값|FunctionId 값|  
|-|-|  
|SQL_API_SQLCOLUMNS|SQL_API_SQLSTATISTICS|  
|SQL_API_SQLSPECIALCOLUMNS|SQL_API_SQLTABLES|  
  
 다음은에 대 한 유효한 값 목록이 *FunctionId* ODBC 표준-준수 수준을를 준수 하는 함수에 대 한 합니다.  
  
|FunctionId 값|FunctionId 값|  
|-|-|  
|SQL_API_SQLBINDPARAMETER|SQL_API_SQLNATIVESQL|  
|SQL_API_SQLBROWSECONNECT|SQL_API_SQLNUMPARAMS|  
|SQL_API_SQLBULKOPERATIONS [1]|SQL_API_SQLPRIMARYKEYS|  
|SQL_API_SQLCOLUMNPRIVILEGES|SQL_API_SQLPROCEDURECOLUMNS|  
|SQL_API_SQLDESCRIBEPARAM|SQL_API_SQLPROCEDURES|  
|SQL_API_SQLDRIVERCONNECT|SQL_API_SQLSETPOS|  
|SQL_API_SQLFOREIGNKEYS|SQL_API_SQLTABLEPRIVILEGES|  
|SQL_API_SQLMORERESULTS| |  
  
 [1]는 ODBC 2를 작업할 때*.x* 드라이버 **SQLBulkOperations** 는 반환 에서만 지원 되는 경우 다음 두 가지 모두: ODBC 2*.x* 드라이버 지원 **SQLSetPos**, 정보 유형 SQL_POS_OPERATIONS SQL_POS_ADD 비트 집합으로 반환 합니다.  
  
 다음은에 대 한 유효한 값 목록이 *FunctionId* 이상 버전에서 ODBC 3.8을 도입 하는 함수에 대 한:  
  
|FunctionId 값|  
|-|  
|SQL_API_SQLCANCELHANDLE [2]|  
  
 [2] **SQLCancelHandle** 반환할만 지원 드라이버가 둘 다를 지 원하는 **SQLCancel** 및 **SQLCancelHandle**합니다. 경우 **SQLCancel** 사용할 수 있지만 **SQLCancelHandle** 는 사용 되지 않는 응용 프로그램이 호출할 수 **SQLCancelHandle** 문 핸들에서 에매핑됩니다때문에 **SQLCancel**합니다.  
  
## <a name="sqlfuncexists-macro"></a>SQL_FUNC_EXISTS 매크로  
 SQL_FUNC_EXISTS (*SupportedPtr*, *FunctionID*) 매크로 ODBC 3의 지원을 확인 하는 데 사용 됩니다*.x* 또는 이전 함수 후 **SQLGetFunctions**  호출한는 *FunctionId* SQL_API_ODBC3_ALL_FUNCTIONS의 인수입니다. 응용 프로그램으로 SQL_FUNC_EXISTS 호출는 *SupportedPtr* 인수로 설정는 *SupportedPtr* 전달 된 *SQLGetFunctions*와  *FunctionID* 인수로 설정 된 **#define** 함수에 대 한 합니다. SQL_FUNC_EXISTS는 그렇지 않으면 함수는 지원 되는 경우에 SQL_TRUE 및 SQL_FALSE 반환 합니다.  
  
> [!NOTE]  
>  ODBC 2 작업할 때*.x* 드라이버에서 ODBC 3*.x* 드라이버 관리자에 대 한 SQL_TRUE를 반환 합니다 **SQLAllocHandle** 및 **SQLFreeHandle**때문에 **SQLAllocHandle** 에 매핑된 **SQLAllocEnv**, **SQLAllocConnect**, 또는 **SQLAllocStmt**, 및 때문에 **SQLFreeHandle** 에 매핑된 **SQLFreeEnv**, **SQLFreeConnect**, 또는 **SQLFreeStmt**합니다. **SQLAllocHandle** 또는 **SQLFreeHandle** 와 *HandleType* SQL_HANDLE_DESC의 인수 지원 되지 않는 반면 SQL_TRUE 있기 때문에 함수에 대해 반환 되는 경우에 없습니다 ODBC 2*.x* 이 예제의를 매핑하 함수입니다.  
  
## <a name="code-example"></a>코드 예  
 다음 세 가지 예제 응용 프로그램에서 사용 하는 방법을 보여 줍니다 **SQLGetFunctions** 드라이버를 지원 하는지 확인 하 **SQLTables**, **SQLColumns**, 및  **SQLStatistics**합니다. 드라이버는 이러한 함수를 지원 하지 않으면, 응용 프로그램이 드라이버에서 연결을 끊습니다. 첫 번째 예제에서는 호출 **SQLGetFunctions** 각 함수에 대해 한 번씩입니다.  
  
```  
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
  
 두 번째 예제에서는 ODBC 3.x 응용 프로그램 호출 **SQLGetFunctions** 는 배열을 전달 하 고 **SQLGetFunctions** 모든 ODBC에 대 한 정보를 반환 3.x 및 이전 함수입니다.  
  
```  
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
  
 세 번째 예제는 ODBC 2.x 응용 프로그램이 호출 **SQLGetFunctions** 는 100 요소의 배열을 전달 **SQLGetFunctions** 모든 ODBC에 대 한 정보를 반환 2.x 및 이전 함수입니다.  
  
```  
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
  
|내용|참조 항목|  
|---------------------------|---------|  
|연결 특성의 설정은 반환|[SQLGetConnectAttr 함수](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|드라이버 또는 데이터 원본에 대 한 정보 반환|[SQLGetInfo 함수](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|문 특성 설정을 반환합니다.|[SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

