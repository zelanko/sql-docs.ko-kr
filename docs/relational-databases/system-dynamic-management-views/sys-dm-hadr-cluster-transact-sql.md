---
description: sys.dm_hadr_cluster(Transact-SQL)
title: sys. dm_hadr_cluster (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_cluster
- dm_hadr_cluster_HADR
- sys.dm_hadr_cluster_TSQL
- dm_hadr_cluster
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_cluster catalog view
- Availability Groups [SQL Server], WSFC clusters
ms.assetid: 13ce70e4-9d43-4a80-a826-099e6213bf85
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b8bc19f3e73c00c2148cba2fb0381d73a36d6eb2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89533115"
---
# <a name="sysdm_hadr_cluster-transact-sql"></a>sys.dm_hadr_cluster(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  에 대해 사용 하도록 설정 된 인스턴스를 호스팅하는 WSFC (Windows Server 장애 조치 (Failover) 클러스터링) 노드에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] wsfc 쿼럼이 있는 경우 **dm_hadr_cluster** 는 쿼럼에 대 한 클러스터 이름 및 정보를 제공 하는 행을 반환 합니다. WSFC 노드에 쿼럼이 없으면 반환되는 행이 없습니다.  
 > [!TIP]
 > 부터 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이 동적 관리 뷰는 Always On 가용성 그룹 외에도 Always On 장애 조치 (Failover) 클러스터 인스턴스를 지원 합니다.

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**cluster_name**|**nvarchar(128)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대해 사용하도록 설정된 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]의 인스턴스를 호스팅하는 WSFC 클러스터의 이름입니다.|  
|**quorum_type**|**tinyint**|이 WSFC 클러스터에서 사용되는 쿼럼 유형이며 다음 중 하나입니다.<br /><br /> 0 = 노드 과반수. 이 쿼럼 구성은 노드 개수의 절반(반올림)에서 1을 뺀 개수의 오류를 유지할 수 있습니다. 예를 들어 7 노드 클러스터에서 이 쿼럼 구성은 3개의 노드 오류를 유지할 수 있습니다.<br /><br /> 1 = 노드 및 디스크 과반수. 디스크 미러링 모니터가 온라인 상태로 유지되는 경우 이 쿼럼 구성은 노드 개수의 절반(반올림)에 해당하는 오류를 유지할 수 있습니다. 예를 들어 디스크 미러링 모니터가 온라인 상태인 6노드 클러스터는 3개의 노드 오류를 유지할 수 있습니다. 디스크 미러링 모니터가 오프라인 상태이거나 실패한 경우 이 쿼럼 구성은 노드 개수의 절반(반올림)에서 1을 뺀 개수의 오류를 유지할 수 있습니다. 예를 들어 실패한 디스크 미러링 모니터가 있는 6노드 클러스터는 2개(3-1=2)의 노드 오류를 유지할 수 있습니다.<br /><br /> 2 = 노드 및 파일 공유 과반수. 이 쿼럼 구성은 노드 및 디스크 과반수와 비슷한 방식으로 작동하지만 디스크 미러링 모니터 대신 파일 공유 미러링 모니터를 사용합니다.<br /><br /> 3 = 과반수 없음: 디스크만 해당 쿼럼 디스크가 온라인 상태인 경우 이 쿼럼 구성은 하나를 제외한 모든 노드의 오류를 유지할 수 있습니다.<br /><br /> 4 = 알 수 없는 쿼럼. 클러스터에 대 한 알 수 없는 쿼럼입니다.<br /><br /> 5 = 클라우드 감시 클러스터는 쿼럼 조정을 위해 Microsoft Azure를 활용 합니다. 클라우드 감시를 사용할 수 있는 경우 클러스터는 노드 절반의 오류 (반올림)를 유지할 수 있습니다.|  
|**quorum_type_desc**|**varchar(50)**|**Quorum_type**에 대 한 설명 이며 다음 중 하나입니다.<br /><br /> NODE_MAJORITY<br /><br /> NODE_AND_DISK_MAJORITY<br /><br /> NODE_AND_FILE_SHARE_MAJORITY<br /><br /> NO_MAJORITY:_DISK_ONLY <br /><br /> UNKNOWN_QUORUM <br /><br /> CLOUD_WITNESS|  
|**quorum_state**|**tinyint**|WSFC의 상태이며 다음 중 하나입니다.<br /><br /> 0 = 쿼럼 상태를 알 수 없음<br /><br /> 1 = 일반 쿼럼<br /><br /> 2 = 강제 쿼럼|  
|**quorum_state_desc**|**varchar(50)**|**Quorum_state**에 대 한 설명 이며 다음 중 하나입니다.<br /><br /> UNKNOWN_QUORUM_STATE<br /><br /> NORMAL_QUORUM<br /><br /> FORCED_QUORUM|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 동적 관리 뷰 및 함수 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 가용성 그룹 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;가용성 그룹 모니터링 ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_hadr_cluster_members&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)  
  
  
