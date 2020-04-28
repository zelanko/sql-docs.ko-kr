---
title: 비동기 실행 (알림 방법) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e509dad9-5263-4a10-9a4e-03b84b66b6b3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 250e71dcb47d44a6e437d12c269ea23fa6fb3c2c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306414"
---
# <a name="asynchronous-execution-notification-method"></a>비동기 실행(알림 방법)
ODBC에서는 연결 및 문 작업을 비동기적으로 실행할 수 있습니다. 응용 프로그램 스레드는 비동기 모드에서 ODBC 함수를 호출할 수 있으며,이 함수는 작업이 완료 되기 전에 반환할 수 있으므로 응용 프로그램 스레드에서 다른 작업을 수행할 수 있습니다. Windows 7 SDK에서 비동기 문 또는 연결 작업의 경우 응용 프로그램은 폴링 메서드를 사용 하 여 비동기 작업이 완료 되었음을 확인 합니다. 자세한 내용은 [비동기 실행 (폴링 방법)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)을 참조 하세요. Windows 8 SDK부터 알림 방법을 사용 하 여 비동기 작업이 완료 되었는지 확인할 수 있습니다.  
  
 폴링 메서드에서 응용 프로그램은 작업 상태를 원할 때마다 비동기 함수를 호출 해야 합니다. 알림 방법은 콜백과 ADO.NET의 대기와 비슷합니다. 그러나 ODBC는 알림 개체로 Win32 이벤트를 사용 합니다.  
  
 ODBC 커서 라이브러리와 ODBC 비동기 알림은 동시에 사용할 수 없습니다. 두 특성을 모두 설정 하면 SQLSTATE S1119와 함께 오류가 반환 됩니다 (커서 라이브러리와 비동기 알림은 동시에 사용 하도록 설정할 수 없음).  
  
 드라이버 개발자에 대 한 자세한 내용은 [비동기 함수 완료 알림](../../../odbc/reference/develop-driver/notification-of-asynchronous-function-completion.md) 을 참조 하세요.  
  
> [!NOTE]  
>  알림 방법은 커서 라이브러리에서 지원 되지 않습니다. 알림 방법이 사용 하도록 설정 된 경우 응용 프로그램에서 SQLSetConnectAttr을 통해 커서 라이브러리를 사용 하도록 설정 하려고 하면 오류 메시지가 표시 됩니다.  
  
## <a name="overview"></a>개요  
 비동기 모드에서 ODBC 함수를 호출 하면 반환 코드를 사용 하 여 컨트롤이 호출 응용 프로그램에 즉시 반환 됩니다 SQL_STILL_EXECUTING. 응용 프로그램은 SQL_STILL_EXECUTING 이외의 값을 반환할 때까지 함수를 반복적으로 폴링해야 합니다. 폴링 루프를 사용 하면 CPU 사용률이 높아지므로 많은 비동기 시나리오에서 성능이 저하 됩니다.  
  
 알림 모델을 사용할 때마다 폴링 모델을 사용할 수 없습니다. 응용 프로그램에서 원래 함수를 다시 호출 해서는 안 됩니다. [SQLCompleteAsync 함수](../../../odbc/reference/syntax/sqlcompleteasync-function.md) 를 호출 하 여 비동기 작업을 완료 합니다. 비동기 작업이 완료 되기 전에 응용 프로그램에서 원래 함수를 다시 호출 하는 경우에는 호출에서 SQLSTATE IM017를 사용 하 여 SQL_ERROR을 반환 합니다 (폴링은 비동기 알림 모드에서 사용 하지 않도록 설정 됨).  
  
 알림 모델을 사용 하는 경우 응용 프로그램은 **sqlcancel** 또는 **sqlcancelhandle** 을 호출 하 여 문이나 연결 작업을 취소할 수 있습니다. 취소 요청이 성공 하면 ODBC는 SQL_SUCCESS을 반환 합니다. 이 메시지는 함수가 실제로 취소 되었음을 나타내는 것은 아닙니다. 이는 취소 요청이 처리 되었음을 나타냅니다. 함수가 실제로 취소 되었는지 여부는 드라이버 종속 및 데이터 소스에 따라 다릅니다. 작업이 취소 되 면 드라이버 관리자는 이벤트에 신호를 보낼 수 있습니다. 드라이버 관리자는 반환 코드 버퍼에 SQL_ERROR을 반환 하 고 상태는 SQLSTATE HY008 (작업 취소 됨)로, 취소에 성공 했음을 표시 합니다. 함수가 정상적인 처리를 완료 한 경우 드라이버 관리자는 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO을 반환 합니다.  
  
### <a name="downlevel-behavior"></a>하위 동작  
 전체에서이 알림을 지 원하는 ODBC 드라이버 관리자 버전은 ODBC 3.81입니다.  
  
|응용 프로그램 ODBC 버전|드라이버 관리자 버전|드라이버 버전|동작|  
|------------------------------|----------------------------|--------------------|--------------|  
|ODBC 버전의 새 응용 프로그램|ODBC 3.81|ODBC 3.80 드라이버|드라이버가이 기능을 지 원하는 경우 응용 프로그램에서이 기능을 사용할 수 있습니다. 그렇지 않으면 드라이버 관리자에서 오류를 발생 합니다.|  
|ODBC 버전의 새 응용 프로그램|ODBC 3.81|ODBC 3.80 이전 드라이버|드라이버에서이 기능을 지원 하지 않는 경우 드라이버 관리자에서 오류가 발생 합니다.|  
|ODBC 버전의 새 응용 프로그램|ODBC 이전 3.81|모두|응용 프로그램에서이 기능을 사용 하는 경우 이전 드라이버 관리자는 새 특성을 드라이버별 특성으로 간주 하 고 드라이버에서 오류가 발생 해야 합니다. 새 드라이버 관리자는 이러한 특성을 드라이버에 전달 하지 않습니다.|  
  
 응용 프로그램은이 기능을 사용 하기 전에 드라이버 관리자 버전을 확인 해야 합니다. 그렇지 않으면 잘못 작성 된 드라이버에서 오류가 발생 하지 않고 드라이버 관리자 버전이 ODBC 3.81 이전 버전인 경우 동작이 정의 되지 않습니다.  
  
## <a name="use-cases"></a>사용 사례  
 이 섹션에서는 비동기 실행 및 폴링 메커니즘의 사용 사례를 보여 줍니다.  
  
### <a name="integrate-data-from-multiple-odbc-sources"></a>여러 ODBC 원본의 데이터 통합  
 데이터 통합 응용 프로그램은 여러 데이터 원본에서 데이터를 비동기적으로 인출 합니다. 일부 데이터는 원격 데이터 원본에서 가져온 것 이며 일부 데이터는 로컬 파일에서 가져온 것입니다. 비동기 작업이 완료 될 때까지 응용 프로그램을 계속할 수 없습니다.  
  
 작업이 완료 되었는지 확인 하기 위해 작업을 반복적으로 폴링하는 대신 응용 프로그램은 이벤트 개체를 만들어 ODBC 연결 핸들이 나 ODBC 문 핸들에 연결할 수 있습니다. 그런 다음 응용 프로그램은 운영 체제 동기화 Api를 호출 하 여 하나의 이벤트 개체나 여러 이벤트 개체 (ODBC 이벤트와 기타 Windows 이벤트)를 대기 합니다. ODBC는 해당 ODBC 비동기 작업이 완료 되 면 이벤트 개체에 신호를 보낼 수 있습니다.  
  
 Windows에서는 Win32 이벤트 개체가 사용 되며 사용자에 게 통합 프로그래밍 모델을 제공 합니다. 다른 플랫폼의 드라이버 관리자는 해당 플랫폼과 관련 된 이벤트 개체 구현을 사용할 수 있습니다.  
  
 다음 코드 샘플에서는 연결 및 문 비동기 알림을 사용 하는 방법을 보여 줍니다.  
  
```  
// This function opens NUMBER_OPERATIONS connections and executes one query on statement of each connection.  
// Asynchronous Notification is used  
  
#define NUMBER_OPERATIONS 5  
int AsyncNotificationSample(void)  
{  
    RETCODE     rc;  
  
    SQLHENV     hEnv              = NULL;  
    SQLHDBC     arhDbc[NUMBER_OPERATIONS]         = {NULL};  
    SQLHSTMT    arhStmt[NUMBER_OPERATIONS]        = {NULL};  
  
    HANDLE      arhDBCEvent[NUMBER_OPERATIONS]    = {NULL};  
    RETCODE     arrcDBC[NUMBER_OPERATIONS]        = {0};  
    HANDLE      arhSTMTEvent[NUMBER_OPERATIONS]   = {NULL};  
    RETCODE     arrcSTMT[NUMBER_OPERATIONS]       = {0};  
  
    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &hEnv);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    rc = SQLSetEnvAttr(hEnv,  
        SQL_ATTR_ODBC_VERSION,  
        (SQLPOINTER) SQL_OV_ODBC3_80,  
        SQL_IS_INTEGER);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    // Connection operations begin here  
  
    // Alloc NUMBER_OPERATIONS connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_DBC, hEnv, &arhDbc[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable DBC Async on all connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE, (SQLPOINTER)SQL_ASYNC_DBC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Application must create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhDBCEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhDBCEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all connection handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_EVENT, arhDBCEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate connect establishing  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLDriverConnect(arhDbc[i], NULL, (SQLTCHAR*)TEXT("Driver={ODBC Driver 11 for SQL Server};SERVER=dp-srv-sql2k;DATABASE=pubs;UID=sa;PWD=XYZ;"), SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE); // Wait All  
  
    // Complete connect API calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], & arrcDBC[i]);  
    }  
  
    BOOL fFail = FALSE; // Whether some connection openning fails.  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcDBC[i]) )   
            fFail = TRUE;  
    }  
  
    // If some SQLDriverConnect() fail, clean up.  
    if (fFail)  
    {  
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {  
                SQLDisconnect(arhDbc[i]); // This is also async  
            }  
            else  
            {  
                SetEvent(arhDBCEvent[i]); // Previous SQLDriverConnect() failed. No need to call SQLDisconnect().  
            }  
        }  
        WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE);   
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {     
                SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], &arrcDBC[i]);; // To Complete  
            }  
        }  
  
        goto Cleanup;  
    }  
  
    // Statement Operations begin here  
  
    // Alloc statement handle  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_STMT, arhDbc[i], &arhStmt[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable STMT Async on all statement handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_ENABLE, (SQLPOINTER)SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhSTMTEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhSTMTEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all statement handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_STMT_EVENT, arhSTMTEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate SQLExecDirect() calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLExecDirect(arhStmt[i], (SQLTCHAR*)TEXT("select au_lname, au_fname from authors"), SQL_NTS);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE); // Wait All  
  
    // Now, call SQLCompleteAsync to complete the operation and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return values  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        //Do some binding jobs here, set SQL_ATTR_ROW_ARRAY_SIZE   
    }  
  
    // Now, initiate fetching  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLFetch(arhStmt[i]);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE);   
  
    // Now, to complete the operations and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    // USE fetched data here!!  
  
Cleanup:  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhStmt[NUMBER_OPERATIONS])  
        {  
            SQLFreeHandle(SQL_HANDLE_STMT, arhStmt[i]);  
            arhStmt[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhSTMTEvent[i])  
        {  
            CloseHandle(arhSTMTEvent[i]);  
            arhSTMTEvent[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDbc[i])  
        {  
            SQLFreeHandle(SQL_HANDLE_DBC, arhDbc[i]);  
            arhDbc[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDBCEvent[i])  
        {  
            CloseHandle(arhDBCEvent[i]);  
            arhDBCEvent[i] = NULL;  
        }  
    }  
  
    if (hEnv)  
    {  
        SQLFreeHandle(SQL_HANDLE_ENV, hEnv);  
        hEnv = NULL;  
    }  
  
    return 0;  
}  
  
```  
  
### <a name="determining-if-a-driver-supports-asynchronous-notification"></a>드라이버가 비동기 알림을 지원 하는지 확인  
 ODBC 응용 프로그램은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)를 호출 하 여 odbc 드라이버가 비동기 알림을 지원 하는지 확인할 수 있습니다. 결과적으로 ODBC 드라이버 관리자는 SQL_ASYNC_NOTIFICATION를 사용 하 여 드라이버의 **SQLGetInfo** 를 호출 합니다.  
  
```  
SQLUINTEGER InfoValue;  
SQLLEN      cbInfoLength;  
  
SQLRETURN retcode;  
retcode = SQLGetInfo (hDbc,   
                      SQL_ASYNC_NOTIFICATION,   
                      &InfoValue,  
                      sizeof(InfoValue),  
                      NULL);  
if (SQL_SUCCEEDED(retcode))  
{  
if (SQL_ASYNC_NOTIFICATION_CAPABLE == InfoValue)  
      {  
          // The driver supports asynchronous notification  
      }  
      else if (SQL_ASYNC_NOTIFICATION_NOT_CAPABLE == InfoValue)  
      {  
          // The driver does not support asynchronous notification  
      }  
}  
```  
  
### <a name="associating-a-win32-event-handle-with-an-odbc-handle"></a>ODBC 핸들과 Win32 이벤트 핸들 연결  
 응용 프로그램은 해당 Win32 함수를 사용 하 여 Win32 이벤트 개체를 만듭니다. 응용 프로그램은 하나의 ODBC 연결 핸들이 나 하나의 ODBC 문 핸들을 사용 하 여 하나의 Win32 이벤트 핸들을 연결할 수 있습니다.  
  
 연결 특성 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE 및 SQL_ATTR_ASYNC_DBC_EVENT는 ODBC가 비동기 모드에서 실행 되는지 여부와 ODBC가 연결 핸들에 알림 모드를 사용 하도록 설정할지 여부를 결정 합니다. 문 특성 SQL_ATTR_ASYNC_ENABLE 및 SQL_ATTR_ASYNC_STMT_EVENT는 ODBC가 비동기 모드에서 실행 되는지 여부와 ODBC가 문 핸들에 알림 모드를 사용 하도록 설정할지 여부를 결정 합니다.  
  
|SQL_ATTR_ASYNC_ENABLE 또는 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE|SQL_ATTR_ASYNC_STMT_EVENT 또는 SQL_ATTR_ASYNC_DBC_EVENT|Mode|  
|-------------------------------------------------------------------------|-------------------------------------------------------------------|----------|  
|사용|null이 아닌|비동기 알림|  
|사용|null|비동기 폴링|  
|사용 안 함|any|동기|  
  
 응용 프로그램은 비동기 작업 모드를 일시적으로 비활성화할 수 있습니다. 연결 수준 비동기 작업을 사용할 수 없는 경우 ODBC는 SQL_ATTR_ASYNC_DBC_EVENT의 값을 무시 합니다. 문 수준 비동기 작업을 사용할 수 없는 경우 ODBC는 SQL_ATTR_ASYNC_STMT_EVENT의 값을 무시 합니다.  
  
 **SQLSetStmtAttr** 및 **SQLSetConnectAttr** 의 동기 호출  
 -   **SQLSetConnectAttr** 는 비동기 작업을 지원 하지만 SQL_ATTR_ASYNC_DBC_EVENT 설정 하는 **SQLSetConnectAttr** 의 호출은 항상 동기식입니다.  
  
-   **SQLSetStmtAttr** 는 비동기 실행을 지원 하지 않습니다.  
  
 오류 출력 시나리오  
 연결 하기 전에 **SQLSetConnectAttr** 를 호출 하면 드라이버 관리자가 사용할 드라이버를 결정할 수 없습니다. 따라서 드라이버 관리자는 **SQLSetConnectAttr** 에 대해 success를 반환 하지만 드라이버에서 특성을 설정할 준비가 되지 않았을 수 있습니다. 응용 프로그램에서 연결 함수를 호출할 때 드라이버 관리자는 이러한 특성을 설정 합니다. 드라이버가 비동기 작업을 지원 하지 않으므로 드라이버 관리자가 오류를 발생 시킬 수 있습니다.  
  
 연결 특성의 상속  
 일반적으로 연결의 문은 연결 특성을 상속 합니다. 그러나 SQL_ATTR_ASYNC_DBC_EVENT 특성은 상속 될 수 없으며 연결 작업에만 영향을 줍니다.  
  
 Odbc 연결 핸들과 이벤트 핸들을 연결 하기 위해 ODBC 응용 프로그램은 ODBC API **SQLSetConnectAttr** 를 호출 하 고 특성 및 이벤트 핸들을 특성 값으로 SQL_ATTR_ASYNC_DBC_EVENT 지정 합니다. 새 ODBC 특성 SQL_ATTR_ASYNC_DBC_EVENT SQL_IS_POINTER 유형입니다.  
  
```  
HANDLE hEvent;  
hEvent = CreateEvent(   
            NULL,                // default security attributes  
            FALSE,               // auto-reset event  
            FALSE,               // initial state is non-signaled  
            NULL                 // no name  
            );  
```  
  
 일반적으로 응용 프로그램은 자동 재설정 이벤트 개체를 만듭니다. ODBC는 이벤트 개체를 다시 설정 하지 않습니다. 응용 프로그램은 비동기 ODBC 함수를 호출 하기 전에 개체가 신호를 받은 상태가 아닌지 확인 해야 합니다.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetConnectAttr ( hDBC,  
                              SQL_ATTR_ASYNC_DBC_EVENT, // Attribute name  
                              (SQLPOINTER) hEvent,      // Win32 Event handle  
                              SQL_IS_POINTER);          // Length Indicator  
```  
  
 SQL_ATTR_ASYNC_DBC_EVENT은 드라이버에 설정 되지 않는 드라이버 관리자 전용 특성입니다.  
  
 SQL_ATTR_ASYNC_DBC_EVENT의 기본값은 NULL입니다. 드라이버가 비동기 알림을 지원 하지 않는 경우 SQL_ATTR_ASYNC_DBC_EVENT 가져오거나 설정 하면 SQLSTATE HY092 (잘못 된 특성/옵션 식별자)를 사용 하 여 SQL_ERROR 반환 됩니다.  
  
 ODBC 연결 핸들에 설정 된 마지막 SQL_ATTR_ASYNC_DBC_EVENT 값이 NULL이 아니고 응용 프로그램에서 SQL_ASYNC_DBC_ENABLE_ON 특성 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE를 설정 하 여 비동기 모드를 사용 하도록 설정한 경우 비동기 모드를 지 원하는 ODBC 연결 함수를 호출 하면 완료 알림이 표시 됩니다. ODBC 연결 핸들에 설정 된 마지막 SQL_ATTR_ASYNC_DBC_EVENT 값이 NULL 인 경우 ODBC는 비동기 모드의 설정 여부에 관계 없이 응용 프로그램을 보내지 않습니다.  
  
 응용 프로그램은 특성 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE 설정 하기 전이나 후에 SQL_ATTR_ASYNC_DBC_EVENT를 설정할 수 있습니다.  
  
 응용 프로그램은 연결 함수 (**SQLConnect**, **SQLBrowseConnect**또는 **SQLDriverConnect**)를 호출 하기 전에 ODBC 연결 핸들에 SQL_ATTR_ASYNC_DBC_EVENT 특성을 설정할 수 있습니다. ODBC 드라이버 관리자는 응용 프로그램이 사용 하는 ODBC 드라이버를 알지 못하기 때문에 SQL_SUCCESS를 반환 합니다. 응용 프로그램에서 연결 함수를 호출할 때 ODBC 드라이버 관리자는 드라이버가 비동기 알림을 지원 하는지 여부를 확인 합니다. 드라이버가 비동기 알림을 지원 하지 않는 경우 ODBC 드라이버 관리자는 SQLSTATE S1_118를 사용 하 여 SQL_ERROR을 반환 합니다 (드라이버는 비동기 알림을 지원 하지 않음). 드라이버가 비동기 알림을 지 원하는 경우 ODBC 드라이버 관리자가 드라이버를 호출 하 고 해당 특성 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 설정 하 고 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT 합니다.  
  
 마찬가지로 응용 프로그램은 ODBC 문 핸들에 대해 **SQLSetStmtAttr** 를 호출 하 고 문 수준 비동기 알림을 사용 하거나 사용 하지 않도록 SQL_ATTR_ASYNC_STMT_EVENT 특성을 지정 합니다. 문 함수는 연결이 설정 된 후 항상 호출 되기 때문에 해당 드라이버가 비동기 작업을 지원 하지 않거나 드라이버가 비동기 작업을 지원 하지만 비동기 알림을 지원 하지 않는 경우 **SQLSetStmtAttr** 는 SQLSTATE S1_118 (드라이버는 비동기 알림을 지원 하지 않음)를 사용 하 여 SQL_ERROR을 반환 합니다.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetStmtAttr ( hSTMT,  
                           SQL_ATTR_ASYNC_STMT_EVENT, // Attribute name   
                           (SQLPOINTER) hEvent,       // Win32 Event handle  
                           SQL_IS_POINTER);           // length Indicator  
```  
  
 NULL로 설정할 수 있는 SQL_ATTR_ASYNC_STMT_EVENT은 드라이버에 설정 되지 않는 드라이버 관리자 전용 특성입니다.  
  
 SQL_ATTR_ASYNC_STMT_EVENT의 기본값은 NULL입니다. 드라이버가 비동기 알림을 지원 하지 않는 경우 SQL_ATTR_ASYNC_ STMT_EVENT 특성을 가져오거나 설정 하면 SQLSTATE HY092 (잘못 된 특성/옵션 식별자)를 사용 하 여 SQL_ERROR 반환 됩니다.  
  
 응용 프로그램이 둘 이상의 ODBC 핸들과 동일한 이벤트 핸들을 연결 해서는 안 됩니다. 그렇지 않으면 동일한 이벤트 핸들을 공유 하는 두 개의 핸들에서 두 개의 비동기 ODBC 함수 호출이 완료 되 면 하나의 알림이 손실 됩니다. 연결 핸들에서 동일한 이벤트 핸들을 상속 하는 문 핸들을 방지 하기 위해 ODBC는 응용 프로그램이 연결 핸들에 SQL_ATTR_ASYNC_STMT_EVENT를 설정 하는 경우 SQLSTATE IM016 (문 특성을 연결 핸들로 설정할 수 없음)를 사용 하 여 SQL_ERROR을 반환 합니다.  
  
### <a name="calling-asynchronous-odbc-functions"></a>비동기 ODBC 함수 호출  
 비동기 알림을 사용 하도록 설정 하 고 비동기 작업을 시작한 후에는 응용 프로그램이 임의의 ODBC 함수를 호출할 수 있습니다. 함수가 비동기 작업을 지 원하는 함수 집합에 속하는 경우 함수가 실패 하거나 성공 했는지 여부에 관계 없이 작업이 완료 되 면 응용 프로그램에서 완료 알림을 받게 됩니다.  단, 응용 프로그램에서 잘못 된 연결 또는 문 핸들을 사용 하 여 ODBC 함수를 호출 하는 경우는 예외입니다. 이 경우 ODBC는 이벤트 핸들을 가져와 신호를 받은 상태로 설정 하지 않습니다.  
  
 응용 프로그램은 해당 ODBC 핸들에 대해 비동기 작업을 시작 하기 전에 연결 된 이벤트 개체가 신호를 받지 않은 상태 인지 확인 해야 합니다. ODBC는 이벤트 개체를 다시 설정 하지 않습니다.  
  
### <a name="getting-notification-from-odbc"></a>ODBC에서 알림 받기  
 응용 프로그램 스레드는 **WaitForSingleObject** 을 호출 하 여 이벤트 핸들의 배열을 기다리거나 이벤트 개체 중 하나 또는 모두가 **신호를 받거나** 시간 제한 간격이 경과할 때까지 일시 중단 될 수 있습니다.  
  
```  
DWORD dwStatus = WaitForSingleObject(  
                        hEvent,  // The event associated with the ODBC handle  
                        5000     // timeout is 5000 millisecond   
);  
  
If (dwStatus == WAIT_TIMEOUT)  
{  
    // time-out interval elapsed before all the events are signaled.   
}  
Else  
{  
    // Call the corresponding Asynchronous ODBC API to complete all processing and retrieve the return code.  
}  
```
