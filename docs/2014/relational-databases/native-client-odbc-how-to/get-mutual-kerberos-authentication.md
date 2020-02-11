---
title: 상호 Kerberos 인증 가져오기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 64149fd4-239b-40e4-91e2-f9011f7d9f66
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9158544f40a18ff6dce97483be57e645e15a57d4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63200415"
---
# <a name="get-mutual-kerberos-authentication"></a>상호 Kerberos 인증 가져오기
  이 예제에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에서 ODBC를 사용하여 상호 Kerberos 인증을 가져오는 방법을 보여 줍니다.  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에서는 이 예제를 사용할 수 없습니다.  
  
 자세한 내용은 [클라이언트 연결에서 SPN&#41; 지원 &#40;서비스 사용자 이름](../native-client/features/service-principal-name-spn-support-in-client-connections.md)을 참조 하세요.  
  
## <a name="example"></a>예제  
 이 예제를 64비트 운영 체제에서 32비트 애플리케이션으로 작성하여 실행하려는 경우 %windir%\SysWOW64\odbcad32.exe에서 ODBC 관리자를 사용하여 ODBC 데이터 원본을 만들어야 합니다.  
  
 이 예제는 컴퓨터의 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결됩니다. 명명된 인스턴스에 연결하려면 ODBC 데이터 원본의 정의를 변경하여 server\namedinstance 형식으로 인스턴스를 지정합니다. 기본적으로 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 는 명명된 인스턴스에 설치됩니다.  
  
 "MyServer"를 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전의 인스턴스가 있는 컴퓨터 이름으로 변경합니다.  
  
 고객이 제공한 SPN도 지정해야 합니다. "CP_SPN"을 고객이 제공한 SPN으로 변경합니다.  
  
 /EHsc, /D "_UNICODE", /D "UNICODE" 및 odbc32.lib를 사용하여 컴파일합니다. INCLUDE 환경 변수에 sqlncli.h가 들어 있는 디렉터리를 포함해야 합니다.  
  
```  
// compile with: /EHsc /D "_UNICODE" /D "UNICODE" odbc32.lib  
#define WIN32_LEAN_AND_MEAN  
#include <tchar.h>  
#include <windows.h>  
#include <stdio.h>  
#include <sql.h>  
#include <sqlext.h>  
  
#define _SQLNCLI_ODBC_  
#include <sqlncli.h>  
  
#define SUCCESS(x) (!((x) & 0xFFFE))  
  
#define CHKRC(stmt) do \  
                    { \  
                    rc = (stmt); \  
                    if (!SUCCESS(rc)) \  
                    throw (RETCODE) rc; \  
                    } while(0);  
  
void PrintError(SQLSMALLINT HandleType, SQLHANDLE Handle) {  
   RETCODE rc = SQL_SUCCESS;  
   SQLTCHAR szSqlState[6], szMessage[1024];  
   SQLSMALLINT i = 1, msgLen = 0;  
   SQLINTEGER NativeError;  
  
   do {  
      i = 1;  
      while (SQL_NO_DATA != (rc = SQLGetDiagRec(HandleType, Handle, i, szSqlState, &NativeError,   
         szMessage, sizeof(szMessage)/sizeof(SQLTCHAR), &msgLen)) && SUCCESS(rc)) {  
            _tprintf(_T("SQLState=%s, NativeError=%ld, Message=%s\r\n"), szSqlState, NativeError, szMessage);  
            i++;  
      }  
   }   
   while (SQL_NO_DATA != (rc = SQLMoreResults(Handle)) && SUCCESS(rc));  
}  
  
int _tmain(int argc, _TCHAR* argv[]) {  
   RETCODE rc = SQL_SUCCESS;  
   HENV henv = SQL_NULL_HENV;  
   HDBC hdbc = SQL_NULL_HDBC;  
   SQLHSTMT hstmt = SQL_NULL_HSTMT;  
   SQLTCHAR * pszConnection = _T("DRIVER={SQL Server Native Client 10.0};")  
      _T("Server=MyServer;")          // server with SQL Server 2008 (or later)  
      _T("Trusted_Connection=Yes;")  
      _T("ServerSPN=CP_SPN");    // customer-provided SPN  
  
   TCHAR szIntgAuthMethod[64];  
   SQLSMALLINT fMutuallyAuth = 0;  
  
   try {  
      CHKRC(SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HENV, &henv));  
      CHKRC(SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0));  
      CHKRC(SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc));  
      CHKRC(SQLDriverConnect( hdbc, NULL, pszConnection, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT));  
      CHKRC(SQLGetConnectAttr(hdbc, SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD, szIntgAuthMethod, sizeof(szIntgAuthMethod)/sizeof(szIntgAuthMethod[0]), NULL));  
      CHKRC(::SQLGetConnectAttrW(hdbc, SQL_COPT_SS_MUTUALLY_AUTHENTICATED, &fMutuallyAuth, SQL_IS_SMALLINT, NULL));  
  
      _tprintf(_T("Authentication method: %s\r\n"), szIntgAuthMethod);  
      _tprintf(_T("Mutually authenticated: %s\r\n"), fMutuallyAuth?_T("yes"):_T("no"));  
   }  
   catch (RETCODE retcode) {  
      rc = retcode;  
   }  
  
   if (!SUCCESS(rc)) {  
      if (hstmt)  
         PrintError(SQL_HANDLE_STMT, hstmt);  
      else if (hdbc)  
         PrintError(SQL_HANDLE_DBC, hdbc);  
      else if(henv)  
         PrintError(SQL_HANDLE_ENV, henv);  
   }  
  
   if (hstmt)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
   if (hdbc) {  
      SQLDisconnect(hdbc);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
   }  
   if (henv)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
  
