---
title: bcp_setbulkmode | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bcp_setbulkmode function
ms.assetid: de56f206-1f7e-4c03-bf22-da9c7f9f4433
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9671447a2fba1cd57b021266f29de7af741f0de6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62688792"
---
# <a name="bcpsetbulkmode"></a>bcp_setbulkmode
  bcp_setbulkmode를 사용 하면 단일 함수 호출에서 모든 열 특성을 설정 하는 대량 복사 작업에서 열 형식을 지정할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_setbulkmode (  
   HDBC   
hdbc  
,  
   INT   
property  
,  
   void *   
pField  
,  
   INT   
cbField  
,  
   void *   
pRow  
,  
   INT   
cbRow  
);  
  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
 *속성*  
 BYTE 유형의 상수입니다. 상수 목록은 주의 섹션의 표를 참조하십시오.  
  
 *pField*  
 필드 종결자 값에 대한 포인터입니다.  
  
 *cbField*  
 필드 종결자 값의 길이(바이트)입니다.  
  
 *pRow*  
 행 종결자 값에 대한 포인터입니다.  
  
 *cbRow*  
 행 종결자 값의 길이(바이트)입니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>Remarks  
 bcp_setbulkmode 대량 쿼리 또는 테이블에서 복사를 사용할 수 있습니다. Bcp_setbulkmode 대량 쿼리 문을 복사 하 되, bcp_control BCP_HINT로 호출 하기 전에 호출 해야 합니다.  
  
 bcp_setbulkmode가 사용 하는 대신 [bcp_setcolfmt](bcp-setcolfmt.md) 하 고 [bcp_columns](bcp-columns.md)는 사용 하 여 함수 호출당 한 열의 형식을 지정 합니다.  
  
 다음 표에서는 *property* 매개 변수에 대한 상수를 나열합니다.  
  
|property|Description|  
|--------------|-----------------|  
|BCP_OUT_CHARACTER_MODE|문자 출력 모드를 지정합니다.<br /><br /> BCP의-c 옵션에 해당합니다. EXE를 사용 하 여 bcp_setcolfmt `BCP_FMT_TYPE` 속성이 설정 `SQLCHARACTER`합니다.|  
|BCP_OUT_WIDE_CHARACTER_MODE|유니코드 출력 모드를 지정합니다.<br /><br /> BCP의-w 옵션에 해당합니다. EXE 및 사용 하 여 bcp_setcolfmt `BCP_FMT_TYPE` 속성이 설정 `SQLNCHAR`합니다.|  
|BCP_OUT_NATIVE_TEXT_MODE|비문자 유형의 경우 네이티브 유형을 지정하고 문자 유형의 경우 유니코드를 지정합니다.<br /><br /> BCP의-N 옵션에 해당합니다. EXE 및 사용 하 여 bcp_setcolfmt `BCP_FMT_TYPE` 속성이 설정 `SQLNCHAR` 열 유형이 문자열인 경우 (기본, 문자열이 아닌 경우).|  
|BCP_OUT_NATIVE_MODE|네이티브 데이터베이스 유형을 지정합니다.<br /><br /> BCP의-n 옵션에 해당합니다. EXE 및 사용 하 여 bcp_setcolfmt `BCP_FMT_TYPE` 속성이 기본값으로 설정 합니다.|  
  
 Bcp_setbulkmode bcp_setcolfmt, bcp_control, 및 bcp_readfmt를 포함 하는 함수 호출의 시퀀스를 사용 하 여 사용 하지 않아야 합니다. 예를 들어 bcp_control(BCPTEXTFILE) 및 bcp_setbulkmode 호출 하지 않아야 합니다.  
  
 Bcp_control 및 bcp_setbulkmode bcp_setbulkmode와 충돌 하지 않는 bcp_control 옵션에 대해 호출할 수 있습니다. 예를 들어 bcp_control(BCPFIRST) 및 bcp_setbulkmode 호출할 수 있습니다.  
  
 Bcp_setbulkmode bcp_setcolfmt, bcp_control, 및 bcp_readfmt를 포함 하는 함수 호출의 시퀀스를 사용 하 여 호출 하려고 하면 함수 호출 중 하나는 시퀀스 오류 실패를 반환 합니다. 오류를 해결 하려는 경우 모든 설정을 다시 설정 하 고 다시 시작 하는 bcp_init를 호출 합니다.  
  
 다음 표에서는 함수 시퀀스 오류를 발생시키는 일부 함수 호출의 예를 제공합니다.  
  
 호출 시퀀스  
  
```  
bcp_init("table", DB_IN);  
bcp_setbulkmode();  
```  
  
```  
bcp_init("table", DB_OUT);  
bcp_setbulkmode();  
bcp_readfmt();  
```  
  
```  
bcp_init(NULL, DB_OUT);  
bcp_control(BCPHINTS, "select ...");  
bcp_setbulkmode();  
```  
  
```  
bcp_init("table", DB_OUT);  
bcp_setbulkmode();  
bcp_setcolfmt();  
```  
  
```  
bcp_init("table", DB_OUT);  
bcp_control(BCPDELAYREADFMT, true);  
bcp_readfmt();  
bcp_setcolfmt();  
```  
  
```  
bcp_init(NULL, DB_OUT);  
bcp_control(BCPDELAYREADFMT, true);  
bcp_setbulkmode();  
bcp_control(BCPHINTS, "select ...");  
bcp_readfmt();  
```  
  
```  
bcp_init("table", DB_OUT);  
bcp_control(BCPDELAYREADFMT, true);  
bcp_columns();  
```  
  
```  
bcp_init("table", DB_OUT);  
bcp_control(BCPDELAYREADFMT, true);  
bcp_setcolfmt();  
```  
  
## <a name="example"></a>예제  
 다음 예제에서는 bcp_setbulkmode의 서로 다른 설정을 사용하여 4개의 파일을 만듭니다.  
  
```  
// compile with: sqlncli11.lib odbc32.lib  
  
#include <windows.h>  
#include <stdio.h>  
#include <tchar.h>  
#include <sqlext.h>  
#include "sqlncli.h"  
  
// Global variables  
SQLHENV g_hEnv = NULL;  
SQLHDBC g_hDbc = NULL;  
  
void ODBCCleanUp() {  
   if (g_hDbc) {  
      SQLDisconnect(g_hDbc);  
      SQLFreeHandle(SQL_HANDLE_DBC, g_hDbc);  
      g_hDbc = NULL;  
   }  
   if (g_hEnv) {  
      SQLFreeHandle(SQL_HANDLE_ENV, g_hEnv);  
      g_hEnv = NULL;  
   }  
}  
  
BOOL MakeODBCConnection(TCHAR * pszServer) {  
   TCHAR szConnectionString[500];  
   TCHAR szOutConnectionString[500];  
   SQLSMALLINT iLen;  
   SQLRETURN rc;  
  
   _sntprintf_s(szConnectionString, 500, TEXT("DRIVER={SQL Server Native Client 11.0};Server=%s;Trusted_connection=yes;"), pszServer);  
   rc = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE,&g_hEnv);  
   if (SQL_SUCCESS != rc && SQL_SUCCESS_WITH_INFO != rc) {  
      printf("SQLAllocHandle(SQL_HANDLE_ENV...) failed\n");  
      return false;  
   }  
   rc = SQLSetEnvAttr(g_hEnv,SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, SQL_IS_UINTEGER);  
   if (SQL_SUCCESS != rc && SQL_SUCCESS_WITH_INFO != rc) {  
      printf("SQLSetEnvAttr failed\n");  
      SQLFreeHandle(SQL_HANDLE_ENV, g_hEnv);  
      return false;  
   }  
   rc = SQLAllocHandle( SQL_HANDLE_DBC, g_hEnv , &g_hDbc);  
   if (SQL_SUCCESS != rc && SQL_SUCCESS_WITH_INFO != rc) {  
      printf("SQLAllocHandle(SQL_HANDLE_DBC...) failed\n");  
      SQLFreeHandle(SQL_HANDLE_ENV, g_hEnv);  
      return false;  
   }  
   // Enable BCP  
   rc = SQLSetConnectAttr(g_hDbc, SQL_COPT_SS_BCP, (SQLPOINTER)SQL_BCP_ON, SQL_IS_INTEGER);  
   if (SQL_SUCCESS != rc && SQL_SUCCESS_WITH_INFO != rc) {  
      printf("SQLSetConnectAttr(.. SQL_COPT_SS_BCP, (SQLPOINTER)SQL_BCP_ON ...) failed\n");  
      ODBCCleanUp();  
      return false;  
   }  
   // connecting ...  
   rc = SQLDriverConnect(g_hDbc,NULL, (SQLTCHAR*)szConnectionString, SQL_NTS, (SQLTCHAR*)szOutConnectionString, 500, &iLen, SQL_DRIVER_NOPROMPT);  
   if (SQL_SUCCESS != rc && SQL_SUCCESS_WITH_INFO != rc) {  
      printf("SQLDriverConnect(SQL_HANDLE_DBC...) failed\n");  
      ODBCCleanUp();  
      return false;  
   }  
   return true;  
}  
  
BOOL BCPSetBulkMode(TCHAR * pszServer, TCHAR * pszQureryOut, char BCPType, TCHAR * pszDataFile) {  
   SQLRETURN rc;  
  
   if (!MakeODBCConnection(pszServer))  
      return false;  
   rc = bcp_init(g_hDbc, NULL, pszDataFile, NULL, DB_OUT);   // bcp init for queryout  
   if (SUCCEED != rc) {  
      printf("bcp_init failed\n");  
      ODBCCleanUp();  
      return false;  
   }  
   // setbulkmode  
   char ColTerm[] = "\t";  
   char RowTerm[] = "\r\n";  
   wchar_t wColTerm[] = L"\t";  
   wchar_t wRowTerm[] = L"\r\n";  
   BYTE * pColTerm = NULL;  
   int cbColTerm = NULL;  
   BYTE * pRowTerm = 0;  
   int cbRowTerm = 0;  
   int bulkmode = -1;  
  
   if (BCPType == 'c') {   // bcp -c  
      pColTerm = (BYTE*)ColTerm;  
      pRowTerm = (BYTE*)RowTerm;  
      cbColTerm = 1;  
      cbRowTerm = 2;  
      bulkmode = BCP_OUT_CHARACTER_MODE;  
   }  
   else  
      if (BCPType == 'w') {   // bcp -w   
         pColTerm = (BYTE*)wColTerm;  
         pRowTerm = (BYTE*)wRowTerm;  
         cbColTerm = 2;  
         cbRowTerm = 4;  
         bulkmode = BCP_OUT_WIDE_CHARACTER_MODE;  
      }  
      else  
         if (BCPType == 'n')   // bcp -n  
            bulkmode = BCP_OUT_NATIVE_MODE;  
         else  
            if (BCPType == 'N')   // bcp -n  
               bulkmode = BCP_OUT_NATIVE_TEXT_MODE;  
            else {  
               printf("unknown bcp mode\n");  
               ODBCCleanUp();  
               return false;  
            }  
            rc = bcp_setbulkmode(g_hDbc, bulkmode, pColTerm, cbColTerm, pRowTerm, cbRowTerm);  
            if (SUCCEED != rc) {  
               printf("bcp_setbulkmode failed\n");  
               ODBCCleanUp();  
               return false;  
            }  
            // set queryout TSQL statement  
            rc = bcp_control(g_hDbc, BCPHINTS , pszQureryOut);  
            if (SUCCEED != rc) {  
               printf("bcp_control(..BCP_OPTION_HINTS..) failed\n");  
               ODBCCleanUp();  
               return false;  
            }  
            // bcp copy  
            DBINT nRowsInserted = 0;  
            rc = bcp_exec(g_hDbc, &nRowsInserted);  
            if (SUCCEED != rc) {  
               printf("bcp_exec failed\n");  
               ODBCCleanUp();  
               return false;  
            }  
            printf("bcp done\n");  
            ODBCCleanUp();  
            return true;  
}  
  
int main() {  
   BCPSetBulkMode(TEXT("localhost"), TEXT("SELECT 'this is a bcp -c test', 1,2") , 'c', TEXT("bcpc.dat"));  
   BCPSetBulkMode(TEXT("localhost"), TEXT("SELECT 'this is a bcp -w test', 1,2") , 'w', TEXT("bcpw.dat"));  
   BCPSetBulkMode(TEXT("localhost"), TEXT("SELECT 'this is a bcp -c test', 1,2") , 'n', TEXT("bcpn.dat"));  
   BCPSetBulkMode(TEXT("localhost"), TEXT("SELECT 'this is a bcp -w test', 1,2") , 'N', TEXT("bcp_N.dat"));  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 함수](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
