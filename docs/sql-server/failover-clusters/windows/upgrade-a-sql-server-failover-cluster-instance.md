---
title: SQL Server 장애 조치(failover) 클러스터 인스턴스 업그레이드 | Microsoft 문서
ms.custom: ''
ms.date: 10/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: failover-clusters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- upgrading failover clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
ms.assetid: daac41fe-7d0b-4f14-84c2-62952ad8cbfa
caps.latest.revision: 47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0b2b516e71d14bc8615505c22f1317255925ba5d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="upgrade-a-sql-server-failover-cluster-instance"></a>SQL Server 장애 조치(failover) 클러스터 인스턴스 업그레이드
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 새 버전, 새 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 팩 또는 누적 업데이트로 업그레이드할 수 있습니다. 또한 모든 장애 조치(failover) 클러스터 노드에서 새 Windows 서비스 팩 또는 누적 업데이트를 별도로 설치하여 업그레이드할 때는 가동 중지 시간을 수동 장애 조치(failover) 1회에 걸리는 시간으로 제한할 수 있습니다. 원래 주 서버로 장애 복구(failback)할 때는 수동 장애 조치(failover) 2회에 걸리는 시간이 소요됩니다.  
  
 [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] 이전의 운영 체제에서는 장애 조치(failover) 클러스터의 Windows 운영 체제를 업그레이드할 수 없습니다. [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] 이상에서 실행 중인 클러스터 노드를 업그레이드하려면 [롤링 업그레이드 또는 업데이트 수행](#perform-a-rolling-upgrade-or-update)을 참조하세요.  
  
 자세한 내용은 다음과 같습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 업그레이드는 사용자 인터페이스 및 명령 프롬프트를 통해 수행할 수 있습니다. 각 장애 조치(failover) 클러스터 노드의 명령 프롬프트에서 업그레이드를 실행하거나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램 UI를 사용하여 각 클러스터 노드를 업그레이드할 수 있습니다.  자세한 내용은 [SQL Server 장애 조치(failover) 클러스터 인스턴스 업그레이드 &#40;설정&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md) 및 [명령 프롬프트에서 SQL Server 설치](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)를 참조하세요.  
  
-   다음 시나리오는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 업그레이드의 일부분으로 지원되지 않습니다.  
  
    -   독립 실행형 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 장애 조치(failover) 클러스터로 업그레이드할 수는 없습니다.  
  
    -   장애 조치(failover) 클러스터에 기능을 추가할 수는 없습니다. 예를 들어 기존의 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 전용 장애 조치(Failover) 클러스터에 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]을 추가할 수 없습니다.  
  
    -   장애 조치(Failover) 클러스터 노드를 독립 실행형 인스턴스로 다운그레이드할 수 없습니다.  
  
    -   장애 조치(Failover) 클러스터의 버전 변경은 특정 시나리오로만 제한됩니다. 자세한 내용은 [지원되는 버전 및 에디션 업그레이드](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)를 참조하세요.  
  
-   장애 조치(Failover) 클러스터 업그레이드 도중 작동 중단 시간은 장애 조치(Failover) 시간 및 업그레이드 스크립트 실행에 필요한 시간으로만 제한됩니다. 아래의 장애 조치(failover) 클러스터 롤링 업그레이드 프로세스를 수행하는 경우 업그레이드 프로세스를 시작하기 전에 모든 노드에서 필수 구성 요소를 모두 충족하면 가동 중지 시간을 최소화할 수 있습니다. 메모리 최적화 테이블을 사용하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 업그레이드하려면 시간이 더 걸립니다. 자세한 내용은 [Plan and Test the Database Engine Upgrade Plan](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)를 참조하세요.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 시작하기 전에 다음과 같은 중요한 정보를 검토하십시오.  
  
-   [지원되는 버전 및 버전 업그레이드](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md): 사용자의 Windows 운영 체제 버전 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전에서 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]로 업그레이드할 수 있는지 확인합니다. 예를 들어 SQL Server 2005 장애 조치(failover) 클러스터링 인스턴스에서 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]로 직접 업그레이드하거나 [!INCLUDE[winxpsvr-md](../../../includes/winxpsvr-md.md)]에서 실행 중인 장애 조치(failover) 클러스터를 업그레이드할 수는 없습니다.  
  
-   [Choose a Database Engine Upgrade Method](../../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md): 지원되는 버전 및 버전 업그레이드에 대한 검토와 사용자 환경에 설치된 기타 구성 요소를 바탕으로 적절한 업그레이드 방법 및 단계를 선택하여 올바른 순서로 구성 요소를 업그레이드합니다.  
  
-   [데이터베이스 엔진 업그레이드 계획 및 테스트](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md): 릴리스 정보 및 알려진 업그레이드 문제, 업그레이드 전 검사 목록을 검토한 후 업그레이드 계획을 개발하고 테스트합니다.  
  
-   [SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md): [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]를 설치하기 위한 소프트웨어 요구 사항을 검토합니다. 추가 소프트웨어가 필요한 경우 가동 중지 시간을 최소화하기 위해 업그레이드 프로세스를 시작하기 전에 각 노드에 설치하십시오.  
  
## <a name="perform-a-rolling-upgrade-or-update"></a>롤링 업그레이드 또는 업데이트 수행  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터를 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]로 업그레이드하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 사용해 패시브 노드부터 시작하여 한 번에 하나의 장애 조치(failover) 클러스터 노드를 업그레이드합니다. 업그레이드된 각 노드는 장애 조치 클러스터의 가능한 소유자 노드에서 제외됩니다. 예기치 않은 장애 조치(failover)가 수행되면 클러스터 리소스 그룹 소유권이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램에 의해 업그레이드된 노드로 이동하기 전까지는 업그레이드된 노드가 장애 조치(failover)에 참여하지 않습니다.  
  
 업그레이드된 노드로 장애 조치(failover)를 수행할 시기는 기본적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램에서 자동으로 결정됩니다. 이 시기는 장애 조치 클러스터 인스턴스의 총 노드 수 및 이미 업그레이드된 노드 수에 따라 다릅니다. 절반 이상의 노드가 이미 업그레이드된 경우 다음 노드에서 업그레이드를 수행하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램은 업그레이드된 노드로의 장애 조치(failover)를 수행합니다. 업그레이드된 노드로 장애 조치가 수행되면 곧바로 클러스터 그룹이 업그레이드된 노드로 이동합니다. 업그레이드된 모든 노드가 가능한 소유자 목록에 배치되고 업그레이드되지 않은 모든 노드는 가능한 소유자 목록에서 제거됩니다. 남아 있는 각 노드를 업그레이드하면 이러한 노드는 장애 조치 클러스터의 가능한 소유자 노드에 추가됩니다.  
  
 이 프로세스로 인해 전체 장애 조치(Failover) 클러스터 업그레이드 중의 작동 중단은 장애 조치(Failover) 시간 및 데이터베이스 업그레이드 스크립트 실행 시간으로만 제한됩니다.  
  
 업그레이드 프로세스 중에 클러스터 노드의 장애 조치(Failover) 동작을 제어하려면 명령 프롬프트에서 업그레이드 작업을 실행하고 /FAILOVERCLUSTERROLLOWNERSHIP 매개 변수를 사용합니다. 자세한 내용은 [명령 프롬프트에서 SQL Server 설치](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)를 참조하세요.  
  
## <a name="next-steps"></a>다음 단계  
 [설치 마법사를 사용하여 SQL Server 업그레이드&#40;설치 프로그램&#41;](../../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [명령 프롬프트에서 SQL Server 설치](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [SQL Server 장애 조치(failover) 클러스터 인스턴스 업그레이드&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)  
  
  
