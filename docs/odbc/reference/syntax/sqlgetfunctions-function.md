---
title: SQLGetFunctions 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: edb58ebff212e494b84aed12397def2876d3728d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68345608"
---
# <a name="sqlgetfunctions-function"></a>SQLGetFunctions 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetFunctions** 은 드라이버가 특정 ODBC 함수를 지원 하는지 여부에 대 한 정보를 반환 합니다. 이 함수는 드라이버 관리자에서 구현 됩니다. 드라이버에서 구현할 수도 있습니다. 드라이버에서 **SQLGetFunctions**를 구현 하는 경우 드라이버 관리자는 드라이버에서 함수를 호출 합니다. 그렇지 않으면 함수 자체를 실행 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLGetFunctions(  
     SQLHDBC           ConnectionHandle,  
     SQLUSMALLINT      FunctionId,  
     SQLUSMALLINT *    SupportedPtr);  
```  
  
## <a name="arguments"></a>인수  
 *ConnectionHandle*  
 [Input] 연결 핸들입니다.  
  
 *FunctionId*  
 입력 원하는 ODBC 함수를 식별 하는 **#define** 값입니다. **OrSQL_API_ALL_FUNCTIONS를 SQL_API_ODBC3_ALL_FUNCTIONS**합니다. Odbc*3.x 응용 프로그램* 에서 **SQL_API_ODBC3_ALL_FUNCTIONS** 를 사용 하 여 odbc*2.x 및 이전* 함수를 지원 하는지 확인 합니다. **SQL_API_ALL_FUNCTIONS** 은 odbc*2.x 응용 프로그램* 에서 odbc 2.x 및 이전 함수를 지원 하는지 여부*를 확인* 하는 데 사용 됩니다.  
  
 ODBC 함수를 식별 하는 **#define** 값 목록은 "Comments"의 표를 참조 하십시오.  
  
 *SupportedPtr*  
 출력  *FunctionId* 가 단일 ODBC 함수를 식별 하는 경우 *supportedptr* 은 지정 된 함수가 드라이버에서 지원 되는 경우 SQL_TRUE 되는 단일 SQLUSMALLINT 값을 가리키며 SQL_FALSE 지원 되지 않는 경우에는를 지정 합니다.  
  
 *FunctionId* 가 SQL_API_ODBC3_ALL_FUNCTIONS 인 경우 *supportedptr* 은 SQL_API_ODBC3_ALL_FUNCTIONS_SIZE와 동일한 수의 요소가 있는 sqlsmallint 배열을 가리킵니다. 이 배열은 드라이버 관리자에서 ODBC*2.x 또는 이전* 함수가 지원 되는지 여부를 확인 하는 데 사용할 수 있는 4000 비트 비트맵으로 처리 됩니다. 함수 지원을 확인 하기 위해 SQL_FUNC_EXISTS 매크로가 호출 됩니다. "설명"을 참조 하십시오. ODBC*3.x 응용 프로그램* 은 odbc*3.x 또는 odbc* *2.x 드라이버에* 대해 SQL_API_ODBC3_ALL_FUNCTIONS를 사용 하 여 **SQLGetFunctions** 를 호출할 수 있습니다.  
  
 *FunctionId* 가 SQL_API_ALL_FUNCTIONS 인 경우 *supportedptr* 은 100 요소의 SQLUSMALLINT 배열을 가리킵니다. 배열은 각 ODBC 함수를 식별 하기 위해 *FunctionId* 에서 사용 되는 **#define** 값으로 인덱싱됩니다. 배열의 일부 요소는 사용 되지 않으며 나중에 사용 하도록 예약 되어 있습니다. 요소는 드라이버에서 지 원하는 ODBC*2.x 또는 이전* 함수를 식별 하는 경우 SQL_TRUE 됩니다. 드라이버에서 지원 하지 않는 ODBC 함수를 식별 하거나 ODBC 함수를 식별 하지 않는 경우 SQL_FALSE 됩니다.  
  
 **Supportedptr* 에서 반환 된 배열은 0부터 시작 하는 인덱스를 사용 합니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetFunctions** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 SQL_HANDLE_DBC의 *HandleType* 및 *ConnectionHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLGetFunctions** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------|-----|-----------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) **SQLGetFunctions** 가 **SQLConnect**, **SQLBrowseConnect**또는 **SQLDriverConnect**이전에 호출 되었습니다.<br /><br /> (DM) **SQLBrowseConnect** 가 *ConnectionHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 **SQLBrowseConnect** 가 SQL_SUCCESS_WITH_INFO 또는 SQL_SUCCESS을 반환 하기 전에 호출 되었습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *ConnectionHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY095|함수 형식이 범위를 벗어났습니다.|(DM) 잘못 된 *FunctionId* 값이 지정 되었습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
  
## <a name="comments"></a>주석  
 **SQLGetFunctions** 는 항상 **SQLGetFunctions**, **sqldatasources 원본**및 **sqldatasources** 가 지원 됨을 반환 합니다. 이러한 함수는 드라이버 관리자에서 구현 되기 때문에이를 수행 합니다. 유니코드 함수가 있는 경우 드라이버 관리자는 ANSI 함수를 해당 하는 유니코드 함수에 매핑하고 ANSI 함수가 있는 경우 해당 ANSI 함수에 유니코드 함수를 매핑합니다. 응용 프로그램에서 **SQLGetFunctions**를 사용 하는 방법에 대 한 자세한 내용은 [인터페이스 규칙 수준](../../../odbc/reference/develop-app/interface-conformance-levels.md)을 참조 하세요.  
  
 다음은 ISO 92 표준 준수 수준을 준수 하는 *함수에 대 한 잘못* 된 값의 목록입니다.  
  
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
  
 다음은 오픈 그룹 표준 준수 수준을 준수 하는 *함수에 대 한 잘못* 된 값의 목록입니다.  
  
|FunctionId 값|FunctionId 값|  
|-|-|  
|SQL_API_SQLCOLUMNS|SQL_API_SQLSTATISTICS|  
|SQL_API_SQLSPECIALCOLUMNS|SQL_API_SQLTABLES|  
  
 다음은 ODBC 표준 준수 수준을 준수 하는 *함수에 대 한 잘못* 된 값의 목록입니다.  
  
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
  
 [1] ODBC 2.x 드라이버를 사용 하는 경우 다음 두 가지 모두에 해당 하는 경우에만 **SQLBulkOperations** 이 지원 되는 것으로 반환 됩니다 *. odbc* *2.x 드라이버는* **SQLSetPos**를 지원 하 고 정보 형식 SQL_POS_OPERATIONS 설정 된 SQL_POS_ADD 비트를 반환 합니다.  
  
 다음은 ODBC 3.8 이상에서 도입 된 함수 *에 대 한 잘못* 된 값의 목록입니다.  
  
|FunctionId 값|  
|-|  
|SQL_API_SQLCANCELHANDLE [2]|  
  
 [2] **Sqlcancelhandle** 은 드라이버가 **Sqlcancel** 및 **sqlcancelhandle**을 모두 지 원하는 경우에만 지원 되는 것으로 반환 됩니다. **Sqlcancel** 이 지원 되지만 **sqlcancelhandle** 이 지원 되지 않으면 응용 프로그램은 **sqlcancel**에 매핑되므로 문 핸들에 대해 **sqlcancelhandle** 을 호출할 수 있습니다.  
  
## <a name="sql_func_exists-macro"></a>SQL_FUNC_EXISTS 매크로  
 SQL_FUNC_EXISTS (*Supportedptr*, *FunctionID*) 매크로는 SQL_API_ODBC3_ALL_FUNCTIONS의 *FunctionID* 인수를 사용 하 여 **SQLGetFunctions** 가 호출 된 후 ODBC 2.x 또는 이전 함수를 지원 하는지 확인 하는 데 사용*됩니다.* 응용 프로그램은 *SQLGetFunctions*에 전달 *된 supportedptr 인수를* 사용 *하 고 함수* 에 대 한 **#define** 에 *FunctionID* 인수를 설정 하 여 SQL_FUNC_EXISTS를 호출 합니다. SQL_FUNC_EXISTS는 함수가 지원 되는 경우 SQL_TRUE을 반환 하 고 그렇지 않으면를 SQL_FALSE 합니다.  
  
> [!NOTE]
>  Odbc*2.x 드라이버를* 사용 하는 경우 **SQLAllocHandle** 가 **sqlfreehandle**, **sqlfreehandle**또는 **Sqlfreehandle**에 매핑되고 **SQLFREEHANDLE** 이 **Sqlfreehandle**, **SQLFreeConnect**또는 **SQLFreeStmt**에 매핑되므로 odbc*3.x 드라이버 관리자* 는 **SQLAllocHandle** 및 **sqlfreehandle** 에 대해 SQL_TRUE를 반환 합니다. SQL_TRUE 그러나이 경우에 매핑할 ODBC*2.x 함수는* 없기 때문에 SQL_HANDLE_DESC *HandleType* 인수를 사용 하는 **SQLAllocHandle** 또는 **sqlfreehandle** 은 지원 되지 않습니다.  
  
## <a name="code-example"></a>코드 예  
 다음 세 가지 예제에서는 응용 프로그램이 **SQLGetFunctions** 를 사용 하 여 드라이버가 **sqltables**, **sqltables**및 **SQLStatistics**를 지원 하는지 확인 하는 방법을 보여 줍니다. 드라이버가 이러한 기능을 지원 하지 않는 경우 응용 프로그램은 드라이버에서 연결을 끊습니다. 첫 번째 예제에서는 각 함수에 대해 **SQLGetFunctions** 를 한 번씩 호출 합니다.  
  
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
  
 두 번째 예제에서 ODBC 2.x 응용 프로그램은 **SQLGetFunctions** 를 호출 하 고 **SQLGETFUNCTIONS** 가 모든 ODBC 2.x 및 이전 함수에 대 한 정보를 반환 하는 배열을 전달 합니다.  
  
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
  
 세 번째 예제는 ODBC 2.x 응용 프로그램은 **SQLGetFunctions** 를 호출 하 고 **SQLGETFUNCTIONS** 가 모든 ODBC 2.x 및 이전 함수에 대 한 정보를 반환 하는 100 요소 배열을 전달 합니다.  
  
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
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|연결 특성의 설정 반환|[SQLGetConnectAttr 함수(SQLGetConnectAttr Function)](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|드라이버 또는 데이터 원본에 대 한 정보 반환|[SQLGetInfo 함수](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|문 특성의 설정 반환|[SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
