---
title: 비동기 실행(알림 방법) | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306414"
---
# <a name="asynchronous-execution-notification-method"></a>비동기 실행(알림 방법)
ODBC를 사용하면 연결 및 명령문 작업을 비동기로 실행할 수 있습니다. 응용 프로그램 스레드는 비동기 모드에서 ODBC 함수를 호출할 수 있으며 작업이 완료되기 전에 함수를 반환하여 응용 프로그램 스레드가 다른 작업을 수행할 수 있도록 합니다. Windows 7 SDK에서 비동기 문 또는 연결 작업의 경우 응용 프로그램이 폴링 방법을 사용하여 비동기 작업이 완료되었다고 확인했습니다. 자세한 내용은 [비동기 실행(폴링 메서드)을](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)참조하십시오. Windows 8 SDK에서 시작하여 알림 방법을 사용하여 비동기 작업이 완료되었는지 확인할 수 있습니다.  
  
 폴링 메서드에서 응용 프로그램은 작업 상태를 원할 때마다 비동기 함수를 호출해야 합니다. 알림 메서드는 콜백 및 ADO.NET 대기와 유사합니다. 그러나 ODBC는 Win32 이벤트를 알림 개체로 사용합니다.  
  
 ODBC 커서 라이브러리 및 ODBC 비동기 알림은 동시에 사용할 수 없습니다. 두 특성을 모두 설정하면 SQLSTATE S1119(커서 라이브러리 및 비동기 알림을 동시에 사용할 수 없음)가 있는 오류가 반환됩니다.  
  
 드라이버 개발자에 대한 정보는 [비동기 함수 완료 알림을](../../../odbc/reference/develop-driver/notification-of-asynchronous-function-completion.md) 참조하십시오.  
  
> [!NOTE]  
>  알림 메서드는 커서 라이브러리에서 지원되지 않습니다. 응용 프로그램은 알림 메서드를 사용하도록 설정하면 SQLSetConnectAttr을 통해 커서 라이브러리를 사용하도록 설정하려고 하면 오류 메시지가 표시됩니다.  
  
## <a name="overview"></a>개요  
 비동기 모드에서 ODBC 함수가 호출되면 반환 코드가 SQL_STILL_EXECUTING 즉시 호출 응용 프로그램으로 제어가 반환됩니다. 응용 프로그램은 SQL_STILL_EXECUTING 이외의 것을 반환할 때까지 함수를 반복적으로 폴링해야 합니다. 폴링 루프는 CPU 사용률을 증가시켜 많은 비동기 시나리오에서 성능이 저하됩니다.  
  
 알림 모델을 사용할 때마다 폴링 모델이 비활성화됩니다. 응용 프로그램이 원래 함수를 다시 호출해서는 안 됩니다. [SQLCompleteAsync 함수를](../../../odbc/reference/syntax/sqlcompleteasync-function.md) 호출하여 비동기 작업을 완료합니다. 비동기 작업이 완료되기 전에 응용 프로그램이 원래 함수를 다시 호출하면 SQLSTATE IM017(비동기 알림 모드에서 폴링이 비활성화됨)으로 SQL_ERROR 반환됩니다.  
  
 알림 모델을 사용하는 경우 응용 프로그램은 **SQLCancel** 또는 **SQLCancelHandle을** 호출하여 명령문 또는 연결 작업을 취소할 수 있습니다. 취소 요청이 성공하면 ODBC는 SQL_SUCCESS 반환합니다. 이 메시지는 함수가 실제로 취소되었음을 나타내지 않습니다. 취소 요청이 처리되었지만 있음을 나타냅니다. 함수가 실제로 취소되는지 여부는 드라이버에 따라 다르며 데이터 원본에 따라 다릅니다. 작업이 취소되면 드라이버 관리자는 여전히 이벤트에 신호를 보올합니다. 드라이버 관리자는 반환 코드 버퍼에서 SQL_ERROR 반환하고 상태는 취소가 성공했음을 나타내기 위해 SQLSTATE HY008(작업 취소)입니다. 함수가 일반 처리를 완료하면 드라이버 관리자는 SQL_SUCCESS 반환하거나 SQL_SUCCESS_WITH_INFO.  
  
### <a name="downlevel-behavior"></a>하향 평준화 동작  
 이 알림을 완료하는 ODBC 드라이버 관리자 버전은 ODBC 3.81입니다.  
  
|응용 프로그램 ODBC 버전|드라이버 관리자 버전|드라이버 버전|동작|  
|------------------------------|----------------------------|--------------------|--------------|  
|모든 ODBC 버전의 새로운 응용 프로그램|ODBC 3.81|ODBC 3.80 드라이버|드라이버가 이 기능을 지원하는 경우 응용 프로그램에서 이 기능을 사용할 수 있으며, 그렇지 않으면 드라이버 관리자가 오류가 발생합니다.|  
|모든 ODBC 버전의 새로운 응용 프로그램|ODBC 3.81|사전 ODBC 3.80 드라이버|드라이버가 이 기능을 지원하지 않으면 드라이버 관리자가 오류가 발생합니다.|  
|모든 ODBC 버전의 새로운 응용 프로그램|사전 ODBC 3.81|모두|응용 프로그램에서 이 기능을 사용하는 경우 이전 드라이버 관리자는 새 특성을 드라이버 관련 특성으로 간주하고 드라이버에 오류가 발생합니다. 새 드라이버 관리자는 이러한 특성을 드라이버에 전달하지 않습니다.|  
  
 응용 프로그램은 이 기능을 사용하기 전에 드라이버 관리자 버전을 확인해야 합니다. 그렇지 않으면 잘못 작성된 드라이버에 오류가 발생하지 않고 드라이버 관리자 버전이 ODBC 3.81 이전인 경우 동작이 정의되지 않습니다.  
  
## <a name="use-cases"></a>사용 사례  
 이 섹션에서는 비동기 실행 및 폴링 메커니즘에 대한 사용 사례를 보여 주며  
  
### <a name="integrate-data-from-multiple-odbc-sources"></a>여러 ODBC 소스의 데이터 통합  
 데이터 통합 응용 프로그램은 여러 데이터 원본에서 데이터를 비동기적으로 가져옵니다. 일부 데이터는 원격 데이터 원본에서 제공되며 일부 데이터는 로컬 파일에서 가져옵니다. 비동기 작업이 완료될 때까지 응용 프로그램을 계속할 수 없습니다.  
  
 작업이 완료되었는지 확인하기 위해 작업을 반복적으로 폴링하는 대신 응용 프로그램은 이벤트 개체를 만들고 ODBC 연결 핸들 또는 ODBC 문 핸들과 연결할 수 있습니다. 그런 다음 응용 프로그램은 운영 체제 동기화 API를 호출하여 하나의 이벤트 개체 또는 여러 이벤트 개체(ODBC 이벤트 및 기타 Windows 이벤트 모두)를 기다립니다. ODBC는 해당 ODBC 비동기 작업이 완료되면 이벤트 개체에 신호를 보올합니다.  
  
 Windows에서 Win32 이벤트 개체가 사용되며 사용자에게 통합 프로그래밍 모델을 제공합니다. 다른 플랫폼의 드라이버 관리자는 해당 플랫폼과 관련된 이벤트 개체 구현을 사용할 수 있습니다.  
  
 다음 코드 샘플에서는 연결 및 문 비동기 알림의 사용을 보여 줍니다.  
  
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
  
### <a name="determining-if-a-driver-supports-asynchronous-notification"></a>드라이버가 비동기 알림을 지원하는지 확인  
 ODBC 응용 프로그램은 ODBC 드라이버가 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)를 호출하여 비동기 알림을 지원하는지 확인할 수 있습니다. 따라서 ODBC 드라이버 관리자는 SQL_ASYNC_NOTIFICATION 있는 드라이버의 **SQLGetInfo를** 호출합니다.  
  
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
 응용 프로그램은 해당 Win32 함수를 사용하여 Win32 이벤트 개체를 만드는 데 책임이 있습니다. 응용 프로그램은 하나의 ODBC 연결 핸들 또는 하나의 ODBC 문 핸들과 하나의 Win32 이벤트 핸들을 연결할 수 있습니다.  
  
 연결 특성은 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE SQL_ATTR_ASYNC_DBC_EVENT ODBC가 비동기 모드에서 실행되는지 여부와 ODBC가 연결 핸들에 대한 알림 모드를 활성화하는지 여부를 결정합니다. 명령문 특성은 SQL_ATTR_ASYNC_ENABLE SQL_ATTR_ASYNC_STMT_EVENT ODBC가 비동기 모드에서 실행되는지 여부와 ODBC가 명령문 핸들에 대한 알림 모드를 활성화하는지 여부를 결정합니다.  
  
|SQL_ATTR_ASYNC_ENABLE 또는 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE|SQL_ATTR_ASYNC_STMT_EVENT 또는 SQL_ATTR_ASYNC_DBC_EVENT|Mode|  
|-------------------------------------------------------------------------|-------------------------------------------------------------------|----------|  
|사용|null이 아닌|비동기 알림|  
|사용|null|비동기 폴링|  
|사용 안 함|any|동기|  
  
 응용 프로그램은 일시적으로 비동기 작동 모드를 비활성화할 수 있습니다. ODBC는 연결 수준 비동기 작업이 비활성화된 경우 SQL_ATTR_ASYNC_DBC_EVENT 값을 무시합니다. ODBC는 문 수준 비동기 작업이 비활성화된 경우 SQL_ATTR_ASYNC_STMT_EVENT 값을 무시합니다.  
  
 **SQLSetStmtAttr** 및 **SQLSetConnectAttr의** 동기 호출  
 -   **SQLSetConnectAttr** 비동기 작업을 지원 하지만 SQL_ATTR_ASYNC_DBC_EVENT 설정 하는 **SQLSetConnectAttr의** 호출은 항상 동기.  
  
-   **SQLSetStmtAttr** 비동기 실행을 지원 하지 않습니다.  
  
 오류 아웃 시나리오  
 연결을 하기 전에 **SQLSetConnectAttr이** 호출되면 드라이버 관리자는 사용할 드라이버를 결정할 수 없습니다. 따라서 드라이버 관리자는 **SQLSetConnectAttr에** 대 한 성공을 반환 하지만 특성 드라이버에서 설정할 준비가 되지 않을 수 있습니다. 드라이버 관리자는 응용 프로그램이 연결 함수를 호출할 때 이러한 특성을 설정합니다. 드라이버가 비동기 작업을 지원하지 않기 때문에 드라이버 관리자가 오류가 발생할 수 있습니다.  
  
 연결 특성 상속  
 일반적으로 연결의 문은 연결 특성을 상속합니다. 그러나 SQL_ATTR_ASYNC_DBC_EVENT 특성은 상속할 수 없으며 연결 작업에만 영향을 줍니다.  
  
 ODBC 응용 프로그램은 이벤트 핸들을 ODBC 연결 핸들과 연결하기 위해 ODBC API **SQLSetConnectAttr을** 호출하고 SQL_ATTR_ASYNC_DBC_EVENT 특성 및 이벤트 핸들을 특성 값으로 지정합니다. SQL_ATTR_ASYNC_DBC_EVENT 새로운 ODBC 특성은 SQL_IS_POINTER 형식입니다.  
  
```  
HANDLE hEvent;  
hEvent = CreateEvent(   
            NULL,                // default security attributes  
            FALSE,               // auto-reset event  
            FALSE,               // initial state is non-signaled  
            NULL                 // no name  
            );  
```  
  
 일반적으로 응용 프로그램은 이벤트 개체를 자동으로 재설정합니다. ODBC는 이벤트 개체를 재설정하지 않습니다. 응용 프로그램은 비동기 ODBC 함수를 호출하기 전에 개체가 신호 상태가 아닌지 확인해야 합니다.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetConnectAttr ( hDBC,  
                              SQL_ATTR_ASYNC_DBC_EVENT, // Attribute name  
                              (SQLPOINTER) hEvent,      // Win32 Event handle  
                              SQL_IS_POINTER);          // Length Indicator  
```  
  
 SQL_ATTR_ASYNC_DBC_EVENT 드라이버 관리자 전용 특성으로 드라이버에서 설정되지 않습니다.  
  
 SQL_ATTR_ASYNC_DBC_EVENT 기본값은 NULL입니다. 드라이버가 비동기 알림을 지원하지 않는 경우 SQL_ATTR_ASYNC_DBC_EVENT 가져오거나 설정하면 SQLSTATE HY092(잘못된 특성/옵션 식별자)SQL_ERROR 반환됩니다.  
  
 ODBC 연결 핸들에 설정된 마지막 SQL_ATTR_ASYNC_DBC_EVENT 값이 NULL이 아니고 응용 프로그램이 SQL_ASYNC_DBC_ENABLE_ON SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE 특성을 설정하여 비동기 모드를 사용하도록 설정한 경우 비동기 모드를 지원하는 ODBC 연결 함수를 호출하면 완료 알림이 표시됩니다. ODBC 연결 핸들에 설정된 마지막 SQL_ATTR_ASYNC_DBC_EVENT 값이 NULL인 경우 ODBC는 비동기 모드가 활성화되어 있는지 여부에 관계없이 응용 프로그램에 알림을 보내지 않습니다.  
  
 응용 프로그램은 특성 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE 설정하기 전이나 후에 SQL_ATTR_ASYNC_DBC_EVENT 설정할 수 있습니다.  
  
 응용 프로그램은 연결**함수(SQLConnect,** **SQLBrowseConnect**또는 **SQLDriverConnect)를**호출하기 전에 ODBC 연결 핸들에서 SQL_ATTR_ASYNC_DBC_EVENT 특성을 설정할 수 있습니다. ODBC 드라이버 관리자는 응용 프로그램에서 사용할 ODBC 드라이버를 알지 못하므로 SQL_SUCCESS 반환합니다. 응용 프로그램이 연결 함수를 호출하면 ODBC 드라이버 관리자는 드라이버가 비동기 알림을 지원하는지 여부를 확인합니다. 드라이버가 비동기 알림을 지원하지 않는 경우 ODBC 드라이버 관리자는 SQLSTATE S1_118 SQL_ERROR 반환합니다(드라이버는 비동기 알림을 지원하지 않음). 드라이버가 비동기 알림을 지원하는 경우 ODBC 드라이버 관리자는 드라이버를 호출하고 해당 속성을 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT 설정합니다.  
  
 마찬가지로 응용 프로그램은 ODBC 문 핸들에서 **SQLSetStmtAttr을** 호출하고 SQL_ATTR_ASYNC_STMT_EVENT 특성을 지정하여 문 수준 비동기 알림을 활성화 하거나 비활성화합니다. 연결이 설정된 후에 문 함수가 항상 호출되므로 **SQLSetStmtAttr은** 해당 드라이버가 비동기 작업을 지원하지 않거나 드라이버가 비동기 작업을 지원하지 않지만 비동기 알림을 지원하지 않는 경우 SQLSTATE S1_118(드라이버는 비동기 알림을 지원하지 않음)으로 SQL_ERROR 반환합니다.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetStmtAttr ( hSTMT,  
                           SQL_ATTR_ASYNC_STMT_EVENT, // Attribute name   
                           (SQLPOINTER) hEvent,       // Win32 Event handle  
                           SQL_IS_POINTER);           // length Indicator  
```  
  
 null로 설정할 수 있는 SQL_ATTR_ASYNC_STMT_EVENT 드라이버 관리자 전용 특성으로 드라이버에서 설정되지 않습니다.  
  
 SQL_ATTR_ASYNC_STMT_EVENT 기본값은 NULL입니다. 드라이버가 비동기 알림을 지원하지 않는 경우 SQL_ATTR_ASYNC_ STMT_EVENT 특성을 가져오거나 설정하면 SQLSTATE HY092(잘못된 특성/옵션 식별자)SQL_ERROR 반환됩니다.  
  
 응용 프로그램은 동일한 이벤트 핸들을 두 개 이상의 ODBC 핸들과 연결해서는 안 됩니다. 그렇지 않으면 동일한 이벤트 핸들을 공유하는 두 개의 핸들에서 두 개의 비동기 ODBC 함수 호출이 완료되면 하나의 알림이 손실됩니다. 연결 핸들에서 동일한 이벤트 핸들을 상속 하는 문 핸들을 방지 하려면 ODBC 반환 SQL_ERROR SQLSTATE IM016 (연결 핸들에 문 특성을 설정할 수 없습니다)응용 프로그램이 연결 핸들에서 SQL_ATTR_ASYNC_STMT_EVENT 설정 하는 경우.  
  
### <a name="calling-asynchronous-odbc-functions"></a>비동기 ODBC 함수 호출  
 비동기 알림을 사용하도록 설정 하 고 비동기 작업을 시작 한 후 응용 프로그램 모든 ODBC 함수를 호출할 수 있습니다. 함수가 비동기 작업을 지원하는 함수 집합에 속하는 경우 함수가 실패하거나 성공한지 여부에 관계없이 작업이 완료될 때 응용 프로그램에 완료 알림이 표시됩니다.  유일한 예외는 응용 프로그램이 잘못된 연결 또는 문 핸들이 있는 ODBC 함수를 호출한다는 것입니다. 이 경우 ODBC는 이벤트 핸들을 얻고 신호된 상태로 설정하지 않습니다.  
  
 응용 프로그램은 해당 ODBC 핸들에서 비동기 작업을 시작하기 전에 연결된 이벤트 개체가 비신호 상태에 있는지 확인해야 합니다. ODBC는 이벤트 개체를 재설정하지 않습니다.  
  
### <a name="getting-notification-from-odbc"></a>ODBC에서 알림 받기  
 응용 프로그램 스레드는 **WaitForSingleObject를** 호출하여 하나의 이벤트 핸들에서 대기하거나 **WaitForMultipleObjects를** 호출하여 이벤트 핸들의 배열을 대기하고 하나 또는 모든 이벤트 개체가 신호를 표시하거나 시간 시간 간격이 경과할 때까지 일시 중단될 수 있습니다.  
  
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
