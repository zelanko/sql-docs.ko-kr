---
title: 대량 복사 서식 파일 만들기 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], file formats
- bulk copy [ODBC], data files
ms.assetid: 0572fef3-daf5-409e-b557-c2a632f9a06d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 54f57ae8d03037639076e890b93c0cff9021bd78
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63157231"
---
# <a name="create-a-bulk-copy-format-file-odbc"></a>대량 복사 서식 파일 만들기(ODBC)
  이 예제에서는 대량 복사 함수를 사용하여 데이터 파일과 서식 파일을 모두 만드는 방법을 보여 줍니다. 이 예제는 ODBC 버전 3.0 이상용으로 개발되었습니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지 해야 하는 경우에는 [Win32 CRYPTO API](https://go.microsoft.com/fwlink/?LinkId=64532)를 사용 하 여 자격 증명을 암호화 해야 합니다.  
  
### <a name="to-create-a-bulk-copy-format-file"></a>대량 복사 서식 파일을 만들려면  
  
1.  환경 핸들 및 연결 핸들을 할당합니다.  
  
2.  대량 복사 작업을 사용하도록 SQL_COPT_SS_BCP 및 SQL_BCP_ON을 설정합니다.  
  
3.  SQL Server에 연결합니다.  
  
4.  [bcp_init](../../native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) 를 호출하여 다음 정보를 설정합니다.  
  
    -   대량 복사를 수행할 원본 또는 대상 테이블/뷰의 이름을 지정합니다.  
  
    -   데이터베이스로 복사할 데이터가 들어 있거나 데이터베이스에서 복사할 때 데이터를 받는 데이터 파일의 이름을 지정합니다.  
  
    -   대량 복사 오류 메시지를 받을 데이터 파일의 이름입니다. 메시지 파일이 필요하지 않으면 NULL을 지정합니다.  
  
    -   복사 방향: 테이블 또는 뷰에서 파일에 대 한 DB_OUT 합니다.  
  
5.  [Bcp_columns](../../native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) 를 호출 하 여 열 수를 설정 합니다.  
  
6.  각 열에 대 한 [bcp_colfmt](../../native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md) 를 호출 하 여 데이터 파일에서 해당 특성을 정의 합니다.  
  
7.  [Bcp_writefmt](../../native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md) 를 호출 하 여 대량 복사 작업에 의해 생성 되는 데이터 파일을 설명 하는 서식 파일을 만듭니다.  
  
8.  [bcp_exec](../../native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) 를 호출하여 대량 복사 작업을 실행합니다.  
  
 이러한 방식으로 실행된 대량 복사 작업은 대량 복사된 데이터가 들어 있는 데이터 파일과 데이터 파일의 레이아웃을 설명하는 서식 파일을 모두 만듭니다.  
  
## <a name="example"></a>예제  
 AdventureWorks 예제 데이터베이스를 기본 데이터베이스로 사용하는 AdventureWorks라는 ODBC 데이터 원본이 필요합니다. AdventureWorks 샘플 데이터베이스는 [Microsoft SQL Server 샘플 및 커뮤니티 프로젝트](https://go.microsoft.com/fwlink/?LinkID=85384) 홈 페이지에서 다운로드할 수 있습니다. 이 데이터 원본은 운영 체제에서 제공 하는 ODBC 드라이버를 기반으로 해야 합니다. 드라이버 이름은 "SQL Server"입니다. 이 예제를 64비트 운영 체제에서 32비트 애플리케이션으로 작성하여 실행하려는 경우 %windir%\SysWOW64\odbcad32.exe에서 ODBC 관리자를 사용하여 ODBC 데이터 원본을 만들어야 합니다.  
  
 이 예제는 컴퓨터의 기본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결됩니다. 명명된 인스턴스에 연결하려면 ODBC 데이터 원본의 정의를 변경하여 server\namedinstance 형식으로 인스턴스를 지정합니다. 기본적으로 [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)] 는 명명된 인스턴스에 설치됩니다.  
  
 첫 번째([!INCLUDE[tsql](../../../includes/tsql-md.md)]) 코드 목록을 실행하여 예제에서 사용할 테이블을 만듭니다.  
  
 odbc32.lib 및 odbcbcp.lib를 사용하여 두 번째(C++) 코드 목록을 컴파일합니다.  
  
 세 번째([!INCLUDE[tsql](../../../includes/tsql-md.md)]) 코드 목록을 실행하여 예제에서 사용한 테이블을 삭제합니다.  
  
```  
use AdventureWorks  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'BCPDate')  
     DROP TABLE BCPDate  
GO  
  
CREATE TABLE BCPDate (cola int, colb datetime)  
insert BCPDate(cola) values(1)   
insert BCPDate(cola) values(2)   
insert BCPDate(cola) values(3)   
insert BCPDate(cola) values(4)  
```  
  
```  
// compile with: odbc32.lib odbcbcp.lib  
#include <stdio.h>  
#include <string.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
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
  
   // BCP variables.  
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
  
   // Allocate ODBC connection handle, set bulk copy mode, and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLSetConnectAttr(hdbc1, SQL_COPT_SS_BCP, (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security, create SQL Server DSN using Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"",SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Initialize the bulk copy.  
   retcode = bcp_init(hdbc1, "BCPDate", "BCPODBC.bcp", NULL, DB_OUT);  
   if (retcode != SUCCEED) {  
      printf("bcp_init() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Set the number of output columns.  
   retcode = bcp_columns(hdbc1, 2);  
   if (retcode != SUCCEED) {  
      printf("bcp_init() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Describe the format of column 1 in the data file.  
   retcode = bcp_colfmt(hdbc1, 1, SQLCHARACTER, -1, 5, NULL, 0, 1);  
   if (retcode != SUCCEED) {  
      printf("bcp_init() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Describe the format of column 2 in the data file.  
   retcode = bcp_colfmt(hdbc1, 2, SQLCHARACTER, -1, 20, NULL, 0, 2);  
   if (retcode != SUCCEED) {  
      printf("bcp_init() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Create the format file.  
   retcode = bcp_writefmt(hdbc1, "c:\\BCPFMT.fmt");  
   if (retcode != SUCCEED) {  
      printf("bcp_init() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the bulk copy.  
   retcode = bcp_exec(hdbc1, &cRows);  
   if (retcode != SUCCEED) {  
      printf("bcp_init() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   printf("Number of rows bulk copied out = %d.\n", cRows);  
  
   // Cleanup  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   return(0);  
}  
```  
  
```  
use AdventureWorks  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'BCPDate')  
     DROP TABLE BCPDate  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server ODBC 드라이버를 사용 하 여 대량 복사 방법 도움말 항목 &#40;ODBC&#41;](bulk-copying-with-the-sql-server-odbc-driver-how-to-topics-odbc.md)   
 [데이터 파일 및 서식 파일 사용](../../native-client-odbc-bulk-copy-operations/using-data-files-and-format-files.md)  
  
  
