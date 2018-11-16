---
title: 핸들을 할당 하 고 SQL Server (ODBC)에 연결 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2144513a5f5de453c93215edcc2bb416d53781bc
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51677382"
---
# <a name="allocate-handles-and-connect-to-sql-server-odbc"></a>핸들 할당 및 SQL Server에 연결(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
### <a name="to-allocate-handles-and-connect-to-sql-server"></a>핸들을 할당하고 SQL Server에 연결하려면  
  
1.  ODBC 헤더 파일 Sql.h, Sqlext.h, Sqltypes.h을 포함합니다.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 드라이버별 헤더 파일인 Odbcss.h를 포함합니다.  
  
3.  호출 [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) 사용 하 여를 **HandleType** 의 SQL_HANDLE_ENV ODBC를 초기화 하 고 환경 핸들을 할당 합니다.  
  
4.  호출 [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) 사용 하 여 **특성** SQL_ATTR_ODBC_VERSION으로 설정 하 고 **ValuePtr** 응용 프로그램은 ODBC 3.x 형식 함수를 사용 하 여 나타내려면 SQL_OV_ODBC3으로 설정 호출합니다.  
  
5.  필요에 따라 호출 [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) 다른 환경을 설정 옵션 또는 호출 [SQLGetEnvAttr](https://go.microsoft.com/fwlink/?LinkId=58403) 환경 옵션을 가져오려고 합니다.  
  
6.  호출 [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) 사용 하 여를 **HandleType** 의 SQL_HANDLE_DBC 연결 핸들을 할당 합니다.  
  
7.  필요에 따라 호출할 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 연결 옵션을 설정 하거나 호출 [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) 연결 옵션을 가져오려고 합니다.  
  
8.  기존 데이터 원본에 연결 하는 데 SQLConnect 호출 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
     또는  
  
     호출 [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 연결 문자열에 연결 하는 데 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
     최소 전체 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 문자열은 다음 두 가지 형태 중 하나입니다.  
  
    ```  
    DSN=dsn_name;Trusted_connection=yes;  
    DRIVER={SQL Server Native Client 10.0};SERVER=server;Trusted_connection=yes;  
    ```  
  
     연결 문자열, 불완전 한 경우 **SQLDriverConnect** 필요한 정보를 확인할 수 있습니다. 지정 된 값으로 제어 합니다 *DriverCompletion* 매개 변수입니다.  
  
     \- 또는-  
  
     호출 [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) 연결 문자열을 작성 하 고 연결할는 반복적인 방식으로 여러 번 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
9. 필요에 따라 호출할 [SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md) 드라이버 특성과 동작을 가져오려면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본입니다.  
  
10. 문을 할당하고 사용합니다.  
  
11. 호출에서 연결을 끊으려면 SQLDisconnect [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 핸들를 새 연결에 사용할 수 있도록 합니다.  
  
12. 호출 [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) 사용 하 여를 **HandleType** SQL_HANDLE_DBC 하 여 연결 핸들입니다.  
  
13. 호출 **SQLFreeHandle** 사용 하 여를 **HandleType** SQL_HANDLE_ENV 환경 핸들입니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지하려면 [Win32 crypto API](https://go.microsoft.com/fwlink/?LinkId=64532)를 사용하여 자격 증명을 암호화해야 합니다.  
  
## <a name="example"></a>예제  
 이 예제에 대 한 호출을 보여 줍니다 **SQLDriverConnect** 인스턴스에 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기존 ODBC 데이터 원본을 요구 하지 않고 있습니다. 불완전 한 연결 문자열을 전달 하 여 **SQLDriverConnect**, ODBC 드라이버가 누락 된 정보를 입력 하 라는 메시지를 발생 합니다.  
  
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
  
  
