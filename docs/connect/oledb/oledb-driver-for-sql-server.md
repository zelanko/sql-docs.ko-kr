---
title: OLE DB Driver for SQL Server | Microsoft Docs
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb
ms.reviewer: ''
ms.suite: sql
description: ''
ms.custom: ''
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: article
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 89e66fe2c61ae17a43e2a58071ba04374f33ea04
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2018
---
# <a name="ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

MSOLEDBSQL, 또는 OLE DB Driver for SQL Server, SQL Server 용 OLE DB Driver를 가리키는 같은 의미로 사용 된 용어입니다.

## <a name="different-incarnations-of-ole-db-drivers"></a>다른 OLE DB 드라이버 버전

SQL Server 용 Microsoft OLE DB 공급자의 고유 버전을 세 가지가 있습니다.


### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1. Microsoft OLE DB Provider for SQL Server (SQLOLEDB)

[Microsoft OLE DB Provider for SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB)의 일부로 계속 제공 [Windows Data Access Components](https://msdn.microsoft.com/en-us/library/ms692897.aspx)합니다. 하지 새로운 개발에이 드라이버를 사용 하는 것이 좋습니다.


### <a name="2-sql-server-native-client-snac"></a>2. SQL Server Native Client SNAC)

SQL Server 2005부터는 [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md) OLE DB 공급자 인터페이스 (SQLNCLI)가 포함 되어 있고 SQL Server 2017을 통해 SQL Server 2005와 함께 제공 되는 OLE DB 공급자입니다.

가 [2011에서 사용 중단으로 발표](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) 새로운 개발에이 드라이버를 사용 하는 권장 되지 않습니다.


### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3. Microsoft OLE DB Driver for SQL Server (MSOLEDBSQL)

OLE db [undeprecated 2017에 있다고 알려진](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/)합니다. 2018에 대 한 새 계획 된 릴리스 발표 되었습니다.

새 OLE DB 공급자는 SQL Server (MSOLEDBSQL)에 대 한 Microsoft OLE DB Driver 호출 됩니다. 새 공급자 앞으로 가장 최근의 서버 기능으로 업데이트 됩니다.

OLE DB 드라이버에 SQL Server 기능에 대 한 정보:

-   [SQL Server Support for LocalDB에 대 한 OLE DB 드라이버](../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  

-   [메타데이터 검색](../oledb/features/metadata-discovery.md)  

-   [SQL Server 용 OLE DB 드라이버의 utf-16 지원](../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  

-   [OLE DB Driver for SQL Server Support for High Availability, Disaster Recovery](../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  

-   [확장 이벤트 로그의 진단 정보 액세스](../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

## <a name="see-also"></a>참고 항목  
[SQL Server 용 OLE DB 드라이버를 설치 합니다.](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
 [OLE DB Driver for SQL Server 기능](../oledb/features/oledb-driver-for-sql-server-features.md )  
