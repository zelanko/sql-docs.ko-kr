---
title: "유연한 자동 장애 조치 정책 - 가용성 그룹 | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], flexible failover policy
- Availability Groups [SQL Server], failover
- flexible failover policy
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 8c504c7f-5c1d-4124-b697-f735ef0084f0
caps.latest.revision: "29"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e23a4e8d2e814f2dba9217b891672d469251882d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="flexible-automatic-failover-policy---availability-group"></a>유연한 자동 장애 조치 정책 - 가용성 그룹
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 유연한 장애 조치(failover) 정책을 통해 가용성 그룹에 대해 [자동 장애 조치(failover)](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)를 수행해야 하는 상태를 세부적으로 제어할 수 있습니다. 자동 장애 조치를 트리거하는 오류 상태 및 상태 확인 빈도를 변경하여 자동 장애 조치가 수행될 가능성을 높이거나 줄임으로써 고가용성에 대한 SLA를 지원할 수 있습니다.  
  
 가용성 그룹에 대한 유연한 장애 조치(Failover) 정책은 가용성 그룹의 오류 상태 수준 및 상태 확인 제한 시간 임계값으로 정의합니다. 가용성 그룹이 해당 오류 상태 수준 또는 해당 상태 확인 제한 시간 임계값을 초과했음이 감지되면 가용성 그룹의 리소스 DLL은 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터에 다시 응답합니다. 그러면 WSFC 클러스터는 보조 복제본으로 자동 장애 조치를 시작합니다.  
  
> [!IMPORTANT]  
>  가용성 그룹이 해당 WSFC 오류 임계값을 초과하면 WSFC 클러스터가 가용성 그룹에 대해 자동 장애 조치를 시도하지 않습니다. 또한 클러스터 관리자가 실패한 리소스 그룹을 수동으로 온라인 상태로 만들거나 데이터베이스 관리자가 가용성 그룹의 수동 장애 조치를 수행할 때까지 가용성 그룹의 WSFC 리소스 그룹이 실패한 상태로 유지됩니다. *WSFC 오류 임계값* 은 특정 기간 동안 가용성 그룹에 대해 지원되는 최대 오류 수로 정의됩니다. 기본 기간은 6시간이며, 이 기간 동안의 최대 오류 수에 대한 기본값은 *n*-1입니다. 여기서 *n* 은 WSFC 노드의 수입니다. 지정된 가용성 그룹에 대한 오류-임계값 값을 변경하려면 WSFC 장애 조치(Failover) 관리자 콘솔을 사용하세요.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [상태 확인 제한 시간 임계값](#HCtimeout)  
  
-   [오류 상태 수준](#FClevel)  
  
-   [관련 태스크](#RelatedTasks)  
  
-   [관련 내용](#RelatedContent)  
  
##  <a name="HCtimeout"></a> 상태 확인 제한 시간 임계값  
 가용성 그룹의 WSFC 리소스 DLL은 주 복제본을 호스트하는 SQL Server 인스턴스에서 *sp_server_diagnostics* 저장 프로시저를 호출하여 주 복제본에 대해 [상태 확인](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) 을 수행합니다. **sp_server_diagnostics** 은 가용성 그룹에 대한 상태 확인 제한 시간 임계값의 1/3에 해당하는 간격으로 결과를 반환합니다. 기본 상태 확인 제한 시간 임계값은 30초이며 이 값에 도달하면 **sp_server_diagnostics** 가 10초 간격으로 결과를 반환합니다. **sp_server_diagnostics** 가 느리거나 정보를 반환하지 않는 경우 리소스 DLL은 주 복제본이 응답하지 않는 것으로 결정하기 전에 상태 확인 제한 시간 임계값의 전체 간격 동안 대기합니다. 주 복제본이 응답하지 않을 경우 자동 장애 조치(현재 지원되는 경우)가 시작됩니다.  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** 는 데이터베이스 수준에서 상태 확인을 수행하지 않습니다.  
  
##  <a name="FClevel"></a> 오류 상태 수준  
 **sp_server_diagnostics** 에서 반환하는 진단 데이터 및 상태 정보는 가용성 그룹의 오류 상태 수준에 따라 자동 장애 조치(failover)가 수행되도록 합니다. *오류 상태 수준* 은 자동 장애 조치(failover)를 트리거하는 오류 상태를 지정합니다. 가장 낮은 제한 수준 1에서 가장 높은 제한 수준 5까지의 다섯 가지 오류 상태 수준이 있습니다. 특정 수준은 그보다 낮은 모든 제한 수준을 포함합니다. 따라서 가장 엄격한 수준 5에는 그보다 낮은 4개의 제한 상태가 포함됩니다.  
  
> [!IMPORTANT]  
>  손상된 데이터베이스 및 손상될 가능성이 있는 데이터베이스는 실패 조건 수준에 의해 검색되지 않습니다. 따라서 손상 원인이 하드웨어 오류, 데이터 손상 또는 다른 문제점인지와 관계없이 손상된 데이터베이스 또는 손상될 가능성이 있는 데이터베이스는 자동 장애 조치(Failover)를 트리거하지 않습니다.  
  
 다음 표에서는 각 수준에 해당하는 오류 상태를 설명합니다.  
  
|Level|오류 상태|[!INCLUDE[tsql](../../../includes/tsql-md.md)] 값|PowerShell 값|  
|-----------|-----------------------|------------------------------|----------------------|  
|1|서버 작동 중지 시. 다음과 같은 경우 자동 장애 조치를 시작하도록 지정합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 다운된 경우<br /><br /> 서버 인스턴스로부터 ACK를 받지 못해 WSFC 클러스터에 연결할 가용성 그룹의 임대가 만료된 경우. 자세한 내용은 [작동 방법: SQL Server Always On 임대 시간 제한](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)을 참조하세요.<br /><br /> <br /><br /> 제한 수준이 가장 낮은 상태입니다.|1|**OnServerDown**|  
|2|서버 응답 없음 발생 시. 다음과 같은 경우 자동 장애 조치를 시작하도록 지정합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 클러스터에 연결되어 있지 않고 가용성 그룹의 사용자 지정 상태 확인 제한 시간 임계값이 초과된 경우<br /><br /> 가용성 복제본이 오류 상태에 있는 경우|2|**OnServerUnresponsive**|  
|3|중대 서버 오류 발생 시. 분리된 스핀 잠금, 중대한 쓰기 액세스 위반 또는 과도한 덤프와 같이 심각한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 내부 오류가 발생할 경우 자동 장애 조치를 시작하도록 지정합니다.<br /><br /> 이 값은 기본 수준입니다.|3|**OnCriticalServerError**|  
|4|일반 서버 오류 발생 시. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 내부 리소스 풀에서 지속적인 메모리 부족 상태와 같은 일반적인 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 내부 오류가 발생할 경우 자동 장애 조치를 시작하도록 지정합니다.|4|**OnModerateServerError**|  
|5|지정된 오류 상태 발생 시. 다음과 같은 지정된 오류 상태가 발생할 경우 자동 장애 조치를 시작하도록 지정합니다.<br /><br /> 스케줄러 교착 상태가 검색된 경우<br /><br /> 해결할 수 없는 교착 상태가 발견된 경우<br /><br /> <br /><br /> 제한 수준이 가장 높은 상태입니다.|5|**OnAnyQualifiedFailureConditions**|  
  
> [!NOTE]  
>  클라이언트 요청에 대해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 응답이 없는 것은 가용성 그룹과 관련이 없습니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **자동 장애 조치를 구성하려면**  
  
-   [가용성 복제본의 가용성 모드 변경&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)(자동 장애 조치(failover)를 사용하려면 동기-커밋 가용성 모드가 필요함)  
  
-   [가용성 복제본의 장애 조치(failover) 모드 변경&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [유연한 장애 조치(failover) 정책을 구성하여 자동 장애 조치(failover)의 상태 제어&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/configure-flexible-automatic-failover-policy.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   [작동 방법: SQL Server Always On 임대 시간 제한](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 모드&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [장애 조치 및 장애 조치 모드&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)   
 [SQL Server의 WSFC&#40;Windows Server 장애 조치(failover) 클러스터링&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [장애 조치(failover) 클러스터 인스턴스용 장애 조치(failover) 정책](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [sp_server_diagnostics&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)  
  
  
