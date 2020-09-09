---
description: sys.geo_replication_links(Azure SQL Database)
title: geo_replication_links (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
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
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 36849d6fc285839ebf99b75452735ddf5073f4ec
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543757"
---
# <a name="sysgeo_replication_links-azure-sql-database"></a>sys.geo_replication_links(Azure SQL Database)

[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  지역에서 복제 파트너 관계에 있는 주 데이터베이스와 보조 데이터베이스 간의 각 복제 링크에 대 한 행을 포함 합니다. 논리적 master 데이터베이스에 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|현재 데이터베이스의 ID입니다.|  
|start_date|**datetimeoffset**|데이터베이스 복제가 시작 된 경우 지역 SQL Database 데이터 센터의 UTC 시간|  
|modify_date|**datetimeoffset**|데이터베이스 지역에서 복제가 완료 된 경우 지역 SQL Database 데이터 센터의 UTC 시간입니다. 새 데이터베이스는이 시간 동안 주 데이터베이스와 동기화 됩니다. .|  
|link_guid|**uniqueidentifier**|지역에서 복제 링크의 고유 ID입니다.|  
|partner_server|**sysname**|지역에서 복제 된 데이터베이스를 포함 하는 SQL Database 서버의 이름입니다.|  
|partner_database|**sysname**|연결 된 SQL Database 서버에서 지역에서 복제 된 데이터베이스의 이름입니다.|  
|replication_state|**tinyint**|이 데이터베이스에 대 한 지역에서 복제 상태 이며 다음 중 하나입니다.<br /><br /> 0 = 보류 중. 활성 보조 데이터베이스를 만드는 작업이 예약 되었지만 필요한 준비 단계가 아직 완료 되지 않았습니다.<br /><br /> 1 = 시드 지역에서 복제 대상이 시드 되 고 있지만 두 데이터베이스가 아직 동기화 되지 않았습니다. 시드가 완료 될 때까지 보조 데이터베이스에 연결할 수 없습니다. 주 데이터베이스에서 보조 데이터베이스를 제거 하면 시드 작업이 취소 됩니다.<br /><br /> 2 = 보완. 보조 데이터베이스가 트랜잭션 측면에서 일관 된 상태 이며 지속적으로 주 데이터베이스와 동기화 되 고 있습니다.|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|역할(role)|**tinyint**|지역에서 복제 역할, 다음 중 하나입니다.<br /><br /> 0 = 기본 Database_id는 지역에서 복제 파트너 관계에서 주 데이터베이스를 참조 합니다.<br /><br /> 1 = 보조  Database_id는 지역에서 복제 파트너 관계에서 주 데이터베이스를 참조 합니다.|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|보조 유형이 며 다음 중 하나입니다.<br /><br /> 0 = 아니요 장애 조치 (failover) 될 때까지 보조 데이터베이스에 액세스할 수 없습니다.<br /><br /> 1 = 읽기 전용입니다. 보조 데이터베이스는 ApplicationIntent = ReadOnly 인 클라이언트 연결에만 액세스할 수 있습니다.<br /><br /> 2  =  모두. 보조 데이터베이스는 모든 클라이언트 연결에 액세스할 수 있습니다.|  
|secondary_allow_connections _desc|**nvarchar(256)**|아니요<br /><br /> 모두<br /><br /> 읽기 전용|  
  
## <a name="permissions"></a>사용 권한

이 뷰는 **master** 데이터베이스에서 서버 수준 보안 주체 로그인에 대해서만 사용할 수 있습니다.  
  
## <a name="example"></a>예제

지역에서 복제 링크를 사용 하 여 모든 데이터베이스를 표시 합니다.  

```sql
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

## <a name="see-also"></a>참고 항목

 [ALTER DATABASE(Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [dm_geo_replication_link_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [dm_operation_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
