---
title: SQL Server용 Microsoft OLE DB 드라이버 | Microsoft Docs
description: SQL Server용 Microsoft OLE DB 드라이버
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server
- MSOLEDBSQL
- native data access [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: befcc84662b2273f81faaded76045d4d44b03e98
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687871"
---
# <a name="microsoft-ole-db-driver-for-sql-server"></a>SQL Server용 Microsoft OLE DB 드라이버
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server는 독립 실행형 데이터 액세스 응용 프로그래밍 인터페이스 (API) OLE DB에 도입 된 데는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]합니다. OLE DB Driver for SQL Server는 하나의 동적 연결 라이브러리 (DLL)에 SQL OLE DB 드라이버를 제공합니다. 또한 Windows Data Access Components(Windows DAC, 이전의 Microsoft Data Access Components 또는 MDAC)에서 제공하는 것보다 뛰어난 새로운 기능을 제공합니다. SQL Server용 OLE DB 드라이버를 사용하여 MARS(Multiple Active Result Sets), UDT(사용자 정의 데이터 형식), 쿼리 알림, 스냅샷 격리, XML 데이터 형식 지원 등 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 도입된 기능을 활용해야 하는 새 응용 프로그램을 작성하거나 기존 응용 프로그램을 개선할 수 있습니다.  
  
> [!NOTE]  
>  OLE DB Driver for SQL Server 용 OLE DB 드라이버 Windows DAC 응용 프로그램을 업데이트 하기 전에 고려해 야 할 문제에 대 한 정보 및 SQL Server 및 Windows DAC 간의 차이점 목록은 참조 하세요. [SQL에 대 한 OLE DB 드라이버로 응용 프로그램을 업데이트 하는 중입니다. MDAC에서 서버](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)합니다.  
  
 SQL Server용 OLE DB 드라이버는 Windows DAC와 함께 공급된 OLE DB 핵심 서비스와 연동하여 사용할 수 있지만 반드시 그래야 하는 것은 아니며 개별 응용 프로그램 요구 사항(예를 들어 연결 풀링이 필요한지 여부)에 따라 핵심 서비스를 사용할지 여부를 선택할 수 있습니다.  
  
 데이터 개체 (ADO (ActiveX) 응용 프로그램이 SQL Server 용 OLE DB 드라이버를 사용할 수 있지만와 함께에서 ADO를 사용 하는 것이 좋습니다.는 **DataTypeCompatibility** 연결 문자열 키워드 (또는 해당  **DataSource** 속성). ADO 응용 프로그램에 도입 된 새로운 기능을 이용할 수 있습니다 SQL Server 용 OLE DB 드라이버를 사용할 경우 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 는 OLE DB Driver for SQL Server를 통해 연결 문자열 키워드 또는 OLE DB 속성을 통해 사용할 수 있는 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다. ADO 사용 하 여 이러한 기능을 사용 하는 방법에 대 한 자세한 내용은 참조 [OLE DB Driver for SQL Server를 사용 하 여 ADO를 사용 하 여](../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md)입니다.  
  
 SQL Server용 OLE DB 드라이버는 OLE DB를 사용하여 SQL Server의 네이티브 데이터에 액세스하는 간단한 방법을 제공하도록 디자인되었습니다. 혁신적이 고 현재 Windows DAC 구성 요소를 이제 Microsoft Windows 플랫폼의 일부인 변경 하지 않고 새로운 데이터 액세스 기능을 발전 하는 방법을 제공 합니다.  
  
 SQL Server용 OLE DB 드라이버가 Windows DAC의 구성 요소를 사용하기는 하지만 Windows DAC의 특정 버전에 명시적으로 종속되지는 않습니다. SQL Server 용 OLE DB 드라이버에서 지 원하는 운영 체제와 함께 설치 된 Windows DAC의 버전을 사용 하 여 SQL Server 용 OLE DB 드라이버를 사용할 수 있습니다.  

 ## <a name="different-generations-of-ole-db-drivers"></a>OLE DB 드라이버의 다양 한 세대

SQL Server 용 Microsoft OLE DB 공급자의 세 가지 고유한 세대가 있습니다.

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1. SQL Server용 Microsoft OLE DB 공급자(SQLOLEDB)
합니다 [Microsoft OLE DB Provider for SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB)의 일부로 계속 제공 되 [Windows Data Access Components](https://msdn.microsoft.com/library/ms692897.aspx)합니다. 더 이상 유지 되지 않습니다 하 고 새로운 개발에 대 한이 드라이버를 사용 하는 것은 권장 되지 않습니다.

### <a name="2-sql-server-native-client-snac"></a>2. SQL Server Native Client(SNAC)
부터 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]서 [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md) OLE DB 공급자 인터페이스 (SQLNCLI)를 포함 하 고 함께 제공 되는 OLE DB 공급자 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 통해 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]합니다.

되었기 [2011에서 사용 중단 될 예정](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) 새로운 개발에이 드라이버를 사용 하는 권장 되지 않습니다. SNAC 수명 주기 및 제공 되는 다운로드에 대 한 자세한 내용은 참조 [SNAC 수명 주기를 설명](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)합니다.

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3. SQL Server용 Microsoft OLE DB 드라이버(MSOLEDBSQL)
OLE DB가 [다시 사용](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) 2018에 릴리스 합니다.

새 OLE DB 공급자는 SQL Server (MSOLEDBSQL)에 대 한 Microsoft OLE DB 드라이버 호출 됩니다. 새 공급자를 앞으로 최신 서버 기능을 사용 하 여 업데이트 됩니다.

> [!NOTE]
> 새 Microsoft OLE DB Driver for SQL Server 기존 응용 프로그램에서를 사용 하려면 SQLOLEDB 또는 SQLNCLI에서 MSOLEDBSQL 연결 문자열을 변환할 계획 해야 합니다.
  
## <a name="in-this-section"></a>섹션 내용  
[SQL Server용 OLE DB 드라이버를 사용해야 하는 경우](../oledb/when-to-use-oledb-driver-for-sql-server.md)  
 SQL Server용 OLE DB 드라이버를 Microsoft 데이터 액세스 기술과 연동하는 방법, Windows DAC 및 ADO.NET과 비교되는 특징을 설명하고, 사용할 데이터 액세스 기술을 결정하는 데 도움이 되는 팁을 제공합니다.  
  
 [SQL Server 기능용 OLE DB 드라이버](../oledb/features/oledb-driver-for-sql-server-features.md )  
 SQL Server 용 OLE DB 드라이버에서 지 원하는 기능을 설명 합니다.  
  
 [SQL Server용 OLE DB 드라이버로 응용 프로그램 빌드](../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
 SQL Server용 OLE DB 드라이버가 Windows DAC와 다른 점, 사용되는 구성 요소, ADO와 연동하는 방법 등 개발에 대한 개요를 제공합니다.  
  
 또한이 섹션에서는 SQL Server 설치 및 배포에 포함 된 OLE DB Driver for SQL Server 라이브러리를 재배포 하는 방법에 대 한 OLE DB 드라이버를 설명 합니다.  
  
 [SQL Server용 OLE DB 드라이버의 시스템 요구 사항](../oledb/system-requirements-for-oledb-driver-for-sql-server.md)  
 SQL Server 용 OLE DB 드라이버를 사용 하는 데 필요한 시스템 리소스에 설명 합니다.  
  
 [SQL Server 프로그래밍용 OLE DB 드라이버](../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
 SQL Server 용 OLE DB 드라이버를 사용 하는 방법에 대 한 정보를 제공 합니다.  
  
 [SQL Server 정보에 대한 더 많은 OLE DB 드라이버 찾기](../oledb/finding-more-oledb-driver-for-sql-server-information.md)  
 받기 및 외부 리소스에 대 한 링크를 포함 하 여 SQL Server 용 OLE DB 드라이버에 대 한 추가 리소스를 제공 합니다.  
  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2005 Native Client에서 응용 프로그램 업데이트](../oledb/applications/updating-an-application-from-sql-server-2005-native-client.md)    
 [OLE DB 방법 도움말 항목](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
