---
title: 대량 복사 서식 파일 (ODBC) 없이 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], file formats
- bulk copy [ODBC]
- bulk copy [ODBC], data files
- bulk copy [ODBC], about bulk copy
ms.assetid: 4ee969a7-44ba-40d0-b9ab-8306f1a2b19d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4298c3cc0283ab268dbf5336fef32ddfb35856f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074013"
---
# <a name="bulk-copy-without-a-format-file-odbc"></a>서식 파일 없이 대량 복사(ODBC)
  이 예제에서는 대량 복사 함수를 사용하여 서식 파일 없이 기본 모드 데이터 파일을 만드는 방법을 보여 줍니다. 이 예제는 ODBC 버전 3.0 이상용으로 개발되었습니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지하려면 [Win32 crypto API](http://go.microsoft.com/fwlink/?LinkId=64532)를 사용하여 자격 증명을 암호화해야 합니다.  
  
### <a name="to-bulk-copy-without-a-format-file"></a>서식 파일 없이 대량 복사하려면  
  
1.  환경 핸들 및 연결 핸들을 할당합니다.  
  
2.  대량 복사 작업을 사용하도록 SQL_COPT_SS_BCP 및 SQL_BCP_ON을 설정합니다.  
  
3.  SQL Server에 연결합니다.  
  
4.  호출 [bcp_init](../../native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) 다음 정보를 설정 하려면:  
  
    -   대량 복사를 수행할 원본 또는 대상 테이블/뷰의 이름을 지정합니다.  
  
    -   데이터베이스로 복사할 데이터가 들어 있거나 데이터베이스에서 복사할 때 데이터를 받는 데이터 파일의 이름을 지정합니다.  
  
    -   대량 복사 오류 메시지를 받을 데이터 파일의 이름입니다. 메시지 파일이 필요하지 않으면 NULL을 지정합니다.  
  
    -   복사 방향을: DB_IN 파일에서 뷰 또는 테이블, 테이블 또는 뷰에서 파일로 DB_OUT입니다.  
  
5.  호출 [bcp_exec](../../native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) 대량 복사 작업을 실행 합니다.  
  
 이러한 단계를 사용하여 DB_OUT을 설정하면 기본 형식으로 파일이 만들어집니다. 그런 다음 DB_IN 대신 DB_OUT을 설정한다는 것을 제외하고 동일한 단계에 따라 파일을 서버에 대량 복사할 수 있습니다. 이 작업은 원본 테이블과 대상 테이블의 구조가 정확히 일치하는 경우에만 수행할 수 있습니다.  
  
## <a name="example"></a>예제  
 이 예제는 IA64에서 지원되지 않습니다.  
  
 AdventureWorks 예제 데이터베이스를 기본 데이터베이스로 사용하는 AdventureWorks라는 ODBC 데이터 원본이 필요합니다. AdventureWorks 샘플 데이터베이스는 [Microsoft SQL Server Samples and Community Projects](http://go.microsoft.com/fwlink/?LinkID=85384)(Microsoft SQL Server 샘플 및 커뮤니티 프로젝트) 홈 페이지에서 다운로드할 수 있습니다. 이 데이터 원본은 운영 체제에서 제공하는 ODBC 드라이버를 기반으로 해야 합니다. 이 드라이버의 이름은 "SQL Server"입니다. 이 예제를 64비트 운영 체제에서 32비트 응용 프로그램으로 작성하여 실행하려는 경우 %windir%\SysWOW64\odbcad32.exe에서 ODBC 관리자를 사용하여 ODBC 데이터 원본을 만들어야 합니다.  
  
 이 예제는 컴퓨터의 기본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결됩니다. 명명된 인스턴스에 연결하려면 ODBC 데이터 원본의 정의를 변경하여 server\namedinstance 형식으로 인스턴스를 지정합니다. 기본적으로 [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)] 는 명명된 인스턴스에 설치됩니다.  
  
 odbc32.lib 및 odbcbcp.lib를 사용하여 컴파일합니다.  
  
```  
// compile with: odbc32.lib odbcbcp.lib  
#include <stdio.h>  
#include <string.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
#define MAXBUFLEN 256  
  
SQLHENV henv = SQL_NULL_HENV;  
HDBC hdbc1 = SQL_NULL_HDBC;  
  
void Cleanup() {  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
  
   // Bulk copy variables.  
   SDWORD cRows;  
  
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
  
   // Allocate ODBC connection handle, set bulk copy mode, and then connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLSetConnectAttr(hdbc1, SQL_COPT_SS_BCP, (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetConnectAttr(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security, create the SQL Server DSN using Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Initialize the bulk copy.  
   retcode = bcp_init(hdbc1, "Purchasing.Vendor", "BCPODBC.bcp", "BCPERROR.out", DB_OUT);  
   // Test is for the bulk copy return of SUCCEED, not the ODBC return of SQL_SUCCESS.  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_init(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the bulk copy.  
   retcode = bcp_exec(hdbc1, &cRows);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_exec(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   printf("Number of rows bulk copied out = %d.\n", cRows);  
  
   // Cleanup  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server ODBC 드라이버 방법 도움말 항목을 사용한 대량 복사 &#40;ODBC&#41;](bulk-copying-with-the-sql-server-odbc-driver-how-to-topics-odbc.md)  
  
  
