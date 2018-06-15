---
title: sys.dm_geo_replication_link_status (Azure SQL 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 10/13/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 15
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: ac416ef7d48655e25002646b6e364d04982688b2
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34464369"
---
# <a name="sysdmgeoreplicationlinkstatus-azure-sql-database"></a>sys.dm_geo_replication_link_status (Azure SQL 데이터베이스)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  지리적 복제 파트너 관계의 기본 및 보조 데이터베이스 간의 각 복제 링크에 대 한 행을 포함합니다. 여기에 기본 및 보조 데이터베이스가 포함 됩니다. 지정된 된 주 데이터베이스에 대 한 연속 복제 링크를 두 개 이상 있는 경우이 테이블 각 관계에 대 한 한 행을 포함 합니다. 뷰 논리 master를 포함 하는 모든 데이터베이스에 만들어집니다. 그러나 논리 master에서 이 뷰를 쿼리하면 빈 집합이 반환됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|link_guid|**uniqueidentifier**|복제 링크의 고유 ID입니다.|  
|partner_server|**sysname**|연결 된 데이터베이스를 포함 하는 논리 서버의 이름입니다.|  
|partner_database|**sysname**|연결 된 논리 서버에 연결 된 데이터베이스의 이름입니다.|  
|last_replication|**datetimeoffset**|주 데이터베이스 클록에 따라 보조 복제본에서 마지막 트랜잭션 승인의 타임 스탬프입니다. 이 값은 주 데이터베이스에서 사용할 수 있습니다.|  
|replication_lag_sec|**int**|Last_replication 값과의 주 데이터베이스 클록을 기준으로 주 서버에서 해당 트랜잭션 커밋 타임 스탬프 간의 시간 차이 (초)에서입니다.  이 값은 주 데이터베이스에서 사용할 수 있습니다.|  
|replication_state|**tinyint**|이 데이터베이스 중 하나에 대 한 지리적 복제 상태: 합니다.<br /><br /> 1 = Seeding 합니다. 지리적 복제 대상이 시드 되는 있지만 두 데이터베이스가 동기화 되지 않습니다. 시드가 완료 될 때까지 보조 데이터베이스에 연결할 수 없습니다. 주 데이터베이스에서 보조 데이터베이스 제거 시드 작업을 취소 합니다.<br /><br /> 2 = 보완 합니다. 보조 데이터베이스가 트랜잭션 측면에서 일관 된 상태에서 이므로 주 데이터베이스와 지속적으로 동기화 되.<br /><br /> 4 = 일시 중단 합니다. 이는 활성 연속 복사 관계가 아닙니다. 일반적으로 이 상태는 상호 링크에 사용할 수 있는 대역폭이 주 데이터베이스의 트랜잭션 작업 수준에 충분하지 않음을 나타냅니다. 그러나 연속 복사 관계는 그대로 유지됩니다.|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|역할(role)|**tinyint**|지리적 복제 역할 중 하나:<br /><br /> 0 = 기본 합니다. database_id 지리적 복제 파트너 관계의 주 데이터베이스를 가리킵니다.<br /><br /> 1 = 보조 합니다.  database_id 지리적 복제 파트너 관계의 주 데이터베이스를 가리킵니다.|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|중 보조 유형:<br /><br /> 0 = 직접 연결이 보조 데이터베이스에 허용 되지 않으며 데이터베이스를 읽기 액세스용으로 사용할 수 없습니다.<br /><br /> 2 = all; 보조 복제에서 데이터베이스에 연결할 수 있습니다 ication 읽기 전용 액세스 합니다.|  
|secondary_allow_connections_desc|**nvarchar(256)**|아니요<br /><br /> 모두|  
|last_commit|**datetimeoffset**|데이터베이스에 커밋된 마지막 트랜잭션의 시간입니다. 주 데이터베이스에서 검색 하는 경우 주 데이터베이스에서 마지막 커밋 시간을 나타냅니다. 보조 데이터베이스에서 검색 하는 경우 보조 데이터베이스에서 마지막 커밋 시간을 나타냅니다. 복제 링크의 기본 중지 되는 경우 보조 데이터베이스에서 검색을 따라 잡으면 보조 어떤 지점까지 나타냅니다.|
  
> [!NOTE]  
>  보조 데이터베이스 (4.2 단원)에서 해당 데이터베이스에 대 한 행을 제거 하 여 복제 관계를 종료 하는 경우는 **sys.dm_geo_replication_link_status** 보기 사라집니다.  
  
## <a name="permissions"></a>Permissions  
 View_database_state 권한이 있는 계정을 쿼리할 수 **sys.dm_geo_replication_link_status**합니다.  
  
## <a name="example"></a>예제  
 복제 시퀀스 번호 보다 낮 및 보조 데이터베이스의 마지막 복제 시간을 표시 합니다.  
  
```  
SELECT   
     link_guid  
   , partner_server  
   , last_replication  
   , replication_lag_sec   
FROM sys.dm_geo_replication_link_status;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER DATABASE &#40;Azure SQL 데이터베이스&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [sys.geo_replication_links &#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [sys.dm_operation_status &#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  
