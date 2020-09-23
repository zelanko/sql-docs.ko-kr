---
title: Windows ODBC 드라이버에서 연결 복원
description: 서버에서 유휴 연결을 닫을 때 ODBC 드라이버의 연결 복원력이 투명하게 연결을 복원하고 애플리케이션 동작을 향상시키는 방법을 알아봅니다.
ms.custom: ''
ms.date: 09/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 614fa0b4-e9fd-4c68-aab3-183f9b9df143
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01b8da5d2a7f7c0e49d54a9fe237367ab3ed405f
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288125"
---
# <a name="connection-resiliency-in-the-windows-odbc-driver"></a>Windows ODBC 드라이버에서 연결 복원
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  애플리케이션이 [!INCLUDE[ssAzure](../../../includes/ssazure_md.md)]에 연결되어 있는지 확인하려면 Windows 기반 ODBC 드라이버가 유휴 연결을 복원하면 됩니다.  
  
> [!IMPORTANT]  
>  연결 복원력 기능은 Microsoft Azure SQL Database 및 SQL Server 2014 이상 서버 버전에서 지원됩니다.  
  
 유휴 연결 복원력에 대한 자세한 내용은 [Technical Article - Idle Connection Resiliency](https://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/Idle%20Connection%20Resiliency.docx)(기술 문서 - 유휴 연결 복원력)를 참조하세요.
  
 재연결 동작을 제어하기 위해 Windows 기반 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에는 다음과 같은 두 가지 옵션이 있습니다.  
  
-   연결 다시 시도 횟수  
  
     연결 다시 시도 횟수는 연결 오류가 발생하는 경우 다시 연결을 시도할 수 있는 횟수를 제어합니다. 유효한 값은 0에서 255 사이입니다. 0은 다시 연결을 시도하지 않는다는 것입니다. 기본값은 다시 연결을 한 번 시도하는 것입니다.  
  
     다음과 같이 하면 연결 다시 시도 횟수를 수정할 수 있습니다.  
  
    -   **연결 다시 시도 횟수** 컨트롤을 사용하여 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용하는 데이터 원본을 정의하거나 수정합니다.  
  
    -   **ConnectRetryCount** 연결 문자열 키워드를 사용합니다.  
  
     연결 다시 시도 횟수를 검색하려면 **SQL_COPT_SS_CONNECT_RETRY_COUNT**(읽기 전용) 연결 특성을 사용합니다. 애플리케이션이 연결 복원력을 지원하지 않는 서버에 연결된 경우 **SQL_COPT_SS_CONNECT_RETRY_COUNT**에서 0을 반환합니다.  
  
-   연결 다시 시도 간격  
  
     연결 다시 시도 간격은 각 연결 다시 시도 간의 시간(초)을 지정합니다. 유효한 값은 1~60입니다. 다시 연결하기 위한 총 시간은 연결 시간 제한(SQLSetStmtAttr에서 SQL_ATTR_QUERY_TIMEOUT)을 초과할 수 없습니다. 기본값은 10초입니다.  
  
     다음과 같이 하면 연결 다시 시도 간격을 수정할 수 있습니다.  
  
    -   **연결 다시 시도 간격** 컨트롤을 사용하여 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용하는 데이터 원본을 정의하거나 수정합니다.  
  
    -   **ConnectRetryInterval** 연결 문자열 키워드를 사용합니다.  
  
     연결 다시 시도 간격 시간을 검색하려면 **SQL_COPT_SS_CONNECT_RETRY_INTERVAL**(읽기 전용) 연결 특성을 사용합니다.  
  
 애플리케이션이 SQL_DRIVER_COMPLETE_REQUIRED에 연결하고 나중에 끊어진 연결에 대해 문을 실행하려는 경우 ODBC 드라이버가 대화 상자를 다시 표시하지 않습니다. 복구가 진행 중인 동안  
  
-   복구 중에 **SQLGetConnectAttr(SQL_COPT_SS_CONNECTION_DEAD)** 에 대한 호출은 **SQL_CD_FALSE**를 반환해야 합니다.  
  
-   복구가 실패한 경우 **SQLGetConnectAttr(SQL_COPT_SS_CONNECTION_DEAD)** 에 대한 호출은 **SQL_CD_TRUE**를 반환해야 합니다.  
  
 다음 상태 코드는 서버에서 명령을 실행하는 함수에 의해 반환됩니다.  
  
|시스템 상태|메시지|  
|-----------|-------------|  
|IMC01|연결이 끊어져서 복구가 불가능합니다. 클라이언트 드라이버가 한 번 이상 연결을 복구하려고 시도했지만 모든 시도가 실패했습니다. 복구 시도 횟수를 늘리려면 ConnectRetryCount의 값을 늘립니다.|  
|IMC02|서버가 복구 시도를 승인하지 않았으므로 연결 복구가 가능하지 않습니다.|  
|IMC03|서버가 복구 시도 중 요청된 정확한 클라이언트 TDS 버전을 유지하지 않았기 때문에 연결 복구가 가능하지 않습니다.|  
|IMC04|서버가 복구 시도 중 요청된 정확한 서버의 주 버전을 유지하지 않았기 때문에 연결 복구가 가능하지 않습니다.|  
|IMC05|연결이 끊어져서 복구가 불가능합니다. 서버에서 연결을 복구할 수 없다고 표시합니다. 연결을 복원하려고 시도하지 않았습니다.|  
|IMC06|연결이 끊어져서 복구가 불가능합니다. 클라이언트 드라이버에서 연결을 복구할 수 없다고 표시합니다. 연결을 복원하려고 시도하지 않았습니다.|  
  
## <a name="example"></a>예제  
 다음 샘플에는 두 가지 함수가 포함되어 있습니다. **func1**은 Windows 기반 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용하는 DSN(데이터 원본 이름)과 연결할 수 있는 방법을 보여 줍니다. DSN은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하고 사용자 ID를 지정합니다. 그러면 **func1**이 **SQL_COPT_SS_CONNECT_RETRY_COUNT**를 사용하여 연결 다시 시도 횟수를 검색합니다.  
  
 **func2** 가 **SQLDriverConnect**, **ConnectRetryCount** 연결 문자열 키워드 및 연결 특성을 사용하여 연결 다시 시도 및 다시 시도 간격에 대한 설정을 검색합니다.  
  
```  
// Connection_resiliency.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
#include <sqlext.h>  
#include <msodbcsql.h>  
  
void func1() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
   SQLSMALLINT i = 21;  

   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLCHAR*) "MyDSN", SQL_NTS, (SQLCHAR*) "userID", SQL_NTS, (SQLCHAR*) "password_for_userID", SQL_NTS);  
            retcode = SQLGetConnectAttr(hdbc, SQL_COPT_SS_CONNECT_RETRY_COUNT, &i, SQL_IS_INTEGER, NULL);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}
  
void func2() {  
   SQLHENV henv;  
   SQLHDBC hdbc1;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
   SQLSMALLINT i = 21;  
  
#define MAXBUFLEN 255  
  
   SQLCHAR ConnStrIn[MAXBUFLEN] = "DRIVER={ODBC Driver 17 for SQL Server};SERVER=server_that_supports_connection_resiliency;UID=userID;PWD= password_for_userID;ConnectRetryCount=2";
   SQLCHAR ConnStrOut[MAXBUFLEN];

   SQLSMALLINT cbConnStrOut = 0;  
 
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3_80, SQL_IS_INTEGER);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            // SQLSetConnectAttr(hdbc1, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect(hdbc1, NULL, ConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
         }  
         retcode = SQLGetConnectAttr(hdbc1, SQL_COPT_SS_CONNECT_RETRY_COUNT, &i, SQL_IS_INTEGER, NULL);  
         retcode = SQLGetConnectAttr(hdbc1, SQL_COPT_SS_CONNECT_RETRY_INTERVAL, &i, SQL_IS_INTEGER, NULL);  
      }  
   }  
}  
  
int main() {  
   func1();  
   func2();  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [Windows의 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
