---
title: "반환 코드 및 출력 매개 변수 (ODBC) 처리 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- return codes [ODBC]
- output parameters [ODBC]
ms.assetid: 102ae1d0-973d-4e12-992c-d844bf05160d
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 883908b47cb5d54d6c89776ec8eee93ae1bdb847
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="running-stored-procedures---process-return-codes-and-output-parameters"></a>저장된 프로시저 실행-프로세스 반환 코드 및 출력 매개 변수
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 드라이버를 사용하면 저장 프로시저를 원격 저장 프로시저로 실행할 수 있습니다. 저장 프로시저를 원격 저장 프로시저로 실행하면 드라이버와 서버에서 프로시저의 실행 성능을 최적화할 수 있습니다.  
  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저는 정수 반환 코드 및 출력 매개 변수를 사용할 수 있습니다. 반환 코드 및 출력 매개 변수는 서버의 마지막 패킷으로 전달 되므로 및 때까지 응용 프로그램을 사용할 수 없는 [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) SQL_NO_DATA를 반환 합니다. 오류가 저장된 프로시저에서 반환 되 면 호출 SQLMoreResults 하 SQL_NO_DATA가 반환 될 때까지 다음 결과로 이동 합니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지하려면 [Win32 crypto API](http://go.microsoft.com/fwlink/?LinkId=64532)를 사용하여 자격 증명을 암호화해야 합니다.  
  
### <a name="to-process-return-codes-and-output-parameters"></a>반환 코드 및 출력 매개 변수를 처리하려면  
  
1.  ODBC CALL 이스케이프 시퀀스를 사용하는 SQL 문을 생성합니다. 이 문에서는 각 입력, 입/출력 및 출력 매개 변수와 프로시저 반환 값(있는 경우)에 대해 매개 변수 표식을 사용해야 합니다.  
  
2.  호출 [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) 각 입력에 대 한 입/출력 및 출력 매개 변수 및 프로시저에 대 한 반환 값 (있는 경우).  
  
3.  **SQLExecDirect**를 사용하여 문을 실행합니다.  
  
4.  마지막 결과 집합을 처리하는 동안 **SQLFetch** 또는 **SQLFetchScroll** 에서 SQL_NO_DATA를 반환하거나 **SQLMoreResults** 에서 SQL_NO_DATA를 반환할 때까지 결과 집합을 처리합니다. 이때 반환 코드 및 출력 매개 변수에 바인딩된 변수가 반환된 데이터 값으로 채워집니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 반환 코드 및 출력 매개 변수를 처리하는 방법을 보여 줍니다. 이 예제는 IA64에서 지원되지 않습니다. 이 예제는 ODBC 버전 3.0 이상용으로 개발되었습니다.  
  
 AdventureWorks 예제 데이터베이스를 기본 데이터베이스로 사용하는 AdventureWorks라는 ODBC 데이터 원본이 필요합니다. AdventureWorks 샘플 데이터베이스는 [Microsoft SQL Server Samples and Community Projects](http://go.microsoft.com/fwlink/?LinkID=85384)(Microsoft SQL Server 샘플 및 커뮤니티 프로젝트) 홈 페이지에서 다운로드할 수 있습니다. 이 데이터 원본은 운영 체제에서 제공하는 ODBC 드라이버를 기반으로 해야 합니다. 이 드라이버의 이름은 "SQL Server"입니다. 이 예제를 64비트 운영 체제에서 32비트 응용 프로그램으로 작성하여 실행하려는 경우 %windir%\SysWOW64\odbcad32.exe에서 ODBC 관리자를 사용하여 ODBC 데이터 원본을 만들어야 합니다.  
  
 이 예제는 컴퓨터의 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결됩니다. 명명된 인스턴스에 연결하려면 ODBC 데이터 원본의 정의를 변경하여 server\namedinstance 형식으로 인스턴스를 지정합니다. 기본적으로 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 는 명명된 인스턴스에 설치됩니다.  
  
 첫 번째([!INCLUDE[tsql](../../includes/tsql-md.md)]) 코드 목록은 이 예제에서 사용하는 저장 프로시저를 만듭니다.  
  
 odbc32.lib를 사용하여 두 번째(C++) 코드 목록을 컴파일합니다. 그리고 나서 프로그램을 실행합니다.  
  
 세 번째([!INCLUDE[tsql](../../includes/tsql-md.md)]) 코드 목록은 이 예제에서 사용하는 저장 프로시저를 삭제합니다.  
  
```  
use AdventureWorks  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'TestParm')  
   DROP PROCEDURE TestParm  
GO  
  
CREATE PROCEDURE TestParm   
@OutParm int OUTPUT   
AS  
SELECT Name FROM Purchasing.Vendor  
SELECT @OutParm = 88  
RETURN 99  
go  
```  
  
```  
// compile with: odbc32.lib  
#include \<stdio.h>  
#include \<string.h>  
#include \<windows.h>  
#include \<sql.h>  
#include \<sqlext.h>  
#include \<odbcss.h>  
  
#define MAXBUFLEN 255  
  
SQLHENV henv = SQL_NULL_HENV;  
SQLHDBC hdbc1 = SQL_NULL_HDBC;       
SQLHSTMT hstmt1 = SQL_NULL_HSTMT;  
  
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
   // SQLBindParameter variables.  
   SWORD sParm1 = 0, sParm2 = 1;  
   SQLLEN cbParm1 = SQL_NTS;  
   SQLLEN cbParm2 = SQL_NTS;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
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
  
   // This sample use Integrated Security. Create the SQL Server DSN by using the Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"",SQL_NTS, (UCHAR*)"", SQL_NTS);  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle(hstmt1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Bind the return code to variable sParm1.  
   retcode = SQLBindParameter(hstmt1, 1, SQL_PARAM_OUTPUT, SQL_C_SSHORT, SQL_INTEGER, 0, 0, &sParm1, 0, &cbParm1);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLBindParameter(sParm1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Bind the output parameter to variable sParm2.  
   retcode = SQLBindParameter(hstmt1, 2, SQL_PARAM_OUTPUT, SQL_C_SSHORT, SQL_INTEGER, 0, 0, &sParm2, 0, &cbParm2);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLBindParameter(sParm2) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the command.   
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"{? = call TestParm(?)}", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Show parameters are not filled.  
   printf("Before result sets cleared: RetCode = %d, OutParm = %d.\n", sParm1, sParm2);  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA )  
      ;  
  
   // Show parameters are now filled.  
   printf("After result sets drained: RetCode = %d, OutParm = %d.\n", sParm1, sParm2);  
  
   // Clean up.   
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
```  
use AdventureWorks  
DROP PROCEDURE TestParm  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
[저장 프로시저 &#40; ODBC &#41; 호출](../../relational-databases/native-client-odbc-how-to/running-stored-procedures-call-stored-procedures.md)  
  
  
