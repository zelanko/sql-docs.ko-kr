---
description: C 또는 Visual C++ 응용 프로그램과 함께 Visual FoxPro ODBC 드라이버 사용
title: C 또는 Visual C++ 응용 프로그램에서 Visual FoxPro ODBC 드라이버 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- FoxPro ODBC driver [ODBC], C or C++ applications
- C++ applications [ODBC]
- Visual FoxPro ODBC driver [ODBC], C or C++ applications
- Visual FoxPro data [ODBC], C or C++ applications
- C applications [ODBC]
ms.assetid: beb11a68-849e-4fe0-b217-d3722b1b1389
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d8e7dcbc0d14dfddb4aa8a2318d424dc6c7222e5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471295"
---
# <a name="use-the-visual-foxpro-odbc-driver-with-your-c-or-visual-c-application"></a>C 또는 Visual C++ 응용 프로그램과 함께 Visual FoxPro ODBC 드라이버 사용
C 또는 c + + 응용 프로그램은 Visual foxpro에 [Sqlexecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md) 또는 [sqlexecdirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md) 문을 전송 하 여 visual foxpro 데이터와 통신 합니다. 이 문에는 다음이 포함 될 수 있습니다.  
  
-   [DROP TABLE](../../odbc/microsoft/drop-table-command.md) 명령과 같은 Visual FoxPro 언어에 대 한 기본 SQL 문입니다.  
  
-   [지원 되는 ODBC SQL 문법](../../odbc/microsoft/supported-odbc-sql-grammar-visual-foxpro-odbc-driver.md)입니다.  
  
-   [지원 되는 SET 명령과](../../odbc/microsoft/supported-set-commands-visual-foxpro-odbc-driver.md)같은 SQL Visual FoxPro 언어가 지원 되지 않습니다.  
  
 SQL native에서 Visual FoxPro에 대 한 자세한 내용은 Visual FoxPro 설명서를 참조 하세요.  
  
## <a name="example-using-the-visual-foxpro-odbc-driver-with-your-c-or-c-application"></a>예제: C 또는 c + + 응용 프로그램과 함께 Visual FoxPro ODBC 드라이버 사용  
 다음 예에서는 ODBC C API를 사용 하 여 TasTrade 라는 Microsoft® Visual FoxPro 샘플 데이터베이스의 employee 테이블에서 last_name 필드에 저장 된 데이터를 검색 합니다. 이 데이터베이스는 Visual FoxPro와 함께 제공 되며 기본적으로 다음 위치에 설치 됩니다.  
  
 `c:\vfp\samples\mainsamp\data\tastrade.dbc`  
  
 이 예에서는 메시지 상자에서 확인을 클릭 하 여 다음 성을 볼 수 있도록 한 번에 성을 하나씩 표시 합니다. Tastrade 라는 데이터 원본이 tastrade 데이터베이스를 사용 하도록 설정 된 것으로 가정 합니다.  
  
> [!NOTE]  
>  모든 ODBC API 호출에 대해 오류 검사를 수행 해야 합니다. 이 예에서는 간결 하 게 하기 위해 오류 검사를 제외 합니다.  
  
```  
// FoxPro_ODBC_Driver_with_C.cpp  
// compile with: odbc32.lib user32.lib /c  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <stdio.h>  
#include <mbstring.h>  
  
#define MAX_DATA 100  
#define MYSQLSUCCESS(rc) ((rc==SQL_SUCCESS)||(rc==SQL_SUCCESS_WITH_INFO))  
  
class direxec {  
   RETCODE rc;        // ODBC return code  
   HENV henv;         // Environment     
   HDBC hdbc;         // Connection handle  
   HSTMT hstmt;       // Statement handle  
   unsigned char szData[MAX_DATA];   // Returned data storage  
   SDWORD cbData;     // Output length of data  
   unsigned char chr_ds_name[SQL_MAX_DSN_LENGTH];   // Data source name  
  
public:  
   direxec();           // Constructor  
   void sqlconn();      // Allocate env, stat, and conn  
   void sqlexec(unsigned char *);   // Execute SQL statement  
   void sqldisconn();   // Free pointers to env, stat, conn, and disconnect  
   void error_out();    // Displays errors  
};  
  
// Constructor initializes the string chr_ds_name with the data source name.  
direxec::direxec() {  
   _mbscpy_s(chr_ds_name, (const unsigned char *)"tastrade");  
}  
  
// Allocate environment handle, allocate connection handle,  
// connect to data source, and allocate statement handle.  
void direxec::sqlconn() {  
   SQLAllocEnv(&henv);  
   SQLAllocConnect(henv, &hdbc);  
   rc=SQLConnect(hdbc, chr_ds_name, SQL_NTS, NULL, 0, NULL, 0);  
  
   // Deallocate handles, display error message, and exit.  
   if (!MYSQLSUCCESS(rc)) {  
      SQLFreeEnv(henv);  
      SQLFreeConnect(hdbc);  
      error_out();  
      exit(-1);  
   }  
  
   rc = SQLAllocStmt(hdbc, &hstmt);  
}  
  
// Execute SQL command with SQLExecDirect() ODBC API.  
void direxec::sqlexec(unsigned char * cmdstr) {  
   rc = SQLExecDirect(hstmt, cmdstr, SQL_NTS);  
   if (!MYSQLSUCCESS(rc)) {   // Error  
      error_out();  
      // Deallocate handles and disconnect.  
      SQLFreeStmt(hstmt, SQL_DROP);  
      SQLDisconnect(hdbc);  
      SQLFreeConnect(hdbc);  
      SQLFreeEnv(henv);  
      exit(-1);  
   }  
   else {  
      for (rc = SQLFetch(hstmt) ; rc == SQL_SUCCESS; rc=SQLFetch(hstmt)) {  
         SQLGetData(hstmt, 1, SQL_C_CHAR, szData, sizeof(szData), &cbData);  
         // In this example, the data is returned in a messagebox for  
         // simplicity. However, normally the SQLBindCol() ODBC API could  
         // be called to bind individual data rows and assign for a rowset.  
         MessageBox(NULL, (const char *)szData, "ODBC", MB_OK);  
      }  
   }  
}  
  
// Free the statement handle, disconnect, free the connection handle, and  
// free the environment handle.  
void direxec::sqldisconn() {  
   SQLFreeStmt(hstmt, SQL_DROP);  
   SQLDisconnect(hdbc);  
   SQLFreeConnect(hdbc);  
   SQLFreeEnv(henv);  
}  
  
// Display error message in a message box that has an OK button.  
void direxec::error_out() {  
   unsigned char szSQLSTATE[10];  
   SDWORD nErr;  
   unsigned char msg[SQL_MAX_MESSAGE_LENGTH + 1];  
   SWORD cbmsg;  
  
   while(SQLError(0, 0, hstmt, szSQLSTATE, &nErr, msg, sizeof(msg), &cbmsg) == SQL_SUCCESS) {  
      sprintf_s((char *)szData, MAX_DATA, "Error:\nSQLSTATE=%s, Native error=%ld, msg='%s'",   
         szSQLSTATE, nErr, msg);  
  
      MessageBox(NULL, (const char *)szData, "ODBC Error", MB_OK);  
   }  
}  
  
int main (){  
   // Declare an instance of the direxec object.  
   direxec x;  
  
   // Allocate handles and connect.  
   x.sqlconn();  
  
   // Execute SQL command "SELECT last_name FROM employee".  
   x.sqlexec((UCHAR FAR *)"SELECT last_name FROM employee");  
  
   // Free handles, and disconnect.  
   x.sqldisconn();  
  
   // Return success code; example executed successfully.  
   return (TRUE);  
}  
```
