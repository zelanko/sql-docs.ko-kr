---
title: sys.dm_geo_replication_link_status (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 94d5a2e924cfe4aa7625f6cfce40c5758eecb6a5
ms.sourcegitcommit: 97340deee7e17288b5eec2fa275b01128f28e1b8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55421160"
---
# <a name="sysdmgeoreplicationlinkstatus-azure-sql-database"></a>sys.dm_geo_replication_link_status(Azure SQL Database)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  지역에서 복제 파트너 관계의 주 및 보조 데이터베이스 간의 각 복제 링크에 대 한 행을 포함 합니다. 이 기본 및 보조 데이터베이스가 포함 됩니다. 지정된 된 주 데이터베이스에 대 한 둘 이상의 연속 복제 링크가 있는 경우이 테이블 각 관계에 대 한 행을 포함 합니다. 뷰 논리 마스터를 포함 한 모든 데이터베이스에 만들어집니다. 그러나 논리 master에서 이 뷰를 쿼리하면 빈 집합이 반환됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|link_guid|**uniqueidentifier**|복제 링크의 고유 ID입니다.|  
|partner_server|**sysname**|연결 된 데이터베이스가 포함 된 SQL Database 서버의 이름입니다.|  
|partner_database|**sysname**|연결된 SQL Database 서버의 연결된 데이터베이스 이름입니다.|  
|last_replication|**datetimeoffset**|주 데이터베이스 클록에 따라 보조에서 승인 마지막 트랜잭션의 타임 스탬프입니다. 이 값은 주 데이터베이스 에서만 사용할 수 있습니다.|  
|replication_lag_sec|**int**|주 데이터베이스 클록에 따라 주 서버에서 해당 트랜잭션 커밋 타임 스탬프와 last_replication 값 사이의 시간 차이 (초)에서입니다.  이 값은 주 데이터베이스 에서만 사용할 수 있습니다.|  
|replication_state|**tinyint**|이 데이터베이스 중 하나에 대 한 지역에서 복제의 상태:입니다.<br /><br /> 1 = Seeding 합니다. 지역에서 복제 대상이 시드 되는 있지만 두 데이터베이스는 아직 동기화 하지 못했습니다. 시드가 완료 될 때까지는 보조 데이터베이스에 연결할 수 없습니다. 기본에서 보조 데이터베이스 제거 시드 작업을 취소 합니다.<br /><br /> 2 회 =. 보조 데이터베이스가 트랜잭션 측면에서 일관 된 상태에서 이며 주 데이터베이스와 지속적으로 동기화 되.<br /><br /> 4 = 일시 중단 합니다. 이는 활성 연속 복사 관계가 아닙니다. 일반적으로 이 상태는 상호 링크에 사용할 수 있는 대역폭이 주 데이터베이스의 트랜잭션 작업 수준에 충분하지 않음을 나타냅니다. 그러나 연속 복사 관계는 그대로 유지됩니다.|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|역할(role)|**tinyint**|지리적 복제 역할 중 하나:<br /><br /> 0 = 기본입니다. Database_id를 지역에서 복제 파트너 관계에서 주 데이터베이스를 가리킵니다.<br /><br /> 1 = 보조 합니다.  Database_id를 지역에서 복제 파트너 관계에서 주 데이터베이스를 가리킵니다.|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|중 보조 유형:<br /><br /> 0 = 직접 데이터베이스를 읽기 액세스를 위해 사용할 수 없는 및 보조 데이터베이스에 연결할 수 있습니다.<br /><br /> 2 = all 보조 repl; 데이터베이스에 연결할 수 있습니다 ication 읽기 전용 액세스에 대 한 합니다.|  
|secondary_allow_connections_desc|**nvarchar(256)**|아니요<br /><br /> All|  
|last_commit|**datetimeoffset**|데이터베이스에 커밋된 마지막 트랜잭션의 시간입니다. 주 데이터베이스에서 검색 하는 경우 주 데이터베이스의 마지막 커밋 시간을 나타냅니다. 보조 데이터베이스에서 검색 하는 경우 보조 데이터베이스의 마지막 커밋 시간을 나타냅니다. 복제 링크의 주 서버가 다운 되 면 보조 데이터베이스에서 검색 하는 경우 보조 시점 따라잡을 때까지 나타냅니다.|
  
> [!NOTE]  
>  보조 데이터베이스 (4.2 섹션)에서 해당 데이터베이스에 대 한 행을 제거 하 여 복제 관계를 종료 하는 경우는 **sys.dm_geo_replication_link_status** 뷰가 사라집니다.  
  
## <a name="permissions"></a>사용 권한  
 View_database_state 권한 있는 계정을 쿼리하면 **sys.dm_geo_replication_link_status**합니다.  
  
## <a name="example"></a>예제  
 복제 지연 및 보조 데이터베이스의 마지막 복제 시간을 표시 합니다.  
  
```  
SELECT   
     link_guid  
   , partner_server  
   , last_replication  
   , replication_lag_sec   
FROM sys.dm_geo_replication_link_status;  
```  
  
## <a name="see-also"></a>관련 항목  
 [ALTER DATABASE &#40;Azure SQL Database&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [sys.geo_replication_links &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [sys.dm_operation_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  
