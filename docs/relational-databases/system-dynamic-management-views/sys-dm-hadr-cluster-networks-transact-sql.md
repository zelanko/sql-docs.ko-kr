---
title: sys. dm_hadr_cluster_networks (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_hadr_cluster_networks
- sys.dm_hadr_cluster_networks_TSQL
- sys.dm_hadr_cluster_networks
- dm_hadr_cluster_networks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_cluster_networks dynamic management view
ms.assetid: ece32b15-d63f-4f93-92b7-e2930333e97a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: dd37e1f39291e12bd313b03b556506eb51eb131d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829377"
---
# <a name="sysdm_hadr_cluster_networks-transact-sql"></a>sys.dm_hadr_cluster_networks(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  가용성 그룹의 서브넷 구성에 참여하는 모든 WSFC 클러스터 구성원에 대해 하나의 행을 반환합니다. 이 동적 관리 뷰를 사용하여 각 가용성 복제본에 대해 구성된 네트워크 가상 IP의 유효성을 검사할 수 있습니다.  
  
 기본 키: **member_name**  +  **network_subnet_IP**  +  **network_subnet_prefix_length**  
  
 > [!TIP]
 > 부터 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이 동적 관리 뷰는 Always On 가용성 그룹 외에도 Always On 장애 조치 (Failover) 클러스터 인스턴스를 지원 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|WSFC 클러스터에 있는 노드의 컴퓨터 이름입니다.|  
|**network_subnet_ip**|**nvarchar (48)**|컴퓨터가 속한 서브넷의 네트워크 IP 주소입니다. IPv4 또는 IPv6 주소일 수 있습니다.|  
|**network_subnet_ipv4_mask**|**nvarchar (45)**|IP 주소가 속한 서브넷을 지정하는 네트워크 서브넷 마스크입니다. [CREATE AVAILABILITY group](../../t-sql/statements/create-availability-group-transact-sql.md) 또는 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) 문의 WITH dhcp 절에서 dhcp <network_subnet_option> 옵션을 지정 **network_subnet_ipv4_mask** 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] .<br /><br /> NULL = IPv6 서브넷.|  
||||  
|**network_subnet_prefix_length**|**int**|컴퓨터가 속한 서브넷을 지정하는 네트워크 IP 접두사 길이입니다.|  
|**is_public**|**bit**|WSFC 클러스터에서 프라이빗 네트워크인지 퍼블릭 네트워크인지 여부를 나타내며 다음 중 하나입니다.<br /><br /> 0 = 프라이빗<br /><br /> 1 = 공용|  
|**is_ipv4**|**bit**|서브넷의 유형이며 다음 중 하나입니다.<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [장애 조치 (Failover) 클러스터링 및 Always On 가용성 그룹 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Transact-sql&#41;&#40;가용성 그룹 모니터링](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [dm_os_cluster_nodes &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
