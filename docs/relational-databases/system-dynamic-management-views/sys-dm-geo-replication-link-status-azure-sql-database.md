---
description: sys.dm_geo_replication_link_status(Azure SQL Database)
title: sys.dm_geo_replication_link_status
titleSuffix: Azure SQL Database
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- dm_geo_replication_link_status
- dm_geo_replication_link_status_TSQL
- sys.dm_geo_replication_link_status
- sys.dm_geo_replication_link_status_TSQL
helpviewer_keywords:
- dm_geo_replication_link_status dynamic management view
- sys.dm_geo_replication_link_status dynamic management view
ms.assetid: d763d679-470a-4c21-86ab-dfe98d37e9fd
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: 433bcea8a7d0a1f719aac9f76a782f666113189f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548482"
---
# <a name="sysdm_geo_replication_link_status-azure-sql-database"></a>sys.dm_geo_replication_link_status(Azure SQL Database)

[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  지역에서 복제 파트너 관계에 있는 주 데이터베이스와 보조 데이터베이스 간의 각 복제 링크에 대 한 행을 포함 합니다. 주 및 보조 데이터베이스가 포함됩니다. 지정된 주 데이터베이스에 두 개 이상의 연속 복제 링크가 있는 경우 이 테이블은 각 관계에 대한 행을 포함합니다. 논리 마스터를 포함한 모든 데이터베이스에 뷰가 생성됩니다. 그러나 논리 master에서 이 뷰를 쿼리하면 빈 집합이 반환됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|link_guid|**uniqueidentifier**|복제 링크의 고유 ID입니다.|  
|partner_server|**sysname**|연결 된 데이터베이스를 포함 하는 SQL Database 서버의 이름입니다.|  
|partner_database|**sysname**|연결된 SQL Database 서버의 연결된 데이터베이스 이름입니다.|  
|last_replication|**datetimeoffset**|주 데이터베이스 클록을 기반으로 하는 보조 복제본의 마지막 트랜잭션 승인 타임 스탬프입니다. 이 값은 주 데이터베이스 에서만 사용할 수 있습니다.|  
|replication_lag_sec|**int**|주 데이터베이스 클록을 기반으로 하는 주 데이터베이스에 대 한 해당 트랜잭션의 커밋 타임 스탬프와 last_replication 값 사이의 시간 차이 (초)입니다.  이 값은 주 데이터베이스 에서만 사용할 수 있습니다.|  
|replication_state|**tinyint**|이 데이터베이스에 대 한 지역에서 복제 상태 이며 다음 중 하나입니다.<br /><br /> 1 = 시드 지역에서 복제 대상이 시드 되 고 있지만 두 데이터베이스가 아직 동기화 되지 않았습니다. 시드가 완료 될 때까지 보조 데이터베이스에 연결할 수 없습니다. 주 데이터베이스에서 보조 데이터베이스를 제거 하면 시드 작업이 취소 됩니다.<br /><br /> 2 = 보완. 보조 데이터베이스가 트랜잭션 측면에서 일관 된 상태 이며 지속적으로 주 데이터베이스와 동기화 되 고 있습니다.<br /><br /> 4 = 일시 중단 됨. 이는 활성 연속 복사 관계가 아닙니다. 일반적으로 이 상태는 상호 링크에 사용할 수 있는 대역폭이 주 데이터베이스의 트랜잭션 작업 수준에 충분하지 않음을 나타냅니다. 그러나 연속 복사 관계는 그대로 유지됩니다.|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|역할(role)|**tinyint**|지역에서 복제 역할, 다음 중 하나입니다.<br /><br /> 0 = 기본 Database_id는 지역에서 복제 파트너 관계에서 주 데이터베이스를 참조 합니다.<br /><br /> 1 = 보조  Database_id는 지역에서 복제 파트너 관계에서 주 데이터베이스를 참조 합니다.|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|보조 유형이 며 다음 중 하나입니다.<br /><br /> 0 = 보조 데이터베이스에 대 한 직접 연결이 허용 되지 않으며 읽기 액세스를 위해 데이터베이스를 사용할 수 없습니다.<br /><br /> 2 = 보조 repl의 데이터베이스에 대 한 모든 연결을 허용 하 고 읽기 전용 액세스를 허용 합니다.|  
|secondary_allow_connections_desc|**nvarchar(256)**|아니요<br /><br /> 모두|  
|last_commit|**datetimeoffset**|데이터베이스에 마지막으로 커밋된 트랜잭션 시간입니다. 주 데이터베이스에서 검색 된 경우 주 데이터베이스에 대 한 마지막 커밋 시간을 나타냅니다. 보조 데이터베이스에서 검색 된 경우 보조 데이터베이스의 마지막 커밋 시간을 나타냅니다. 복제 링크의 주 복제본이 다운 되 면 보조 데이터베이스에서 검색 된 경우 보조 데이터베이스에서 발견 된 지점을 나타냅니다.|
  
> [!NOTE]  
>  보조 데이터베이스를 제거 하 여 복제 관계를 종료 하는 경우 (4.2 섹션) **dm_geo_replication_link_status** 뷰의 해당 데이터베이스에 대 한 행이 사라집니다.  
  
## <a name="permissions"></a>사용 권한  
 View_database_state 권한이 있는 계정은 **dm_geo_replication_link_status**를 쿼리할 수 있습니다.  
  
## <a name="example"></a>예제  
 보조 데이터베이스의 복제 지연 및 마지막 복제 시간을 표시 합니다.  
  
```  
SELECT   
     link_guid  
   , partner_server  
   , last_replication  
   , replication_lag_sec   
FROM sys.dm_geo_replication_link_status;  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE &#40;Azure SQL Database&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [geo_replication_links &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [dm_operation_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)   
 [sp_wait_for_database_copy_sync](../system-stored-procedures/active-geo-replication-sp-wait-for-database-copy-sync.md)
  
