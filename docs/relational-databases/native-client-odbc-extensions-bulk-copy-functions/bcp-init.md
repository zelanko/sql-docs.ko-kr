---
title: bcp_init | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- bcp_init
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_init function
ms.assetid: 6a25862c-7f31-4873-ab65-30f3abde89d2
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 619c1c5b150d31f8fd283ef365c476674fb8b427
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="bcpinit"></a>bcp_init
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  대량 복사 작업을 초기화합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_init (  
        HDBC hdbc,  
        LPCTSTR szTable,  
        LPCTSTR szDataFile,  
        LPCTSTR szErrorFile,  
        INT eDirection);  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
 *szTable*  
 복사의 원본 또는 대상이 될 데이터베이스 테이블의 이름입니다. 이 이름은 데이터베이스 이름 또는 소유자 이름도 포함할 수 있습니다. 예를 들어 **pubs.gracie.titles**, **pubs... 제목**, **gracie.titles**, 및 **타이틀** 은 모두 유효한 테이블 이름입니다.  
  
 경우 *eDirection* 이 DB_OUT 이면 *szTable* 데이터베이스 뷰의 이름일 수도 있습니다.  
  
 경우 *eDirection* 이 DB_OUT이 고 SELECT 문을 사용 하 여 지정 [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) 전에 [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) 호출 **bcp_init** *szTable* NULL로 설정 해야 합니다.  
  
 *szDataFile*  
 복사의 원본 또는 대상이 될 사용자 파일의 이름입니다. 데이터를 사용 하 여 변수에서 직접 복사 되는 경우 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)설정, *szDataFile* NULL로 합니다.  
  
 *szErrorFile*  
 진행 메시지, 오류 메시지, 그리고 어떤 이유로 인해 사용자 파일에서 테이블로 복사하지 못한 모든 행의 복사본으로 채워질 오류 파일의 이름입니다. NULL로 전달 되 면 *szErrorFile*, 없음 오류 파일을 사용 합니다.  
  
 *eDirection*  
 복사의 방향이며 DB_IN 또는 DB_OUT입니다. DB_IN은 프로그램 변수 또는 사용자 파일에서 테이블로의 복사를 나타냅니다. DB_OUT은 데이터베이스 테이블에서 사용자 파일로의 복사를 나타냅니다. DB_OUT에는 사용자 파일 이름을 지정해야 합니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>주의  
 호출 **bcp_init** 다른 대량 복사 함수를 호출 하기 전에. **bcp_init** 워크스테이션 간의 데이터 대량 복사에 필요한 초기화를 수행 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 **bcp_init** 대량 복사 함수에 사용할 수 있는 ODBC 연결 핸들 기능을 제공 해야 합니다. 핸들을 사용 하려면 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 에 SQL_COPT_SS_BCP 할당 되었지만 연결 되지 않음 연결 핸들에 SQL_BCP_ON을 설정 합니다. 연결된 핸들에 특성을 할당하려고 하면 오류가 발생합니다.  
  
 데이터 파일을 지정 하는 경우 **bcp_init** 데이터베이스 원본 또는 대상 테이블의 데이터 파일이 아니라 구조를 검사 합니다. **bcp_init** 데이터베이스 테이블, 뷰 또는 SELECT 결과 집합의 각 열에 따라 데이터 파일에 대 한 데이터 형식 값을 지정 합니다. 이 지정에는 각 열의 데이터 형식, 데이터에 길이 또는 Null 표시자 및 종결자 바이트 문자열이 있는지 여부, 고정 길이 데이터 형식의 길이가 포함됩니다. **bcp_init** 이러한 값을 다음과 같이 설정 합니다.  
  
-   지정되는 데이터 형식은 데이터베이스 테이블, 뷰 또는 SELECT 결과 집합에 있는 열의 데이터 형식입니다. 데이터 형식은 sqlncli.h에 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 데이터 형식으로 열거됩니다. 데이터 자체는 해당 컴퓨터 형식으로 표현됩니다. 즉, 데이터 열에서 **정수** big는 4 바이트 시퀀스를 통해 표시 되는 데이터 형식-또는 little endian 데이터 파일을 만든 컴퓨터에 기반 합니다.  
  
-   데이터베이스 데이터 형식의 길이가 고정된 경우 데이터 파일 데이터의 길이도 고정됩니다. 데이터를 처리 하는 대량 복사 함수 (예를 들어 [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md))와 동일 하 게 데이터베이스 테이블, 뷰 또는 SELECT 열 목록에 지정 된 데이터의 길이 데이터 파일에 있는 데이터의 길이 예상 하는 데이터 행을 구문 분석 합니다. 로 정의 된 데이터베이스 열에 대 한 예를 들어 데이터 **char (13)** 파일에는 데이터의 각 행은 13 자로 표현 되어야 합니다. 데이터베이스 열이 Null 값을 허용하는 경우에는 고정 길이 데이터 앞에 Null 표시자를 붙일 수 있습니다.  
  
-   종결자 바이트 시퀀스가 정의된 경우 종결자 바이트 시퀀스의 길이는 0으로 설정됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 복사 대상일 때는 데이터 파일의 데이터베이스 테이블에 있는 각 열에 데이터가 있어야 하며, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 복사 원본일 때는 데이터베이스 테이블, 뷰 또는 SELECT 결과 집합의 모든 열에서 데이터 파일로 데이터가 복사됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 복사 대상일 때는 데이터 파일에 있는 열의 서수 위치가 데이터베이스 테이블에 있는 열의 서수 위치와 동일해야 하며, 복사할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **bcp_exec** 데이터베이스 테이블에서 열의 서 수 위치에 따라 데이터를 배치 합니다.  
  
-   데이터베이스 데이터 형식의 길이가 가변적인 경우 (예를 들어 **varbinary(22)**) 또는 데이터 파일의 데이터 길이 또는 null 표시기가 붙은 경우 데이터베이스 열에서 null 값을 포함할 수 있습니다. 표시자의 길이는 데이터 형식 및 대량 복사 버전에 따라 다릅니다.  
  
 데이터 파일에 대해 지정 된 데이터 형식 값을 변경 하려면 호출 [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) 및 [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로의 대량 복사 작업을 인덱스가 없는 테이블에 맞게 최적화하려면 데이터베이스 복구 모델을 SIMPLE 또는 BULK_LOGGED로 설정하면 됩니다. 자세한 내용은 참조 [대량 가져오기의 최소 로깅을 위한 선행 조건](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md) 및 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)합니다.  
  
 없는 데이터 파일을 사용 하는 경우 호출 해야 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) 형식 및 위치에 각 열에 대 한 데이터의 메모리를 지정 하려면 다음 데이터 행을 복사는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하 여 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)합니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 ODBC bcp_init 함수를 서식 파일과 함께 사용하는 방법을 보여 줍니다.  
  
 C++ 코드를 컴파일하고 실행하기 전에 다음을 수행해야 합니다.  
  
-   Test라는 ODBC 데이터 원본을 만듭니다. 이 데이터 원본을 데이터베이스와 연관시킬 수 있습니다.  
  
-   데이터베이스에서 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 실행합니다.  
  
    ```  
    CREATE TABLE BCPDate (cola int, colb datetime);  
    ```  
  
-   응용 프로그램을 실행할 디렉터리에 Bcpfmt.fmt라는 파일을 추가하고 이 파일에 다음 코드를 추가합니다.  
  
    ```  
    8.0  
    2  
    1SQLCHAR04"\t"1colaSQL_Latin1_General_Cp437_Bin  
    2SQLCHAR08"\r\n"2colbSQL_Latin1_General_Cp437_Bin  
    ```  
  
-   응용 프로그램을 실행할 디렉터리에 Bcpodbc.bcp라는 파일을 추가하고 이 파일에 다음 코드를 추가합니다.  
  
    ```  
    1  
    2  
    ```  
  
 이제 C++ 코드를 컴파일하고 실행할 준비가 되었습니다.  
  
```  
// compile with: odbc32.lib sqlncli11.lib  
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
   retcode = SQLConnect(hdbc1, (UCHAR*)"Test", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
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
  
## <a name="see-also"></a>관련 항목:  
 [대량 복사 함수](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
