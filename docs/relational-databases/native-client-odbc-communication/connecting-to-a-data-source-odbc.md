---
title: 데이터 원본에 연결 (ODBC) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eb1f2133aa335f266da75e00638dbb484dae1431
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784708"
---
# <a name="connecting-to-a-data-source-odbc"></a>데이터 원본에 연결(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  애플리케이션은 환경 및 연결 핸들을 할당하고 연결 특성을 설정한 후 데이터 원본이나 드라이버에 연결합니다. 연결에 사용할 수 있는 함수는 다음과 같이 세 가지가 있습니다.  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLBrowseConnect**  
  
 사용할 수 있는 다양 한 연결 문자열 옵션을 포함 하 여 데이터 원본에 연결 하는 방법에 대 한 자세한 내용은 [SQL Server Native Client 연결 문자열 키워드 사용](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조 하세요.  
  
## <a name="sqlconnect"></a>SQLConnect  
 **SQLConnect** 는 가장 간단한 연결 함수입니다. 이 함수는 데이터 원본 이름, 사용자 ID 및 암호의 세 가지 매개 변수를 허용합니다. 이 세 매개 변수에 데이터베이스에 연결 하는 데 필요한 모든 정보가 포함 된 경우 **SQLConnect** 를 사용 합니다. 이렇게 하려면 **sqldatasources**원본을 사용 하 여 데이터 원본 목록을 작성 합니다. 사용자에 게 데이터 원본, 사용자 ID 및 암호를 입력 하 라는 메시지 표시 그런 다음 **SQLConnect**를 호출 합니다.  
  
 **SQLConnect** 는 데이터 원본 이름, 사용자 ID 및 암호가 데이터 원본에 연결 하기에 충분 한 것으로 가정 하 고 odbc 드라이버에서 연결을 설정 하는 데 필요한 다른 모든 정보를 odbc 데이터 원본에 포함 합니다. [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 및 [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)와 달리 **SQLConnect** 는 연결 문자열을 사용 하지 않습니다.  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
 **SQLDriverConnect** 는 데이터 원본 이름, 사용자 ID 및 암호에 대 한 자세한 정보가 필요한 경우에 사용 됩니다. **SQLDriverConnect** 에 대 한 매개 변수 중 하나는 드라이버 관련 정보를 포함 하는 연결 문자열입니다. 다음과 같은 이유로 **SQLConnect** 대신 **SQLDriverConnect** 를 사용할 수 있습니다.  
  
-   연결 시 드라이버 관련 정보를 지정하려는 경우  
  
-   드라이버가 연결 정보를 묻는 메시지를 사용자에게 표시하도록 하려는 경우  
  
-   ODBC 데이터 원본을 사용하지 않고 연결하려는 경우  
  
 **SQLDriverConnect** 연결 문자열에는 ODBC 드라이버에서 지 원하는 모든 연결 정보를 지정 하는 일련의 키워드-값 쌍이 포함 되어 있습니다. 각 드라이버는 드라이버에서 지원하는 모든 연결 정보에 대해 해당 드라이버의 키워드와 함께 표준 ODBC 키워드(DSN, FILEDSN, DRIVER, UID, PWD 및 SAVEFILE)를 지원합니다. **SQLDriverConnect** 는 데이터 원본 없이 연결 하는 데 사용할 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 "DSN 없는" 연결을 만들도록 디자인 된 응용 프로그램은 로그인 ID, 암호, 네트워크 라이브러리, 연결할 서버 이름 및 기본값을 정의 하는 연결 문자열을 사용 하 여 **SQLDriverConnect** 를 호출할 수 있습니다. 사용할 데이터베이스입니다.  
  
 **SQLDriverConnect**를 사용 하는 경우 사용자에 게 필요한 연결 정보를 요청 하는 두 가지 옵션이 있습니다.  
  
-   애플리케이션 대화 상자  
  
     연결 정보를 묻는 메시지를 표시 하는 응용 프로그램 대화 상자를 만든 다음 NULL 창 핸들 및 *Drivercompletion* 가 SQL_DRIVER_NOPROMPT로 설정 된 상태에서 를 호출할 수 있습니다. 매개 변수를 이렇게 설정하면 ODBC 드라이버가 자체 대화 상자를 열지 않습니다. 이 방법은 애플리케이션의 사용자 인터페이스를 제어해야 하는 경우 사용합니다.  
  
-   드라이버 대화 상자  
  
     응용 프로그램을 코딩 하 여 유효한 창 핸들을 **SQLDriverConnect** 에 전달 하 고 *drivercompletion* 매개 변수를 SQL_DRIVER_COMPLETE, SQL_DRIVER_PROMPT 또는 SQL_DRIVER_COMPLETE_REQUIRED로 설정할 수 있습니다. 그러면 사용자에게 연결 정보를 묻는 대화 상자를 드라이버에서 생성합니다. 이 방법을 사용할 경우 애플리케이션 코드가 단순해집니다.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
 **SQLDriverConnect**와 같은 **SQLBrowseConnect**는 연결 문자열을 사용 합니다. 그러나 **SQLBrowseConnect**을 사용 하면 응용 프로그램에서 런타임에 데이터 소스와 함께 반복적으로 전체 연결 문자열을 생성할 수 있습니다. 이를 통해 애플리케이션에서는 다음 두 가지 작업이 가능해집니다.  
  
-   해당 정보를 묻는 고유의 대화 상자를 만듭니다. 따라서 해당 사용자 인터페이스에 대한 제어를 유지할 수 있습니다.  
  
-   특정 드라이버에서 사용할 수 있는 데이터 원본을 몇 개의 단계에 따라 시스템에서 찾습니다.  
  
     예를 들어 사용자는 먼저 네트워크에서 서버를 찾아서 선택한 다음 이 서버에서 드라이버가 액세스할 수 있는 데이터베이스를 찾습니다.  
  
 **SQLBrowseConnect** 가 성공적으로 연결 되 면 **SQLDriverConnect**에 대 한 후속 호출에서 사용할 수 있는 연결 문자열을 반환 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 항상 성공적인 **SQLConnect**, **SQLDriverConnect**또는 **SQLBrowseConnect**에 대 한 SQL_SUCCESS_WITH_INFO을 반환 합니다. SQL_SUCCESS_WITH_INFO 가져온 후 ODBC 응용 프로그램이 **SQLGetDiagRec** 를 호출 하면 다음과 같은 메시지가 표시 될 수 있습니다.  
  
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
  
 메시지 5701 및 5703은 정보 메시지일 뿐이므로 무시해도 됩니다. 그러나 5701이나 5703 이외의 메시지가 반환될 수 있으므로 SQL_SUCCESS_WITH_INFO 반환 코드를 주의해서 검토해야 합니다. 예를 들어 드라이버가 오래 된 카탈로그 저장 프로시저를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행 하는 서버에 연결 하는 경우 SQL_SUCCESS_WITH_INFO 후 **SQLGetDiagRec** 를 통해 반환 되는 오류 중 하나는 다음과 같습니다.  
  
```  
SqlState:   01000  
pfNative:   0  
szErrorMsg: "[Microsoft][SQL Server Native Client]The ODBC  
            catalog stored procedures installed on server  
            my65server are version 06.50.0193; version 07.00.0205  
            or later is required to ensure proper operation.  
            Please contact your system administrator."  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결에 대 한 응용 프로그램의 오류 처리 함수는 SQL_NO_DATA 반환 될 때까지 **SQLGetDiagRec** 를 호출 해야 합니다. 그런 다음 *pfNative* 코드가 5701 또는 5703 인 메시지 이외의 모든 메시지에 대해 작업을 수행 해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server &#40;ODBC와 통신&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
