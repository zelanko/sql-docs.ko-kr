---
title: 가용성 그룹 수신기 속성 보기(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygrouplistenerproperties.general.f1
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
ms.assetid: aca0d016-3228-40b8-bdc3-285ed6d9b280
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 86c111300429215baaa787611ffebb9103d7757a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66780128"
---
# <a name="view-availability-group-listener-properties-sql-server"></a>가용성 그룹 수신기 속성 보기(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 *에서* 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)] Always On 가용성 그룹 수신기 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]의 속성을 보는 방법에 대해 설명합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **수신기 속성을 보려면**  
  
1.  개체 탐색기에서 수신기를 볼 가용성 그룹의 가용성 복제본을 호스팅하는 서버 인스턴스에 연결합니다. 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  가용성 그룹의 노드를 확장하고 **가용성 그룹 수신기** 노드를 확장합니다.  
  
4.  보려는 수신기를 마우스 오른쪽 단추로 클릭하고 **속성** 명령을 선택합니다.  
  
5.  **가용성 그룹 수신기 속성** 대화 상자가 열립니다. 자세한 내용은 이 항목의 뒷부분에 나와 있는 [가용성 그룹 수신기 속성(대화 상자)](#AgListenerPropertiesDialog)을 참조하세요.  
  
###  <a name="AgListenerPropertiesDialog"></a> 가용성 그룹 수신기 속성(대화 상자)  
 **수신기 DNS 이름**  
 가용성 그룹 수신기의 네트워크 이름입니다.  
  
 **포트**  
 이 수신기에서 사용되는 TPC 포트입니다.  
  
> [!NOTE]  
>  주 복제본을 연결한 경우 이 필드를 사용하여 수신기의 포트 번호를 수정할 수 있습니다. 이렇게 하려면 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  
  
 **네트워크 모드**  
 수신기에 사용되는 TCP 프로토콜을 나타내며 다음 중 하나입니다.  
  
 **DHCP**  
 수신기는 DHCP(동적 호스트 구성 프로토콜)를 실행하는 서버에 의해 할당되는 동적 IP 주소를 사용합니다.  
  
 **고정 IP**  
 수신기는 하나 이상의 고정 IP 주소를 사용합니다. 다른 서브넷에 액세스하려면 가용성 그룹 수신기가 정적 고정 IP 주소를 사용해야 합니다.  
  
 표에는 수신기가 수신하는 각 서브넷 및 해당 서브넷과 연결된 IP 주소가 표시됩니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **수신기 속성을 보려면**  
  
 가용성 그룹 수신기를 모니터링하려면 다음 뷰를 사용합니다.  
  
 [sys.availability_group_listener_ip_addresses](../../../relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql.md)  
 가용성 그룹 수신기에 대해 현재 온라인인 규칙에 부합하는 모든 가상 IP 주소에 대해 하나의 행을 반환합니다.  
  
 **열 이름:** listener_id, ip_address, ip_subnet_mask, is_dhcp, network_subnet_ip, network_subnet_prefix_length, network_subnet_ipv4_mask, state, state_desc  
  
 [sys.availability_group_listeners](../../../relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql.md)  
 지정된 가용성 그룹에 대해 0개의 행을 반환하여 가용성 그룹에 연결된 네트워크 이름이 없음을 나타내거나 WSFC 클러스터의 각 가용성 그룹 수신기 구성에 대해 하나의 행을 반환합니다.  
  
 **열 이름:** group_id, listener_id, dns_name, port, is_conformant, ip_configuration_string_from_cluster  
  
 [sys.dm_tcp_listener_states](../../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md)  
 각 TCP 수신기에 대한 동적 상태 정보를 포함하는 행을 반환합니다.  
  
 **열 이름:** listener_id, ip_address, is_ipv4, port, type, type_desc, state, state_desc, start_time  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 사용하여 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 환경을 모니터링하는 방법은 [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)을 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [가용성 그룹 수신기 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
