---
title: SQL Server 장애 조치 (Failover) 클러스터 업그레이드 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading failover clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
ms.assetid: daac41fe-7d0b-4f14-84c2-62952ad8cbfa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a7a8d5f04808582bd56c106adce0df2c1f66aa77
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62913728"
---
# <a name="upgrade-a-sql-server-failover-cluster"></a>SQL Server 장애 조치(Failover) 클러스터 업그레이드
  
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 모든 장애 조치(Failover) 클러스터 노드에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 및 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 장애 조치(Failover) 클러스터의 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 및 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]를 개별적으로 업그레이드할 수 있도록 지원합니다.  
  
 자세한 내용은 다음과 같습니다.  
  
-   업그레이드는 사용자 인터페이스 및 명령 프롬프트를 사용하여 수행할 수 있습니다. 자세한 내용은 [SQL Server 장애 조치(failover) 클러스터 인스턴스 업그레이드&#40;설치 프로그램&#41;](upgrade-a-sql-server-failover-cluster-instance-setup.md) 및 [명령 프롬프트에서 SQL Server 2014 설치](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)를 참조하세요.  
  
-   에서 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 업그레이드-각 장애 조치 (failover) 클러스터 노드의 명령 프롬프트에서 업그레이드를 실행 하거나 설치 UI를 사용 하 여 각 클러스터 노드를 업그레이드할 수 있습니다. 전체 텍스트 검색 및 복제 기능이 업그레이드 중인 인스턴스에 없는 경우 자동으로 설치되고 이를 생략할 수 있는 옵션은 없습니다.  
  
-   서비스 팩 설치 - 모든 노드의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 개별적으로 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 서비스 팩 및 패치를 적용해야 합니다.  
  
-   다음과 같은 시나리오는 지원되지 않습니다.  
  
    -   독립 실행형 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 장애 조치(Failover) 클러스터로 마이그레이션할 수 없습니다.  
  
    -   장애 조치(Failover) 클러스터에 기능을 추가합니다. 예를 들어 기존의 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 전용 장애 조치(Failover) 클러스터에 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]을 추가할 수 없습니다.  
  
    -   장애 조치(Failover) 클러스터 노드를 독립 실행형 인스턴스로 다운그레이드할 수 없습니다.  
  
-   자세한 내용은 [Always On 장애 조치(failover) 클러스터 인스턴스(SQL Server)](always-on-failover-cluster-instances-sql-server.md)를 참조하세요.  
  
## <a name="upgrading-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다중 서브넷 장애 조치(Failover) 클러스터로 업그레이드  
 다중 서브넷 장애 조치 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (failover) 클러스터를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다중 서브넷 장애 조치 (failover) 클러스터로 직접 업그레이드할 수 없습니다. 자세한 내용은 [SQL Server 장애 조치(failover) 클러스터 인스턴스 업그레이드&#40;설치 프로그램&#41;](upgrade-a-sql-server-failover-cluster-instance-setup.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [지원되는 버전 및 에디션 업그레이드](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [SQL Server 장애 조치 (Failover) 클러스터 인스턴스를 업그레이드 &#40;설정&#41;](upgrade-a-sql-server-failover-cluster-instance-setup.md)   
 [Install SQL Server 2014 from the Command Prompt](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  
  
  
