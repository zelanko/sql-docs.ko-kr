---
title: "SQL Server 장애 조치(Failover) 클러스터 인스턴스 제거(설치) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clusters [SQL Server], removing failover clustered instance
- failover clustering [SQL Server], removing failover clustered instance
- uninstalling failover clustered instances
- removing failover clustered instances
ms.assetid: bf63353b-69cf-4c5c-98ea-7b151e36537f
caps.latest.revision: 38
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4e3b14ec10f8fcc252363ac061a16469c9f8284c
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="remove-a-sql-server-failover-cluster-instance-setup"></a>SQL Server 장애 조치(Failover) 클러스터 인스턴스 제거(설치)
  이 절차를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치 클러스터형 인스턴스를 제거할 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 업데이트하거나 제거하려면 장애 조치(Failover) 클러스터의 모든 노드에 서비스로 로그인할 수 있는 권한을 가진 로컬 관리자여야 합니다.  
  
 **시작하기 전 주의 사항**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 제거하기 전에 다음 중요 사항을 고려하십시오.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 실수로 제거한 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스가 시작되지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 다시 설치하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 필수 구성 요소를 설치합니다.  
  
-   두 개 이상의 SQL IP 클러스터 리소스를 갖고 있는 장애 조치(Failover) 클러스터를 제거한 경우 클러스터 관리자를 사용하여 추가 SQL IP 리소스를 제거해야 합니다.  
  
 명령 프롬프트 구문에 대한 자세한 내용은 [명령 프롬프트에서 SQL Server 2016 설치](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)를 참조하세요.  
  
### <a name="to-uninstall-a-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 제거하려면  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터를 제거하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램이 제공하는 노드 제거 기능을 사용하여 각 노드를 개별적으로 제거합니다. 자세한 내용은 [SQL Server 장애 조치(failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 설치 로그 파일 보기 및 읽기](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
