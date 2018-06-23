---
title: 드라이버 성능 데이터 (ODBC)을 프로 파일링 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- driver performance data [ODBC]
ms.assetid: b997790a-8cc6-4800-8867-74c1bef07be3
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5eac379b8a77a071571982cade36e88c8831bacd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181115"
---
# <a name="profile-driver-performance-data-odbc"></a>드라이버 성능 데이터 프로파일링(ODBC)
  이 예제에서는 성능 통계를 기록하기 위한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 드라이버 관련 옵션을 보여 줍니다. 이 샘플에서는 하나의 파일을 만듭니다: odbcperf.log 성능 데이터 로그 파일 및 (SQLPERF 구조는 Odbcss.h에 정의 됩니다.) SQLPERF 데이터 구조에서 직접 성능 데이터를 표시 만드는 방법을 보여 줍니다. 이 예제는 ODBC 버전 3.0 이상용으로 개발되었습니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지하려면 [Win32 crypto API](http://go.microsoft.com/fwlink/?LinkId=64532)를 사용하여 자격 증명을 암호화해야 합니다.  
  
### <a name="to-log-driver-performance-data-using-odbc-administrator"></a>ODBC 관리자를 사용하여 드라이버 성능 데이터를 기록하려면  
  
1.  **제어판**를 두 번 클릭 **관리 도구** 두 번 클릭 하 고 **데이터 원본 (ODBC)** 합니다. 또는 odbcad32.exe를 호출할 수도 있습니다.  
  
2.  클릭는 **사용자 DSN**, **시스템 DSN**, 또는 **파일 DSN** 탭 합니다.  
  
3.  성능 데이터를 기록할 데이터 원본을 클릭합니다.  
  
4.  클릭 **구성**합니다.  
  
5.  Microsoft SQL Server DSN 구성 마법사를 사용 하 여 페이지를 이동 **로그 파일에 ODBC 드라이버 통계**합니다.  
  
6.  선택 **로그 파일에 ODBC 드라이버 통계**합니다. 상자에서 통계를 기록할 파일 이름을 입력합니다. 필요에 따라 **찾아보기** 의 통계 로그에 대 한 파일 시스템에서 찾아보려면 합니다.  
  
### <a name="to-log-driver-performance-data-programmatically"></a>드라이버 성능 데이터를 프로그래밍 방식으로 기록하려면  
  
1.  호출 [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) SQL_COPT_SS_PERF_DATA_LOG 및 성능 데이터 로그 파일의 전체 경로 파일 이름을 사용 합니다. 예를 들어:  
  
    ```  
    "C:\\Odbcperf.log"  
    ```  
  
2.  호출 [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) 성능 데이터 기록을 시작 하려면 SQL_COPT_SS_PERF_DATA 및 SQL_PERF_START를 사용 합니다.  
  
3.  필요에 따라 호출 [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) SQL_COPT_SS_LOG_NOW 및 NULL 성능 데이터 로그 파일에 탭으로 구분 된 기록 성능 데이터를 쓰려고 합니다. 이 작업은 응용 프로그램 실행 시 여러 번 수행할 수 있습니다.  
  
4.  호출 [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) 성능 데이터 기록을 중지 하려면 SQL_COPT_SS_PERF_DATA 및 SQL_PERF_STOP을 사용 합니다.  
  
### <a name="to-pull-driver-performance-data-into-an-application"></a>드라이버 성능 데이터를 응용 프로그램으로 가져오려면  
  
1.  호출 [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) 성능 데이터 프로 파일링을 시작 하려면 SQL_COPT_SS_PERF_DATA 및 SQL_PERF_START를 사용 합니다.  
  
2.  호출 [SQLGetConnectAttr](../native-client-odbc-api/sqlgetconnectattr.md) SQL_COPT_SS_PERF_DATA 및 SQLPERF 구조에 대 한 포인터의 주소를 사용 합니다. 첫 번째 호출에서는 현재 성능 데이터가 포함된 올바른 SQLPERF 구조의 주소에 대한 포인터를 설정합니다. 드라이버는 성능 구조의 데이터를 지속적으로 새로 고치지 않습니다. 응용 프로그램에 대 한 호출을 반복 해야 [SQLGetConnectAttr](../native-client-odbc-api/sqlgetconnectattr.md) 를 보다 최신 성능 데이터로 구조를 새로 고쳐야 할 때마다 합니다.  
  
3.  호출 [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) 성능 데이터 기록을 중지 하려면 SQL_COPT_SS_PERF_DATA 및 SQL_PERF_STOP을 사용 합니다.  
  
## <a name="example"></a>예제  
 AdventureWorks 예제 데이터베이스를 기본 데이터베이스로 사용하는 AdventureWorks라는 ODBC 데이터 원본이 필요합니다. AdventureWorks 샘플 데이터베이스는 [Microsoft SQL Server Samples and Community Projects](http://go.microsoft.com/fwlink/?LinkID=85384)(Microsoft SQL Server 샘플 및 커뮤니티 프로젝트) 홈 페이지에서 다운로드할 수 있습니다. 이 데이터 원본은 운영 체제에서 제공하는 ODBC 드라이버를 기반으로 해야 합니다. 이 드라이버의 이름은 "SQL Server"입니다. 이 예제를 64비트 운영 체제에서 32비트 응용 프로그램으로 작성하여 실행하려는 경우 %windir%\SysWOW64\odbcad32.exe에서 ODBC 관리자를 사용하여 ODBC 데이터 원본을 만들어야 합니다.  
  
 이 예제는 컴퓨터의 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결됩니다. 명명된 인스턴스에 연결하려면 ODBC 데이터 원본의 정의를 변경하여 server\namedinstance 형식으로 인스턴스를 지정합니다. 기본적으로 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 는 명명된 인스턴스에 설치됩니다.  
  
 odbc32.lib를 사용하여 컴파일합니다.  
  
```  
// compile with: odbc32.lib  
#include <stdio.h>  
#include <string.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
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
  
   // Pointer to the ODBC driver performance structure.  
   SQLPERF *PerfPtr;  
   SQLINTEGER cbPerfPtr;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // This sample use Integrated Security. Please create the SQL Server   
   // DSN by using the Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Set options to log performance statistics.  Specify file to use for the log.  
   retcode = SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA_LOG, &"odbcperf.log", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Start the performance statistics log.  
   retcode =   
      SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA, (SQLPOINTER)SQL_PERF_START, SQL_IS_UINTEGER);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle, then execute command.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"SELECT * FROM Purchasing.Vendor", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"SELECT * FROM Sales.Store", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   // Generate a long-running query.  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"waitfor delay '00:00:04' ", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   // Write current statistics to the performance log.  
   retcode =   
      SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA_LOG_NOW, (SQLPOINTER)NULL, SQL_IS_UINTEGER);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Get pointer to current SQLPerf structure.  
   // Print a couple of statistics.  
   retcode =   
      SQLGetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA, (SQLPOINTER)&PerfPtr, SQL_IS_POINTER, &cbPerfPtr);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLGetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   printf("SQLSelects = %d, SQLSelectRows = %d\n", PerfPtr->SQLSelects, PerfPtr->SQLSelectRows);  
  
   // Cleanup  
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 드라이버 성능 방법 도움말 항목을 프로 파일링 &#40;ODBC&#41;](profiling-odbc-driver-performance-odbc.md)   
 [ODBC 드라이버 성능 프로파일링](../native-client/odbc/profiling-odbc-driver-performance.md)  
  
  