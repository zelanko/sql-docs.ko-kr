---
title: SQLFreeStmt 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeStmt
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFreeStmt
helpviewer_keywords:
- SQLFreeStmt function [ODBC]
ms.assetid: 03408162-8b63-4470-90c4-e6c7d8d33892
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e252769c26a5491100094b1243b9c2c6bb67d94d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285703"
---
# <a name="sqlfreestmt-function"></a>SQLFreeStmt 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLFreeStmt는** 특정 명령문과 관련된 처리를 중지하고, 명령문과 연결된 열린 커서를 닫거나, 보류 중인 결과를 삭제하거나, 선택적으로 문 핸들과 관련된 모든 리소스를 해제합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLFreeStmt(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Option);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들  
  
 *옵션*  
 [입력] 다음 옵션 중 하나:  
  
 SQL_ 닫기: *명령문 핸들(정의된* 경우)과 연결된 커서를 닫고 보류 중인 모든 결과를 모두 삭제합니다. 응용 프로그램은 동일하거나 다른 매개 변수 값으로 **SELECT** 문을 다시 실행하여 나중에 이 커서를 다시 열 수 있습니다. 커서가 열려 있지 않으면 이 옵션은 응용 프로그램에 영향을 주지 않습니다. **SQLCloseCursor를** 호출하여 커서를 닫을 수도 있습니다. 자세한 내용은 [커서 닫기](../../../odbc/reference/develop-app/closing-the-cursor.md)를 참조하십시오.  
  
 SQL_DROP: 이 옵션은 더 이상 사용되지 않습니다. SQL_DROP *옵션이* 있는 **SQLFreeStmt** 호출은 드라이버 관리자에서 [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)에 매핑됩니다.  
  
 SQL_UNBIND: ARD의 SQL_DESC_COUNT 필드를 0으로 설정하여 지정된 *StatementHandle*에 대해 **SQLBindCol에** 바인딩된 모든 열 버퍼를 해제합니다. 이렇게 하면 책갈피 열의 바인딩이 해제되지 않습니다. 이렇게 하려면 책갈피 열에 대한 ARD의 SQL_DESC_DATA_PTR 필드가 NULL로 설정됩니다. 이 작업이 두 개 이상의 문에서 공유되는 명시적으로 할당된 설명자에서 수행되는 경우 이 작업은 설명자 공유를 공유하는 모든 문의 바인딩에 영향을 미칩니다. 자세한 내용은 [검색 결과(기본) 개요를](../../../odbc/reference/develop-app/retrieving-results-basic.md)참조하십시오.  
  
 SQL_RESET_PARAMS: APD의 SQL_DESC_COUNT 필드를 0으로 설정하고 지정된 *StatementHandle*에 대해 **SQLBindParameter에서** 설정한 모든 매개 변수 버퍼를 해제합니다. 이 작업이 두 개 이상의 문에서 공유되는 명시적으로 할당된 설명자에서 수행되는 경우 이 작업은 설명자 공유를 공유하는 모든 문의 바인딩에 영향을 미칩니다. 자세한 내용은 [바인딩 매개 변수](../../../odbc/reference/develop-app/binding-parameters-odbc.md)를 참조하십시오.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLFreeStmt가** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환하는 경우 *핸들 유형* SQL_HANDLE_STMT 및 *명령문* *핸들* 핸들을 사용하는 **SQLGetDiagRec를** 호출하여 연결된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 **SQLFreeStmt에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. **SQLFreeStmt가** 호출될 때 이 비동기 함수는 여전히 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대해 데이터를 검색하기 전에 *SQL_RESET_PARAMS* 옵션으로 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 *함수는 StatementHandle에* 대 한 호출 하 고이 함수를 호출 하는 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY092|범위를 벗어난 옵션 유형|(DM) 인수 *옵션에* 대해 지정된 값이 아닙니다.<br /><br /> SQL_CLOSE SQL_DROP SQL_UNBIND SQL_RESET_PARAMS|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 SQL_CLOSE 옵션으로 **SQLFreeStmt를** 호출하는 것은 **SQLCloseCursor를**호출하는 것과 동일하지만 SQL_CLOSE **SQLFreeStmt는** 명령문에 커서가 열려 있지 않은 경우 응용 프로그램에 영향을 주지 않습니다. 커서가 열려 있지 않으면 **SQLCloseCursor를** 호출하면 SQLSTATE 24000(잘못된 커서 상태)이 반환됩니다.  
  
 응용 프로그램이 해제된 후에는 문 핸들을 사용해서는 안 됩니다. 드라이버 관리자는 함수 호출에서 핸들의 유효성을 확인하지 않습니다.  
  
## <a name="example"></a>예제  
 핸들을 자유롭게 하는 것이 좋습니다. 그러나 간단히 하기 위해 다음 샘플에는 할당된 핸들을 해제하는 코드가 포함되어 있지 않습니다. 핸들을 해제하는 방법에 대한 예는 [SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)를 참조하십시오.  
  
```cpp  
// SQLFreeStmt.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
   retCode = SQLFreeStmt(hstmt, SQL_UNBIND);  
   retCode = SQLFreeStmt(hstmt, SQL_RESET_PARAMS);  
}  
```  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|명령문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|커서 닫기|[SQLCloseCursor 함수](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|손잡이 해제|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|커서 이름 설정|[SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
