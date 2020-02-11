---
title: 날짜 및 시간 형식 사용 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: a2aa5644-1e39-4d78-b149-0599d3502cda
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fc57a2c286c9870421a223ce6a14ef201bef0c3d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68205504"
---
# <a name="use-date-and-time-types"></a>날짜 및 시간 형식 사용
  이 예제에서는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에 추가된 날짜/시간 데이터 구조체를 초기화하는 방법을 보여 줍니다. 그런 다음 입력 값을 준비하고, 매개 변수를 바인딩하고, 쿼리를 실행합니다. 이러한 유형을 사용 하는 방법에 대 한 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 향상 ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)을 참조 하세요.  
  
## <a name="example"></a>예제  
 DateTime이라는 ODBC 데이터 원본이 필요합니다. DateTime의 기본 데이터베이스는 tempdb입니다. 이 데이터 원본은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에 대한 ODBC 드라이버를 기반으로 해야 합니다.  
  
 이 예제를 64비트 운영 체제에서 32비트 애플리케이션으로 작성하여 실행하려는 경우 %windir%\SysWOW64\odbcad32.exe에서 ODBC 관리자를 사용하여 ODBC 데이터 원본을 만들어야 합니다.  
  
 이 예제는 컴퓨터의 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결됩니다. 명명된 인스턴스에 연결하려면 ODBC 데이터 원본의 정의를 변경하여 server\namedinstance 형식으로 인스턴스를 지정합니다. 기본적으로 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 는 명명된 인스턴스에 설치됩니다.  
  
 첫 번째([!INCLUDE[tsql](../../includes/tsql-md.md)]) 코드 목록은 이 예제에서 사용하는 테이블을 만듭니다.  
  
 odbc32.lib 및 user32.lib를 사용하여 두 번째(C++) 코드 목록을 컴파일합니다. INCLUDE 환경 변수에 sqlncli.h가 들어 있는 디렉터리를 포함해야 합니다.  
  
 세 번째([!INCLUDE[tsql](../../includes/tsql-md.md)]) 코드 목록은 이 예제에서 사용하는 테이블을 삭제합니다.  
  
```sql
use tempdb  
GO  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'DateTimeTypes')  
DROP TABLE DateTimeTypes  
GO  
  
CREATE TABLE DateTimeTypes (datecol date, time2col time(7), datetime2col datetime2(7), datetimeoffsetcol datetimeoffset(7))  
GO  
```  
  
```cpp
// compile with: odbc32.lib user32.lib  
#include <windows.h>  
#include <Sqlext.h>  
#include <mbstring.h>  
#include <sqlncli.h>  
#include <stdio.h>  
  
#define MAX_DATA 1024  
#define MYSQLSUCCESS(rc) ( (rc == SQL_SUCCESS) || (rc == SQL_SUCCESS_WITH_INFO) )  
  
class direxec {  
   RETCODE rc;   // ODBC return code  
   HENV henv;   // Environment  
   HDBC hdbc;   // Connection Handle  
   HSTMT hstmt;   // Statement Handle  
   SQLHDESC hdesc;   // Descriptor handle  
   unsigned char szData[MAX_DATA];   // Returned Data Storage  
   SDWORD cbData;   // Output Length of data  
   unsigned char char_ds_name[SQL_MAX_DSN_LENGTH];   // Data Source Name  
  
   SQL_DATE_STRUCT date;   // date structure  
   SQL_SS_TIME2_STRUCT time2;   // time2 structure  
   SQL_TIMESTAMP_STRUCT datetime2;   // datetime2 structure  
   SQL_SS_TIMESTAMPOFFSET_STRUCT dateTimeOffset;   // datetimeoffset structure  
  
   SQLLEN cbdate;   // size of date structure  
   SQLLEN cbtime2;   // size of time structure  
   SQLLEN cbdatetime2;   // size of datetime2  
   SQLLEN cbtimestampoffset;   //size of dateTimeOffset  
  
public:  
   direxec();   // Constructor  
   void sqlconn();   // Allocate env, stat and conn  
  
   void sqldisconn();   // Free pointers to env, stat, conn and disconnect  
   void error_out();   // Display errors  
   void check_rc(RETCODE rc);   // Checks for success of the return code  
  
   void sqlinsert();   // Insert into the table  
};  
  
// Constructor initializes the string char_ds_name with the data source name and  
// initialize the data structures to with the date to be inserted.  
direxec::direxec() {  
   _mbscpy_s(char_ds_name, (const unsigned char *)"DateTime");  
  
   // Initialize the date structure  
   date.day = 12;  
   date.month = 10;  
   date.year = 2001;  
  
   // Initialize the time structure  
   time2.hour = 21;  
   time2.minute = 45;  
   time2.second = 52;  
   time2.fraction = 100  ;  
  
   // Initialize the datetime2 structure  
   datetime2.year = 2007;  
   datetime2.month = 12;  
   datetime2.day = 26;  
   datetime2.hour = 0;  
   datetime2.minute = 0;  
   datetime2.second = 0;  
   datetime2.fraction = 100;   
  
   // Initialize the timestampoffset structure  
   dateTimeOffset.year = 2007;  
   dateTimeOffset.month = 3;  
   dateTimeOffset.day = 11;  
   dateTimeOffset.hour = 2;  
   dateTimeOffset.minute = 30;  
   dateTimeOffset.second = 29;  
   dateTimeOffset.fraction = 200;  
   dateTimeOffset.timezone_hour = -8;  
   dateTimeOffset.timezone_minute = 0;  
  
   // Size of structures   
   cbdate = sizeof(SQL_DATE_STRUCT);  
   cbtime2 = sizeof(SQL_SS_TIME2_STRUCT);  
   cbdatetime2 = sizeof(SQL_TIMESTAMP_STRUCT);  
   cbtimestampoffset = sizeof(SQL_SS_TIMESTAMPOFFSET_STRUCT);  
  
}   // direxec  
  
// Allocate environment handles, connection handle, connect to data source, and allocate statement handle  
void direxec::sqlconn() {  
   // Allocate the environment handle  
   rc = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   check_rc(rc);  
  
   // Set the ODBC version to version 3  
   rc = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   check_rc(rc);  
  
   // Allocate the database connection handle  
   rc = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   check_rc(rc);  
  
   // Connect to the database  
   rc = SQLConnect(hdbc, char_ds_name, SQL_NTS, NULL, 0, NULL, 0);  
   check_rc(rc);  
  
   // Allocate the statement handle  
   rc = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
   check_rc(rc);    
  
   // Allocate the descriptor handle  
   rc = rc = SQLAllocHandle(SQL_HANDLE_DESC, hdbc, &hdesc);  
   check_rc(rc);  
  
}   // direxec::sqlconn  
  
// Display error message from the DiagRecord  
void direxec::error_out() {  
   // String to hold the SQL State  
   unsigned char szSQLSTATE[10];  
  
   // Error code  
   SDWORD nErr;  
  
   // The error message  
   unsigned char msg[SQL_MAX_MESSAGE_LENGTH + 1];  
  
   // Size of the message  
   SWORD cbmsg;  
  
   // If hstmt is not null use that for getting the DiagRec  
   if (hstmt)  
      rc = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, 1, szSQLSTATE, &nErr, msg, sizeof(msg), &cbmsg);  
   // else get the diag record from the env  
   else  
      rc = SQLGetDiagRec(SQL_HANDLE_ENV, henv, 1, szSQLSTATE, &nErr, msg, sizeof(msg), &cbmsg);  
  
   // If the rc is successful, show the message using a message box  
   if ( rc == SQL_SUCCESS) {  
      char hold_err[100];  
      _itoa_s(nErr, hold_err, 100, 10);  
      _snprintf_s((char *)szData, MAX_DATA, MAX_DATA - 1, "%s" "%s" "%s" "%s" "%s" "%s" "%s" "%s",   
        "Error:", "\n", "SQLSTATE= ", szSQLSTATE, ", Native error=", hold_err, ", msg = ", msg);  
      MessageBox(NULL, (const char *)szData, "ODBC Error", MB_OK);  
   }  
}   // direxec::error_out  
  
// Checks the return code.  If failure, displays the error, free the memory and exits the program  
void direxec::check_rc(RETCODE rc) {  
   if (!MYSQLSUCCESS(rc)) {  
      error_out();  
      SQLFreeEnv(henv);  
      SQLFreeConnect(hdbc);  
      exit(-1);  
   }   
}   // direxec::check_rc  
  
// Function to insert dates into the table.  
void direxec::sqlinsert() {     
   rc = SQLPrepare(hstmt, (SQLCHAR *) "INSERT INTO DateTimeTypes (datecol, time2col, datetime2col, datetimeoffsetcol) VALUES (?, ?, ?, ?)", SQL_NTS);  
   check_rc(rc);  
  
   rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 10, 0, &date, 0, &cbdate);  
   check_rc(rc);  
  
   rc = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_BINARY, SQL_SS_TIME2, 16, 7, &time2, 0, &cbtime2);  
   check_rc(rc);  
  
   rc = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_TIMESTAMP, SQL_TYPE_TIMESTAMP, 27, 7, &datetime2, 0, &cbdatetime2);  
   check_rc(rc);  
  
   rc = SQLBindParameter(hstmt, 4, SQL_PARAM_INPUT, SQL_C_BINARY, SQL_SS_TIMESTAMPOFFSET, 34, 7, &dateTimeOffset, 0, &cbtimestampoffset);  
   check_rc(rc);  
  
   rc = SQLExecute(hstmt);  
   check_rc(rc);  
}   // direxec::sqlinsert  
  
int main() {  
   direxec x;  
  
   // Allocate handles, and connect.  
   x.sqlconn();   
  
   // Insert all into the table  
   x.sqlinsert();  
}  
```  
  
```sql
USE tempdb  
GO  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'DateTimeTypes')  
DROP TABLE DateTimeTypes  
GO  
```  
  
  
