---
title: 비동기 실행 (알림 방법) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e509dad9-5263-4a10-9a4e-03b84b66b6b3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c2504962a81d9e9e3a5ac8bd4f57f3fe74f9441
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914248"
---
# <a name="asynchronous-execution-notification-method"></a>비동기 실행(알림 방법)
ODBC 연결 및 문 작업의 비동기 실행을 허용 합니다. 비동기 모드에서 ODBC 함수를 호출할 수는 응용 프로그램 스레드 및 함수는 작업이 완료 되 면 다른 작업을 수행 하는 응용 프로그램 스레드를 허용 하기 전에 반환할 수 있습니다. Windows 7 SDK 비동기 문이나 연결 작업에 대 한 응용 프로그램 비동기 작업이 폴링 메서드를 사용 하 여 완료 되었음을 확인 했습니다. 자세한 내용은 참조 [비동기 실행 (폴링 방법)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)합니다. Windows 8 SDK부터, 비동기 작업이 알림 방법을 사용 하 여 완료 되었음을 확인할 수 있습니다.  
  
 폴링 방법에서 응용 프로그램은 작업의 상태를 원하는 때마다 비동기 함수를 호출 해야 합니다. 알림 방법을 콜백 및 ADO.NET에서 대기 하는 것과 비슷합니다. 그러나, ODBC, 알림 개체로 Win32 이벤트를 사용합니다.  
  
 ODBC 커서 라이브러리와 ODBC 비동기 알림을 동시에 사용할 수 없습니다. 두 특성을 설정 하면 SQLSTATE S1119와 오류가 반환 됩니다 (커서 라이브러리 및 비동기 알림을 사용할 수 없습니다 동시에).  
  
 참조 [비동기 함수 완료 알림을](../../../odbc/reference/develop-driver/notification-of-asynchronous-function-completion.md) 드라이버 개발자에 대 한 정보에 대 한 합니다.  
  
> [!NOTE]  
>  알림 방법은 커서 라이브러리와 함께 지원 되지 않습니다. 응용 프로그램 알림 방법을 사용 하도록 설정한 경우 SQLSetConnectAttr 통해 커서 라이브러리를 사용 하도록 설정 하려고 하면 오류 메시지가 표시 됩니다.  
  
## <a name="overview"></a>개요  
 비동기 모드에서 ODBC 함수 호출 되 면 컨트롤 반환 코드를 SQL_STILL_EXECUTING으로 즉시 호출 응용 프로그램에 반환 됩니다. 응용 프로그램 SQL_STILL_EXECUTING 이외의 반환 될 때까지 함수를 폴링하여 반복 해 서 가져와야 합니다. 폴링 루프는 다양 한 비동기 시나리오에서 성능 저하를 일으키는 되는 CPU 사용률을 증가 합니다.  
  
 알림 모델을 사용할 때마다 폴링 모델은 사용할 수 없습니다. 응용 프로그램 다시 원래 함수를 호출 하지 않습니다. 호출 [SQLCompleteAsync 함수](../../../odbc/reference/syntax/sqlcompleteasync-function.md) 비동기 작업을 완료할 수 있습니다. 비동기 작업이 완료 되기 전에 원래 함수를 다시 호출 하는 응용 프로그램을 호출 SQLSTATE IM017 포함 된 sql_error가 반환 됩니다 (폴링 비동기 알림 모드에서 해제 됨).  
  
 응용 프로그램을 호출할 수 알림 모델을 사용할 때는 **SQLCancel** 또는 **SQLCancelHandle** 문 또는 연결 작업을 취소 합니다. 취소 요청에 성공한 경우 ODBC와 관계 없이 SQL_SUCCESS를 반환 합니다. 이 메시지는 함수가 실제로 취소 된; 나타내지 않습니다. 취소 요청을 처리 하는 것을 나타냅니다. 함수는 실제로 취소 하는지 여부를 이며 드라이버 종속 데이터 소스에 따라 다릅니다. 작업이 취소 될 때 드라이버 관리자는 여전히 신호를 보내는 이벤트입니다. 드라이버 관리자는 반환 코드 버퍼에서 SQL_ERROR를 반환 하 고 SQLSTATE HY008 상태가 (작업이 취소 됨)를 나타내는 취소 되었습니다. 함수는 일반적으로 처리를 완료 한 경우 드라이버 관리자는 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다.  
  
### <a name="downlevel-behavior"></a>하위 수준 동작  
 전체에서이 알림을 지 원하는 ODBC 드라이버 관리자 버전이 ODBC 3.81 합니다.  
  
|ODBC 응용 프로그램 버전|드라이버 관리자 버전|드라이버 버전|동작|  
|------------------------------|----------------------------|--------------------|--------------|  
|ODBC 버전에 관계 없이 새 응용 프로그램|ODBC 3.81|3.80 ODBC 드라이버|응용 프로그램이 드라이버에서이 기능을 지 원하는 경우이 기능을 사용할 수 되어, 그렇지 않으면 드라이버 관리자 오류가 있습니다.|  
|ODBC 버전에 관계 없이 새 응용 프로그램|ODBC 3.81|이전 버전 3.80 ODBC 드라이버|드라이버 관리자 드라이버는이 기능을 지원 하지 않는 경우 오류가 됩니다.|  
|ODBC 버전에 관계 없이 새 응용 프로그램|이전 ODBC 3.81|전체|응용 프로그램에서이 기능을 사용 하는 경우 이전 드라이버 관리자는 생각 드라이버 관련 특성으로 새 특성 및 드라이버 오류 아웃 해야 합니다. 새 드라이버 관리자 드라이버에 이러한 특성을 통과 하지 않습니다.|  
  
 응용 프로그램이 기능을 사용 하기 전에 드라이버 관리자 버전을 확인 해야 합니다. 그렇지 않은 경우 잘못 작성 된 드라이버 오류 하지 않는 경우 드라이버 관리자 버전은 이전 ODBC 3.81 동작이 정의 되지 않습니다.  
  
## <a name="use-cases"></a>사용 사례  
 이 섹션에서는 비동기 실행 및 폴링 메커니즘에 대 한 사용 사례를 보여 줍니다.  
  
### <a name="integrate-data-from-multiple-odbc-sources"></a>여러 개의 ODBC 원본의 데이터를 통합  
 데이터 통합 응용 프로그램은 비동기적으로 여러 데이터 원본에서 데이터를 가져옵니다. 원격 데이터 원본에서 데이터의 일부는 및 로컬 파일의 일부 데이터가 됩니다. 응용 프로그램 작업이 비동기 작업이 완료 될 때까지 계속할 수 없습니다.  
  
 반복 해 서 폴링 완료 되었는지 확인 하기 위해 작업 하는 대신 응용 프로그램 이벤트 개체를 만들 수 있습니다 및 ODBC 연결 핸들 또는 ODBC 문 핸들에 연결 합니다. 그런 다음 응용 프로그램은 운영 체제 동기화 하나의 이벤트 개체 또는 여러 이벤트 개체 (ODBC 이벤트 및 기타 Windows 이벤트)에 대해 기다려야 Api를 호출 합니다. ODBC 해당 ODBC 비동기 작업이 완료 되 면 이벤트 개체에 신호를 보내면 됩니다.  
  
 Windows에서는 Win32 이벤트 개체는 사용자는 통합된 프로그래밍 모델 제공 됩니다 하며 합니다. 다른 플랫폼에서 드라이버 관리자는 해당 플랫폼에 특정 이벤트 개체 구현을 사용할 수 있습니다.  
  
 다음 코드 예제에서는 연결 및 문 비동기 알림을 사용 하는 보여 줍니다.  
  
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
  
### <a name="determining-if-a-driver-supports-asynchronous-notification"></a>드라이버는 비동기 알림을 지원 하는지 확인  
 ODBC 응용 프로그램에서 ODBC 드라이버를 호출 하 여 비동기 알림을 지 원하는 경우를 결정할 수 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)합니다. ODBC 드라이버 관리자는 결과적으로 호출 된 **SQLGetInfo** SQL_ASYNC_NOTIFICATION 사용 하 여 드라이버의 합니다.  
  
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
  
### <a name="associating-a-win32-event-handle-with-an-odbc-handle"></a>Win32 이벤트 핸들 ODBC 핸들에 연결  
 응용 프로그램은 해당 Win32 함수를 사용 하 여 Win32 이벤트 개체를 만듭니다. 응용 프로그램 하나 Win32 이벤트 핸들 또는을 연결할 수 한 ODBC 연결 핸들 하나 ODBC 문 핸들입니다.  
  
 연결 특성 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE 및 SQL_ATTR_ASYNC_DBC_EVENT ODBC 비동기 모드에서 실행 되는 여부 및 ODBC 연결 핸들에 대 한 알림 모드를 사용 하는 여부를 결정 합니다. 문 특성 SQL_ATTR_ASYNC_ENABLE 및 SQL_ATTR_ASYNC_STMT_EVENT ODBC 비동기 모드에서 실행 되는 여부 및 ODBC 문 핸들에 대 한 알림 모드를 사용 하는 여부를 결정 합니다.  
  
|SQL_ATTR_ASYNC_ENABLE 또는 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE|SQL_ATTR_ASYNC_STMT_EVENT 또는 SQL_ATTR_ASYNC_DBC_EVENT|모드|  
|-------------------------------------------------------------------------|-------------------------------------------------------------------|----------|  
|사용|null이 아닌|비동기 알림|  
|사용|null|비동기 폴링|  
|사용 안함|any|동기|  
  
 응용 프로그램 비동기 작업 모드를 일시적으로 해제할 수 있습니다. ODBC 연결 수준 비동기 작업을 사용할 수 없는 경우 SQL_ATTR_ASYNC_DBC_EVENT의 값을 무시 합니다. ODBC 문 수준 비동기 작업을 사용할 수 없는 경우 SQL_ATTR_ASYNC_STMT_EVENT의 값을 무시 합니다.  
  
 동기 호출 **SQLSetStmtAttr** 및 **SQLSetConnectAttr**  
 -   **SQLSetConnectAttr** 에서는 비동기 작업의 호출을 사용할 수 있지만 **SQLSetConnectAttr** SQL_ATTR_ASYNC_DBC_EVENT를 설정 하는 항상 동기 합니다.  
  
-   **SQLSetStmtAttr** 비동기 실행을 지원 하지 않습니다.  
  
 오류 아웃 시나리오  
 때 **SQLSetConnectAttr** 연결을 드라이버 관리자는 드라이버를 사용 하 여 확인할 수 없습니다 하기 전에 호출 됩니다. 따라서 드라이버 관리자 반환에 대 한 성공 **SQLSetConnectAttr** 특성 드라이버에서 설정할 수 있습니다. 드라이버 관리자는 응용 프로그램이 연결 함수를 호출할 때 이러한 특성을 설정 합니다. 드라이버 관리자 드라이버에서 비동기 작업을 지원 하지 않으므로 오류-초과할 수 있습니다.  
  
 연결 특성의 상속  
 일반적으로 한 연결의 문을 연결 특성을 상속 합니다. 그러나 SQL_ATTR_ASYNC_DBC_EVENT 특성 상속 가능 하지 않으며 연결 작업에만 영향을 줍니다.  
  
 ODBC 응용 프로그램 이벤트 핸들 ODBC 연결 핸들을 연결 하려면 ODBC API를 호출 **SQLSetConnectAttr** 특성 값으로 처리 하는 특성 및 이벤트 처럼 SQL_ATTR_ASYNC_DBC_EVENT를 지정 합니다. 새 ODBC 특성 SQL_ATTR_ASYNC_DBC_EVENT SQL_IS_POINTER 유형입니다.  
  
```  
HANDLE hEvent;  
hEvent = CreateEvent(   
            NULL,                // default security attributes  
            FALSE,               // auto-reset event  
            FALSE,               // initial state is non-signaled  
            NULL                 // no name  
            );  
```  
  
 일반적으로 응용 프로그램 자동 재설정 이벤트 개체를 만듭니다. ODBC는 이벤트 개체는 다시 설정 되지 않습니다. 응용 프로그램 개체 되지 않았는지 신호를 받은 상태에서 모든 비동기 ODBC 함수를 호출 하기 전에 확인 해야 합니다.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetConnectAttr ( hDBC,  
                              SQL_ATTR_ASYNC_DBC_EVENT, // Attribute name  
                              (SQLPOINTER) hEvent,      // Win32 Event handle  
                              SQL_IS_POINTER);          // Length Indicator  
```  
  
 SQL_ATTR_ASYNC_DBC_EVENT은 드라이버 관리자 전용 특성 드라이버에 설정 되지 것입니다.  
  
 SQL_ATTR_ASYNC_DBC_EVENT의 기본값은 NULL입니다. 가져오거나 설정할 SQL_ATTR_ASYNC_DBC_EVENT SQLSTATE HY092와 SQL_ERROR를 반환 합니다 드라이버는 비동기 알림을 지원 하지 않으면, (잘못 된 특성/옵션 식별자)입니다.  
  
 ODBC 연결 핸들 NULL이 아니고 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE SQL_ASYNC_DBC_ENABLE_ON 호출 하는 모든 ODBC 연결 된 특성을 설정 하 여 비동기 모드를 활성화 하는 응용 프로그램에 마지막 SQL_ATTR_ASYNC_DBC_EVENT 값 설정 비동기 모드를 지 원하는 함수 완료 알림을 받게 됩니다. ODBC 연결 핸들에 설정 된 마지막 SQL_ATTR_ASYNC_DBC_EVENT 값이 NULL 인 경우 ODBC 보내지 않습니다 응용 프로그램이 별도 알림 메시지에 관계 없이 비동기 모드를 사용할지 여부를 합니다.  
  
 응용 프로그램 전이나 SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE 특성을 설정한 후 SQL_ATTR_ASYNC_DBC_EVENT를 설정할 수 있습니다.  
  
 응용 프로그램 연결 함수를 호출 하기 전에 ODBC 연결 핸들에 SQL_ATTR_ASYNC_DBC_EVENT 특성을 설정할 수 (**SQLConnect**, **SQLBrowseConnect**, 또는  **SQLDriverConnect**). ODBC 드라이버 관리자에는 ODBC 드라이버는 응용 프로그램에서 사용할 모르기 때문에 관계 없이 SQL_SUCCESS를 반환 합니다. 연결 함수를 호출 하는 응용 프로그램을 ODBC 드라이버 관리자가 드라이버 비동기 알림을 지원 하는지 여부를 확인 합니다. ODBC 드라이버 관리자와 SQLSTATE S1_118 SQL_ERROR를 반환 합니다 드라이버 비동기 알림의 지원 하지 않으면 (드라이버 비동기 알림을 지원 하지 않음). 드라이버에서 비동기 알림의 지 원하는 경우 ODBC 드라이버 관리자 드라이버를 호출 하 고 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 및 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT 해당 특성을 설정 됩니다.  
  
 마찬가지로, 응용 프로그램이 호출 **SQLSetStmtAttr** ODBC 문 핸들 및 문 수준 비동기 알림을 사용 하지 않도록 설정 하거나 설정 하려면 SQL_ATTR_ASYNC_STMT_EVENT 특성을 지정 합니다. 연결이 설정 된 후에 항상 문 함수 호출 되기 때문에 **SQLSetStmtAttr** SQLSTATE S1_118 된 sql_error가 반환 됩니다 (드라이버 비동기 알림을 지원 하지 않음) 경우 즉시 해당 드라이버는 비동기 작업을 지원 하지 않습니다 또는 드라이버는 비동기 작업을 지원 하지만 비동기 알림을 지원 하지 않습니다.  
  
```  
SQLRETURN retcode;  
retcode = SQLSetStmtAttr ( hSTMT,  
                           SQL_ATTR_ASYNC_STMT_EVENT, // Attribute name   
                           (SQLPOINTER) hEvent,       // Win32 Event handle  
                           SQL_IS_POINTER);           // length Indicator  
```  
  
 NULL로 설정할 수 있는 SQL_ATTR_ASYNC_STMT_EVENT은 드라이버에 설정 되지 것입니다 드라이버 관리자 전용 특성입니다.  
  
 SQL_ATTR_ASYNC_STMT_EVENT의 기본값은 NULL입니다. 가져오거나 설정할 SQL_ATTR_ASYNC_ STMT_EVENT 특성 SQLSTATE HY092와 SQL_ERROR를 반환 합니다 드라이버는 비동기 알림을 지원 하지 않으면, (잘못 된 특성/옵션 식별자)입니다.  
  
 응용 프로그램은 ODBC 핸들을 여러 개 사용 하 여 동일한 이벤트 핸들을 연결 하지 않습니다. 그렇지 않은 경우 동일한 이벤트 핸들을 공유 하는 두 개의 핸들에 두 개의 비동기 ODBC 함수 호출을 완료 하는 경우 하나의 알림을 손실 됩니다. 연결 핸들에서 동일한 이벤트 핸들을 상속 하는 문 핸들을 방지 하려면 ODBC 응용 프로그램 연결 핸들에 SQL_ATTR_ASYNC_STMT_EVENT 설정 (연결 핸들에 문 특성을 설정할 수 없습니다) SQLSTATE i m 016이 포함 된 sql_error가 반환 합니다.  
  
### <a name="calling-asynchronous-odbc-functions"></a>비동기 ODBC 함수 호출  
 비동기 알림을 사용 하도록 설정 하는 비동기 작업 시작 후 응용 프로그램이 ODBC 함수를 호출할 수 있습니다. 함수에 비동기 작업을 지원 하는 함수 집합에 속한 경우 응용 프로그램 알림을 받게 됩니다 완료 작업이 완료 되는 함수가 실패 여부에 관계 없이 또는 성공 합니다.  유일한 예외는 응용 프로그램이 잘못 된 연결 또는 명령문 핸들을 사용 하는 ODBC 함수를 호출 합니다. 이 경우 ODBC는 하지 이벤트 핸들 가져오고 신호 된 상태로 설정 합니다.  
  
 응용 프로그램 관련된 이벤트 개체는 신호 되지 않은 상태 인지 해당 ODBC 핸들에 대 한 비동기 작업을 시작 하기 전에 확인 해야 합니다. ODBC는 이벤트 개체는 다시 설정 되지 않습니다.  
  
### <a name="getting-notification-from-odbc"></a>ODBC에서 알림 가져오기  
 응용 프로그램 스레드를 호출할 수 **WaitForSingleObject** 하나의 이벤트 핸들 또는 호출 대기 **WaitForMultipleObjects** 이벤트 핸들 배열에 기다렸다가 이벤트 개체 중 하나 또는 전부가 될 때까지 일시 중단 신호 또는 시간 제한 간격이 경과 합니다.  
  
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
