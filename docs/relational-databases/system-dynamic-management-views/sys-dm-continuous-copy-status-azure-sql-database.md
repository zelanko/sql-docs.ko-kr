---
description: sys.dm_continuous_copy_status(Azure SQL Database)
title: sys.dm_continuous_copy_status
titleSuffix: Azure SQL Database
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_continuous_copy_status_TSQL
- dm_continuous_copy_status_TSQL
- dm_continuous_copy_status
- sys.dm_continuous_copy_status
dev_langs:
- TSQL
helpviewer_keywords:
- dm_continuous_copy_status
- sys.dm_continuous_copy_status
ms.assetid: 411b2e71-4421-4ef5-900d-5af068750899
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: f06228aaec7abb9d9eb7de6237be696319cd661f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550330"
---
# <a name="sysdm_continuous_copy_status-azure-sql-database"></a>sys.dm_continuous_copy_status(Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  현재 지역 복제 연속 복사 관계에 참여 하 고 있는 각 사용자 데이터베이스 (V11)에 대 한 행을 반환 합니다. 지정된 주 데이터베이스에 대해 둘 이상의 연속 복사 관계가 시작된 경우 이 테이블에는 각 활성 보조 데이터베이스에 대한 행이 하나씩 포함됩니다.  
  
SQL Database V12를 사용 하는 경우 V11에만 적용 *dm_continuous_copy_status* 되므로 [dm_geo_replication_link_status](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md) 를 사용 해야 합니다.

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**copy_guid**|**uniqueidentifier**|복제본 데이터베이스의 고유 ID입니다.|  
|**partner_server**|**sysname**|연결된 SQL Database 서버의 이름입니다.|  
|**partner_database**|**sysname**|연결된 SQL Database 서버의 연결된 데이터베이스 이름입니다.|  
|**last_replication**|**datetimeoffset**|마지막으로 적용된 복제된 트랜잭션의 타임스탬프입니다.|  
|**replication_lag_sec**|**int**|현재 시간과 활성 보조 데이터베이스에서 승인되지 않은 주 데이터베이스에서 성공적으로 커밋된 마지막 트랜잭션의 타임스탬프 간의 시간 차이(초)입니다.|  
|**replication_state**|**tinyint**|이 데이터베이스에 대 한 연속 복사 복제 상태입니다. 다음은 가능한 값과 그에 대 한 설명입니다.<br /><br /> 1: 시드 복제 대상이 시드되고 있고 트랜잭션 측면에서 일관되지 않은 상태입니다. 시드가 완료될 때까지 활성 보조 데이터베이스에 연결할 수 없습니다. <br />2: catch 합니다. 활성 보조 데이터베이스가 주 데이터베이스를 현재 따라잡고 있고 트랜잭션 측면에서 일관된 상태입니다.<br />3: 다시 시드해야 합니다. 활성 보조 데이터베이스가 복구할 수 없는 복제 오류로 인해 자동으로 다시 시드되고 있습니다.<br />4: 일시 중단 됨. 이는 활성 연속 복사 관계가 아닙니다. 일반적으로 이 상태는 상호 링크에 사용할 수 있는 대역폭이 주 데이터베이스의 트랜잭션 작업 수준에 충분하지 않음을 나타냅니다. 그러나 연속 복사 관계는 그대로 유지됩니다.|  
|**replication_state_desc**|**nvarchar(256)**|replication_state에 대한 설명으로, 다음 중 하나입니다.<br /><br /> SEEDING<br /><br /> CATCH_UP<br /><br /> RE_SEEDING<br /><br /> SUSPENDED|  
|**is_rpo_limit_reached**|**bit**|이 값은 항상 0으로 설정됩니다.|  
|**is_target_role**|**bit**|0 = 복사 관계의 원본<br /><br /> 1 = 복사 관계의 대상|  
|**is_interlink_connected**|**bit**|1 = 상호 링크가 연결되었습니다.<br /><br /> 0 = 상호 링크가 끊어졌습니다.|  
  
## <a name="permissions"></a>사용 권한  
 데이터를 검색 하려면 **db_owner** 데이터베이스 역할의 멤버 자격이 필요 합니다. Dbo 사용자, **dbmanager** 데이터베이스 역할의 멤버 및 sa 로그인도 모두이 뷰를 쿼리할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 **Dm_continuous_copy_status** 뷰는 **리소스** 데이터베이스에서 만들어지며 논리적 master를 비롯 한 모든 데이터베이스에 표시 됩니다. 그러나 논리 master에서 이 뷰를 쿼리하면 빈 집합이 반환됩니다.  
  
 데이터베이스에서 연속 복사 관계가 종료 되 면 **dm_continuous_copy_status** 보기에서 해당 데이터베이스의 행이 사라집니다.  
  
 **Dm_database_copies** 뷰와 마찬가지로, **dm_continuous_copy_status** 는 데이터베이스가 주 데이터베이스 이거나 활성 보조 데이터베이스 인 연속 복사 관계의 상태를 반영 합니다. **Dm_database_copies**와는 달리, **dm_continuous_copy_status** 에는 작업과 성능에 대 한 세부 정보를 제공 하는 여러 열이 포함 되어 있습니다. 이러한 열에는 **last_replication**및 **replication_lag_sec**가 포함 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [dm_database_copies &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)   
 [Transact-sql&#41;&#40;활성 지역 복제 저장 프로시저 ](https://msdn.microsoft.com/library/81658ee4-4422-4d73-bf7a-86a07422cb0d)  
  
  
