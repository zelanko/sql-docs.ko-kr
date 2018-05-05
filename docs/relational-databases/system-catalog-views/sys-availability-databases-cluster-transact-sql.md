---
title: sys.availability_databases_cluster (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a82fc4ac24d43d5e41fbde5542a94972a82a0ac7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysavailabilitydatabasescluster-transact-sql"></a>sys.availability_databases_cluster(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  인스턴스에서 각 가용성 데이터베이스에 대 한 하나의 행을 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로컬 데이터베이스를 복사 하는 여부에 관계 없이 Windows Server 장애 조치 클러스터링 (WSFC) 클러스터의 Always On 가용성 그룹에 대 한 가용성 복제본을 호스팅 중인지 호스팅 조인 되어에 가용성 그룹에 있습니다.  
  
> [!NOTE]  
>  데이터베이스가 가용성 그룹에 추가되면 주 데이터베이스가 그룹에 자동으로 조인됩니다. 보조 데이터베이스를 가용성 그룹에 조인하려면 각 보조 복제본에서 보조 데이터베이스를 준비해야 합니다.   
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|데이터베이스가 참여하는 가용성 그룹(있는 경우) 내의 가용성 그룹에 대한 고유 식별자입니다.<br /><br /> NULL = 데이터베이스가 가용성 그룹에 포함된 가용성 복제본의 일부가 아닙니다.|  
|**group_database_id**|**uniqueidentifier**|데이터베이스가 참여하는 가용성 그룹(있는 경우) 내의 데이터베이스에 대한 고유 식별자입니다. **group_database_id** 데이터베이스가 주 복제본 및에 조인 된 가용성 그룹에 모든 보조 복제본이이 데이터베이스에 대해 동일 합니다.<br /><br /> NULL = 데이터베이스가 가용성 그룹에 포함된 가용성 복제본의 일부가 아닙니다.|  
|**database_name**|**sysname**|가용성 그룹에 추가된 데이터베이스의 이름입니다.|  
  
## <a name="permissions"></a>Permissions  
 하는 경우의 호출자 **sys.availability_databases_cluster** 데이터베이스, ALTER ANY DATABASE 해당 행을 보는 데 필요한 최소 사용 권한 또는 VIEW ANY DATABASE 서버 수준 사용 권한 또는 CREATE의 소유자가 아닙니다 데이터베이스 사용 권한에서의 **마스터** 데이터베이스입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sys.availability_groups&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.dm_hadr_database_replica_states &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)   
 [sys.dm_hadr_database_replica_cluster_states &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
