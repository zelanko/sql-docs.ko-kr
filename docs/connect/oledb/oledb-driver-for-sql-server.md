---
title: SQL Server용 Microsoft OLE DB 드라이버 | Microsoft Docs
description: SQL Server용 Microsoft OLE DB 드라이버
ms.custom: ''
ms.date: 02/12/2019
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
manager: jroth
ms.openlocfilehash: bf7f80fb6488e4508d4a7abda59d690e7f7dc805
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66795864"
---
# <a name="microsoft-ole-db-driver-for-sql-server"></a>SQL Server용 Microsoft OLE DB 드라이버
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

OLE DB Driver for SQL Server는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 도입된 기술로, OLE DB에 사용되는 독립 실행형 데이터 액세스 API(애플리케이션 프로그래밍 인터페이스)입니다. OLE DB Driver for SQL Server는 하나의 DLL(동적 연결 라이브러리)로 SQL OLE DB 드라이버를 제공합니다. 또한 Windows Data Access Components(Windows DAC, 이전의 Microsoft Data Access Components 또는 MDAC)에서 제공하는 것보다 뛰어난 새로운 기능을 제공합니다. OLE DB Driver for SQL Server를 사용하여 MARS(Multiple Active Result Sets), UDT(사용자 정의 데이터 형식), 쿼리 알림, 스냅샷 격리, XML 데이터 형식 지원 등 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 도입된 기능을 활용해야 하는 기존 애플리케이션을 개선하거나 새 애플리케이션을 만들 수 있습니다.  
  
> [!NOTE]  
> OLE DB Driver for SQL Server와 Windows DAC 간의 차이점 목록과 Windows DAC 애플리케이션을 OLE DB Driver for SQL Server로 업데이트하기 전에 고려해야 할 문제에 대한 자세한 내용은 [MDAC에서 OLE DB Driver for SQL Server로 애플리케이션 업데이트](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)를 참조하세요.  

> [!IMPORTANT]
> 이전의 [Microsoft OLE DB Provider for SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)(SQLOLEDB) 및 [SQL Server Native Client OLE DB](../../relational-databases/native-client/sql-server-native-client.md) 공급자(SQLNCLI)는 계속 사용되지 않으며, 새로운 개발 작업에 사용하지 않는 것이 좋습니다.
  
 SQL Server용 OLE DB 드라이버는 Windows DAC와 함께 공급된 OLE DB 핵심 서비스와 연동하여 사용할 수 있지만 반드시 그래야 하는 것은 아니며 개별 애플리케이션 요구 사항(예를 들어 연결 풀링이 필요한지 여부)에 따라 핵심 서비스를 사용할지 여부를 선택할 수 있습니다.  
  
 ADO(ActiveX Data Objects) 애플리케이션은 OLE DB Driver for SQL Server를 사용할 수 있지만, **DataTypeCompatibility** 연결 문자열 키워드(또는 해당 **DataSource** 속성)와 함께 ADO를 사용하는 것이 좋습니다. OLE DB Driver for SQL Server를 사용하는 경우, ADO 애플리케이션은 연결 문자열 키워드 또는 OLE DB 속성이나 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 통해 OLE DB Driver for SQL Server에서 제공되는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]의 새로운 기능을 이용할 수 있습니다. ADO에서 이러한 기능을 사용하는 방법에 대한 자세한 내용은 [OLE DB Driver for SQL Server에서 ADO 사용](../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md)을 참조하세요.  
  
 SQL Server용 OLE DB 드라이버는 OLE DB를 사용하여 SQL Server의 네이티브 데이터에 액세스하는 간단한 방법을 제공하도록 디자인되었습니다. SQL Server용 OLE DB 드라이버를 사용하면 이제 Microsoft Windows 플랫폼에 통합된 현재 Windows DAC 구성 요소를 변경하지 않고 새로운 데이터 액세스 기능을 혁신적으로 발전시킬 수 있습니다.  
  
 SQL Server용 OLE DB 드라이버가 Windows DAC의 구성 요소를 사용하기는 하지만 Windows DAC의 특정 버전에 명시적으로 종속되지는 않습니다. OLE DB Driver for SQL Server에서 지원하는 운영 체제에 설치된 모든 Windows DAC 버전에서 OLE DB Driver for SQL Server를 사용할 수 있습니다.  

 ## <a name="different-generations-of-ole-db-drivers"></a>OLE DB 드라이버의 다양한 세대

Microsoft OLE DB Provider for SQL Server의 세 가지 고유한 세대가 있습니다.

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1. SQL Server용 Microsoft OLE DB 공급자(SQLOLEDB)
[Microsoft OLE DB Provider for SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)(SQLOLEDB)는 [Windows Data Access Components](https://msdn.microsoft.com/library/ms692897.aspx)의 일부로 계속 제공됩니다. 더 이상 유지 관리되지 않으며, 새로운 개발에 이 드라이버를 사용하지 않는 것이 좋습니다.

### <a name="2-sql-server-native-client-snac"></a>2. SQL Server Native Client(SNAC)
[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터 [SNAC(SQL Server Native Client)](../../relational-databases/native-client/sql-server-native-client.md)가 OLE DB 공급자 인터페이스(SQLNCLI)를 포함하며, [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ~ [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 제공된 OLE DB 공급자입니다.

[2011년에 사용되지 않는 드라이버로 발표](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)되었으며, 새로운 개발에 이 드라이버를 사용하지 않는 것이 좋습니다. SNAC 수명 주기 및 사용 가능한 다운로드에 대한 자세한 내용은 [SNAC 수명 주기 설명](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)을 참조하세요.

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3. SQL Server용 Microsoft OLE DB 드라이버(MSOLEDBSQL)
OLE DB가 [다시 사용](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/)되었으며, 2018년에 릴리스되었습니다.

새 OLE DB 공급자를 Microsoft OLE DB Driver for SQL Server(MSOLEDBSQL)라고 합니다. 새 공급자는 앞으로 최신 서버 기능으로 업데이트될 예정입니다.

> [!NOTE]
> 기존 애플리케이션에서 새 Microsoft OLE DB Driver for SQL Server를 사용하려면 연결 문자열을 SQLOLEDB 또는 SQLNCLI에서 MSOLEDBSQL로 변환할 계획을 해야 합니다.
  
## <a name="in-this-section"></a>섹션 내용  
[SQL Server용 OLE DB 드라이버를 사용해야 하는 경우](../oledb/when-to-use-oledb-driver-for-sql-server.md)  
 SQL Server용 OLE DB 드라이버를 Microsoft 데이터 액세스 기술과 연동하는 방법, Windows DAC 및 ADO.NET과 비교되는 특징을 설명하고, 사용할 데이터 액세스 기술을 결정하는 데 도움이 되는 팁을 제공합니다.  
  
 [SQL Server용 OLE DB 드라이버 기능](../oledb/features/oledb-driver-for-sql-server-features.md )  
 OLE DB Driver for SQL Server에서 지원하는 기능을 설명합니다.  
  
 [SQL Server용 OLE DB 드라이버로 애플리케이션 빌드](../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
 SQL Server용 OLE DB 드라이버가 Windows DAC와 다른 점, 사용되는 구성 요소, ADO와 연동하는 방법 등 개발에 대한 개요를 제공합니다.  
  
 이 섹션에서는 OLE DB Driver for SQL Server 라이브러리를 재배포하는 방법을 포함하여 OLE DB Driver for SQL Server 설치 및 배포에 관해서도 설명합니다.  
  
 [SQL Server용 OLE DB 드라이버 시스템 요구 사항](../oledb/system-requirements-for-oledb-driver-for-sql-server.md)  
 OLE DB Driver for SQL Server를 사용하는 데 필요한 시스템 리소스에 대해 설명합니다.  
  
 [SQL Server용 OLE DB 드라이버 프로그래밍](../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
 OLE DB Driver for SQL Server를 사용하는 방법을 설명합니다.  
  
 [더 많은 SQL Server용 OLE DB 드라이버 정보 찾기](../oledb/finding-more-oledb-driver-for-sql-server-information.md)  
 외부 리소스 및 추가 지원 링크를 포함하여 OLE DB Driver for SQL Server에 대한 추가 리소스를 제공합니다.  
  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 2005 Native Client에서 애플리케이션 업데이트](../oledb/applications/updating-an-application-from-sql-server-2005-native-client.md)    
 [OLE DB 방법 도움말 항목](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
