---
title: 헤더 및 라이브러리 파일
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- header files [SQL Server Native Client]
- SQLNCLI, header files
- OLE DB, header files
- library files [SQL Server Native Client]
- SQL Server Native Client, header files
- data access [SQL Server Native Client], header files
- SQL Server Native Client ODBC driver,header files
- data access [SQL Server Native Client], library files
- SQL Server Native Client, library files
- ODBC applications, header files
- SQLNCLI, library files
ms.assetid: 69889a98-7740-4667-aecd-adfc0b37f6f0
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 57e4b7c27ed32beaa1139300fdb83c4fb79583df
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81388463"
---
# <a name="using-the-sql-server-native-client-header-and-library-files"></a>SQL Server Native Client 헤더 및 라이브러리 파일 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더 및 라이브러리 파일은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 함께 설치됩니다. 애플리케이션을 개발할 때는 개발에 필요한 모든 파일을 사용자의 개발 환경으로 복사하고 설치해야 합니다. Native Client를 설치 하 고 재배포 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 하는 방법에 대 한 자세한 내용은 [SQL Server Native Client 설치](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)를 참조 하세요.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더 및 라이브러리 파일은 다음 위치에 설치됩니다.  
  
 *% PROGRAM FILES%* \Microsoft SQL Server\110\SDK  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더 파일(sqlncli.h)을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 데이터 액세스 기능을 사용자의 사용자 지정 애플리케이션에 추가할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더 파일에는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 새로운 기능을 활용하는 데 필요한 모든 정의, 특성, 속성 및 인터페이스가 포함되어 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더 파일 외에도 ODBC의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] BCP(대량 복사 프로그램) 기능에 사용되는 내보내기 라이브러리인 sqlncli11.lib 라이브러리 파일도 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더 파일은 Microsoft Data Access Components(MDAC)에서 사용되는 sqloledb.h 및 odbcss.h 헤더 파일과 호환되지만 SQLOLEDB(MDAC에 포함된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용 OLE DB Provider)에 사용되는 CLSID 또는 XML 기능([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 지원되지 않음)에 사용되는 기호는 포함하지 않습니다.  
  
 여러 개의 ODBC 애플리케이션이 동일한 프로그램에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더(sqlncli.h) 및 odbcss.h를 참조할 수 없습니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 기능을 전혀 사용하지 않더라도 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더 파일이 기존 odbcss.h 대신 사용됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB Provider를 사용하는 OLE DB 애플리케이션은 sqlncli.h만 참조하면 됩니다. MDAC(SQLOLEDB)와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB Provider를 모두 사용하는 애플리케이션은 sqloledb.h 및 sqlncli.h를 모두 참조할 수 있지만 sqloledb.h를 먼저 참조해야 합니다.  
  
## <a name="using-the-sql-server-native-client-header-file"></a>SQL Server Native Client 헤더 파일 사용  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더 파일을 사용 하려면 C/c + + 프로그래밍 코드 내에서 **include** 문을 사용 해야 합니다. 다음 섹션에서는 OLE DB 및 ODBC 애플리케이션에서 이를 수행하는 방법을 설명합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더 및 라이브러리 파일은 Visual Studio C++ 2002 이상을 사용해야 컴파일할 수 있습니다.  
  
### <a name="ole-db"></a>OLE DB  
 OLE DB 애플리케이션에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더 파일을 사용하려면 다음 프로그래밍 코드 행을 사용합니다.  
  
```  
#define _SQLNCLI_OLEDB_  
include "sqlncli.h";  
```  
  
> [!NOTE]  
>  애플리케이션에서 OLE DB 및 ODBC API를 모두 사용하는 경우에는 위의 코드에서 첫 번째 행을 생략해야 합니다. 또한 응용 프로그램에 sqloledb의 **include** 문이 있는 경우 sqlncli에 대 한 **include** 문이 그 뒤에와 야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 통해 데이터 원본에 대한 연결을 만들 때 공급자 이름 문자열에는 "SQLNCLI11"을 사용합니다.  
  
### <a name="odbc"></a>ODBC  
 ODBC 애플리케이션에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더 파일을 사용하려면 다음 프로그래밍 코드 행을 사용합니다.  
  
```  
#define _SQLNCLI_ODBC_  
include "sqlncli.h";  
```  
  
> [!NOTE]  
>  애플리케이션에서 OLE DB 및 ODBC API를 모두 사용하는 경우에는 위의 코드에서 첫 번째 행을 생략해야 합니다. 또한 애플리케이션에 odbcss.h에 대한 `#include` 문이 있는 경우 이를 제거해야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 통해 데이터 원본에 대한 연결을 만들 때 드라이버 이름 문자열에는 "SQL Server Native Client 11.0"을 사용합니다.  
  
## <a name="component-names-and-properties-by-version"></a>버전별 구성 요소 이름 및 속성  
  
|속성|SQL Server Native Client<br /><br /> SQL Server 2005|SQL Server Native Client 10.0<br /><br /> SQL Server 2008|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]|MDAC|  
|--------------|--------------------------------------------------|-------------------------------------------------------|---------------------------------------------------------------|----------|  
|ODBC 드라이버 이름|SQL Native Client|SQL Server Native Client 10.0|SQL Server Native Client 11.0|SQL Server|  
|ODBC 헤더 파일 이름|Sqlncli.h|Sqlncli.h|Sqlncli.h|Odbcss.h|  
|ODBC 드라이버 DLL|Sqlncli.dll|Sqlncl10.dll|Sqlncl11.dll|sqlsrv32.dll|  
|BCP API용 ODBC 라이브러리 파일|Sqlncli.lib|Sqlncli10.lib|Sqlncli11.lib|Odbcbcp.lib|  
|BCP API용 ODBC DLL|Sqlncli.dll|Sqlncli10.dll|Sqlncli11.dll|Odbcbcp.dll|  
|OLE DB PROGID|SQLNCLI|SQLNCLI10|SQLNCLI11|SQLOLEDB|  
|OLE DB 헤더 파일 이름|Sqlncli.h|Sqlncli.h|Sqlncli.h|Sqloledb.h|  
|OLE DB Provider DLL|Sqlncli.dll|Sqlncli10.dll|Sqlncli11.dll|Sqloledb.dll|  
  
 sqlncli.h는 SQLNCLI_VER 매크로를 통해 여러 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 지원합니다. 기본적으로 SQLNCLI_VER의 기본값은 최신 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client입니다. sqlncli11.dll 대신 sqlncli10.dll을 사용하는 애플리케이션을 작성하려면 SQLNCLI_VER를 10으로 설정합니다.  
  
## <a name="static-linking-and-bcp-functions"></a>정적 연결 및 BCP 함수  
 애플리케이션에서 BCP 함수를 사용하는 경우 애플리케이션의 연결 문자열에 애플리케이션을 컴파일하는 데 사용된 헤더 파일 및 라이브러리가 함께 제공되는 동일한 버전의 드라이버를 지정해야 합니다.  
  
 예를 들어, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client와 \Program Files\Microsoft SQL Server\110\SDK의 연결된 라이브러리 파일(sqlncli11.lib) 및 헤더 파일(sqlncli.h)을 사용하여 애플리케이션을 컴파일하는 경우 연결 문자열에 &quot;DRIVER={SQL Server Native Client 11.0}&quot;을 지정해야 합니다(예로 ODBC 사용).  
  
 자세한 내용은 [대량 복사 작업 수행](../../../relational-databases/native-client/features/performing-bulk-copy-operations.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client를 사용하여 애플리케이션 빌드](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
