---
title: sys.availability_databases_cluster (TRANSACT-SQL) | Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 206c9b1c250cb95a6ad49ccf20f8badf11f870ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046541"
---
# <a name="sysavailabilitydatabasescluster-transact-sql"></a>sys.availability_databases_cluster(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  인스턴스에서 각 가용성 데이터베이스에 대해 하나의 행을 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로컬 데이터베이스를 복사 하는 여부에 관계 없이 Windows Server 장애 조치 클러스터링 (WSFC) 클러스터의 Always On 가용성 그룹의 가용성 복제본을 호스팅하는 에 가입 된 가용성 그룹에 아직 있습니다.  
  
> [!NOTE]  
>  데이터베이스가 가용성 그룹에 추가되면 주 데이터베이스가 그룹에 자동으로 조인됩니다. 보조 데이터베이스를 가용성 그룹에 조인하려면 각 보조 복제본에서 보조 데이터베이스를 준비해야 합니다.   
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|데이터베이스가 참여하는 가용성 그룹(있는 경우) 내의 가용성 그룹에 대한 고유 식별자입니다.<br /><br /> NULL = 데이터베이스가 가용성 그룹에 포함된 가용성 복제본의 일부가 아닙니다.|  
|**group_database_id**|**uniqueidentifier**|데이터베이스가 참여하는 가용성 그룹(있는 경우) 내의 데이터베이스에 대한 고유 식별자입니다. **group_database_id** 주 복제본에서 가용성 그룹에 조인에 데이터베이스를 모든 보조 복제본이이 데이터베이스에 대해 동일 합니다.<br /><br /> NULL = 데이터베이스가 가용성 그룹에 포함된 가용성 복제본의 일부가 아닙니다.|  
|**database_name**|**sysname**|가용성 그룹에 추가된 데이터베이스의 이름입니다.|  
  
## <a name="permissions"></a>사용 권한  
 경우 호출자 **sys.availability_databases_cluster** 데이터베이스, ALTER ANY DATABASE 해당 행을 보는 데 필요한 최소 권한은 또는 VIEW ANY DATABASE 서버 수준 사용 권한 만들기의 소유자가 아니고 DATABASE 권한이 있어야 합니다 **마스터** 데이터베이스입니다.  
  
## <a name="see-also"></a>관련 항목  
 [sys.availability_groups&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.dm_hadr_database_replica_states &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)   
 [sys.dm_hadr_database_replica_cluster_states &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
