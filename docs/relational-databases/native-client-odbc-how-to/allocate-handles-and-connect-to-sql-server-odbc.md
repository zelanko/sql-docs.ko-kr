---
description: 핸들 할당 및 SQL Server에 연결(ODBC)
title: 핸들을 할당 하 고 SQL Server에 연결 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- handles [ODBC]
- handles [ODBC], connection
- handles [ODBC], about handles
ms.assetid: 6172cd52-9c9a-467d-992f-def07f3f3bb1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 100973ff2e7ae4d3bf066bfe49f09aa3a979230f
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866967"
---
# <a name="allocate-handles-and-connect-to-sql-server-odbc"></a>핸들 할당 및 SQL Server에 연결(ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
### <a name="to-allocate-handles-and-connect-to-sql-server"></a>핸들을 할당하고 SQL Server에 연결하려면  
  
1.  ODBC 헤더 파일 Sql.h, Sqlext.h, Sqltypes.h을 포함합니다.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 드라이버별 헤더 파일인 Odbcss.h를 포함합니다.  
  
3.  [SQLAllocHandle](../../odbc/reference/syntax/sqlallochandle-function.md) 를 SQL_HANDLE_ENV **HandleType** 로 호출 하 여 ODBC를 초기화 하 고 환경 핸들을 할당 합니다.  
  
4.  SQL_ATTR_ODBC_VERSION **로 설정 된** **특성** 을 사용 하 여 SQLSetEnvAttr를 호출 하 고, [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) 로 SQL_OV_ODBC3 설정 하 여 응용 프로그램에서 ODBC 3. x 형식의 함수 호출을 사용 하도록 지정 합니다.  
  
5.  필요에 따라 [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) 를 호출 하 여 다른 환경 옵션을 설정 하거나 [SQLGetEnvAttr](../../odbc/reference/syntax/sqlgetenvattr-function.md) 를 호출 하 여 환경 옵션을 가져옵니다.  
  
6.  [SQLAllocHandle](../../odbc/reference/syntax/sqlallochandle-function.md) 를 SQL_HANDLE_DBC **HandleType** 로 호출 하 여 연결 핸들을 할당 합니다.  
  
7.  필요에 따라 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 를 호출 하 여 연결 옵션을 설정 하거나 [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) 를 호출 하 여 연결 옵션을 가져옵니다.  
  
8.  SQLConnect를 호출 하 여 기존 데이터 원본을 사용 하 여에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
     또는  
  
     [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 를 호출 하 여 연결 문자열을 사용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
     최소 전체 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 문자열은 다음 두 가지 형태 중 하나입니다.  
  
    ```  
    DSN=dsn_name;Trusted_connection=yes;  
    DRIVER={SQL Server Native Client 10.0};SERVER=server;Trusted_connection=yes;  
    ```  
  
     연결 문자열이 완전 하지 않은 경우 **SQLDriverConnect** 는 필요한 정보를 묻는 메시지를 표시할 수 있습니다. *Drivercompletion* 매개 변수에 지정 된 값으로 제어 됩니다.  
  
     \- 또는 -  
  
     [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) 를 반복적으로 여러 번 호출 하 여 연결 문자열을 작성 하 고에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
9. 필요에 따라 [SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md) 를 호출 하 여 데이터 원본에 대 한 드라이버 특성 및 동작을 가져옵니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
10. 문을 할당하고 사용합니다.  
  
11. SQLDisconnect를 호출 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결을 끊고 연결 핸들을 새 연결에 사용할 수 있도록 합니다.  
  
12. **HandleType** of SQL_HANDLE_DBC로 [sqlfreehandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) 을 호출 하 여 연결 핸들을 해제 합니다.  
  
13. **HandleType** of SQL_HANDLE_ENV로 **sqlfreehandle** 을 호출 하 여 환경 핸들을 해제 합니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지하려면 [Win32 crypto API](/windows/win32/seccrypto/cryptography-reference)를 사용하여 자격 증명을 암호화해야 합니다.  
  
## <a name="example"></a>예제  
 이 예에서는 **SQLDriverConnect** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기존 ODBC 데이터 원본을 요구 하지 않고 인스턴스에 연결 하기 위해 SQLDriverConnect를 호출 하는 방법을 보여 줍니다. **SQLDriverConnect**에 불완전 한 연결 문자열을 전달 하면 ODBC 드라이버가 누락 된 정보를 입력 하 라는 메시지를 표시 합니다.  
  
```  
#define MAXBUFLEN   255  
  
SQLHENV      henv = SQL_NULL_HENV;  
SQLHDBC      hdbc1 = SQL_NULL_HDBC;  
SQLHSTMT      hstmt1 = SQL_NULL_HSTMT;  
  
SQLCHAR      ConnStrIn[MAXBUFLEN] =  
         "DRIVER={SQL Server Native Client 10.0};SERVER=MyServer";  
  
SQLCHAR      ConnStrOut[MAXBUFLEN];  
SQLSMALLINT   cbConnStrOut = 0;  
  
// Make connection without data source. Ask that driver   
// prompt if insufficient information. Driver returns  
// SQL_ERROR and application prompts user  
// for missing information. Window handle not needed for  
// SQL_DRIVER_NOPROMPT.  
retcode = SQLDriverConnect(hdbc1,      // Connection handle  
                  NULL,         // Window handle  
                  ConnStrIn,      // Input connect string  
                  SQL_NTS,         // Null-terminated string  
                  ConnStrOut,      // Address of output buffer  
                  MAXBUFLEN,      // Size of output buffer  
                  &cbConnStrOut,   // Address of output length  
                  SQL_DRIVER_PROMPT);  
```  
  
