---
title: 핸들을 할당 하 고 SQL Server (ODBC)에 연결 | Microsoft Docs
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
- handles [ODBC]
- handles [ODBC], connection
- handles [ODBC], about handles
ms.assetid: 6172cd52-9c9a-467d-992f-def07f3f3bb1
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: adf51bdb9181030079d8b3f94628a1280299c856
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080860"
---
# <a name="allocate-handles-and-connect-to-sql-server-odbc"></a>핸들 할당 및 SQL Server에 연결(ODBC)
    
### <a name="to-allocate-handles-and-connect-to-sql-server"></a>핸들을 할당하고 SQL Server에 연결하려면  
  
1.  ODBC 헤더 파일 Sql.h, Sqlext.h, Sqltypes.h을 포함합니다.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 드라이버별 헤더 파일인 Odbcss.h를 포함합니다.  
  
3.  호출 [SQLAllocHandle](http://go.microsoft.com/fwlink/?LinkId=58396) 와 `HandleType` 의 SQL_HANDLE_ENV ODBC를 초기화 하 고 환경 핸들을 할당 합니다.  
  
4.  호출 [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md) 와 `Attribute` 를 sql_attr_odbc_version으로 설정 하 고 `ValuePtr` SQL_OV_ODBC3 나타내는로 설정 된 응용 프로그램이 ODBC 3.x 형식 함수 호출을 사용 합니다.  
  
5.  필요에 따라 호출 [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md) 다른 환경을 설정 옵션 또는 호출 [SQLGetEnvAttr](http://go.microsoft.com/fwlink/?LinkId=58403) 에 환경 옵션입니다.  
  
6.  호출 [SQLAllocHandle](http://go.microsoft.com/fwlink/?LinkId=58396) 와 `HandleType` 의 sql_handle_dbc 라는 연결 핸들을 할당 합니다.  
  
7.  을 호출 [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) 연결 옵션을 설정 하거나 호출 [SQLGetConnectAttr](../native-client-odbc-api/sqlgetconnectattr.md) 연결 옵션을 얻으려고 합니다.  
  
8.  기존 데이터 원본에 연결 하는 데 SQLConnect 호출 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
     또는  
  
     호출 [SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md) 에 연결할 연결 문자열을 사용 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
     최소 전체 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 문자열은 다음 두 가지 형태 중 하나입니다.  
  
    ```  
    DSN=dsn_name;Trusted_connection=yes;  
    DRIVER={SQL Server Native Client 10.0};SERVER=server;Trusted_connection=yes;  
    ```  
  
     연결 문자열이 완료되지 않은 경우 `SQLDriverConnect`에서 필요한 정보를 확인할 수 있습니다. 이 대 한 지정 된 값에 의해 제어 되는 *DriverCompletion* 매개 변수입니다.  
  
     \- 또는-  
  
     호출 [SQLBrowseConnect](../native-client-odbc-api/sqlbrowseconnect.md) 반복적으로 연결 문자열을 작성 하 고 연결할에 여러 번 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
9. 필요에 따라 호출 [SQLGetInfo](../native-client-odbc-api/sqlgetinfo.md) 드라이버 특성 및 동작을 얻으려면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본입니다.  
  
10. 문을 할당하고 사용합니다.  
  
11. 연결을 끊으려면 SQLDisconnect 호출 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 핸들를 새 연결에 사용할 수 있도록 합니다.  
  
12. 호출 [SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md) 와 `HandleType` 의 sql_handle_dbc 라는 연결 핸들을 해제 합니다.  
  
13. SQL_HANDLE_ENV라는 `SQLFreeHandle`으로 `HandleType`을 호출하여 환경 핸들을 해제합니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지하려면 [Win32 crypto API](http://go.microsoft.com/fwlink/?LinkId=64532)를 사용하여 자격 증명을 암호화해야 합니다.  
  
## <a name="example"></a>예제  
 이 예에서는 `SQLDriverConnect` 호출을 통해 ODBC 데이터 원본을 요구하지 않고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 방법을 보여 줍니다. 불완전한 연결 문자열을 `SQLDriverConnect`에 전달하면 ODBC 드라이버에서 누락된 정보를 입력하라는 메시지를 사용자에게 표시합니다.  
  
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
  
  