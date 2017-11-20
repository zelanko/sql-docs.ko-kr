---
title: "일부 가용성 복제본에 상태 역할이 없음 | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.agdashboard.agp6allroleshealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 7ec5b337-7201-4a66-a541-7560f8b18784
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f5d0767d61b178905b5675fa1b2b5d8f59650510
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="some-availability-replicas-do-not-have-a-healthy-role"></a>일부 가용성 복제본에 정상 상태의 역할이 없음
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>소개  
  
|||  
|-|-|  
|**정책 이름**|가용성 복제본 역할 상태|  
|**문제점**|일부 가용성 복제본에 정상 상태의 역할이 없습니다.|  
|**범주**|**경고**|  
|**패싯**|가용성 그룹|  
  
## <a name="description"></a>설명  
 이 정책은 모든 가용성 복제본의 연결 상태를 롤업하며 정상 상태의 역할에 없는 가용성 복제본이 있는지 확인합니다. 가용성 복제본이 주 복제본이나 보조 복제본이 아닌 경우 정책은 비정상 상태에 있습니다. 그렇지 않으면 정책은 정상 상태입니다.  
  
> [!NOTE]  
>  이 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]릴리스의 경우 가능한 원인 및 해결 방법은 TechNet Wiki의 [일부 가용성 복제본에 정상 상태의 역할이 없음](http://go.microsoft.com/fwlink/p/?LinkId=220854) 을 참조하세요.  
  
## <a name="possible-causes"></a>가능한 원인  
 이 가용성 그룹의 하나 이상의 가용성 복제본에는 현재 주 역할이나 보조 역할이 없습니다.  
  
## <a name="possible-solution"></a>가능한 해결 방법  
 가용성 복제본 정책 상태를 사용하여 역할이 주 역할이나 보조 역할이 아닌 가용성 복제본을 찾은 다음 가용성 복제본에서 문제를 해결합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 대시보드 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  

