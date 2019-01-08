---
title: SQLFreeHandle 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeHandle
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFreeHandle
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
ms.assetid: 17a6fcdc-b05a-4de7-be93-a316f39696a1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f63af414d59afed2bbe2e8eed3fba7a1362bb4bb
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53203912"
---
# <a name="sqlfreehandle-function"></a>SQLFreeHandle 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLFreeHandle** 특정 환경, 연결, 문 또는 설명자 핸들과 연결 된 리소스를 해제 합니다.  
  
> [!NOTE]
>  이 함수는 제네릭 함수 핸들을 해제 합니다. ODBC 2.0 함수 대체 **SQLFreeConnect** (에 대 한 연결 핸들을 해제) 하 고 **SQLFreeEnv** (에 대 한 환경 핸들을 해제) 합니다. **SQLFreeConnect** 하 고 **SQLFreeEnv** 둘 다에서 사용 되지 않는 ODBC 3 *.x*합니다. **SQLFreeHandle** 또한 ODBC 2.0 함수를 대체 **SQLFreeStmt** (SQL_DROP를 사용 하 여 *옵션*) 문 핸들을 해제 합니다. 자세한 내용은 "설명입니다."을 참조 하세요. 새로운 드라이버 관리자는이 함수를 경우 맵을 ODBC 3 대 한 자세한 내용은 *.x* 는 ODBC 2를 사용 하 여 응용 프로그램이 작동 *.x* 드라이버를 참조 하세요. [뒤로 대 한 대체 함수 매핑 응용 프로그램의 호환성](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 [입력] 해제할 핸들의 형식을 **SQLFreeHandle**합니다. 다음 값 중 하나 여야 합니다.  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   호출 하 여  
  
 드라이버 관리자 및 드라이버에 의해서만 SQL_HANDLE_DBC_INFO_TOKEN 핸들을 사용 합니다. 응용 프로그램에는이 핸들 형식은 사용 하지 마십시오. SQL_HANDLE_DBC_INFO_TOKEN에 대 한 자세한 내용은 참조 하세요. [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)합니다.  
  
 하는 경우 *HandleType* 두이 값 중 하나가 아닙니다 **SQLFreeHandle** 에서 SQL_INVALID_HANDLE을 반환 합니다.  
  
 *Handle*  
 [입력] 해제할 핸들입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
 하는 경우 **SQLFreeHandle** 가 여전히 유효한 핸들 SQL_ERROR를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLFreeHandle** 핸들에 대 한 진단 데이터 구조에서 SQL_ERROR를 연관된 된 SQLSTATE 값 반환을 얻을 수 있습니다 하 **SQLFreeHandle** 해제 하려고 했으나 없습니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLFreeHandle** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 실행 또는 완료 함수를 지원 하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)는 *HandleType* 인수가 SQL_HANDLE_ENV, 및 하나 이상의 연결 된 할당 또는 연결 된 상태에 있는 합니다. **SQLDisconnect** 하 고 **SQLFreeHandle** 사용 하 여를 *HandleType* SQL_HANDLE_DBC의 호출 하기 전에 각 연결에 대해 호출 되어야 합니다 **SQLFreeHandle** 으로 *HandleType* SQL_HANDLE_ENV입니다.<br /><br /> (DM)는 *HandleType* 인수가 SQL_HANDLE_DBC, 및 함수를 호출 하기 전에 호출한 **SQLDisconnect** 연결에 대 한 합니다.<br /><br /> (DM)는 *HandleType* 인수가 SQL_HANDLE_DBC 합니다. 비동기적으로 실행 중인 함수를 사용 하 여 호출한 *처리* 이 함수가 호출 되었을 때 함수를 계속 실행 하 고 있습니다.<br /><br /> (DM)는 *HandleType* 인수가 호출 합니다. **SQLExecute**, **SQLExecDirect**합니다 **SQLBulkOperations**, 또는 **SQLSetPos** 문 핸들을 사용 하 여 호출 되 고 SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.<br /><br /> (DM)는 *HandleType* 인수가 호출 합니다. 연결 핸들 또는 문 핸들에서 비동기적으로 실행 중인 함수를 호출한 하 고이 함수가 호출 되었을 때 함수를 계속 실행 합니다.<br /><br /> (DM)는 *HandleType* 인수가 SQL_HANDLE_DESC 합니다. 연결 핸들에서 비동기적으로 실행 중인 함수를 호출한 및이 함수가 호출 되었을 때 함수를 계속 실행 합니다.<br /><br /> (DM) 모든 종속 핸들 및 기타 리소스 해제 되지 않으므로 앞 **SQLFreeHandle** 호출 되었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 관련 된 문 핸들 중 하나에 대해 호출한 합니다 *처리* 및 *HandleType* 호출으로 설정 된 또는 SQL_HANDLE_DESC SQL_PARAM_DATA_AVAILABLE를 반환 합니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|합니다 *HandleType* 인수 호출 되었거나 SQL_HANDLE_DESC, 및 기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 했으므로 함수 호출을 처리할 수 없습니다.|  
|HY017|자동으로 할당 된 설명자 핸들을 잘못 사용 했습니다.|(DM)는 *처리* 인수를 자동으로 할당 된 설명자에 대 한 핸들을로 설정 되었습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)는 *HandleType* 인수가 SQL_HANDLE_DESC, 했는데 드라이버는 ODBC 2 *.x* 드라이버입니다.<br /><br /> (DM)는 *HandleType* 인수를 호출 하 여 되었으며 유효한 ODBC 드라이버가 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLFreeHandle** 다음 섹션에 설명 된 대로 환경, 연결, 문 및 설명자에 대 한 핸들을 해제 하는 데 사용 됩니다. 핸들에 대 한 일반적인 정보를 참조 하세요 [핸들](../../../odbc/reference/develop-app/handles.md)합니다.  
  
 응용 프로그램 해제 된; 후 핸들을 사용 하지 않아야 드라이버 관리자는 함수 호출에 대 한 핸들의 유효성을 검사 하지 않습니다.  
  
## <a name="freeing-an-environment-handle"></a>환경 핸들을 해제합니다.  
 호출 하기 전에 **SQLFreeHandle** 사용 하 여를 *HandleType* SQL_HANDLE_ENV의 응용 프로그램에서 호출 해야 **SQLFreeHandle** 사용 하 여를 *HandleType*환경에서 할당 된 모든 연결에 대해 SQL_HANDLE_DBC입니다. 이 고, 그렇지 호출 **SQLFreeHandle** SQL_ERROR 환경 및 모든 활성 연결이 유효 반환 합니다. 자세한 내용은 [환경 처리](../../../odbc/reference/develop-app/environment-handles.md) 하 고 [환경 핸들 할당](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)합니다.  
  
 환경에서는 공유 환경 인 경우 응용 프로그램 호출 하는 **SQLFreeHandle** 사용 하 여를 *HandleType* SQL_HANDLE_ENV의 호출 후 환경이 하지만 환경에 대 한 액세스를 더 이상 반드시 리소스가 해제 되지 않습니다. 에 대 한 호출 **SQLFreeHandle** 환경의 참조 횟수를 줄입니다. 참조 횟수에는 드라이버 관리자에 의해 유지 관리 됩니다. 0에 도달 하지 않는 경우 공유 환경은 하지도 다른 구성 요소에서 사용 중 이므로 해제 됩니다. 참조 횟수가 0에 도달 하면 공유 환경의 리소스를 해제 됩니다.  
  
## <a name="freeing-a-connection-handle"></a>연결 핸들 해제  
 호출 하기 전에 **SQLFreeHandle** 사용 하 여를 *HandleType* SQL_HANDLE_DBC의 응용 프로그램에서 호출 해야 **SQLDisconnect** 이 연결 되어 있는 경우 연결에 대 한 처리*합니다.* 이 고, 그렇지 호출 **SQLFreeHandle** 연결과 SQL_ERROR를 유효한 상태로 유지를 반환 합니다.  
  
 자세한 내용은 참조 하세요. [연결 핸들](../../../odbc/reference/develop-app/connection-handles.md) 하 고 [데이터 원본 또는 드라이버에서 연결 끊기](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)합니다.  
  
## <a name="freeing-a-statement-handle"></a>문 핸들 해제  
 에 대 한 호출 **SQLFreeHandle** 사용 하 여를 *HandleType* 호출 하 여의를 호출 하 여 할당 된 모든 리소스를 해제 **SQLAllocHandle** 사용 하 여는  *HandleType* 호출입니다. 응용 프로그램을 호출할 때 **SQLFreeHandle** 보류 중인 결과가 있는 문을 확보 하기 위해 보류 중인 결과가 삭제 됩니다. 문 핸들을 해제 하는 응용 프로그램, 드라이버는 핸들과 연결 된 4 개의 자동으로 할당 된 설명자를 해제 합니다. 자세한 내용은 [문은 처리](../../../odbc/reference/develop-app/statement-handles.md) 하 고 [문 핸들 해제](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md).  
  
 있음을 **SQLDisconnect** 연결에서 모든 문 및 설명자 열기를 자동으로 삭제 합니다.  
  
## <a name="freeing-a-descriptor-handle"></a>설명자 핸들 해제  
 에 대 한 호출 **SQLFreeHandle** 사용 하 여를 *HandleType* SQL_HANDLE_DESC의에 있는 설명자 핸들을 해제 *처리*합니다. 에 대 한 호출 **SQLFreeHandle** 의 포인터 필드 (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, 및 SQL_DESC_OCTET_LENGTH_PTR 포함)에서 참조 될 수 있는 응용 프로그램에서 할당 된 메모리를 해제 하지 않습니다 설명자 레코드 *처리*합니다. 포인터 필드 되지 않는 필드에 대 한 드라이버에 의해 할당 된 메모리는 핸들이 해제 될 때 해제 됩니다. 사용자 할당 된 설명자 핸들을 해제 되 면 모든 문 핸들을 해제 했습니다 연결 된 해당 해당 자동으로 할당 된 설명자 핸들 되돌아갑니다.  
  
> [!NOTE]
>  ODBC 2 *.x* 설명자 핸들 할당을 지원 하지 않는 것 처럼 드라이버 해제 설명자 핸들을 지원 하지 않습니다.  
  
 있음을 **SQLDisconnect** 연결에서 모든 문 및 설명자 열기를 자동으로 삭제 합니다. 문 핸들을 해제 하는 응용 프로그램, 드라이버는 핸들과 연결 된 모든 자동으로 생성 된 설명자를 해제 합니다.  
  
 설명자에 대 한 자세한 내용은 참조 하세요. [설명자](../../../odbc/reference/develop-app/descriptors.md)합니다.  
  
## <a name="code-example"></a>코드 예  
 추가 코드 샘플을 보려면 [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) 하 고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)합니다.  
  
### <a name="code"></a>코드  
  
```  
// SQLFreeHandle.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include <stdio.h>  
  
int main() {  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
  
   // Initialize the environment, connection, statement handles.  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   // Allocate the environment.  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set environment attributes.  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
  
   // Allocate the connection.  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
   // Set the login timeout.  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
  
   // Let the user select the data source and connect to the database.  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Free handles, and disconnect.     
   if (hstmt) {   
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
      hstmt = NULL;   
   }  
   if (hdbc) {   
      SQLDisconnect(hdbc);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
      hdbc = NULL;   
   }  
   if (henv) {   
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
      henv = NULL;   
   }  
}  
```  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|문 처리를 취소합니다.|[SQLCance Functionl](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|커서 이름을 설정합니다.|[SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)
