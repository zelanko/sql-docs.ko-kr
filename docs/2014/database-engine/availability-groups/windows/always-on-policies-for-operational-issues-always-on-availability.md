---
title: Always On 가용성 그룹의 운영 문제에 대 한 Always On 정책 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], troubleshooting
- Availability Groups [SQL Server], policies
ms.assetid: afa5289c-641a-4c03-8749-44862384ec5f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 815f549cf9ab6dd7fe748c08ae7f32683c9d8551
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62815758"
---
# <a name="always-on-policies-for-operational-issues-with-always-on-availability-groups-sql-server"></a>Always On 가용성 그룹의 운영 문제에 대한 Always On 정책(SQL Server)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 상태 모델은 미리 정의된 PBM(정책 기반 관리) 정책 집합을 평가합니다. 이를 사용하여 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서 가용성 그룹 및 가용성 복제본과 데이터베이스의 상태를 볼 수 있습니다.  
  
 
  
##  <a name="terms-and-definitions"></a><a name="TermsAndDefinitions"></a>용어 및 정의  
 AlwaysOn 미리 정의된 정책  
 데이터베이스 관리자를 통해 가용성 그룹과 해당 가용성 복제본 및 데이터베이스가 AlwaysOn 정책에서 정의하는 상태를 준수하는지 확인할 수 있도록 하는 기본 제공 정책 집합입니다.  
  
 [AlwaysOn 가용성 그룹](always-on-availability-groups-sql-server.md) 데이터베이스 미러링에 대 한 엔터프라이즈 수준의 대안을 제공 하는 고가용성 및 재해 복구 솔루션입니다.  
  
 가용성 그룹  
 함께 장애 조치(failover)되는 사용자 데이터베이스의 불연속 집합인 *가용성 데이터베이스*의 컨테이너입니다.  
  
 가용성 복제본  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 특정 인스턴스에 의해 호스팅되고 가용성 그룹에 속하는 각 가용성 데이터베이스의 로컬 복사본을 유지 관리하는 가용성 그룹 인스턴스화입니다. 가용성 복제본에는 *주 복제본* 과 1-4개의 *보조 복제본*이라는 두 가지 유형이 있습니다. 지정된 가용성 그룹에 대한 가용성 복제본을 호스팅하는 서버 인스턴스는 단일 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터의 다른 노드에 있어야 합니다.  
  
 가용성 데이터베이스  
 가용성 그룹에 속하는 데이터베이스입니다. 가용성 그룹은 각 가용성 데이터베이스에 대해 하나의 읽기/쓰기 복사본( *주 데이터베이스*)과 1~4개의 읽기 전용 복사본(*보조 데이터베이스*)을 유지 관리합니다.  
  
 AlwaysOn 대시보드  
 가용성 그룹의 상태를 한 눈에 보이도록 표시하는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 대시보드입니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [AlwaysOn 대시보드](#Dashboard)를 참조하세요.  
  
##  <a name="predefined-policies-and-issues"></a><a name="AlwaysOnPBM"></a> 미리 정의된 정책 및 문제  
 다음 표에는 미리 정의된 정책이 요약되어 있습니다.  
  
|정책 이름|문제|범주**<sup>*</sup>**|패싯|  
|-----------------|-----------|------------------------------|-----------|  
|WSFC 클러스터 상태|[WSFC 클러스터 서비스가 오프 라인 상태입니다](wsfc-cluster-service-is-offline.md).|위험|SQL Server 인스턴스|  
|가용성 그룹 온라인 상태|[가용성 그룹이 오프 라인 상태입니다](availability-group-is-offline.md).|위험|가용성 그룹|  
|가용성 그룹 자동 장애 조치(Failover) 준비|[가용성 그룹에 자동 장애 조치 (failover)가 준비 되지 않았습니다](availability-group-is-not-ready-for-automatic-failover.md).|위험|가용성 그룹|  
|가용성 복제본 데이터 동기화 상태|[일부 가용성 복제본에서 데이터를 동기화 하지 않습니다](some-availability-replicas-are-not-synchronizing-data.md).|Warning|가용성 그룹|  
|동기 복제본 데이터 동기화 상태|[일부 동기 복제본이 동기화 되지 않았습니다](some-synchronous-replicas-are-not-synchronized.md).|Warning|가용성 그룹|  
|가용성 복제본 역할 상태|[일부 가용성 복제본에 정상 상태의 역할이 없습니다](some-availability-replicas-do-not-have-a-healthy-role.md).|Warning|가용성 그룹|  
|가용성 복제본 연결 상태|[일부 가용성 복제본의 연결을 끊습니다](some-availability-replicas-are-disconnected.md).|Warning|가용성 그룹|  
|가용성 복제본 역할 상태|[가용성 복제본에 정상 상태의 역할이 없습니다](availability-replica-does-not-have-a-healthy-role.md).|위험|가용성 복제본|  
|가용성 복제본 연결 상태|[가용성 복제본의 연결이 끊어졌습니다](availability-replica-is-disconnected.md).|위험|가용성 복제본|  
|가용성 복제본 조인 상태|[가용성 복제본이 조인 되지](availability-replica-is-not-joined.md)않았습니다.|Warning|가용성 복제본|  
|가용성 복제본 데이터 동기화 상태|[일부 가용성 데이터베이스의 데이터 동기화 상태가 정상이 아닙니다](data-synchronization-state-of-some-availability-database-is-not-healthy.md).|Warning|가용성 복제본|  
|가용성 데이터베이스 일시 중지 상태|[가용성 데이터베이스가 일시 중지 되었습니다](availability-database-is-suspended.md).|Warning|가용성 데이터베이스|  
|가용성 데이터베이스 조인 상태|[보조 데이터베이스가 조인 되지](secondary-database-is-not-joined.md)않았습니다.|Warning|가용성 데이터베이스|  
|가용성 데이터베이스 데이터 동기화 상태|[가용성 데이터베이스의 데이터 동기화 상태가 정상이 아닙니다](data-synchronization-state-of-availability-database-is-not-healthy.md).|Warning|가용성 데이터베이스|  
  
> [!IMPORTANT]  
>  **<sup>*</sup>** AlwaysOn 정책의 경우 범주 이름이 Id로 사용 됩니다. AlwaysOn 범주의 이름을 변경하면 상태 평가 기능이 작동하지 않으므로 이름을 수정하지 마세요.  
  
##  <a name="alwayson-dashboard"></a><a name="Dashboard"></a>AlwaysOn 대시보드  
 AlwaysOn 대시보드에서는 가용성 그룹의 상태를 한 눈에 보이도록 표시합니다. AlwaysOn 대시보드에는 다음과 같은 기능이 포함되어 있습니다.  
  
-   지정한 가용성 그룹, 해당 가용성 복제본 및 해당 데이터베이스에 대한 세부 정보를 손쉽게 표시할 수 있습니다.  
  
-   데이터베이스 관리자가 빠르게 운영에 대한 의사 결정을 할 수 있도록 주요 상태를 시각적으로 표시합니다.  
  
-   다양한 문제를 해결할 수 있는 시작 지점을 제공합니다.  
  
-   특정 운영 문제에 대해 **정책 평가 결과** 대화 상자를 특정 AlwaysOn 상태 정책 위반에 대한 정보 및 문제 해결 도움말에 대한 링크로 채웁니다.  
  
-   AlwaysOn 관련 문제에 대한 이전 이벤트를 표시하는 상태 확장 이벤트 뷰어를 제공합니다.  
  
-   가용성 그룹에 대한 장애 조치가 문제를 해결할 수 있는 경우[가용성 그룹 장애 조치(Failover) 마법사](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)링크에 대한 시작 지점을 제공합니다. 이 마법사는 데이터베이스 관리자에게 수동 장애 조치 과정을 안내합니다.  
  
##  <a name="extending-the-alwayson-health-model"></a><a name="ExtendHealthModel"></a>AlwaysOn 상태 모델 확장  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 상태 모델 확장은 단순히 사용자의 고유한 사용자 정의 정책을 만들고 사용자가 모니터링하는 개체 유형에 따라 이를 특정 범주에 넣는 작업입니다.  일부 설정을 변경한 후에는 AlwaysOn 대시보드가 AlwaysOn 미리 정의된 정책뿐만 아니라 사용자의 고유한 사용자 정의 정책을 자동으로 평가합니다.  
  
 사용자 정의 정책은 AlwaysOn 미리 정의된 정책에서 사용되는 패싯을 포함하여 사용 가능한 모든 PBM 패싯을 사용할 수 있습니다(이 항목의 앞 부분에 나오는 [미리 정의된 정책 및 문제](#AlwaysOnPBM) 참조). 서버 패싯은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 상태 모니터링을 위해 `IsHadrEnabled` 및 `HadrManagerStatus` 속성을 제공합니다. 서버 패싯은 또한 WSFC 클러스터 구성을 모니터링하기 위해 `ClusterQuorumType` 및 `ClusterQuorumState` 정책의 속성을 제공합니다.  
  
 자세한 내용은 [The AlwaysOn Health Model Part 2 -- Extending the Health Model](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)(AlwaysOn 상태 모델 2부 -- 상태 모델 확장)(SQL Server AlwaysOn 팀 블로그)을 참조하세요.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [AlwaysOn 정책을 사용 하 여 가용성 그룹 &#40;SQL Server 상태를 확인&#41;](use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
-   [AlwaysOn 대시보드 사용&#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [강제 쿼럼을 통해 WSFC 재해 복구&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
-   [쿼럼 없이 WSFC 클러스터 강제 시작](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
-   [가용성 그룹의 강제 수동 장애 조치(Failover) 수행&#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [실패 한 파일 추가 작업 문제 해결 AlwaysOn 가용성 그룹 &#40;&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 관련 내용  
  
-   [AlwaysOn 상태 모델 파트 1 -- 상태 모델 아키텍처](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)  
  
-   [AlwaysOn 상태 모델 파트 2 -- 상태 모델 확장](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)  
  
-   [고가용성 및 재해 복구를 위한 Microsoft SQL Server AlwaysOn 솔루션 가이드](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
## <a name="see-also"></a>참고 항목  
 [AlwaysOn 가용성 그룹 (SQL Server)](always-on-availability-groups-sql-server.md)   
 [AlwaysOn 가용성 그룹 &#40;SQL Server 개요&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 관리 &#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)   
 [가용성 그룹 모니터링&#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
  
