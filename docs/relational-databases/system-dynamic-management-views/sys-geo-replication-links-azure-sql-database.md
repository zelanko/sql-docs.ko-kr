---
title: sys.geo_replication_links (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- dm_geo_replication_links_TSQL
- dm_geo_replication_links
- sys.dm_geo_replication_links
- sys.dm_geo_replication_links_TSQL
helpviewer_keywords:
- sys.dm_geo_replication_links dynamic management view
- dm_geo_replication_links dynamic management view
ms.assetid: 58911798-1d60-4f28-87ab-2def2bfc3de7
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 5e59dcd6550c006b5a1e0f3e3be6440669e05021
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37997745"
---
# <a name="sysgeoreplicationlinks-azure-sql-database"></a>sys.geo_replication_links (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  지역에서 복제 파트너 관계의 주 및 보조 데이터베이스 간의 각 복제 링크에 대 한 행을 포함 합니다. 이 보기는 논리적 master 데이터베이스에 상주합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|Sys.databases 뷰의 현재 데이터베이스의 ID입니다.|  
|start_date|**datetimeoffset**|데이터베이스 복제를 시작한 경우 지역 SQL Database 데이터 센터의 UTC 시간|  
|modify_date|**datetimeoffset**|데이터베이스 지역 복제를 완료 하는 경우 지역 SQL Database 데이터 센터에서 UTC 시간입니다. 새 데이터베이스는이 시간을 기준으로 주 데이터베이스와 동기화 됩니다. 의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다.|  
|link_guid|**uniqueidentifier**|지역에서 복제 링크의 고유 ID입니다.|  
|partner_server|**sysname**|지역에서 복제 된 데이터베이스를 포함 하는 논리 서버의 이름입니다.|  
|partner_database|**sysname**|연결된 된 논리 서버에서 지역에서 복제 된 데이터베이스의 이름입니다.|  
|replication_state|**tinyint**|이 데이터베이스 중 하나에 대 한 지역에서 복제의 상태:입니다.<br /><br /> 0 = 보류 중입니다. 활성 보조 데이터베이스 만들기 예약 되었지만 필요한 준비 단계가 아직 완료 되지 않은.<br /><br /> 1 = Seeding 합니다. 지역에서 복제 대상이 시드 되는 있지만 두 데이터베이스는 아직 동기화 하지 못했습니다. 시드가 완료 될 때까지는 보조 데이터베이스에 연결할 수 없습니다. 기본에서 보조 데이터베이스 제거 시드 작업을 취소 합니다.<br /><br /> 2 회 =. 보조 데이터베이스가 트랜잭션 측면에서 일관 된 상태에서 이며 주 데이터베이스와 지속적으로 동기화 되.|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|역할(role)|**tinyint**|지리적 복제 역할 중 하나:<br /><br /> 0 = 기본입니다. Database_id를 지역에서 복제 파트너 관계에서 주 데이터베이스를 가리킵니다.<br /><br /> 1 = 보조 합니다.  Database_id를 지역에서 복제 파트너 관계에서 주 데이터베이스를 가리킵니다.|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|중 보조 유형:<br /><br /> 0 = 아니요 보조 데이터베이스로 장애 조치 될 때까지 액세스할 수 없는 합니다.<br /><br /> 1 = ReadOnly. 보조 데이터베이스가 ApplicationIntent 사용 하 여 클라이언트 연결에만 액세스할 수 있는 = ReadOnly.<br /><br /> 2  =  모두. 보조 데이터베이스는 모든 클라이언트 연결에 액세스할 수 있습니다.|  
|secondary_allow_connections _desc|**nvarchar(256)**|아니요<br /><br /> All<br /><br /> 읽기 전용|  
  
## <a name="permissions"></a>사용 권한  
 이 보기는 에서만 사용할 수는 **마스터** 데이터베이스 서버 수준 보안 주체 로그인 합니다.  
  
## <a name="example"></a>예제  
 지역에서 복제 링크를 사용 하 여 모든 데이터베이스를 표시 합니다.  
  
```  
SELECT   
     database_id  
   , start_date  
   , partner_server  
   , partner_database  
   , replication_state  
   , role_desc  
   , secondary_allow_connections_desc   
FROM sys.geo_replication_links;  
```  
  
## <a name="see-also"></a>관련 항목  
 [ALTER DATABASE(Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [sys.dm_geo_replication_link_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [sys.dm_operation_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  
