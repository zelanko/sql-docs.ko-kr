---
title: sys.dm_hadr_instance_node_map (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sys.dm_hadr_instance_node_map_TSQL
- sys.sys.dm_hadr_instance_node_map
- sys.dm_hadr_instance_node_map_TSQL
- sys.dm_hadr_instance_node_map
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.sys.dm_hadr_instance_node_map dynamic management view
ms.assetid: ccfaf62c-9f87-43cf-a5e7-8942e91dd041
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61d86f7ac8fda6d975f9f0ff2fc9aaf58af55aa9
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmhadrinstancenodemap-transact-sql"></a>sys.dm_hadr_instance_node_map(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  모든 인스턴스에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Always On 가용성 그룹에 조인, 서버 인스턴스를 호스팅하는 Windows Server 장애 조치 클러스터링 (WSFC) 노드의 이름을 반환 하는 가용성 복제본을 호스팅하는 합니다. 이러한 동적 관리 뷰는 다음과 같이 사용됩니다.  
  
-   이 동적 관리 뷰는 동일한 WSFC 노드에서 호스팅되는 여러 가용성 복제본이 포함된 가용성 그룹을 검색하는 데 유용합니다. 이러한 구성은 가용성 그룹이 잘못 구성된 경우 FCI 장애 조치(failover) 이후 발생 가능한 지원되지 않는 구성입니다. 자세한 내용은 [장애 조치(failover) 클러스터링 및 Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)을 참조하세요.  
  
-   여러 SQL Server 인스턴스가 동일한 WSFC 노드에 호스팅되는 경우 리소스 DLL이 이 동적 관리 뷰를 사용하여 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 확인합니다.  
   
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**ag_resource_id**|**nvarchar(256)**|가용성 그룹의 고유 ID를 WSFC 클러스터의 리소스로 나타낸 것입니다.|  
|**instance_name**|**nvarchar(256)**|이름-*서버*/*인스턴스*-가용성 그룹에 대 한 복제본을 호스팅하는 서버 인스턴스.|  
|**node_name**|**nvarchar(256)**|WSFC 클러스터 노드의 이름입니다.|  
  
## <a name="permissions"></a>Permissions  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Always On 가용성 그룹 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 가용성 그룹 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [가용성 그룹 모니터링 &#40; Transact SQL &#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
