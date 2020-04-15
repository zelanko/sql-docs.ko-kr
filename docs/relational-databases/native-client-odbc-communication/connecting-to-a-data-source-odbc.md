---
title: 데이터 소스(ODBC)에 연결 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- checking connection states
- ODBC data sources, connections
- data sources [SQL Server Native Client]
- SQLBrowseConnect function
- ODBC applications, connections
- ODBC applications, data sources
- connections [SQL Server Native Client]
- SQLConnect function
- SQLDriveConnect function
- verifying connection states
- SQL Server Native Client ODBC driver, data sources
- SQL Server Native Client ODBC driver, connections
ms.assetid: ae30dd1d-06ae-452b-9618-8fd8cd7ba074
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ae59e0bdb005d296341970f4582100b15a0dfdf7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307724"
---
# <a name="connecting-to-a-data-source-odbc"></a>데이터 원본에 연결(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  애플리케이션은 환경 및 연결 핸들을 할당하고 연결 특성을 설정한 후 데이터 원본이나 드라이버에 연결합니다. 연결에 사용할 수 있는 함수는 다음과 같이 세 가지가 있습니다.  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLBrowseConnect**  
  
 다양한 연결 문자열 옵션을 포함하여 데이터 원본에 대한 연결을 사용할 수 있도록 하는 자세한 내용은 [SQL Server 네이티브 클라이언트에서 연결 문자열 키워드 사용을](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)참조하십시오.  
  
## <a name="sqlconnect"></a>SQLConnect  
 **SQLConnect는** 가장 간단한 연결 기능입니다. 이 함수는 데이터 원본 이름, 사용자 ID 및 암호의 세 가지 매개 변수를 허용합니다. 이러한 세 매개 변수에 데이터베이스에 연결하는 데 필요한 모든 정보가 포함된 경우 **SQLConnect를** 사용합니다. 이렇게 하려면 **SQLDataSource를**사용하여 데이터 원본 목록을 작성합니다. 데이터 원본, 사용자 ID 및 암호를 사용자에게 묻는 메시지를 표시합니다. 그런 다음 **SQLConnect를**호출합니다.  
  
 **SQLConnect는** 데이터 원본 이름, 사용자 ID 및 암호가 데이터 원본에 연결하기에 충분하고 ODBC 데이터 원본에 ODBC 드라이버가 연결하는 데 필요한 다른 모든 정보가 포함되어 있다고 가정합니다. [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 및 [SQLBrowseConnect와](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)달리 **SQLConnect는** 연결 문자열을 사용하지 않습니다.  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
 **SQLDriverConnect는** 데이터 원본 이름, 사용자 ID 및 암호보다 많은 정보가 필요한 경우에 사용됩니다. **SQLDriverConnect에** 대한 매개 변수 중 하나는 드라이버 관련 정보를 포함하는 연결 문자열입니다. 다음과 같은 이유로 **SQLDriverConnect** 대신 **SQLDriverConnect를** 사용할 수 있습니다.  
  
-   연결 시 드라이버 관련 정보를 지정하려는 경우  
  
-   드라이버가 연결 정보를 묻는 메시지를 사용자에게 표시하도록 하려는 경우  
  
-   ODBC 데이터 원본을 사용하지 않고 연결하려는 경우  
  
 **SQLDriverConnect** 연결 문자열에는 ODBC 드라이버에서 지원하는 모든 연결 정보를 지정하는 일련의 키워드 값 쌍이 포함되어 있습니다. 각 드라이버는 드라이버에서 지원하는 모든 연결 정보에 대해 해당 드라이버의 키워드와 함께 표준 ODBC 키워드(DSN, FILEDSN, DRIVER, UID, PWD 및 SAVEFILE)를 지원합니다. **SQLDriverConnect는** 데이터 원본 없이 연결하는 데 사용할 수 있습니다. 예를 들어 인스턴스에 "DSN 이없는" 연결을 사용하도록 설계된 응용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로그램은 로그인 ID, 암호, 네트워크 라이브러리, 연결할 서버 이름 및 사용할 기본 데이터베이스를 정의하는 연결 문자열로 **SQLDriverConnect를** 호출할 수 있습니다.  
  
 **SQLDriverConnect를**사용하는 경우 필요한 연결 정보를 사용자에게 묻는 두 가지 옵션이 있습니다.  
  
-   애플리케이션 대화 상자  
  
     연결 정보를 묻는 응용 프로그램 대화 상자를 만든 다음 NULL 창 핸들을 사용 하 고 *Driver완성* 을 SQL_DRIVER_NOPROMPT 설정 **하는 SQLDriverConnect를** 호출할 수 있습니다. 매개 변수를 이렇게 설정하면 ODBC 드라이버가 자체 대화 상자를 열지 않습니다. 이 방법은 애플리케이션의 사용자 인터페이스를 제어해야 하는 경우 사용합니다.  
  
-   드라이버 대화 상자  
  
     응용 프로그램을 코딩하여 유효한 창 핸들을 **SQLDriverConnect에** 전달하고 *DriverComplete* 매개 변수를 SQL_DRIVER_COMPLETE, SQL_DRIVER_PROMPT 또는 SQL_DRIVER_COMPLETE_REQUIRED 설정할 수 있습니다. 그러면 사용자에게 연결 정보를 묻는 대화 상자를 드라이버에서 생성합니다. 이 방법을 사용할 경우 애플리케이션 코드가 단순해집니다.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
 **SQLDriverConnect와**같은 **SQLBrowseConnect는**연결 문자열을 사용합니다. 그러나 **SQLBrowseConnect를**사용 하 여 응용 프로그램은 런타임에 데이터 원본과 반복적으로 전체 연결 문자열을 생성할 수 있습니다. 이를 통해 애플리케이션에서는 다음 두 가지 작업이 가능해집니다.  
  
-   해당 정보를 묻는 고유의 대화 상자를 만듭니다. 따라서 해당 사용자 인터페이스에 대한 제어를 유지할 수 있습니다.  
  
-   특정 드라이버에서 사용할 수 있는 데이터 원본을 몇 개의 단계에 따라 시스템에서 찾습니다.  
  
     예를 들어 사용자는 먼저 네트워크에서 서버를 찾아서 선택한 다음 이 서버에서 드라이버가 액세스할 수 있는 데이터베이스를 찾습니다.  
  
 **SQLBrowseConnect가** 성공적인 연결을 완료하면 SQLDriverConnect 에 대한 후속 호출에서 사용할 수 있는 연결 문자열을 **반환합니다.**  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 항상 성공적인 **SQLConnect,** **SQLDriverConnect**또는 **SQLBrowseConnect에서**SQL_SUCCESS_WITH_INFO 반환합니다. ODBC 응용 프로그램이 SQL_SUCCESS_WITH_INFO 후 **SQLGetDiagRec를** 호출하면 다음 메시지를 받을 수 있습니다.  
  
 5701  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터 원본에 정의된 기본 데이터베이스 또는 데이터 원본에 기본 데이터베이스가 없는 경우 연결에 사용된 로그인 ID에 대해 정의된 기본 데이터베이스에 사용자의 컨텍스트를 가져옴을 나타냅니다.  
  
 5703  
 서버에서 사용 중인 언어를 나타냅니다.  
  
 다음 예에서는 시스템 관리자가 연결을 성공적으로 수행한 경우 반환되는 메시지를 보여 줍니다.  
  
```  
szSqlState = "01000", *pfNativeError = 5701,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
       Changed database context to 'pubs'."  
szSqlState = "01000", *pfNativeError = 5703,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
       Changed language setting to 'us_english'."  
```  
  
 메시지 5701 및 5703은 정보 메시지일 뿐이므로 무시해도 됩니다. 그러나 5701이나 5703 이외의 메시지가 반환될 수 있으므로 SQL_SUCCESS_WITH_INFO 반환 코드를 주의해서 검토해야 합니다. 예를 들어 드라이버가 오래된 카탈로그 저장 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로시저로 인스턴스를 실행하는 서버에 연결하는 경우 SQL_SUCCESS_WITH_INFO 후 **SQLGetDiagRec를** 통해 반환된 오류 중 하나는 다음과 같은 것입니다.  
  
```  
SqlState:   01000  
pfNative:   0  
szErrorMsg: "[Microsoft][SQL Server Native Client]The ODBC  
            catalog stored procedures installed on server  
            my65server are version 06.50.0193; version 07.00.0205  
            or later is required to ensure proper operation.  
            Please contact your system administrator."  
```  
  
 연결에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 응용 프로그램의 오류 처리 함수는 SQL_NO_DATA 반환될 때까지 **SQLGetDiagRec를** 호출 해야 합니다. 그런 다음 *pfNative* 코드가 5701 또는 5703인 메시지 이외의 메시지에 대해 작동해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL 서버와 통신 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
