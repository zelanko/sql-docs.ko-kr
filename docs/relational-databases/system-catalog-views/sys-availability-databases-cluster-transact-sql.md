---
title: sys. availability_databases_cluster (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.availability_databases_cluster_TSQL
- sys.availability_databases_cluster
- availability_databases_cluster_TSQL
- availability_databases_cluster
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.availability_databases_cluster catalog view
- Availability Groups [SQL Server], databases
ms.assetid: 8d9c57e5-7f39-4315-b466-92748231140a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2c36c1574ae1ad289c9980e1df9bfbe3b241e164
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829175"
---
# <a name="sysavailability_databases_cluster-transact-sql"></a>sys.availability_databases_cluster(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로컬 복사본 데이터베이스가 가용성 그룹에 조인 되어 있는지 여부에 관계 없이 WSFC (Windows Server 장애 조치 (Failover) 클러스터링) 클러스터의 모든 Always On 가용성 그룹에 대 한 가용성 복제본을 호스팅하는 인스턴스의 각 가용성 데이터베이스에 대해 하나의 행을 포함 합니다.  
  
> [!NOTE]  
>  데이터베이스가 가용성 그룹에 추가되면 주 데이터베이스가 그룹에 자동으로 조인됩니다. 보조 데이터베이스를 가용성 그룹에 조인하려면 각 보조 복제본에서 보조 데이터베이스를 준비해야 합니다.   
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|데이터베이스가 참여하는 가용성 그룹(있는 경우) 내의 가용성 그룹에 대한 고유 식별자입니다.<br /><br /> NULL = 데이터베이스가 가용성 그룹에 포함된 가용성 복제본의 일부가 아닙니다.|  
|**group_database_id**|**uniqueidentifier**|데이터베이스가 참여하는 가용성 그룹(있는 경우) 내의 데이터베이스에 대한 고유 식별자입니다. 주 복제본의이 데이터베이스와 데이터베이스가 가용성 그룹에 조인 된 모든 보조 복제본에 대 한 **group_database_id** 동일 합니다.<br /><br /> NULL = 데이터베이스가 가용성 그룹에 포함된 가용성 복제본의 일부가 아닙니다.|  
|**database_name**|**sysname**|가용성 그룹에 추가된 데이터베이스의 이름입니다.|  
  
## <a name="permissions"></a>권한  
 **Availability_databases_cluster** 의 호출자가 데이터베이스의 소유자가 아닌 경우 해당 행을 보는 데 필요한 최소 권한은 **MASTER** 데이터베이스에서 ALTER ANY DATABASE 또는 VIEW any database 서버 수준 권한 또는 CREATE database 권한입니다.  
  
## <a name="see-also"></a>참고 항목  
 [availability_groups &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [dm_hadr_database_replica_states &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)   
 [dm_hadr_database_replica_cluster_states &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
