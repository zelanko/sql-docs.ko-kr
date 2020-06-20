---
title: 프로세스 ODBC 오류 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- errors [ODBC]
ms.assetid: 66ab0762-79fe-4a31-b655-27dd215a0af7
author: rothja
ms.author: jroth
ms.openlocfilehash: 0b700e41eef8bf3cb2f856a2dd68aa3a96a06e7a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85039733"
---
# <a name="process-odbc-errors-odbc"></a>프로세스 ODBC 오류(ODBC)
  ODBC 메시지를 검색 하는 데는 두 개의 ODBC 함수 호출 ( [SQLGetDiagRec](https://go.microsoft.com/fwlink/?LinkId=58402) 및 [SQLGetDiagField](../native-client-odbc-api/sqlgetdiagfield.md))을 사용할 수 있습니다. **SQLState**, **pfNative**및 **ErrorMessage** 진단 필드에 있는 기본 ODBC 관련 정보를 가져오려면 SQL_NO_DATA를 반환할 때까지 [SQLGetDiagRec](https://go.microsoft.com/fwlink/?LinkId=58402) 를 호출합니다. 각 진단 레코드에 대해 [SQLGetDiagField](../native-client-odbc-api/sqlgetdiagfield.md) 를 호출하여 개별 필드를 검색할 수 있습니다. 드라이버별 필드는 모두 `SQLGetDiagField`를 사용하여 검색해야 합니다.  
  
 [SQLGetDiagRec](https://go.microsoft.com/fwlink/?LinkId=58402) 및 [SQLGetDiagField](../native-client-odbc-api/sqlgetdiagfield.md) 는 개별 드라이버가 아니라 ODBC 드라이버 관리자에 의해 처리됩니다. ODBC 드라이버 관리자는 성공적으로 연결될 때까지 드라이버별 진단 필드를 캐시하지 않습니다. 성공적으로 연결되기 전에는 드라이버별 진단 필드에 대해 [SQLGetDiagField](../native-client-odbc-api/sqlgetdiagfield.md) 를 호출할 수 없습니다. 여기에는 ODBC 연결 명령이 포함되며, 이러한 명령에서 SQL_SUCCESS_WITH_INFO를 반환하는 경우에도 마찬가지입니다. 다음에 ODBC 함수를 호출할 때까지 드라이버별 진단 필드를 사용할 수 없습니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>Description  
 이 예제에서는 표준 ODBC 정보용 [SQLGetDiagRec](https://go.microsoft.com/fwlink/?LinkId=58402) 을 호출하는 간단한 오류 처리기를 보여 줍니다. 그런 다음 유효한 연결이 있는지 테스트하고, 있을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 드라이버별 진단 필드에 대해 `SQLGetDiagField`를 호출합니다. 이 예제는 IA64에서 지원되지 않습니다.  
  
 이 예제는 ODBC 버전 3.0 이상용으로 개발되었습니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지 해야 하는 경우에는 [Win32 CRYPTO API](https://go.microsoft.com/fwlink/?LinkId=64532)를 사용 하 여 자격 증명을 암호화 해야 합니다.  
  
 AdventureWorks 예제 데이터베이스를 기본 데이터베이스로 사용하는 AdventureWorks라는 ODBC 데이터 원본이 필요합니다. AdventureWorks 샘플 데이터베이스는 [Microsoft SQL Server 샘플 및 커뮤니티 프로젝트](https://go.microsoft.com/fwlink/?LinkID=85384) 홈 페이지에서 다운로드할 수 있습니다. 이 데이터 원본은 운영 체제에서 제공 하는 ODBC 드라이버를 기반으로 해야 합니다. 드라이버 이름은 "SQL Server"입니다. 이 예제를 64비트 운영 체제에서 32비트 애플리케이션으로 작성하여 실행하려는 경우 %windir%\SysWOW64\odbcad32.exe에서 ODBC 관리자를 사용하여 ODBC 데이터 원본을 만들어야 합니다.  
  
 이 예제는 컴퓨터의 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결됩니다. 명명된 인스턴스에 연결하려면 ODBC 데이터 원본의 정의를 변경하여 server\namedinstance 형식으로 인스턴스를 지정합니다. 기본적으로 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 는 명명된 인스턴스에 설치됩니다.  
  
 첫 번째([!INCLUDE[tsql](../../includes/tsql-md.md)]) 코드 목록을 실행하여 이 예제에서 사용하는 저장 프로시저를 만듭니다.  
  
 odbc32.lib를 사용하여 두 번째(C++) 코드 목록을 컴파일합니다. 그리고 나서 프로그램을 실행합니다.  
  
 세 번째([!INCLUDE[tsql](../../includes/tsql-md.md)]) 코드 목록을 실행하여 이 예제에서 사용하는 저장 프로시저를 삭제합니다.  
  
### <a name="code"></a>코드  
  
```  
use AdventureWorks  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'BadOne')  
   DROP PROCEDURE BadOne  
  
Go  
  
CREATE PROCEDURE BadOne   
AS   
SELECT * FROM Purchasing.Vendor  
Go  
```  
  
### <a name="code"></a>코드  
  
```  
// compile with: odbc32.lib  
#include <stdio.h>  
#include <string.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
#define MAXBUFLEN 256  
  
SQLHENV henv = SQL_NULL_HENV;  
SQLHDBC hdbc1 = SQL_NULL_HDBC;       
SQLHSTMT hstmt1 = SQL_NULL_HSTMT;  
  
void ProcessLogMessages(SQLSMALLINT plm_handle_type, SQLHANDLE plm_handle, char *logstring, int ConnInd);  
  
void Cleanup() {  
   if (hstmt1 != SQL_NULL_HSTMT)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // This sample use Integrated Security. Please create the SQL Server   
   // DSN by using the Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"",SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) &&  
      (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         ProcessLogMessages(SQL_HANDLE_DBC, hdbc1, "SQLConnect() Failed\n\n", FALSE);  
         Cleanup();  
         return(9);  
   }  
   else {  
      ProcessLogMessages(SQL_HANDLE_DBC, hdbc1,  
         "\nConnect Successful\n\n", FALSE);  
   }  
  
   // Allocate statement handle, and then execute command.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      ProcessLogMessages(SQL_HANDLE_DBC, hdbc1, "SQLAllocHandle(hstmt1) Failed\n\n", TRUE);  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"exec BadOne", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         ProcessLogMessages(SQL_HANDLE_STMT, hstmt1, "SQLExecute() Failed\n\n", TRUE);  
         Cleanup();  
         return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA )  
      ;  
  
   // Clean up.   
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
void ProcessLogMessages(SQLSMALLINT plm_handle_type, SQLHANDLE plm_handle, char *logstring, int ConnInd) {  
   RETCODE plm_retcode = SQL_SUCCESS;  
   UCHAR plm_szSqlState[MAXBUFLEN] = "", plm_szErrorMsg[MAXBUFLEN] = "";  
   SDWORD plm_pfNativeError = 0L;  
   SWORD plm_pcbErrorMsg = 0;  
   SQLSMALLINT plm_cRecNmbr = 1;  
   SDWORD plm_SS_MsgState = 0, plm_SS_Severity = 0;  
   SQLINTEGER plm_Rownumber = 0;  
   USHORT plm_SS_Line;  
   SQLSMALLINT plm_cbSS_Procname, plm_cbSS_Srvname;  
   SQLCHAR plm_SS_Procname[MAXNAME], plm_SS_Srvname[MAXNAME];  
  
   if (logstring)  
      printf(logstring);  
  
   while (plm_retcode != SQL_NO_DATA_FOUND) {  
      plm_retcode = SQLGetDiagRec(plm_handle_type, plm_handle, plm_cRecNmbr,   
                                  plm_szSqlState, &plm_pfNativeError, plm_szErrorMsg,   
                                  MAXBUFLEN - 1, &plm_pcbErrorMsg);  
  
      // Note that if the application has not yet made a successful connection,   
      // the SQLGetDiagField information has not yet been cached by ODBC Driver Manager and   
      // these calls to SQLGetDiagField will fail.  
      if (plm_retcode != SQL_NO_DATA_FOUND) {  
         if (ConnInd) {   
            plm_retcode = SQLGetDiagField( plm_handle_type, plm_handle, plm_cRecNmbr,  
                                                        SQL_DIAG_ROW_NUMBER, &plm_Rownumber,  
                                                        SQL_IS_INTEGER, NULL);  
  
            plm_retcode = SQLGetDiagField( plm_handle_type, plm_handle, plm_cRecNmbr,  
                                           SQL_DIAG_SS_LINE, &plm_SS_Line, SQL_IS_INTEGER, NULL);  
  
            plm_retcode = SQLGetDiagField( plm_handle_type, plm_handle, plm_cRecNmbr,   
                                           SQL_DIAG_SS_MSGSTATE, &plm_SS_MsgState,  
                                           SQL_IS_INTEGER, NULL);  
  
            plm_retcode = SQLGetDiagField( plm_handle_type, plm_handle, plm_cRecNmbr,  
                                           SQL_DIAG_SS_SEVERITY, &plm_SS_Severity,  
                                           SQL_IS_INTEGER, NULL);  
  
            plm_retcode = SQLGetDiagField( plm_handle_type, plm_handle, plm_cRecNmbr,  
                                           SQL_DIAG_SS_PROCNAME, &plm_SS_Procname,  
                                           sizeof(plm_SS_Procname), &plm_cbSS_Procname);  
  
            plm_retcode = SQLGetDiagField( plm_handle_type, plm_handle, plm_cRecNmbr,  
                                           SQL_DIAG_SS_SRVNAME, &plm_SS_Srvname,   
                                           sizeof(plm_SS_Srvname), &plm_cbSS_Srvname);  
         }  
  
         printf("szSqlState = %s\n", plm_szSqlState);  
         printf("pfNativeError = %d\n", plm_pfNativeError);  
         printf("szErrorMsg = %s\n", plm_szErrorMsg);  
         printf("pcbErrorMsg = %d\n\n", plm_pcbErrorMsg);  
  
         if (ConnInd) {  
            printf("ODBCRowNumber = %d\n", plm_Rownumber);  
            printf("SSrvrLine = %d\n", plm_Rownumber);  
            printf("SSrvrMsgState = %d\n", plm_SS_MsgState);  
            printf("SSrvrSeverity = %d\n", plm_SS_Severity);  
            printf("SSrvrProcname = %s\n", plm_SS_Procname);  
            printf("SSrvrSrvname = %s\n\n", plm_SS_Srvname);  
         }  
      }  
  
      plm_cRecNmbr++;   // Increment to next diagnostic record.  
   }  
}  
```  
  
### <a name="code"></a>코드  
  
```  
use AdventureWorks  
DROP PROCEDURE BadOne  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 방법 도움말 항목](odbc-how-to-topics.md)  
  
  
