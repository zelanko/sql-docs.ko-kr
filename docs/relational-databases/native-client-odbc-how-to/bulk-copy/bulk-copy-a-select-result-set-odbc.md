---
title: SELECT 결과 집합 대량 복사 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC]
- bulk copy [ODBC], data files
- bulk copy [ODBC], about bulk copy
ms.assetid: 63d5a87b-4d5f-449b-8c77-9f9cc6b190d4
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7c73b98d623490d9885188a5d71fd5caac02e4c4
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908095"
---
# <a name="bulk-copy-a-select-result-set-odbc"></a>SELECT 결과 집합 대량 복사(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  이 예제에서는 대량 복사 함수를 사용하여 SELECT 문의 결과 집합을 대량 복사하는 방법을 보여 줍니다. 이 예제는 ODBC 버전 3.0 이상용으로 개발되었습니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지하려면 [Win32 crypto API](https://go.microsoft.com/fwlink/?LinkId=64532)를 사용하여 자격 증명을 암호화해야 합니다.  
  
### <a name="to-bulk-copy-out-the-result-set-of-a-select-statement"></a>SELECT 문의 결과 집합을 대량 복사하려면  
  
1.  환경 핸들 및 연결 핸들을 할당합니다.  
  
2.  대량 복사 작업을 사용하도록 SQL_COPT_SS_BCP 및 SQL_BCP_ON을 설정합니다.  
  
3.  SQL Server에 연결합니다.  
  
4.  [bcp_init](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) 를 호출하여 다음 정보를 설정합니다.  
  
    -   *Sztable* 매개 변수에 대해 NULL을 지정 합니다.  
  
    -   결과 집합 데이터를 받는 데이터 파일의 이름입니다.  
  
    -   대량 복사 오류 메시지를 받을 데이터 파일의 이름입니다. 메시지 파일이 필요하지 않으면 NULL을 지정합니다.  
  
    -   복사 방향: DB_OUT.  
  
5.  [Bcp_control](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)를 호출 하 고 EOPTION을 bcphints로 설정 하 고 SELECT 문을 포함 하는 sql96array에 대 한 포인터를 ivalue에 놓습니다.  
  
6.  [bcp_exec](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) 를 호출하여 대량 복사 작업을 실행합니다.  

 이러한 단계를 사용하면 기본 형식으로 파일이 만들어집니다. [Bcp_colfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)를 사용 하 여 데이터 값을 다른 데이터 형식으로 변환할 수 있습니다. 자세한 내용은 [ODBC &#40;&#41;(대량 복사 형식 파일) 만들기](../../../relational-databases/native-client-odbc-how-to/bulk-copy/create-a-bulk-copy-format-file-odbc.md)를 참조 하세요.  
  
## <a name="example"></a>예제  
 AdventureWorks 예제 데이터베이스를 기본 데이터베이스로 사용하는 AdventureWorks라는 ODBC 데이터 원본이 필요합니다. AdventureWorks 샘플 데이터베이스는 [Microsoft SQL Server 샘플 및 커뮤니티 프로젝트](https://go.microsoft.com/fwlink/?LinkID=85384) 홈 페이지에서 다운로드할 수 있습니다. 이 데이터 원본은 운영 체제에서 제공 하는 ODBC 드라이버를 기반으로 해야 합니다. 드라이버 이름은 "SQL Server"입니다. 이 예제를 64비트 운영 체제에서 32비트 애플리케이션으로 작성하여 실행하려는 경우 %windir%\SysWOW64\odbcad32.exe에서 ODBC 관리자를 사용하여 ODBC 데이터 원본을 만들어야 합니다.  
  
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
   SQLTCHAR szBCPQuery[] = "SELECT BirthDate FROM HumanResources.Employee";  
  
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
  
   // Sample use Integrated Security, create SQL Server DSN using Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Initialize the bulk copy.  
   retcode = bcp_init(hdbc1, NULL, "BCPODBC.bcp", "BCPERROR.out", DB_OUT);  
   // The test is for the bulk copy return of SUCCEED, not the ODBC return of SQL_SUCCESS.  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_init(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Specify the query to use.  
   retcode = bcp_control(hdbc1, BCPHINTS, (void *)szBCPQuery);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_control(hdbc1) Failed\n\n");  
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
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server ODBC 드라이버를 사용 하 여 대량 복사 방법 항목 &#40;odbc&#41;](../../../relational-databases/native-client-odbc-how-to/bulk-copy/bulk-copying-with-the-sql-server-odbc-driver-how-to-topics-odbc.md)  
  
  
