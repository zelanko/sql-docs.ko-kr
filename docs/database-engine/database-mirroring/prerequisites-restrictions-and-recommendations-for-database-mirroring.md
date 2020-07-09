---
title: '데이터베이스 미러링: 필수 조건, 제한 사항 및 권장 사항'
description: SQL Server를 사용하여 데이터베이스 미러링을 구성하기 위한 필수 구성 요소, 제한 사항 및 권장 사항에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- partners [SQL Server]
- database mirroring [SQL Server], prerequisites
- database mirroring [SQL Server], recommendations
- database mirroring [SQL Server], restrictions
- database mirroring [SQL Server], planning
- database mirroring [SQL Server], about database mirroring
ms.assetid: fdcf2251-9895-44c6-b81e-768fef32e732
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1b6a98658ec6d550ff9255361cc343bb617fac46
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85735221"
---
# <a name="prerequisites-restrictions-and-recommendations-for-database-mirroring"></a>데이터베이스 미러링을 위한 필수 구성 요소, 제한 사항 및 권장 사항
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)]을 대신 사용합니다.  
  
 이 항목에서는 데이터베이스 미러링을 설정하기 위한 사전 요구 사항 및 권장 사항에 대해 설명합니다. 데이터베이스 미러링에 대한 소개는 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)을 참조하세요.  
  
  
##  <a name="support-for-database-mirroring"></a><a name="DbmSupport"></a> 데이터베이스 미러링 지원  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 데이터베이스 미러링 지원에 대한 자세한 내용은 [SQL Server 2016의 버전 및 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.
  
 데이터베이스 미러링은 지원되는 모든 데이터베이스 호환성 수준에서 작동합니다. 지원되는 호환성 수준에 대한 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.  
  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a> 필수 조건  
  
-   미러링 세션을 설정하려면 파트너 및 미러링 모니터 서버(있는 경우)가 같은 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 실행되어야 합니다.  
  
-   각각 주 서버와 미러 서버인 두 파트너가 같은 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행해야 합니다. 미러링 모니터 서버(있는 경우)는 데이터베이스 미러링을 지원하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 모든 버전에서 실행할 수 있습니다.  
  
    > [!NOTE]  
    >  미러링 세션의 파트너인 서버 인스턴스를 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 업그레이드할 수 있습니다. 자세한 내용은 [Upgrading Mirrored Instances](../../database-engine/database-mirroring/upgrading-mirrored-instances.md)을 참조하세요.  
  
-   이 데이터베이스는 전체 복구 모델을 사용해야 합니다. 단순 복구 모델 및 대량 로그 복구 모델에서는 데이터베이스 미러링이 지원되지 않습니다. 따라서 대량 작업이 미러링된 데이터베이스에 대해 항상 전체 로깅됩니다. 복구 모델에 대한 자세한 내용은 [복구 모델&#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)을 참조하세요.  
  
-   미러 서버에 미러 데이터베이스를 위한 디스크 공간이 충분히 있는지 확인합니다.  
  
    > [!NOTE]  
    >  복제된 데이터베이스에서 데이터베이스 미러링을 사용하는 방법은 [데이터베이스 미러링 및 복제&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)를 참조하세요.  
  
-   미러 서버에 미러 데이터베이스를 만들 때는 WITH NORECOVERY로 동일한 데이터베이스 이름을 지정하여 주 데이터베이스의 백업을 복원하도록 해야 합니다. 백업 후에 생성된 모든 로그 백업 또한 WITH NORECOVERY를 사용하여 적용해야 합니다.  
  
    > [!IMPORTANT]  
    >  데이터베이스 미러링이 중지된 경우 주 데이터베이스에서 수행된 모든 후속 로그 백업을 미러 데이터베이스에 적용해야만 미러링을 다시 시작할 수 있습니다.  
  
  
##  <a name="restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   사용자 데이터베이스만 미러링할 수 있습니다. **master**, **msdb**, **tempdb**또는 **model** 데이터베이스는 미러링할 수 없습니다.  
  
-   데이터베이스 미러링 세션 동안에는 미러된 데이터베이스의 이름을 바꿀 수 없습니다.  
  
-   데이터베이스 미러링은 FILESTREAM을 지원하지 않습니다. 주 서버에서 FILESTREAM 파일 그룹을 만들 수 없습니다. FILESTREAM 파일 그룹이 포함된 데이터베이스에 대해 데이터베이스 미러링을 구성할 수 없습니다.  
  
-   데이터베이스 미러링은 데이터베이스 간 트랜잭션 또는 분산 트랜잭션에서 지원되지 않습니다. 자세한 내용은 [Always On 가용성 그룹 및 데이터베이스 미러링에 대한 데이터베이스 간 트랜잭션 및 분산 트랜잭션&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)를 참조하세요.  
  
  
##  <a name="recommendations-for-configuring-partner-servers"></a><a name="RecommendationsForPartners"></a> 파트너 서버 구성에 대한 권장 사항  
  
-   동일한 작업을 처리할 수 있는 동등한 시스템에서 파트너를 실행해야 합니다.  
  
    > [!NOTE]  
    >  자동 장애 조치(Failover)가 있는 보호 우선 모드를 사용하려면 각 장애 조치(Failover) 파트너의 일반적인 로드에서 사용하는 CPU 양이 50% 미만이어야 합니다. 작업이 CPU를 오버로드하면 장애 조치(Failover) 파트너에서 미러링 세션의 다른 서버 인스턴스에 ping을 실행할 수 없어 불필요한 장애 조치가 발생할 수 있습니다. CPU 사용을 50% 미만으로 유지할 수 없는 경우 자동 장애 조치 없는 보호 우선 모드나 성능 우선 모드를 사용하는 것이 좋습니다.  
  
-   가능한 경우 드라이브 문자를 포함한 미러 데이터베이스의 경로가 주 데이터베이스의 경로와 같아야 합니다. 파일 레이아웃이 다른 경우 RESTORE 문에 MOVE 옵션을 포함해야 합니다. 예를 들어 주 데이터베이스가 'F:' 드라이브에 있는데 미러링 시스템에는 F: 드라이브가 없을 수 있습니다.  
  
    > [!IMPORTANT]  
    >  미러 데이터베이스를 만들 때 데이터베이스 파일을 이동한 경우 나중에 데이터베이스에 파일을 추가하려면 미러링을 일시 중지해야 할 수도 있습니다.  
  
-   미러링 세션의 모든 서버 인스턴스에서 같은 마스터 코드 페이지와 데이터 정렬을 사용해야 합니다. 차이가 있으면 미러링 설정 중에 문제가 발생할 수 있습니다.  
  
-   필요에 따라 데이터베이스 장애 조치에 걸리는 시간을 예상하여 현재 시스템 구성이 필요한 성능을 제공하는지 확인합니다. 자세한 내용은 [역할 전환 중 서비스 중단 예측&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/estimate-the-interruption-of-service-during-role-switching-database-mirroring.md)프로세스를 통해 주 역할과 미러 역할을 서로 바꿀 수 있습니다.  
  
-   최상의 성능을 위해 미러링 전용 네트워크 어댑터(네트워크 인터페이스 카드)를 사용하십시오.  
  
-   보호 우선 모드 사용 시 WAN(광역 통신망)은 데이터베이스 미러링에 대해 안정적이지 않을 수 있습니다. WAN에서 보호 우선 모드를 사용할 경우 필요 없는 자동 장애 조치가 발생할 수 있으므로 세션에 미러링 모니터 서버를 추가하는 방식에 대해 주의해야 합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [데이터베이스 미러링 배포 시의 권장 구성](#RecommendationsForDeploying)을 참조하십시오.  
  
  
##  <a name="recommendations-for-deploying-database-mirroring"></a><a name="RecommendationsForDeploying"></a> 데이터베이스 미러링 배포 시의 권장 구성  
 비동기 작업을 사용하면 데이터베이스 미러링 성능이 최적화됩니다. 동기 작업을 사용하는 미러링 세션의 경우 작업에서 대량의 트랜잭션 로그 데이터가 생성될 때 성능이 저하될 수 있습니다.  
  
 테스트 환경에서 모든 운영 모드를 시험하여 데이터베이스 미러링 성능을 평가하는 것도 좋지만 프로덕션 환경에 미러링을 배포하기 전에 실제 네트워크 작동 방식을 이해하는 것이 중요합니다.  
  
 자동 장애 조치 있는 보호 우선 모드는 가능한 네트워크 오류 출처를 최소화하는 비교적 단순한 네트워크 구성이나 전용 연결이 있는 고품질 서비스 네트워크를 위해 설계되었습니다. 이러한 고품질 네트워크 환경은 자동 장애 조치 있는 보호 우선 모드에 반드시 필요하며 모든 데이터베이스 미러링 세션에 권장됩니다. 그러나 성능 우선 모드와 자동 장애 조치 없는 보호 우선 모드는 네트워크 안정성의 영향을 훨씬 적게 받습니다.  
  
 따라서 프로덕션 환경에 대해 다음 배포 지침을 따르는 것이 좋습니다.  
  
1.  비동기 성능 우선 모드로 실행하기 시작합니다. 이 모드는 네트워크 환경의 영향을 가장 적게 받으며 미러링 작동 방식을 살펴 보기에 가장 좋은 구성을 제공합니다. 대역폭이 미러링을 지원한다는 것이 확인되고 환경에서의 비동기 모드 성능과 미러링 설정을 충분히 이해할 때까지 시스템을 비동기적으로 실행하는 것이 좋습니다. 자세한 내용은 [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)을 참조하세요.  
  
    > [!IMPORTANT]  
    >  테스트 작업 중 세션에서 데이터베이스 미러링 실패를 발생시키는 네트워크 오류를 모니터링하는 것이 좋습니다. 잠재적 오류 출처에 대한 자세한 내용은 [Possible Failures During Database Mirroring](../../database-engine/database-mirroring/possible-failures-during-database-mirroring.md)를 참조하십시오. 데이터베이스 미러링을 모니터링하는 방법은 [데이터베이스 미러링 모니터링&#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)을 참조하세요.  
  
2.  비동기 작업이 비즈니스 요구를 만족시킨다고 확신하는 경우 데이터 보호를 향상시키기 위해 동기 작업을 시도할 수 있습니다. 환경에서 동기 미러링이 어떻게 작동하는지 테스트할 때는 먼저 자동 장애 조치 없는 보호 우선 모드를 테스트하는 것이 좋습니다. 이 테스트의 주요 목적은 동기 작업이 데이터베이스 성능에 미치는 영향을 확인하는 것입니다. 자세한 내용은 [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)을 참조하세요.  
  
3.  자동 장애 조치 없는 보호 우선 모드에서 비즈니스 요구를 만족시키며 네트워크 오류로 인해 실패하지 않는다고 확신하기 전에는 자동 장애 조치를 설정하지 마십시오. 자세한 내용은 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)에서만 사용할 수 있습니다.  
  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 설정&#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [데이터베이스 미러링 및 Always On 가용성 그룹에 대한 전송 보안&#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [데이터베이스 미러링 구성 문제 해결&#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
  
