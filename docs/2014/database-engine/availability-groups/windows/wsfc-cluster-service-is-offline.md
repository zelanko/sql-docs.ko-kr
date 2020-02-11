---
title: WSFC 클러스터 서비스가 오프라인 상태임 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp1WSFCquorum.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: d502548d-ece6-4a42-9ded-2157d33e3d21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cfab5de4cd3d171d4d8b7515e65b0a9cd117ac16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62812901"
---
# <a name="wsfc-cluster-service-is-offline"></a>WSFC 클러스터 서비스가 오프라인 상태임
    
## <a name="introduction"></a>소개  
  
|||  
|-|-|  
|**정책 이름**|WSFC 클러스터 상태|  
|**문제점**|WSFC 클러스터 서비스가 오프라인 상태입니다.|  
|**범주**|**심각**|  
|**패싯**|SQL Server 인스턴스|  
  
## <a name="description"></a>Description  
 이 정책은 WSFC(Windows Server Failover Cluster)의 상태를 확인합니다. WSFC 클러스터가 오프라인 상태이거나 강제 쿼럼 상태에 있는 경우 정책은 비정상 상태에 있으며 경고가 발생합니다. 이 클러스터 내에서 호스팅되는 모든 가용성 그룹이 오프라인이거나 재해 복구 동작이 필요합니다.  
  
 정책 상태는 클러스터 상태가 정상 쿼럼 상태에 있을 때 정상입니다.  
  
> [!NOTE]  
>  이 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]릴리스의 경우 가능한 원인 및 해결 방법은 TechNet Wiki의 [WSFC 클러스터 서비스가 오프라인 상태임](https://go.microsoft.com/fwlink/p/?LinkId=220849) 을 참조하세요.  
  
## <a name="possible-causes"></a>가능한 원인  
 이 문제는 클러스터 서비스 문제 또는 클러스터의 쿼럼 손실로 인해 발생할 수 있습니다.  
  
## <a name="possible-solution"></a>가능한 해결 방법  
 클러스터 관리자 도구를 사용하여 강제 쿼럼 또는 재해 복구 워크플로를 수행합니다. 강제 쿼럼 또는 재해 복구 워크플로를 수행하여 문제를 해결할 수 없는 경우 클러스터 관리자에게 이 문제의 해결 방법을 문의하십시오. 자세한 내용은 [온라인 설명서의](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md) 쿼럼 없이 WSFC 클러스터 강제 시작 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [AlwaysOn 가용성 그룹 &#40;SQL Server 개요&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 대시보드 &#40;SQL Server Management Studio를 사용&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
