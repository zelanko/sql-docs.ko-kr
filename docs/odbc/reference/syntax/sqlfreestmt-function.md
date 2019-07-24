---
title: SQLFreeStmt 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6141f3efe357bfb3f14c04aa2f6760e9470649a6
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345153"
---
# <a name="sqlfreestmt-function"></a>SQLFreeStmt 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLFreeStmt** 특정 문과 연결 된 처리를 중지 하거나, 문과 연결 된 열려 있는 모든 커서를 닫거나, 보류 중인 결과를 삭제 하거나, 필요에 따라 문 핸들과 연결 된 모든 리소스를 해제 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLFreeStmt(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Option);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들  
  
 *옵션*  
 입력 다음 옵션 중 하나입니다.  
  
 SQL_ CLOSE: *StatementHandle* 와 연결 된 커서 (정의 된 경우)를 닫고 모든 보류 중인 결과를 삭제 합니다. 응용 프로그램은 나중에 동일한 또는 다른 매개 변수 값으로 **SELECT** 문을 다시 실행 하 여 나중에이 커서를 다시 열 수 있습니다. 커서가 열려 있지 않으면이 옵션은 응용 프로그램에 영향을 주지 않습니다. **SQLCloseCursor** 을 호출 하 여 커서를 닫을 수도 있습니다. 자세한 내용은 [커서 닫기](../../../odbc/reference/develop-app/closing-the-cursor.md)를 참조 하세요.  
  
 SQL_DROP: 이 옵션은 더 이상 사용되지 않습니다. SQL_DROP의 *옵션* 을 사용 하는 **SQLFreeStmt** 호출은 드라이버 관리자에서 [sqlfreehandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)으로 매핑됩니다.  
  
 SQL_UNBIND: SQLBindCol의 SQL_DESC_COUNT 필드를 0으로 설정 하 여 지정 된 *StatementHandle*에 대해  에 의해 바인딩된 모든 열 버퍼를 해제 합니다. 책갈피 열의 바인딩을 해제 하지 않습니다. 이렇게 하려면 책갈피 열에 대 한 SQL_DESC_DATA_PTR 필드가 NULL로 설정 됩니다. 둘 이상의 문에서 공유 하는 명시적으로 할당 된 설명자에 대해이 작업을 수행 하면 해당 작업은 설명자를 공유 하는 모든 문의 바인딩에 영향을 줍니다. 자세한 내용은 [결과 검색 개요 (Basic)](../../../odbc/reference/develop-app/retrieving-results-basic.md)를 참조 하세요.  
  
 SQL_RESET_PARAMS: APD의 SQL_DESC_COUNT 필드를 0으로 설정 하 여 지정 된 *StatementHandle*에 대해 **SQLBindParameter** 에 의해 설정 된 모든 매개 변수 버퍼를 해제 합니다. 둘 이상의 문에 의해 공유 되는 명시적으로 할당 된 설명자에 대해이 작업을 수행 하는 경우이 작업은 설명자를 공유 하는 모든 문의 바인딩에 영향을 줍니다. 자세한 내용은 [바인딩 매개 변수](../../../odbc/reference/develop-app/binding-parameters-odbc.md)를 참조 하세요.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLFreeStmt** 에서 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 *HandleType의 SQL_HANDLE_STMT* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLFreeStmt** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR입니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec에** 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.  *\**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLFreeStmt** 가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE이 반환 되었습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 SQL_RESET_PARAMS로 설정 된 *옵션* 을 사용 하 여이 함수를 호출 했습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수가 호출 되었으며이 함수가 호출 될 때 여전히 실행 되 고 있습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA이 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY092|옵션 유형이 범위를 벗어났습니다.|(DM) 인수 *옵션* 에 지정 된 값이이 아닙니다.<br /><br /> SQL_CLOSE SQL_DROP SQL_UNBIND SQL_RESET_PARAMS|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 SQL_CLOSE 옵션을 사용 하 여 **SQLFreeStmt** 를 호출 하는 것은 **SQLCloseCursor**를 호출 하는 것과 같습니다. 단, 문에 커서가 열려 있지 않은 경우 **SQLFreeStmt** with SQL_CLOSE는 응용 프로그램에 영향을 주지 않습니다. 커서가 열려 있지 않으면 **SQLCloseCursor** 에 대 한 호출이 SQLSTATE 24000 (잘못 된 커서 상태)를 반환 합니다.  
  
 응용 프로그램은 문 핸들을 해제 한 후에는 사용 하면 안 됩니다. 드라이버 관리자는 함수 호출에서 핸들의 유효성을 검사 하지 않습니다.  
  
## <a name="example"></a>예제  
 핸들을 해제 하는 것이 좋은 프로그래밍 습관입니다. 그러나 편의상 다음 샘플에는 할당 된 핸들을 해제 하는 코드가 포함 되어 있지 않습니다. 핸들을 해제 하는 방법에 대 한 예제는 [Sqlfreehandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)를 참조 하세요.  
  
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
  
|내용|참조 항목|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|커서 닫기|[SQLCloseCursor 함수](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|핸들 해제|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|커서 이름 설정|[SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
