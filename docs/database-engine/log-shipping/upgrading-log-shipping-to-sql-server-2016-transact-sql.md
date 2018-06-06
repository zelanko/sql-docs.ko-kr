---
title: SQL Server 2016으로 로그 전달 업그레이드(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], upgrading
ms.assetid: b1289cc3-f5be-40bb-8801-0e3eed40336e
caps.latest.revision: 59
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5bf10629a4f28ae4bc41fe7ea1d7a87d82b041ec
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34771719"
---
# <a name="upgrading-log-shipping-to-sql-server-2016-transact-sql"></a>SQL Server 2016으로 로그 전달 업그레이드(Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 전달 구성에서 새 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전, 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]서비스 팩, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]누적 업데이트로 업그레이드할 경우 적적한 순서로 로그 전달 서버를 업그레이드하면 로그 전달 재해 복구 솔루션이 보존됩니다.  
  
> [!NOTE]  
>  [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md) 은 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]에서 도입되었습니다. 업그레이드된 로그 전달 구성은 **백업 압축 기본값** 서버 수준 구성 옵션을 사용하여 백업 압축을 트랜잭션 로그 백업 파일에 사용할지 여부를 제어합니다. 로그 백업에 대한 백업 압축 동작은 각 로그 전달 구성에 지정할 수 있습니다. 자세한 내용은 [로그 전달 구성&#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)에서 도입되었습니다.  
  
 **항목 내용:**  
  
-   [필수 구성 요소](#Prerequisites)  
  
-   [업그레이드하기 전에 데이터 보호](#ProtectData)  
  
-   [모니터 서버 인스턴스 업그레이드](#UpgradeMonitor)  
  
-   [보조 서버 인스턴스 업그레이드](#UpgradeSecondaries)  
  
-   [주 인스턴스 업그레이드](#UpgradePrimary)  
  
##  <a name="Prerequisites"></a> 사전 요구 사항  
 시작하기 전에 다음과 같은 중요한 정보를 검토하십시오.  
  
-   [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md): 사용자의 Windows 운영 체제 버전 및 SQL Server 버전에서 SQL Server 2016으로 업그레이드할 수 있는지 확인합니다. 예를 들어, SQL Server 2005 인스턴스에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 직접 업그레이드할 수 없습니다.  
  
-   [Choose a Database Engine Upgrade Method](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md): 지원되는 버전 및 버전 업그레이드에 대한 검토와 사용자 환경에 설치된 기타 구성 요소를 바탕으로 적절한 업그레이드 방법 및 단계를 선택하여 올바른 순서로 구성 요소를 업그레이드합니다.  
  
-   [데이터베이스 엔진 업그레이드 계획 및 테스트](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md): 릴리스 정보 및 알려진 업그레이드 문제, 업그레이드 전 검사 목록을 검토한 후 업그레이드 계획을 개발하고 테스트합니다.  
  
-   [SQL Server 2016 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md): [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]를 설치하기 위한 소프트웨어 요구 사항을 검토합니다. 추가 소프트웨어가 필요한 경우 가동 중지 시간을 최소화하기 위해 업그레이드 프로세스를 시작하기 전에 각 노드에 설치하십시오.  
  
##  <a name="ProtectData"></a> 업그레이드하기 전에 데이터 보호  
 가능하면 로그 전달 업그레이드 전에 데이터를 보호하는 것이 좋습니다.  
  
 **데이터를 보호하려면**  
  
1.  모든 주 데이터베이스에 대해 전체 데이터베이스 백업을 수행합니다.  
  
     자세한 내용은 [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)에서 차등 데이터베이스 백업을 만듭니다.  
  
2.  모든 주 데이터베이스에서 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 명령을 실행합니다.  
  
> [!IMPORTANT]  
>  보조 서버의 업그레이드가 실행될 것으로 예상될 경우 주 서버에 로그 백업 사본을 저장할 충분한 공간이 있는지 확인합니다.  보조 서버에 대한 장애 조치 중일 경우 이 동일한 문제가 보조 서버(새 주 서버)에 적용됩니다  
  
##  <a name="UpgradeMonitor"></a> (선택 사항) 모니터 서버 인스턴스 업그레이드  
 모니터 서버 인스턴스(있는 경우)는 언제든지 업그레이드할 수 있습니다. 그러나 주 및 보조 서버를 업그레이드할 경우 선택 사항 모니터 서버는 업그레이드하지 않아도 됩니다.  
  
 모니터 서버가 업그레이드되는 동안 로그 전달 구성은 계속 작동하지만 해당 상태는 모니터 테이블에 기록되지 않습니다. 따라서 모니터 서버가 업그레이드되는 동안에는 구성된 경고가 트리거되지 않습니다. 업그레이드 후에는 [sp_refresh_log_shipping_monitor](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md) 시스템 저장 프로시저를 실행하여 모니터 테이블의 정보를 업데이트할 수 있습니다.   모니터 서버에 대한 자세한 내용은 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)를 참조하세요.  
  
##  <a name="UpgradeSecondaries"></a> 보조 서버 인스턴스 업그레이드  
 업그레이드 프로세스에는 주 서버 인스턴스를 업그레이드하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 보조 서버 인스턴스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 로 업그레이드하는 과정이 포함됩니다. 업그레이드할 때는 항상 보조 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 먼저 업그레이드해야 합니다. 업그레이드된 보조 서버 인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 주 서버 인스턴스에서 로그 백업을 계속 복원하기 때문에 전체 업그레이드 프로세스 동안 로그 전달은 계속됩니다. 주 서버 인스턴스를 보조 서버 인스턴스보다 먼저 업그레이드하면 새 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 만든 백업을 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 복원할 수 없기 때문에 로그 전달이 실패합니다. 보조 인스턴스를 동시 또는 차례로 업그레이드할 수 있지만, 로그 전달 오류를 방지하려면 주 인스턴스를 업그레이드하기 전에 모든 보조 인스턴스를 업그레이드해야 합니다.  
  
 보조 서버 인스턴스가 업그레이드되는 동안에는 로그 전달 복사 및 복원 작업은 실행되지 않습니다. 즉, 복원되지 않은 트랜잭션 로그 백업은 주 서버에 누적되며 이러한 복원되지 않은 백업을 저장할 충분한 공간아 있어야 합니다. 누적되는 양은 주 서버 인스턴스에서 예약된 백업의 빈도와 보조 인스턴스를 업그레이드하는 시퀀스에 따라 다릅니다. 또한 별도의 모니터 서버가 구성된 경우 지정된 간격보다 오랫동안 복원이 수행되지 않았음을 나타내는 경고가 발생할 수 있습니다.  
  
 보조 서버 인스턴스가 업그레이드된 후에는 로그 전달 에이전트 작업이 다시 시작되어 계속 주 서버 인스턴스에서 보조 서버 인스턴스로 로그 백업을 복사하고 복원합니다. 보조 서버 인스턴스에서 보조 데이터베이스를 최신 상태로 만드는 데 필요한 시간은 보조 서버 인스턴스를 업그레이드하는 데 걸리는 시간과 주 서버에서 수행되는 백업 빈도에 따라 달라집니다.  
  
> [!NOTE]  
>  서버 업그레이드 도중 보조 데이터베이스 자체는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 데이터베이스로 업그레이드되지 않습니다. 로그 전달 데이터베이스의 장애 조치를 개시하여 온라인 상태가 된 경우에만 업그레이드됩니다. 이론적으로, 이 조건은 무한 지속될 수 있습니다. 장애 조치가 시작되면 데이터베이스 메타데이터를 업그레이드하는 데 소요되는 시간은 짧습니다.  
  
> [!IMPORTANT]  
>  업그레이드가 필요한 데이터베이스에는 RESTORE WITH STANDBY 옵션이 지원되지 않습니다. RESTORE WITH STANDBY를 사용하여 업그레이드된 보조 데이터베이스를 구성한 경우에는 업그레이드 후에 트랜잭션 로그를 더 이상 복원할 수 없습니다. 해당 보조 데이터베이스에서 로그 전달을 재개하려면 해당 대기 서버에서 로그 전달을 다시 설정해야 합니다. STANDBY 옵션에 대한 자세한 내용은 [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)을 참조하세요.  
  
##  <a name="UpgradePrimary"></a> 주 서버 인스턴스 업그레이드  
 로그 전달은 주로 재해 복구 솔루션이므로, 가장 단순하고 가장 일반적인 시나리오는 준비된 주 인스턴스를 업그레이드하는 것이며 해당 데이터베이스는 이 업그레이드 도중에 사용할 수 없게 됩니다. 서버가 업그레이드된 후에는 데이터베이스가 자동으로 업그레이드가 가능한 온라인 상태로 다시 설정됩니다. 데이터베이스가 업그레이드되면 로그 전달 작업이 다시 시작됩니다.  
  
> [!NOTE]  
>  또한 로그 전달은 [로그 전달 보조 데이터베이스로 장애 조치(failover)&#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)에 대한 옵션, 그리고 선택적으로 [주 로그 전달 서버와 보조 로그 전달 서버 간 역할 변경&#40;SQL Server&#41;](../../database-engine/log-shipping/change-roles-between-primary-and-secondary-log-shipping-servers-sql-server.md)을 지원합니다. 그러나 로그 전달이 더 이상 고가용성 솔루션으로 구성되는 경우는 거의 없으므로(최신 옵션이 훨씬 더 강력함), 시스템 데이터베이스 개체가 동기화되지 않기 때문에 장애 조치는 일반적으로 가동 중지 시간을 최소화하지 않으며 클라이언트가 승격된 보조 인스턴스를 쉽게 찾아 연결하기는 어려울 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [설치 마법사를 사용하여 SQL Server 2016으로 업그레이드&#40;설치 프로그램&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [명령 프롬프트에서 SQL Server 2016 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [로그 전달 구성&#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)   
 [로그 전달 모니터링&#40;Transact-SQL&#41;](../../database-engine/log-shipping/monitor-log-shipping-transact-sql.md)   
 [로그 전달 테이블 및 저장 프로시저](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  
