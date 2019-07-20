---
title: SQLFreeHandle 함수 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeHandle
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFreeHandle
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
ms.assetid: 17a6fcdc-b05a-4de7-be93-a316f39696a1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e312bcbc6efcb96ff02657b98034f0340ae377dc
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345178"
---
# <a name="sqlfreehandle-function"></a>SQLFreeHandle 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **Sqlfreehandle** 은 특정 환경, 연결, 문 또는 설명자 핸들과 연결 된 리소스를 해제 합니다.  
  
> [!NOTE]
>  이 함수는 핸들을 해제 하기 위한 제네릭 함수입니다. 이 2.0는 **SQLFreeConnect** (연결 핸들을 해제 하기 위해) 및 **sqlfreeenv** (환경 핸들 해제)를 대체 합니다. **SQLFreeConnect** 및 **sqlfreeenv** 는 모두 ODBC 3.x에서 더  이상 사용 되지 않습니다. 또한 **Sqlfreehandle** 은 문 핸들을 해제 하기 위해 ODBC 2.0 함수 **SQLFreeStmt** (SQL_DROP *옵션*포함)를 대체 합니다. 자세한 내용은 "설명"을 참조 하십시오. ODBC*2.x 응용 프로그램이* odbc*2.x 드라이버를* 사용할 때 드라이버 관리자가이 기능을에 매핑하는 방법에 대 한 자세한 내용은 [응용 프로그램의 이전 버전과의 호환성을 위한 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)을 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 입력 **Sqlfreehandle**에서 해제할 핸들의 형식입니다. 다음 값 중 하나 여야 합니다.  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN 핸들은 드라이버 관리자 및 드라이버 에서만 사용 됩니다. 응용 프로그램은이 핸들 형식을 사용 하면 안 됩니다. SQL_HANDLE_DBC_INFO_TOKEN에 대 한 자세한 내용은 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)을 참조 하세요.  
  
 *HandleType* 가 이러한 값 중 하나가 아닌 경우 **SQLFREEHANDLE** 은 SQL_INVALID_HANDLE를 반환 합니다.  
  
 *Handle*  
 입력 해제할 핸들입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
 **Sqlfreehandle** 이 SQL_ERROR를 반환 하는 경우 핸들이 여전히 유효 합니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlfreehandle** 이 SQL_ERROR를 반환 하는 경우 **sqlfreehandle** 에서 free를 시도한 핸들의 진단 데이터 구조에서 연결 된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 일반적으로 **Sqlfreehandle** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR입니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec에** 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.  *\**|  
|HY001|메모리 할당 오류|드라이버가 실행 또는 함수의 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) *HandleType* 인수는 SQL_HANDLE_ENV이 고 하나 이상의 연결이 할당 되거나 연결 된 상태입니다. *HANDLETYPE* SQL_HANDLE_ENV를 사용 하 여 **sqlfreehandle** 을 호출 하기 전에 각 연결에 대해 **Sqldisconnect** 및 **sqlfreehandle** 을 호출 해야 합니다. *HandleType* SQL_HANDLE_DBC.<br /><br /> (DM) *HandleType* 인수는 SQL_HANDLE_DBC이 고, 연결에 대해 **sqldisconnect** 를 호출 하기 전에 함수가 호출 되었습니다.<br /><br /> (DM) *HandleType* 인수는 SQL_HANDLE_DBC입니다. 이 함수가 호출 될 때 *핸들* 을 사용 하 여 비동기적으로 실행 되는 함수가 호출 되었으며 함수가 여전히 실행 되 고 있습니다.<br /><br /> (DM) *HandleType* 인수는 SQL_HANDLE_STMT입니다. 문 핸들을 사용 하 여 **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 를 호출 하 고 SQL_NEED_DATA를 반환 했습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.<br /><br /> (DM) *HandleType* 인수는 SQL_HANDLE_STMT입니다. 비동기 방식으로 실행 되는 함수가 문 핸들 또는 연결 된 연결 핸들에서 호출 되 고 함수가 호출 될 때 함수가 여전히 실행 되 고 있습니다.<br /><br /> (DM) *HandleType* 인수는 SQL_HANDLE_DESC입니다. 연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. 이 함수가 호출 될 때 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlfreehandle** 을 호출 하기 전에 모든 자회사 핸들 및 기타 리소스가 해제 되지 않았습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *핸들과* 연결 된 문 핸들 중 하나에 대해 호출 되었으며 *HandleType* 가 SQL_HANDLE_STMT 또는 SQL_HANDLE_DESC 반환 SQL_PARAM_DATA_로 설정 되었습니다. 있게. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|*HandleType* 인수는 SQL_HANDLE_STMT 또는 SQL_HANDLE_DESC이 고, 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다. 메모리가 부족 하기 때문일 수 있습니다.|  
|HY017|자동으로 할당 된 설명자 핸들 사용이 잘못 되었습니다.|(DM) *핸들* 인수가 자동으로 할당 된 설명자에 대 한 핸들로 설정 되었습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *HandleType* 인수는 SQL_HANDLE_DESC이 고 드라이버는 ODBC*2.x 드라이버 였습니다* .<br /><br /> (DM) *HandleType* 인수가 SQL_HANDLE_STMT이 고 드라이버가 올바른 ODBC 드라이버가 아닙니다.|  
  
## <a name="comments"></a>주석  
 **Sqlfreehandle** 은 다음 섹션에 설명 된 대로 환경, 연결, 문 및 설명자에 대 한 핸들을 해제 하는 데 사용 됩니다. 핸들에 대 한 일반적인 내용은 [핸들](../../../odbc/reference/develop-app/handles.md)을 참조 하십시오.  
  
 응용 프로그램은 해제 된 후에 핸들을 사용 하면 안 됩니다. 드라이버 관리자는 함수 호출에서 핸들의 유효성을 검사 하지 않습니다.  
  
## <a name="freeing-an-environment-handle"></a>환경 핸들 해제  
 SQL_HANDLE_ENV의 *HandleType* 를 사용 하 여 **sqlfreehandle** 을 호출 하기 전에 응용 프로그램은 환경에서 할당 된 모든 연결에 대해 *HandleType* SQL_HANDLE_DBC를 사용 하 여 **sqlfreehandle** 을 호출 해야 합니다. 그렇지 않으면 **Sqlfreehandle** 을 호출 하면 SQL_ERROR이 반환 되 고 환경이 활성 상태로 유지 됩니다. 자세한 내용은 [환경](../../../odbc/reference/develop-app/environment-handles.md) 핸들 및 [환경 핸들 할당](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)을 참조 하세요.  
  
 환경이 공유 환경인 경우 SQL_HANDLE_ENV의 *HandleType* 를 사용 하 여 **sqlfreehandle** 을 호출 하는 응용 프로그램은 더 이상 호출 후 환경에 액세스할 수 없지만 환경의 리소스는 반드시 해제 되는 것은 아닙니다. **Sqlfreehandle** 에 대 한 호출은 환경의 참조 횟수를 감소 시킵니다. 참조 횟수는 드라이버 관리자에 의해 유지 관리 됩니다. 이 값이 0에 도달 하지 않으면 공유 환경은 다른 구성 요소에서 사용 되 고 있기 때문에 해제 되지 않습니다. 참조 횟수가 0에 도달 하면 공유 환경의 리소스가 해제 됩니다.  
  
## <a name="freeing-a-connection-handle"></a>연결 핸들 해제  
 SQL_HANDLE_DBC의 *HandleType* 를 사용 하 여 **sqlfreehandle** 을 호출 하기 전에 응용 프로그램은이 핸들에 대 한 연결이 있는 경우 연결에 대해 **sqldisconnect** 를 호출 해야 합니다 *.* 그렇지 않으면 **Sqlfreehandle** 을 호출 하면 SQL_ERROR가 반환 되 고 연결이 유효한 상태로 유지 됩니다.  
  
 자세한 내용은 [연결 핸들](../../../odbc/reference/develop-app/connection-handles.md) 및 [데이터 원본 또는 드라이버에서 연결 끊기](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)를 참조 하세요.  
  
## <a name="freeing-a-statement-handle"></a>문 핸들 해제  
 *HANDLETYPE* SQL_HANDLE_STMT를 사용 하 여 **sqlfreehandle** 을 호출 하면 *HandleType* SQL_HANDLE_STMT를 사용 하 여 **SQLAllocHandle** 에 대 한 호출에 의해 할당 된 모든 리소스가 해제 됩니다. 응용 프로그램에서 **Sqlfreehandle** 을 호출 하 여 보류 중인 결과가 포함 된 문을 해제할 때 보류 중인 결과가 삭제 됩니다. 응용 프로그램에서 문 핸들을 해제 하면 드라이버는 해당 핸들과 연결 된 4 개의 자동 할당 설명자를 해제 합니다. 자세한 내용은 문 [핸들 및](../../../odbc/reference/develop-app/statement-handles.md) [문 핸들 해제](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)를 참조 하세요.  
  
 **Sqldisconnect** 는 연결에서 열려 있는 문과 설명자를 자동으로 삭제 합니다.  
  
## <a name="freeing-a-descriptor-handle"></a>설명자 핸들 해제  
 *HandleType* 가 SQL_HANDLE_DESC 인 **sqlfreehandle** 을 호출 하면 *핸들*에서 설명자 핸들이 해제 됩니다. **Sqlfreehandle** 을 호출 하면 응용 프로그램에서 할당 한 모든 메모리를 해제 하지 않습니다 .이는의 *모든 설명자 레코드에 대 한 포인터 필드 (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 포함)에서 참조 될 수 있는 메모리를 해제 하지 않습니다. 핸들*. 포인터 필드가 아닌 필드에 대해 드라이버가 할당 한 메모리는 핸들을 해제할 때 해제 됩니다. 사용자 할당 설명자 핸들을 해제 하면 해제 된 핸들이 연결 된 모든 문이 자동으로 할당 된 해당 설명자 핸들로 돌아갑니다.  
  
> [!NOTE]
>  ODBC 2.x*드라이버는* 설명자 핸들 할당을 지원 하지 않으므로 설명자 핸들을 해제 하는 것을 지원 하지 않습니다.  
  
 **Sqldisconnect** 는 연결에서 열려 있는 문과 설명자를 자동으로 삭제 합니다. 응용 프로그램에서 문 핸들을 해제 하면 드라이버는 해당 핸들과 연결 된 자동으로 생성 된 모든 설명자를 해제 합니다.  
  
 설명자에 대 한 자세한 내용은 [설명자](../../../odbc/reference/develop-app/descriptors.md)를 참조 하십시오.  
  
## <a name="code-example"></a>코드 예  
 추가 코드 샘플은 [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) 및 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)를 참조 하세요.  
  
### <a name="code"></a>코드  
  
```cpp  
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
|문 처리 취소|[SQLCance Functionl](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|커서 이름 설정|[SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)
