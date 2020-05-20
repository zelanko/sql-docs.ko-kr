---
title: sys. dm_hadr_availability_replica_cluster_states (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cdc5edf1c752478c96cd0f7e4cb3eef441bd078c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82811970"
---
# <a name="sysdm_hadr_availability_replica_cluster_states-transact-sql"></a>sys.dm_hadr_availability_replica_cluster_states(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터에 있는 모든 Always On 가용성 그룹(복제본 위치에 상관없음)의 각 Always On 가용성 복제본(조인 상태에 상관없음)에 대해 하나의 행을 반환합니다.  
  
##  <a name="connected_state"></a>  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|가용성 복제본의 고유한 식별자입니다.|  
|**replica_server_name**|**nvarchar(256)**|복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|  
|**group_id**|**uniqueidentifier**|가용성 그룹의 고유한 식별자입니다.|  
|**join_state**|**tinyint**|0 = 조인되지 않음<br /><br /> 1 = 조인 됨, 독립 실행형<br /><br /> 2 = 조인된 장애 조치(Failover) 클러스터 인스턴스|  
|**join_state_desc**|**nvarchar(60)**|NOT_JOINED<br /><br /> JOINED_STANDALONE<br /><br /> JOINED_FAILOVER_CLUSTER_INSTANCE|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
