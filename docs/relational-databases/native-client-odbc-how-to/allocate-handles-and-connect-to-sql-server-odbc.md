---
title: 핸들 할당 및 SQL 서버(ODBC)에 연결 | 마이크로 소프트 문서
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
ms.openlocfilehash: 5d26af711c07c4ea296d5351d0fcb0d1f9710706
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294528"
---
# <a name="allocate-handles-and-connect-to-sql-server-odbc"></a>핸들 할당 및 SQL Server에 연결(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-allocate-handles-and-connect-to-sql-server"></a>핸들을 할당하고 SQL Server에 연결하려면  
  
1.  ODBC 헤더 파일 Sql.h, Sqlext.h, Sqltypes.h을 포함합니다.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 드라이버별 헤더 파일인 Odbcss.h를 포함합니다.  
  
3.  **SQL_HANDLE_ENV 핸들 타입을** 사용하여 [SQLAllocHandle을](https://go.microsoft.com/fwlink/?LinkId=58396) 호출하여 ODBC를 초기화하고 환경 핸들을 할당합니다.  
  
4.  SQL_ATTR_ODBC_VERSION 설정된 **특성을** 사용하여 [SQLSetEnvAttr을](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) 호출하고 **값Ptr은** SQL_OV_ODBC3 설정하여 응용 프로그램이 ODBC 3.x 형식 함수 호출을 사용함을 나타냅니다.  
  
5.  선택적으로 [SQLSetEnvAttr을](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) 호출하여 다른 환경 옵션을 설정하거나 [SQLGetEnvAttr에](https://go.microsoft.com/fwlink/?LinkId=58403) 전화하여 환경 옵션을 가져옵니다.  
  
6.  연결 핸들을 할당하려면 **핸들 유형** SQL_HANDLE_DBC 사용하여 [SQLAllocHandle을](https://go.microsoft.com/fwlink/?LinkId=58396) 호출합니다.  
  
7.  선택적으로 [SQLSetConnectAttr를](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 호출하여 연결 옵션을 설정하거나 [SQLGetConnectAttr을](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) 호출하여 연결 옵션을 가져옵니다.  
  
8.  SQLConnect를 호출하여 기존 데이터 원본을 사용하여 에 연결합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
     Or  
  
     [SQLDriverConnect를](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 호출하여 연결 문자열을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]사용하여 에 연결합니다.  
  
     최소 전체 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 문자열은 다음 두 가지 형태 중 하나입니다.  
  
    ```  
    DSN=dsn_name;Trusted_connection=yes;  
    DRIVER={SQL Server Native Client 10.0};SERVER=server;Trusted_connection=yes;  
    ```  
  
     연결 문자열이 완료되지 않은 경우 **SQLDriverConnect에서** 필요한 정보를 묻는 메시지를 표시할 수 있습니다. 드라이버완성 매개 변수에 대해 *DriverCompletion* 지정된 값에 의해 제어됩니다.  
  
     \- 또는-  
  
     [SQLBrowseConnect를](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) 반복방식으로 여러 번 호출하여 연결 문자열을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]빌드하고 에 연결합니다.  
  
9. 선택적으로 [SQLGetInfo를](../../relational-databases/native-client-odbc-api/sqlgetinfo.md) 호출하여 데이터 원본에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대한 드라이버 특성 및 동작을 가져옵니다.  
  
10. 문을 할당하고 사용합니다.  
  
11. SQLDisconnect를 호출하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결을 끊고 새 연결에 대해 연결 핸들을 사용할 수 있도록 합니다.  
  
12. **핸들 유형** SQL_HANDLE_DBC [사용하여 SQLFreeHandle을](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) 호출하여 연결 핸들을 해제합니다.  
  
13. **SQL_HANDLE_ENV 핸들 유형을** 사용하여 **SQLFreeHandle을** 호출하여 환경 핸들을 해제합니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지해야 하는 경우 [Win32 암호화 API를](https://go.microsoft.com/fwlink/?LinkId=64532)통해 자격 증명을 암호화해야 합니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 기존 ODBC 데이터 원본을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 필요로 하지 않고 인스턴스에 연결 하기 위해 **SQLDriverConnect에** 대 한 호출을 보여 주며 있습니다. 불완전한 연결 문자열을 **SQLDriverConnect에**전달하면 ODBC 드라이버가 누락된 정보를 입력하라는 메시지를 표시합니다.  
  
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
  
  
