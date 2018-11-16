---
title: 대량 복사 서식 파일 (ODBC)를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy using format file [ODBC]
- ODBC, bulk copy operations
ms.assetid: 970fd3af-f918-4fc3-a5b1-92596515d4de
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 836e9724f05caa82eb0be01e6ab49cfa1519136e
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51671022"
---
# <a name="bulk-copy-by-using-a-format-file-odbc"></a>서식 파일을 사용하여 대량 복사(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  이 예제에서는 ODBC bcp_init 함수를 서식 파일과 함께 사용하는 방법을 보여 줍니다.  
  
### <a name="to-bulk-copy-by-using-a-format-file"></a>서식 파일을 사용하여 대량 복사하려면  
  
1.  환경 핸들 및 연결 핸들을 할당합니다.  
  
2.  대량 복사 작업을 사용하도록 SQL_COPT_SS_BCP 및 SQL_BCP_ON을 설정합니다.  
  
3.  Microsoft  SQL Server™에 연결합니다.  
  
4.  [bcp_init](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) 를 호출하여 다음 정보를 설정합니다.  
  
    -   대량 복사를 수행할 원본 또는 대상 테이블/뷰의 이름을 지정합니다.  
  
    -   데이터베이스로 복사할 데이터가 들어 있거나 데이터베이스에서 복사할 때 데이터를 받는 데이터 파일의 이름을 지정합니다.  
  
    -   대량 복사 오류 메시지를 받을 데이터 파일의 이름입니다. 메시지 파일이 필요하지 않으면 NULL을 지정합니다.  
  
    -   복사 방향을 지정합니다. DB_IN이면 파일에서 테이블 또는 뷰로 복사됩니다.  
  
5.  [bcp_readfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md) 를 호출하여 대량 복사 작업에 사용할 데이터 파일을 설명하는 서식 파일을 만듭니다.  
  
6.  [bcp_exec](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) 를 호출하여 대량 복사 작업을 실행합니다.  
  
## <a name="example"></a>예제  
 이 예제는 IA64에서 지원되지 않습니다.  
  
 AdventureWorks 예제 데이터베이스를 기본 데이터베이스로 사용하는 AdventureWorks라는 ODBC 데이터 원본이 필요합니다. AdventureWorks 샘플 데이터베이스는 [Microsoft SQL Server Samples and Community Projects](https://go.microsoft.com/fwlink/?LinkID=85384)(Microsoft SQL Server 샘플 및 커뮤니티 프로젝트) 홈 페이지에서 다운로드할 수 있습니다. 이 데이터 원본은 운영 체제에서 제공하는 ODBC 드라이버를 기반으로 해야 합니다. 이 드라이버의 이름은 "SQL Server"입니다. 이 예제를 64비트 운영 체제에서 32비트 응용 프로그램으로 작성하여 실행하려는 경우 %windir%\SysWOW64\odbcad32.exe에서 ODBC 관리자를 사용하여 ODBC 데이터 원본을 만들어야 합니다.  
  
 이 예제는 컴퓨터의 기본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결됩니다. 명명된 인스턴스에 연결하려면 ODBC 데이터 원본의 정의를 변경하여 server\namedinstance 형식으로 인스턴스를 지정합니다. 기본적으로 [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)] 는 명명된 인스턴스에 설치됩니다.  
  
 첫 번째([!INCLUDE[tsql](../../../includes/tsql-md.md)]) 코드 목록을 실행하여 예제에서 사용할 테이블을 만듭니다.  
  
 두 번째 코드 목록을 복사하고 Bcpfmt.fmt라는 파일로 붙여 넣습니다. 테이블의 각 열은 탭 문자로 구분됩니다.  
  
 세 번째 코드 목록을 복사하고 Bcpodbc.bcp라는 파일로 붙여 넣습니다. 파일에서 캐리지 리턴 앞에 탭 문자가 옵니다.  
  
 odbc32.lib 및 odbcbcp.lib를 사용하여 네 번째(C++) 코드 목록을 컴파일합니다. MSBuild.exe를 사용하여 빌드한 경우 먼저 Bcpfmt.fmt 및 Bcpodbc.bcp를 프로젝트 디렉터리에서 .exe가 있는 디렉터리에 복사한 다음 .exe를 호출합니다.  
  
 다섯 번째([!INCLUDE[tsql](../../../includes/tsql-md.md)]) 코드 목록을 실행하여 예제에서 사용한 테이블을 삭제합니다.  
  
```  
use AdventureWorks  
CREATE TABLE BCPDate (cola int, colb datetime)  
```  
  
```  
8.0  
2  
1SQLCHAR04"\t"1colaSQL_Latin1_General_Cp437_Bin  
2SQLCHAR08"\r\n"2colbSQL_Latin1_General_Cp437_Bin  
```  
  
```  
1  
2  
  
```  
  
```  
// compile with: odbc32.lib odbcbcp.lib  
#include <stdio.h>  
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
  
   // Allocate ODBC connection handle, set BCP mode, and connect.  
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
  
   // Sample uses Integrated Security. Create SQL Server DSN using Windows NT authentication.  
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Initialize the bulk copy.  
   retcode = bcp_init(hdbc1, "BCPDate", "BCPODBC.bcp", NULL, DB_IN);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_init(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Read the format file.  
   retcode = bcp_readfmt(hdbc1, "BCPFMT.fmt");  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_readfmt(hdbc1) Failed\n\n");  
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
  
   printf("Number of rows bulk copied in = %d.\n", cRows);  
  
   // Cleanup  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
```  
use AdventureWorks  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'BCPDate')  
     DROP TABLE BCPDate  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server ODBC 드라이버 방법 도움말 항목을 사용한 대량 복사 &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/bulk-copy/bulk-copying-with-the-sql-server-odbc-driver-how-to-topics-odbc.md)   
 [데이터 파일 및 서식 파일 사용](../../../relational-databases/native-client-odbc-bulk-copy-operations/using-data-files-and-format-files.md)  
  
  
