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
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 5f009cf311c1eb395915e017bf202abea5ae5290
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

MSOLEDBSQL, 또는 OLE DB Driver for SQL Server, SQL Server 용 OLE DB 드라이버를 참조 하는 데 구분 없이 사용 되는 용어입니다.

## <a name="different-generations-of-ole-db-drivers"></a>OLE DB 드라이버의 서로 다른 세대

SQL Server 용 Microsoft OLE DB 공급자의 세 가지 세대가 있습니다.

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1. Microsoft OLE DB Provider for SQL Server (SQLOLEDB)
[Microsoft OLE DB Provider for SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB)의 일부로 계속 제공 [Windows Data Access Components](https://msdn.microsoft.com/en-us/library/ms692897.aspx)합니다. 더 이상 유지 되지 않으므로 하 있으며 새로운 개발에이 드라이버를 사용 하는 권장 되지 않습니다. 


### <a name="2-sql-server-native-client-snac"></a>2. SQL Server Native Client SNAC)
부터는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md) 함께 제공 되는 OLE DB 공급자는 OLE DB 공급자 인터페이스 (SQLNCLI)가 포함 되어 있고 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 통해 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]합니다.

가 [2011에서 사용 중단으로 발표](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) 새로운 개발에이 드라이버를 사용 하는 권장 되지 않습니다. SNAC 수명 주기 및 사용 가능한 다운로드 하는 방법에 대 한 자세한 내용은를 참조 [설명 SNAC 수명 주기](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)합니다.

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3. Microsoft OLE DB Driver for SQL Server (MSOLEDBSQL)
OLE db [undeprecated](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) 2018에 릴리스 하며 다운로드할 수 있습니다 및 [여기](https://go.microsoft.com/fwlink/?linkid=871294)합니다.

새 OLE DB 공급자는 SQL Server (MSOLEDBSQL)에 대 한 Microsoft OLE DB Driver 호출 됩니다. 새 공급자 앞으로 가장 최근의 서버 기능으로 업데이트 됩니다.

> [!NOTE]
> 새 Microsoft OLE DB Driver for SQL Server에서 기존 응용 프로그램을 사용 하려면 SQLOLEDB 또는 SQLNCLI, MSOLEDBSQL 연결 문자열을 변환 하 계획 해야 합니다.   

OLE DB 드라이버에 SQL Server 기능에 대 한 정보:

-   [SQL Server용 OLE DB 드라이버의 LocalDB 지원](../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  

-   [메타데이터 검색](../oledb/features/metadata-discovery.md)  

-   [SQL Server용 OLE DB 드라이버에서 UTF-16 지원](../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  

-   [SQL Server용 OLE DB 드라이버의 고가용성, 재해 복구 지원](../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  

-   [확장 이벤트 로그의 진단 정보 액세스](../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

## <a name="see-also"></a>참고 항목  
[SQL Server 용 OLE DB 드라이버를 설치 합니다.](../oledb/applications/installing-oledb-driver-for-sql-server.md)     
[SQL Server 기능용 OLE DB 드라이버](../oledb/features/oledb-driver-for-sql-server-features.md )     
