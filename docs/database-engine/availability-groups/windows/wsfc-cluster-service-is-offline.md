---
title: "WSFC 클러스터 서비스가 오프라인 상태임 | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.agdashboard.agp1WSFCquorum.issues.f1"
helpviewer_keywords: 
  - "가용성 그룹 [SQL Server], 정책"
ms.assetid: d502548d-ece6-4a42-9ded-2157d33e3d21
caps.latest.revision: 16
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 16
---
# WSFC 클러스터 서비스가 오프라인 상태임
    
## 소개  
  
|||  
|-|-|  
|**정책 이름**|WSFC 클러스터 상태|  
|**문제점**|WSFC 클러스터 서비스가 오프라인 상태입니다.|  
|**범주**|**심각**|  
|**패싯**|SQL Server 인스턴스|  
  
## 설명  
 이 정책은 WSFC(Windows Server Failover Cluster)의 상태를 확인합니다. WSFC 클러스터가 오프라인 상태이거나 강제 쿼럼 상태에 있는 경우 정책은 비정상 상태에 있으며 경고가 발생합니다. 이 클러스터 내에서 호스팅되는 모든 가용성 그룹이 오프라인이거나 재해 복구 동작이 필요합니다.  
  
 정책 상태는 클러스터 상태가 정상 쿼럼 상태에 있을 때 정상입니다.  
  
> [!NOTE]  
>  이 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 릴리스의 경우 가능한 원인 및 해결 방법은 TechNet Wiki의 [WSFC 클러스터 서비스가 오프라인 상태임](http://go.microsoft.com/fwlink/p/?LinkId=220849)을 참조하세요.  
  
## 가능한 원인  
 이 문제는 클러스터 서비스 문제 또는 클러스터의 쿼럼 손실로 인해 발생할 수 있습니다.  
  
## 가능한 해결 방법  
 클러스터 관리자 도구를 사용하여 강제 쿼럼 또는 재해 복구 워크플로를 수행합니다. 강제 쿼럼 또는 재해 복구 워크플로를 수행하여 문제를 해결할 수 없는 경우 클러스터 관리자에게 이 문제의 해결 방법을 문의하십시오. 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서의 [쿼럼 없이 WSFC 클러스터 강제 시작](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md)을 참조하세요.  
  
## 참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 대시보드 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  