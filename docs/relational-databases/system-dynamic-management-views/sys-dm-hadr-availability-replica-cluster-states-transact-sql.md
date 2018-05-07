---
title: sys.dm_hadr_availability_replica_cluster_states (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_availability_replica_cluster_states_TSQL
- dm_hadr_availability_replica_cluster_states
- sys.dm_hadr_availability_replica_cluster_states
- dm_hadr_availability_replica_cluster_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_availability_replica_cluster_states dynamic management view
ms.assetid: 2e0dd780-6a71-4f4b-b7f7-6e063bec71d6
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 004857a97be6be430e2f7e88335ba0abf4a03dbd
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmhadravailabilityreplicaclusterstates-transact-sql"></a>sys.dm_hadr_availability_replica_cluster_states(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Windows Server 장애 조치 클러스터링 (WSFC) 클러스터의 Always On의 각 가용성 복제본 (조인 상태)에 관계 없이 모든 Always On 가용성 그룹 (복제본 위치)와 상관 없이 대 한 행을 반환합니다.  
  
##  <a name="connected_state"></a>  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|가용성 복제본의 고유한 식별자입니다.|  
|**replica_server_name**|**nvarchar(256)**|복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|  
|**group_id**|**uniqueidentifier**|가용성 그룹의 고유한 식별자입니다.|  
|**join_state**|**tinyint**|0 = 조인되지 않음<br /><br /> 1 = 조인된 독립 실행형 인스턴스<br /><br /> 2 = 조인된 장애 조치(Failover) 클러스터 인스턴스|  
|**join_state_desc**|**nvarchar(60)**|NOT_JOINED<br /><br /> JOINED_STANDALONE_INSTANCE<br /><br /> JOINED_FAILOVER_CLUSTER_INSTANCE|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
