---
title: SQLFreeHandle 기능 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0b136dec98a19676aa67c78615d8fe931f62aafa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285774"
---
# <a name="sqlfreehandle-function"></a>SQLFreeHandle 함수
**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLFreeHandle** 특정 환경, 연결, 문 또는 설명자 핸들과 관련 된 리소스를 해제 합니다.  
  
> [!NOTE]
>  이 함수는 핸들을 해제하기 위한 일반 함수입니다. ODBC 2.0 함수 인 **SQLFreeConnect** (연결 핸들 해제) 및 **SQLFreeEnv** (환경 핸들 해제)를 대체합니다. **SQLFreeConnect** 및 **SQLFreeEnv는** 모두 ODBC 3 *.x .* **또한 SQLFreeHandle은** ODBC 2.0 함수 **SQLFreeStmt(SQL_DROP** *옵션*포함)를 대체하여 문 핸들을 해제합니다. 자세한 내용은 '댓글'을 참조하세요. ODBC 3 *.x* 응용 프로그램이 ODBC 2 *.x* 드라이버로 작업할 때 드라이버 관리자가 이 함수를 매핑하는 작업에 대한 자세한 내용은 [응용 프로그램의 이전 버전과의 호환성에 대한 매핑 교체 함수를](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 [입력] **SQLFreeHandle에서**해제할 핸들 유형입니다. 다음 값 중 하나여야 합니다.  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN 핸들은 드라이버 관리자와 드라이버에서만 사용됩니다. 응용 프로그램에서는 이 핸들 형식을 사용해서는 안 됩니다. SQL_HANDLE_DBC_INFO_TOKEN 대한 자세한 내용은 [ODBC 드라이버에서 연결-풀 인식 개발을](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)참조하십시오.  
  
 *핸들 Type이* 이러한 값 중 하나가 아닌 경우 **SQLFreeHandle은** SQL_INVALID_HANDLE 반환합니다.  
  
 *Handle*  
 [입력] 해제할 핸들입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
 **SQLFreeHandle** SQL_ERROR 반환하는 경우 핸들은 여전히 유효합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLFreeHandle** SQL_ERROR 반환 하는 경우 **SQLFreeHandle** 해제 하려고 하지만 할 수 없는 핸들에 대 한 진단 데이터 구조에서 관련 된 SQLSTATE 값을 가져올 수 있습니다. 다음 표에서는 일반적으로 **SQLFreeHandle에서** 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|(DM) *HandleType* 인수가 SQL_HANDLE_ENV 하나 이상의 연결이 할당또는 연결된 상태에 있었습니다. **SQLDisconnect** *핸들 유형* SQL_HANDLE_DBC **SQLFreeHandle을** SQL_HANDLE_ENV *핸들 유형으로* **SQLFreeHandle을** 호출하기 전에 각 연결에 대해 호출해야 합니다.<br /><br /> (DM) *핸들타이* 인수가 SQL_HANDLE_DBC 연결에 대해 **SQLDisconnect를** 호출하기 전에 함수가 호출되었습니다.<br /><br /> (DM) *핸들 타이* 인수가 SQL_HANDLE_DBC. *핸들을* 사용 하 여 비동기적으로 실행 하는 함수를 호출 하 고 이 함수를 호출 할 때 함수는 여전히 실행 되 고 있었습니다.<br /><br /> (DM) *핸들타이* 인수가 SQL_HANDLE_STMT. **SQLExecDirect**, **SQLBulkOperations**또는 **SQLSetPos는** 명령문 핸들을 호출하고 SQL_NEED_DATA 반환했습니다. **SQLExecDirect** 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.<br /><br /> (DM) *핸들타이* 인수가 SQL_HANDLE_STMT. 문 핸들 또는 연결된 연결 핸들에서 비동기적으로 실행 되는 함수가 호출 되었으며 이 함수가 호출 될 때 함수가 계속 실행 되었습니다.<br /><br /> (DM) *핸들 타이* 인수가 SQL_HANDLE_DESC. 연결된 연결 핸들에서 비동기적으로 실행되는 함수가 호출되었습니다. 이 함수가 호출될 때 함수가 계속 실행되고 있었습니다.<br /><br /> (DM) **SQLFreeHandle이** 호출되기 전에 모든 보조 핸들 및 기타 리소스가 해제되지 않았습니다.<br /><br /> (DM) **SQLExecDirect**또는 **SQLMoreResults핸들** 및 *핸들유형과* 연관된 명령문 핸들 중 하나를 호출하여 *SQL_HANDLE_STMT* 반환된 SQL_PARAM_DATA_AVAILABLE SQL_HANDLE_DESC. **SQLExecute** 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|*HandleType* 인수가 SQL_HANDLE_STMT SQL_HANDLE_DESC 메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY017|자동으로 할당된 설명자 핸들을 잘못 사용합니다.|(DM) *핸들* 인수가 자동으로 할당된 설명자의 핸들로 설정되었습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *핸들타이* 인수가 SQL_HANDLE_DESC 드라이버가 ODBC*2.x* 드라이버였습니다.<br /><br /> (DM) *핸들타이* 인수가 SQL_HANDLE_STMT 드라이버가 유효한 ODBC 드라이버가 아닙니다.|  
  
## <a name="comments"></a>주석  
 **SQLFreeHandle은** 다음 섹션에 설명된 대로 환경, 연결, 명령문 및 설명자에 대한 핸들을 해제하는 데 사용됩니다. 핸들에 대한 일반적인 정보는 [핸들 을](../../../odbc/reference/develop-app/handles.md)참조하십시오.  
  
 응용 프로그램이 해제된 후에는 핸들을 사용해서는 안 됩니다. 드라이버 관리자는 함수 호출에서 핸들의 유효성을 확인하지 않습니다.  
  
## <a name="freeing-an-environment-handle"></a>환경 핸들 해제  
 *SQL_HANDLE_ENV 핸들 타입을* 사용 하 여 **SQLFreeHandle를** 호출 하기 전에 응용 프로그램은 환경에서 할당 된 모든 연결에 대 한 *SQL_HANDLE_DBC 핸들 유형으로* **SQLFreeHandle을** 호출 해야 합니다. 그렇지 않으면 **SQLFreeHandle에** 대 한 호출 SQL_ERROR 반환 하 고 환경 및 활성 연결 유효 하 게 유지 합니다. 자세한 내용은 [환경 핸들](../../../odbc/reference/develop-app/environment-handles.md) 및 환경 [핸들 할당을](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)참조하십시오.  
  
 환경이 공유 환경인 경우 *핸들유형* SQL_HANDLE_ENV **SQLFreeHandle을** 호출하는 응용 프로그램은 호출 후 환경에 더 이상 액세스할 수 없지만 환경의 리소스가 반드시 해제되지는 않습니다. **SQLFreeHandle에** 대 한 호출 환경의 참조 수를 감소 합니다. 참조 수는 드라이버 관리자에 의해 유지됩니다. 0에 도달하지 않으면 다른 구성 요소에서 여전히 사용 중이므로 공유 환경이 해제되지 않습니다. 참조 수가 0에 도달하면 공유 환경의 리소스가 해제됩니다.  
  
## <a name="freeing-a-connection-handle"></a>연결 핸들 해제  
 *SQL_HANDLE_DBC 핸들 타입을* 사용 하 여 **SQLFreeHandle를** 호출 하기 전에 응용 프로그램은 이 핸들에 연결 이 면 연결에 대 한 **SQLDisconnect를** 호출 해야*합니다.* 그렇지 않으면 **SQLFreeHandle** 에 대 한 호출 SQL_ERROR 반환 하 고 연결 유효 한 상태로 유지 됩니다.  
  
 자세한 내용은 [연결 핸들 및](../../../odbc/reference/develop-app/connection-handles.md) 데이터 원본 또는 [드라이버의 연결을](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)참조하십시오.  
  
## <a name="freeing-a-statement-handle"></a>문 핸들 해제  
 *핸들 유형* SQL_HANDLE_STMT **SQLFreeHandle을** 호출하면 *핸들 유형* SQL_HANDLE_STMT **SQLAllocHandle** 호출에 의해 할당된 모든 리소스를 해제합니다. 응용 프로그램에서 **SQLFreeHandle을** 호출하여 보류 중인 결과가 있는 문을 해제하면 보류 중인 결과가 삭제됩니다. 응용 프로그램이 명령문 핸들을 해제하면 드라이버는 해당 핸들과 연결된 4개의 자동으로 할당된 설명자가 해제됩니다. 자세한 내용은 [명령문 핸들](../../../odbc/reference/develop-app/statement-handles.md) 및 [명령문 핸들 해제를](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)참조하십시오.  
  
 **SQLDisconnect는** 연결에서 열려 있는 모든 명령문 및 설명자가 자동으로 삭제됩니다.  
  
## <a name="freeing-a-descriptor-handle"></a>설명자 핸들 해제  
 *핸들 SQL_HANDLE_DESC* 핸들 을 사용하여 **SQLFreeHandle을** 호출하려면 *핸들에서*설명자 핸들을 해제합니다. **SQLFreeHandle에** 대 한 호출 *은 핸들의*설명자 레코드의 포인터 필드 (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 포함 하 여) 참조 될 수 있는 응용 프로그램에 의해 할당 된 메모리를 해제 하지 않습니다. 포인터 필드가 아닌 필드에 대해 드라이버에서 할당한 메모리는 핸들이 해제될 때 해제됩니다. 사용자 할당된 설명자 핸들이 해제되면 해제된 핸들이 자동으로 할당된 각 설명자 핸들로 되돌려 연결되던 모든 명령문이 해제됩니다.  
  
> [!NOTE]
>  ODBC 2 *.x* 드라이버는 설명자 할당 핸들을 지원하지 않는 것처럼 해제 설명자 핸들을 지원하지 않습니다.  
  
 **SQLDisconnect는** 연결에서 열려 있는 모든 명령문 및 설명자가 자동으로 삭제됩니다. 응용 프로그램이 명령문 핸들을 해제하면 드라이버는 해당 핸들과 연결된 자동으로 생성된 모든 설명자가 해제됩니다.  
  
 설명자에 대한 자세한 내용은 [설명자](../../../odbc/reference/develop-app/descriptors.md)를 참조하십시오.  
  
## <a name="code-example"></a>코드 예  
 추가 코드 샘플은 [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) 및 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)를 참조하십시오.  
  
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
  
|원하는 정보|참조|  
|---------------------------|---------|  
|핸들 할당|[SQLAllocHandle 함수](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|명령문 처리 취소|[SQLCance 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|커서 이름 설정|[SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)
