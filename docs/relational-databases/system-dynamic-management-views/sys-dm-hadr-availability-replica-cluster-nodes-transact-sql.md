---
description: sys.dm_hadr_availability_replica_cluster_nodes(Transact-SQL)
title: sys. dm_hadr_availability_replica_cluster_nodes (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_hadr_availability_replica_cluster_nodes
- sys.dm_hadr_availability_replica_cluster_nodes_TSQL
- dm_hadr_availability_replica_cluster_nodes_TSQL
- sys.dm_hadr_availability_replica_cluster_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_availability_replica_cluster_nodes dynamic management view
ms.assetid: dbd7e416-badd-4332-a45c-438aa0145a99
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7a63fea89f2457a3b2e033b9cbfef3def46afe0e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550266"
---
# <a name="sysdm_hadr_availability_replica_cluster_nodes-transact-sql"></a>sys.dm_hadr_availability_replica_cluster_nodes(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터에 있는 Always On 가용성 그룹의 모든 가용성 복제본(조인 상태에 상관없음)에 대해 하나의 행을 반환합니다.  

 ##  <a name="connected_state"></a>  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**group_name**|**nvarchar(256)**|가용성 그룹의 이름으로,|  
|**replica_server_name**|**nvarchar(256)**|복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|  
|**node_name**|**nvarchar(256)**|클러스터 노드의 이름입니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;가용성 그룹 모니터링 ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
