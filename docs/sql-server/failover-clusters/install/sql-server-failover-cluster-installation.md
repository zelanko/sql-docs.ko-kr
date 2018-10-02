---
title: SQL Server 장애 조치(Failover) 클러스터 설치 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: c0e75a7c-85c5-423c-a218-77247bf071aa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aa0b798027bbd5eb5d310e31d97378a7375d4d60
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632111"
---
# <a name="sql-server-failover-cluster-installation"></a>SQL Server 장애 조치(Failover) 클러스터 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 설치하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하여 장애 조치(Failover) 클러스터 인스턴스를 만들고 구성해야 합니다.  
  
## <a name="installing-a-failover-cluster"></a>장애 조치(Failover) 클러스터 설치  
 장애 조치(Failover) 클러스터를 설치하려면 서비스로 로그온할 수 있고 장애 조치(Failover) 클러스터의 모든 노드에서 운영 체제의 일부로 실행할 수 있는 로컬 관리자 권한이 있는 도메인 계정을 사용해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 사용하여 장애 조치(Failover) 클러스터를 설치하려면 다음 단계를 따르십시오.  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 설치, 구성 및 유지 관리하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 사용합니다.  
  
    -   우선 장애 조치(Failover) 클러스터 인스턴스를 만드는 데 필요한 정보(예: 클러스터 디스크 리소스, IP 주소 및 네트워크 이름) 및 장애 조치(Failover)에 사용할 수 있는 노드를 확인합니다. 자세한 내용은 다음을 참조하세요.  
  
        -   [장애 조치(Failover) 클러스터링을 설치하기 전에](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)  
  
        -   [SQL Server 설치에 대한 보안 고려 사항](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
    -   구성 단계는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하기 전에 수행해야 합니다. Windows 클러스터 관리자를 사용하여 작업을 수행하십시오. 구성할 각 장애 조치(Failover) 클러스터 인스턴스당 하나의 WSFC 그룹이 있어야 합니다.  
  
    -   시스템이 최소 요구 사항을 충족하는지 확인해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터의 특정 요구 사항에 대한 자세한 내용은 [장애 조치(failover) 클러스터링을 설치하기 전에](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)를 참조하세요.  
  
2.  다른 클러스터 노드에 영향을 주지 않고 장애 조치(Failover) 클러스터 구성에 노드를 추가하거나 제거할 수 있습니다. 자세한 내용은 [SQL Server 장애 조치(failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)을 참조하세요.  
  
    -   장애 조치(Failover) 클러스터의 모든 노드는 32비트 또는 64비트의 동일한 플랫폼에 속해야 하며 동일한 운영 체제 에디션 및 버전을 실행해야 합니다. 또한 64비트 버전의 Windows 운영 체제를 실행 중인 64비트 하드웨어에는 64비트 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 설치해야 합니다. 이 릴리스에서는 장애 조치(Failover) 클러스터링에 WOW64가 지원되지 않습니다.  
  
3.  각 장애 조치(Failover) 클러스터 인스턴스에 대해 IP 주소를 여러 개 지정할 수 있습니다. 각 서브넷에 대해 여러 IP 주소를 지정할 수 있습니다. 같은 서브넷에 여러 IP 주소가 있는 경우에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램에서 종속성을 AND로 설정하고, 여러 서브넷의 노드를 클러스터링하는 경우에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램에서 종속성을 OR로 설정합니다.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-failover-cluster-installation-options"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 설치 옵션  
  
##### <a name="option-1-integrated-installation-with-add-node"></a>옵션 1: 통합 설치 - 노드 추가  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 통합 장애 조치(Failover) 클러스터 설치는 두 단계로 구성됩니다.  
  
1.  단일 노드 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스를 만들고 구성합니다. 노드 구성을 완료하면 완벽하게 작동하는 장애 조치(Failover) 클러스터 인스턴스가 만들어집니다. 이 시점에서는 장애 조치(Failover) 클러스터에 노드가 하나뿐이므로 고가용성은 지원되지 않습니다.  
  
2.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 추가할 각 노드에서 노드 추가 기능으로 설치를 실행하여 해당 노드를 추가합니다.  
  
##### <a name="option-2-advancedenterprise-installation"></a>옵션 2: 고급/엔터프라이즈 설치  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 고급/엔터프라이즈 장애 조치(failover) 클러스터 설치는 두 단계로 구성됩니다.  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 속한 각 노드에서 장애 조치(Failover) 클러스터 준비 기능으로 설치를 실행합니다. 이 단계는 노드를 클러스터링할 수 있도록 준비하지만 이 시점에서는 작동하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 없습니다.  
  
2.  노드를 클러스터링할 수 있도록 준비했으면 공유 디스크를 소유하는 노드에서 장애 조치(Failover) 클러스터 완료 기능으로 설치를 실행합니다. 이 단계는 장애 조치(Failover) 클러스터 인스턴스를 구성하고 완료합니다. 이 단계를 마치면 정상적으로 작동하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스가 만들어집니다.  
  
    > [!NOTE]  
    >  다중 노드 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 설치의 경우 어떤 옵션을 사용해도 됩니다. 어떤 옵션을 사용하든지 간에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 만든 후 노드 추가 기능을 사용하여 노드를 추가할 수 있습니다.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 위치에 대한 운영 체제 드라이브 문자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 추가된 모든 노드와 일치해야 합니다.  
  
#### <a name="ip-address-configuration-during-setup"></a>설치 중 IP 주소 구성  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 통해 다음 작업 중에 IP 리소스 종속성 설정을 설정하거나 변경할 수 있습니다.  
  
-   통합 설치 - [새 SQL Server 장애 조치(failover) 클러스터 만들기&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)  
  
-   CompleteFailoverCluster(고급 설치) - [새 SQL Server 장애 조치(failover) 클러스터 만들기&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)  
  
-   노드 추가 - [SQL Server 장애 조치(failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
-   노드 제거 - [SQL Server 장애 조치(failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
 **참고** IPV6 IP 주소는 지원되지 않습니다.  IPV4와 IPV6을 둘 다 구성하면 서로 다른 서브넷으로 처리되고 IPV6이 먼저 온라인 상태가 됩니다.  
  
##### <a name="includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다중 서브넷 장애 조치(failover) 클러스터  
 클러스터의 노드가 서로 다른 서브넷에 있는 경우 종속성을 OR로 설정할 수 있습니다. 그러나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다중 서브넷 장애 조치(Failover) 클러스터의 각 노드가 지정된 IP 주소를 하나 이상 소유할 수 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [장애 조치(Failover) 클러스터링을 설치하기 전에](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)   
 [새 SQL Server 장애 조치(failover) 클러스터 만들기&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)   
 [명령 프롬프트에서 SQL Server 2016 설치](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [SQL Server 장애 조치(failover) 클러스터 인스턴스 업그레이드](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)  
  
  
