---
title: SQLGetFunctions 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 98fb29265c17970fbcef0f21778d7a9130e52771
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644521"
---
# <a name="sqlgetfunctions-function"></a>SQLGetFunctions 함수
**규칙**  
 버전에 도입 되었습니다: ODBC 1.0 표준 준수 합니다: ISO 92  
  
 **요약**  
 **SQLGetFunctions** 드라이버 관련 ODBC 함수를 지원 하는지 여부에 대 한 정보를 반환 합니다. 이 함수는 구현 드라이버 관리자입니다. 또한 드라이버에서 구현할 수 있습니다. 드라이버를 구현 하는 경우 **SQLGetFunctions**, 드라이버 관리자가 드라이버에서 함수를 호출 합니다. 그렇지 않으면 함수 자체를 실행합니다.  
  
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
 [입력] A **#define** 관심; ODBC 함수를 식별 하는 값 **SQL_API_ODBC3_ALL_FUNCTIONS orSQL_API_ALL_FUNCTIONS**합니다. **SQL_API_ODBC3_ALL_FUNCTIONS** 는 ODBC 3에서 사용 하는 *.x* ODBC 3의 지원을 확인 하기 위해 응용 프로그램 *.x* 및 이전 함수입니다. **SQL_API_ALL_FUNCTIONS** 는 ODBC 2를 사용해 *.x* ODBC 2 지원을 확인 하기 위해 응용 프로그램 *.x* 및 이전 함수입니다.  
  
 목록은 **#define** ODBC 함수를 식별 하는 값 "주석입니다."에서 표를 참조 하세요.  
  
 *SupportedPtr*  
 [출력]  하는 경우 *FunctionId* 는 단일 ODBC 함수를 식별 *SupportedPtr* 단일 지점 SQLUSMALLINT 값 즉 SQL_TRUE 없으면 지정된 된 함수 SQL_FALSE 고 드라이버에서 지원 되는 경우 지원 합니다.  
  
 하는 경우 *FunctionId* SQL_API_ODBC3_ALL_FUNCTIONS, 됩니다 *SupportedPtr* SQL_API_ODBC3_ALL_FUNCTIONS_SIZE 같은 요소의 숫자가 있는 SQLSMALLINT 배열을 가리킵니다. 이 배열은 ODBC 3 여부를 확인 하려면 사용할 수 있는 4,000 비트 비트맵으로 드라이버 관리자에 의해 처리 됩니다 *.x* 또는 earlier 함수는 지원 합니다. SQL_FUNC_EXISTS 매크로 함수 지원을 확인 하기 위해 호출 됩니다. ("주석입니다." 참조) ODBC 3 *.x* 응용 프로그램에서 호출할 수 있습니다 **SQLGetFunctions** 중 하나는 ODBC 3에 대해 SQL_API_ODBC3_ALL_FUNCTIONS를 사용 하 여 *.x* 또는 ODBC 2 *.x* 드라이버입니다.  
  
 하는 경우 *FunctionId* SQL_API_ALL_FUNCTIONS, 됩니다 *SupportedPtr* 100 요소의 SQLUSMALLINT 배열을 가리킵니다. 배열으로 인덱싱된 **#define** 에서 사용 되는 값 *FunctionId* 각 ODBC 함수를 식별 하 배열의 일부 요소는 사용 되지 않는 및 나중에 사용 하도록 예약 합니다. ODBC 2를 식별 하는 경우 요소 이면 SQL_TRUE *.x* 또는 드라이버에서 지원 되는 이전 함수입니다. 드라이버에서 지원 되지 않습니다 ODBC 함수를 식별 하거나 ODBC 함수를 식별 하지 않는 경우 SQL_FALSE입니다.  
  
 반환 된 배열이 **SupportedPtr* 0부터 시작 하는 인덱스를 사용 합니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetFunctions** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* 의 SQL_HANDLE_DBC와 *처리할* 의 *ConnectionHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLGetFunctions** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------|-----|-----------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) **SQLGetFunctions** 하기 전에 호출 되었습니다 **SQLConnect**에 **SQLBrowseConnect**, 또는 **SQLDriverConnect**합니다.<br /><br /> (DM) **SQLBrowseConnect** 에 대해 호출 된 합니다 *ConnectionHandle* SQL_NEED_DATA를 반환 합니다. 하기 전에이 함수를 호출한 **SQLBrowseConnect** SQL_SUCCESS_WITH_INFO 또는 관계 없이 SQL_SUCCESS를 반환 합니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *ConnectionHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY095|함수 유형 범위를 벗어났습니다|(DM)는 잘못 *FunctionId* 값이 지정 되었습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLGetFunctions** 는 항상 반환 **SQLGetFunctions**합니다 **SQLDataSources**, 및 **SQLDrivers** 지원 됩니다. 이러한 함수 드라이버 관리자의 구현 되므로이 수행 합니다. 즉 드라이버 관리자는 Unicode 함수가 존재 하 고 ANSI 함수가 존재 하는 경우 유니코드 함수는 해당 ANSI 함수에 매핑하는 ANSI 함수를 해당 유니코드 함수에 매핑됩니다. 응용 프로그램을 사용 하는 방법에 대 한 자세한 **SQLGetFunctions**를 참조 하십시오 [인터페이스 적합성 수준](../../../odbc/reference/develop-app/interface-conformance-levels.md)합니다.  
  
 다음은 유효한 값 목록을 *FunctionId* ISO 92 표준 – 준수 수준을를 준수 하는 함수에 대 한 합니다.  
  
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
  
 다음은 유효한 값 목록을 *FunctionId* Open Group 표준 – 준수 수준을 준수 하는 함수에 대 한 합니다.  
  
|FunctionId 값|FunctionId 값|  
|-|-|  
|SQL_API_SQLCOLUMNS|SQL_API_SQLSTATISTICS|  
|SQL_API_SQLSPECIALCOLUMNS|SQL_API_SQLTABLES|  
  
 다음은 유효한 값 목록을 *FunctionId* ODBC 표준 – 준수 수준을 준수 하는 함수에 대 한 합니다.  
  
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
  
 [1]는 ODBC 2를 사용 하 여 작업 하는 경우 *.x* 드라이버 **SQLBulkOperations** 반환 됩니다만 지원 되는 경우 다음 모두: ODBC 2 *.x* 드라이버 지원 **SQLSetPos**, 정보 유형 SQL_POS_OPERATIONS SQL_POS_ADD 비트 집합으로 반환 합니다.  
  
 다음은 유효한 값 목록을 *FunctionId* ODBC 3.8 이상 도입 된 함수에 대 한 합니다.  
  
|FunctionId 값|  
|-|  
|SQL_API_SQLCANCELHANDLE [2]|  
  
 [2] **SQLCancelHandle** 반환할만 지원 드라이버가 둘 다를 지 원하는 **SQLCancel** 하 고 **SQLCancelHandle**합니다. 하는 경우 **SQLCancel** 은 지원 하지만 **SQLCancelHandle** 응용 프로그램 수 호출 되지 않습니다 **SQLCancelHandle** 문 핸들에 대해 에매핑될때문에 **SQLCancel**합니다.  
  
## <a name="sqlfuncexists-macro"></a>SQL_FUNC_EXISTS 매크로  
 SQL_FUNC_EXISTS (*SupportedPtr*를 *FunctionID*) 매크로 ODBC 3의 지원을 확인 하는 데 사용 됩니다 *.x* 함수나 이전 후 **SQLGetFunctions**  가 사용 하 여 호출 된를 *FunctionId* SQL_API_ODBC3_ALL_FUNCTIONS의 인수입니다. SQL_FUNC_EXISTS 사용 하 여 호출 하는 응용 프로그램을 *SupportedPtr* 인수와 함께 사용 합니다 *SupportedPtr* 전달 *SQLGetFunctions*와  *FunctionID* 인수와 함께 사용 합니다 **#define** 함수에 대 한 합니다. SQL_FUNC_EXISTS는 그렇지 않은 경우 함수는 지원 되는 경우에 SQL_TRUE 및 SQL_FALSE 반환 합니다.  
  
> [!NOTE]  
>  ODBC 2를 사용 하 여 작업 하는 경우 *.x* 드라이버는 ODBC 3 *.x* 드라이버 관리자에 대 한 SQL_TRUE를 반환 합니다 **SQLAllocHandle** 고 **SQLFreeHandle**때문에 **SQLAllocHandle** 매핑되 **SQLAllocEnv**합니다 **SQLAllocConnect**, 또는 **SQLAllocStmt**, 및 때문에 **SQLFreeHandle** 매핑됩니다 **SQLFreeEnv**를 **SQLFreeConnect**, 또는 **SQLFreeStmt**합니다. **그러나 SQLAllocHandle** 나 **SQLFreeHandle** 사용 하 여를 *HandleType* SQL_HANDLE_DESC 인수의 지원 되지 않는 SQL_TRUE 있기 때문에 함수에 대해 반환 되는 경우에 없음 ODBC 2 *.x* 매핑할이 경우에 함수입니다.  
  
## <a name="code-example"></a>코드 예  
 다음 세 가지 예제 응용 프로그램을 사용 하는 방법을 보여 줍니다 **SQLGetFunctions** 드라이버를 지원 하는지 확인 하 **SQLTables**하십시오 **SQLColumns**, 및  **SQLStatistics**합니다. 드라이버는 이러한 함수를 지원 하지 않으면, 응용 프로그램이 드라이버에서 연결을 끊습니다. 첫 번째 예제에서는 호출 **SQLGetFunctions** 각 함수에 한 번씩입니다.  
  
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
  
 두 번째 예제에서는 ODBC 3.x 응용 프로그램 호출 **SQLGetFunctions** 는 배열을 전달 **SQLGetFunctions** 모든 ODBC에 대 한 정보를 반환 합니다. 3.x 및 이전 함수입니다.  
  
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
  
 세 번째 예제는 ODBC 2.x 응용 프로그램 호출 **SQLGetFunctions** 는 100 개 요소 배열을 전달 **SQLGetFunctions** 모든 ODBC에 대 한 정보를 반환 합니다. 2.x 및 이전 함수입니다.  
  
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
|연결 특성의 설정을 반환합니다.|[SQLGetConnectAttr 함수](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|드라이버 또는 데이터 원본에 대 한 정보를 반환합니다.|[SQLGetInfo 함수](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|반환 문 특성 설정|[SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
