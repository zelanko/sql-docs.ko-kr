---
title: 비동기 실행 (알림 메서드) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e509dad9-5263-4a10-9a4e-03b84b66b6b3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 66b806b698164b306eee4dc7d4c48fbe7835adae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077060"
---
# <a name="asynchronous-execution-notification-method"></a>비동기 실행(알림 방법)
ODBC 연결 및 문 작업의 비동기 실행을 허용 합니다. 응용 프로그램 스레드는 비동기 모드에서는 ODBC 함수를 호출할 수 있습니다 하 고 함수는 작업이 완료 되 면 다른 작업을 수행 하는 응용 프로그램 스레드를 허용 하기 전에 반환할 수 있습니다. Windows 7 SDK 비동기 문이나 연결 작업에 대 한 응용 프로그램 비동기 작업 폴링 메서드를 사용 하 여 완료 되었는지 결정 합니다. 자세한 내용은 [비동기 실행 (폴링 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)합니다. Windows 8 SDK부터 비동기 작업 알림 방법을 사용 하 여 완료 되었음을 확인할 수 있습니다.  
  
 폴링 방법에서는 응용 프로그램 작업의 상태를 좋 때마다 비동기 함수를 호출 해야 합니다. 알림 방법을 콜백 및 ADO.NET의 대기 하는 것과 비슷합니다. 그러나 ODBC는 알림 개체와 Win32 이벤트를 사용합니다.  
  
 ODBC 커서 라이브러리 및 ODBC 비동기 알림을 동시에 사용할 수 없습니다. 두 특성 모두 설정 하면 SQLSTATE S1119 오류로 반환 됩니다 (커서 라이브러리와 비동기 알림을 사용할 수 없습니다 동시).  
  
 참조 [비동기 함수 완료 알림](../../../odbc/reference/develop-driver/notification-of-asynchronous-function-completion.md) 드라이버 개발자를 위한 정보에 대 한 합니다.  
  
> [!NOTE]  
>  알림 방법은 커서 라이브러리를 사용 하 여 지원 되지 않습니다. 응용 프로그램 알림 방법을 사용 하는 경우 SQLSetConnectAttr 통해 커서 라이브러리를 사용 하도록 설정 하려고 하면 오류 메시지가 표시 됩니다.  
  
## <a name="overview"></a>개요  
 비동기 모드에서는 ODBC 함수 호출 되 면 컨트롤 호출 응용 프로그램 반환 코드를 SQL_STILL_EXECUTING으로 즉시 반환 됩니다. 응용 프로그램 SQL_STILL_EXECUTING 이외의 반환 될 때까지 함수를 폴링하여 반복적으로 가져와야 합니다. 폴링 루프에는 CPU 사용률, 대부분의 비동기 시나리오에서 성능 저하를 일으키는 증가 합니다.  
  
 알림 모델을 사용할 때마다 폴링 모델을 사용할 수 없습니다. 응용 프로그램 원본 함수를 다시 호출 하지 않습니다. 호출 [SQLCompleteAsync 함수](../../../odbc/reference/syntax/sqlcompleteasync-function.md) 비동기 작업을 완료 합니다. 비동기 작업이 완료 되기 전에 원래 함수를 다시 호출 하는 응용 프로그램을 호출 SQLSTATE IM017 인 sql_error가 반환 됩니다 (폴링 비동기 알림 모드에서 해제) 합니다.  
  
 알림 모델을 사용 하는 경우 응용 프로그램이 호출할 수 있습니다 **SQLCancel** 하거나 **SQLCancelHandle** 문이나 연결 작업을 취소 합니다. 취소 요청이 성공 하면 ODBC는 관계 없이 SQL_SUCCESS를 반환 합니다. 이 메시지는 실제로 취소 되었음을; 나타내지 않습니다. 취소 요청이 처리 된 것을 나타냅니다. 함수는 실제로 취소 여부 이며 드라이버에 따라 다릅니다 데이터 원본에 따라 결정 됩니다. 작업이 취소 된 드라이버 관리자는 여전히 이벤트를 알립니다. 드라이버 관리자는 반환 코드 버퍼에서 SQL_ERROR를 반환 하 고 SQLSTATE HY008 상태가 (작업이 취소 됨)를 나타내는 취소 되었습니다. 함수는 일반적으로 처리를 완료 하는 경우 드라이버 관리자는 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다.  
  
### <a name="downlevel-behavior"></a>하위 동작  
 전체에서이 알림을 지 원하는 ODBC 드라이버 관리자 버전이 ODBC 3.81 합니다.  
  
|ODBC 응용 프로그램 버전|드라이버 관리자 버전|드라이버 버전|동작|  
|------------------------------|----------------------------|--------------------|--------------|  
|ODBC 버전의 새 응용 프로그램|ODBC 3.81|3\.80 ODBC 드라이버|응용 프로그램 드라이버에서이 기능을 지 원하는 경우이 기능을 사용할 수, 그렇지 않으면 드라이버 관리자는 오류가 발생 합니다.|  
|ODBC 버전의 새 응용 프로그램|ODBC 3.81|이전 버전 3.80 ODBC 드라이버|드라이버 관리자는 드라이버는이 기능을 지원 하지 않는 경우 오류가 출력 됩니다.|  
|ODBC 버전의 새 응용 프로그램|Pre-ODBC 3.81|Any|이 기능을 사용 하는 응용 프로그램을 이전 드라이버 관리자는 드라이버별 특성으로 새 특성을 생각 하 고 드라이버에 오류가 발생 합니다. 새 드라이버 관리자를 드라이버에 이러한 특성을 전달 합니다.|  
  
 응용 프로그램에는이 기능을 사용 하기 전에 드라이버 관리자 버전을 확인 해야 합니다. 그렇지 않으면 잘못 작성 된 드라이버 오류 하지 않으며 드라이버 관리자 버전은 이전 ODBC 3.81, 하는 경우 동작이 정의 되지 않습니다.  
  
## <a name="use-cases"></a>사용 사례  
 이 섹션에서는 비동기 실행 및 폴링 메커니즘에 대 한 사용 사례를 보여 줍니다.  
  
### <a name="integrate-data-from-multiple-odbc-sources"></a>여러 ODBC 원본의 데이터를 통합  
 데이터 통합 응용 프로그램을 비동기적으로 여러 데이터 원본에서 데이터를 인출합니다. 원격 데이터 원본에서 데이터의 일부는 및 로컬 파일에서 일부 데이터가 있습니다. 응용 프로그램은 비동기 작업이 완료 될 때까지 계속할 수 없습니다.  
  
 반복적으로 폴링 전체 인지 확인 하기 위해 작업 하는 대신 응용 프로그램 이벤트 개체를 만들 하 고 있는 ODBC 연결 핸들 또는 ODBC 문 핸들을 사용 하 여 연결할 수 있습니다. 그러면 응용 프로그램이 운영 체제 동기화 이벤트가 하나 개체 또는 여러 이벤트 개체 (ODBC 이벤트 및 기타 Windows 이벤트)에 대해 대기 하는 Api를 호출 합니다. ODBC 해당 ODBC 비동기 작업이 완료 되 면 이벤트 개체에 신호를 보낼 됩니다.  
  
 Windows, Win32 이벤트 개체를 사용할지에 통합 된 프로그래밍 모델을 사용자를 제공 합니다. 다른 플랫폼에서 드라이버 관리자는 해당 플랫폼에 특정 이벤트 개체 구현을 사용할 수 있습니다.  
  
 다음 코드 샘플 연결 및 문 비동기 알림을 사용 하는 방법을 보여 줍니다.  
  
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
  
### <a name="determining-if-a-driver-supports-asynchronous-notification"></a>드라이버 비동기 알림을 지원 하는지 확인 합니다.  
 ODBC 응용 프로그램이 ODBC 드라이버를 호출 하 여 비동기 알림을 지원 하는지 확인할 수 있습니다 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)합니다. ODBC 드라이버 관리자는 결과적으로 호출 하는 **SQLGetInfo** SQL_ASYNC_NOTIFICATION 사용 하 여 드라이버입니다.  
  
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
  
### <a name="associating-a-win32-event-handle-with-an-odbc-handle"></a>ODBC 핸들을 사용 하 여 Win32 이벤트 핸들에 연결  
 응용 프로그램은 해당 Win32 함수를 사용 하 여 Win32 이벤트 개체 생성을 담당 합니다. 응용 프로그램이 ODBC 연결 핸들 하나 또는 한 ODBC 문 핸들을 사용 하 여 한 Win32 이벤트 핸들을 연결할 수 있습니다.  
  
 연결 특성 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE 및 SQL_ATTR_ASYNC_DBC_EVENT ODBC 비동기 모드에서 실행 되는 여부 및 ODBC 연결 핸들에 대 한 알림 모드를 사용 하는 여부를 결정 합니다. 문 특성 SQL_ATTR_ASYNC_ENABLE 및 SQL_ATTR_ASYNC_STMT_EVENT ODBC 비동기 모드에서 실행 되는 여부 및 ODBC 문 핸들에 대 한 알림 모드를 사용 하는 여부를 결정 합니다.  
  
|SQL_ATTR_ASYNC_ENABLE 또는 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE|SQL_ATTR_ASYNC_STMT_EVENT 또는 SQL_ATTR_ASYNC_DBC_EVENT|모드|  
|-------------------------------------------------------------------------|-------------------------------------------------------------------|----------|  
|사용|null이 아닌|비동기 알림|  
|사용|null|비동기 폴링|  
|사용 안함|any|동기|  
  
 응용 프로그램에서 비동기 작업 모드를 해제할 일시적 수 있습니다. ODBC 연결 수준 비동기 작업은 사용 하지 않도록 설정 하는 경우 SQL_ATTR_ASYNC_DBC_EVENT의 값을 무시 합니다. ODBC 문 수준 비동기 작업은 사용 하지 않도록 설정 하는 경우 SQL_ATTR_ASYNC_STMT_EVENT의 값을 무시 합니다.  
  
 동기 호출 **SQLSetStmtAttr** 고 **SQLSetConnectAttr**  
 -   **SQLSetConnectAttr** 에서는 비동기 작업 호출을 사용할 수 있지만 **SQLSetConnectAttr** SQL_ATTR_ASYNC_DBC_EVENT를 설정 하는 항상 동기입니다.  
  
-   **SQLSetStmtAttr** 비동기 실행을 지원 하지 않습니다.  
  
 오류 제한 시나리오  
 때 **SQLSetConnectAttr** 연결을 드라이버 관리자를 사용 하는 드라이버를 확인할 수 없습니다 하기 전에 호출 됩니다. 드라이버 관리자에서 성공 여부를 반환 하는 따라서 **SQLSetConnectAttr** 하지만 특성 드라이버에서 설정할 수 없습니다. 드라이버 관리자는 응용 프로그램 연결 함수를 호출 하는 경우 이러한 특성을 설정 합니다. 드라이버 관리자는 드라이버에서 비동기 작업을 지원 하지 않으므로 하는 오류 초과 될 수 있습니다.  
  
 연결 특성의 상속  
 일반적으로 연결의 문을 연결 특성을 상속 합니다. 그러나 SQL_ATTR_ASYNC_DBC_EVENT 특성은 상속 되지 않습니다 및 연결 작업에만 영향을 줍니다.  
  
 ODBC 응용 프로그램을 ODBC 연결 핸들을 사용 하 여 이벤트 핸들에 연결 하려면 ODBC API를 호출 **SQLSetConnectAttr** 특성 값으로 처리 하는 특성 및 이벤트 SQL_ATTR_ASYNC_DBC_EVENT를 지정 합니다. 새 ODBC 특성 SQL_ATTR_ASYNC_DBC_EVENT SQL_IS_POINTER 형식입니다.  
  
```  
HANDLE hEvent;  
hEvent = CreateEvent(   
            NULL,                // default security attributes  
            FALSE,               // auto-reset event  
            FALSE,               // initial state is non-signaled  
            NULL                 // no name  
            );  
```  
  
 일반적으로 응용 프로그램 자동 재설정 이벤트 개체를 만듭니다. ODBC는 이벤트 개체는 다시 설정 되지 않습니다. 응용 프로그램 인지 개체가 신호를 받은 상태에서 비동기 ODBC 함수를 호출 하기 전에 확인 해야 합니다.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetConnectAttr ( hDBC,  
                              SQL_ATTR_ASYNC_DBC_EVENT, // Attribute name  
                              (SQLPOINTER) hEvent,      // Win32 Event handle  
                              SQL_IS_POINTER);          // Length Indicator  
```  
  
 SQL_ATTR_ASYNC_DBC_EVENT에는 드라이버에서 설정 되지 것입니다는 드라이버 관리자 전용 특성입니다.  
  
 SQL_ATTR_ASYNC_DBC_EVENT의 기본값은 NULL입니다. 드라이버는 비동기 알림을 지원 하지 않으면, 가져오기 또는 설정 SQL_ATTR_ASYNC_DBC_EVENT에서 SQL_ERROR를 반환 SQLSTATE HY092를 사용 하 여 (잘못 된 특성/옵션 식별자)입니다.  
  
 ODBC 연결 핸들을 NULL이 아니고 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE SQL_ASYNC_DBC_ENABLE_ON 호출 하는 모든 ODBC 연결을 사용 하 여 특성을 설정 하 여 비동기 모드를 활성화 하는 응용 프로그램에 마지막 SQL_ATTR_ASYNC_DBC_EVENT 값을 설정 하는 경우 비동기 모드를 지 원하는 함수 완료 알림을 메시지가 표시 됩니다. ODBC 연결 핸들에서 설정 된 마지막 SQL_ATTR_ASYNC_DBC_EVENT 값이 NULL 인 경우 ODBC는 보내지 않습니다 응용 프로그램 알림에 관계 없이 비동기 모드를 사용할지 여부를.  
  
 응용 프로그램 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE 특성을 설정 하기 전후 SQL_ATTR_ASYNC_DBC_EVENT를 설정할 수 있습니다.  
  
 응용 프로그램 연결 함수를 호출 하기 전에 ODBC 연결 핸들에서 SQL_ATTR_ASYNC_DBC_EVENT 특성을 설정할 수 (**SQLConnect**하십시오 **SQLBrowseConnect**, 또는  **SQLDriverConnect**). ODBC 드라이버 관리자에는 ODBC 드라이버 응용 프로그램을 사용할지 모르기 때문에 관계 없이 SQL_SUCCESS를 반환 합니다. 연결 함수를 호출 하는 응용 프로그램을 ODBC 드라이버 관리자가 드라이버에서 비동기 알림을 지원 하는지 여부를 확인 합니다. 드라이버는 비동기 알림을 지원 하지 않으면, ODBC 드라이버 관리자에서 SQLSTATE S1_118를 사용 하 여 SQL_ERROR를 반환 (드라이버 비동기 알림을 지원 하지 않습니다). 드라이버에서 비동기 알림을 지원, ODBC 드라이버 관리자의 드라이버 호출 되며이 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 및 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT 해당 특성을 설정 합니다.  
  
 마찬가지로, 응용 프로그램 호출 **SQLSetStmtAttr** ODBC 문에 처리 및 문 수준 비동기 알림을 사용할지 SQL_ATTR_ASYNC_STMT_EVENT 특성을 지정 합니다. 연결이 설정 되 면 문 함수는 항상 호출 하므로 **SQLSetStmtAttr** SQLSTATE S1_118 인 sql_error가 반환 됩니다 (드라이버 비동기 알림을 지원 하지 않습니다) 경우 즉시 해당 드라이버는 비동기 작업을 지원 하지 않습니다 또는 드라이버는 비동기 작업을 지원 하지만 비동기 알림을 지원 하지 않습니다.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetStmtAttr ( hSTMT,  
                           SQL_ATTR_ASYNC_STMT_EVENT, // Attribute name   
                           (SQLPOINTER) hEvent,       // Win32 Event handle  
                           SQL_IS_POINTER);           // length Indicator  
```  
  
 SQL_ATTR_ASYNC_STMT_EVENT NULL로 설정할 수 있는 드라이버에서 설정 되지 것입니다는 드라이버 관리자 전용 특성을입니다.  
  
 SQL_ATTR_ASYNC_STMT_EVENT의 기본값은 NULL입니다. 드라이버는 비동기 알림을 지원 하지 않으면, 가져오기 또는 설정 SQL_ATTR_ASYNC_ STMT_EVENT 특성에서 SQL_ERROR를 반환 SQLSTATE HY092를 사용 하 여 (잘못 된 특성/옵션 식별자)입니다.  
  
 응용 프로그램은 둘 이상의 ODBC 핸들을 사용 하 여 동일한 이벤트 핸들을 연결 하지 않습니다. 그렇지 않은 경우 동일한 이벤트 핸들을 공유 하는 두 개의 핸들 두 비동기 ODBC 함수 호출을 완료 하는 경우 하나의 알림을 손실 됩니다. 연결 핸들에서 동일한 이벤트 핸들을 상속 하는 문 핸들을 방지 하려면 응용 프로그램 연결 핸들의 SQL_ATTR_ASYNC_STMT_EVENT를 설정 하는 경우 ODBC SQLSTATE IM016 (연결 핸들으로 문 특성을 설정할 수 없습니다)를 사용 하 여 SQL_ERROR를 반환 합니다.  
  
### <a name="calling-asynchronous-odbc-functions"></a>비동기 ODBC 함수 호출  
 비동기 알림을 사용 하도록 설정 하 고 비동기 작업 시작 후 응용 프로그램이 ODBC 함수를 호출할 수 있습니다. 비동기 작업을 지 원하는 함수 집합에 속하는 경우 응용 프로그램 알림을 받게 됩니다 완료 작업이 완료 되 면 함수 실패 여부에 관계 없이 또는 성공 합니다.  유일한 예외는 응용 프로그램 호출 하는 잘못 된 연결 또는 문 핸들을 사용 하 여 ODBC 함수입니다. 이 경우 ODBC 및 하지 않습니다 이벤트 핸들을 가져올 신호 받음 상태로 설정 합니다.  
  
 응용 프로그램 관련된 이벤트 개체가 해당 ODBC 핸들에 대해 비동기 작업을 시작 하기 전에 신호 되지 않은 상태가 되어 있는지 확인 해야 합니다. ODBC는 이벤트 개체는 다시 설정 되지 않습니다.  
  
### <a name="getting-notification-from-odbc"></a>ODBC에서 알림 가져오기  
 응용 프로그램 스레드를 호출할 수 있습니다 **WaitForSingleObject** 하나의 이벤트 핸들 또는 호출 대기할 **WaitForMultipleObjects** 이벤트 핸들 배열에서 대기 하 고 이벤트 개체 중 하나 또는 모두 될 때까지 일시 중단 하려면 신호 또는 시간 제한 간격이 경과 합니다.  
  
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
