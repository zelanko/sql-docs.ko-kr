---
title: 복제본은 가용성 그룹에 대해 정상적인 역할을 수행하지 않습니다.
description: Always On 가용성 그룹 내에서 가용성 복제본이 정상적인 역할을 수행하지 못하는 이유의 가능한 원인을 파악합니다.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.arp1rolehealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: ebb2c9f4-2097-4688-b4fb-8f0571047317
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 91b73682ffd7d626592193c5b729896ec3d593a2
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75241770"
---
# <a name="availability-replica-does-not-have-a-healthy-role-for-an-always-on-availability-group"></a>가용성 복제본은 Always On 가용성 그룹에 대해 정상적인 역할을 수행하지 않습니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>소개  
  
|||  
|-|-|  
|**정책 이름**|가용성 복제본 역할 상태|  
|**문제점**|가용성 복제본에 정상 상태의 역할이 없습니다.|  
|**범주**|**심각**|  
|**패싯**|가용성 복제본|  
  
## <a name="description"></a>Description  
 이 정책은 가용성 복제본의 역할 상태를 확인합니다. 가용성 복제본의 역할이 주 역할이나 보조 역할이 아닌 경우 정책은 비정상 상태에 있습니다. 그렇지 않으면 정책은 정상 상태입니다.  
  
> [!NOTE]  
>  이 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]릴리스의 경우 가능한 원인 및 해결 방법에 대한 자세한 내용은 TechNet Wiki의 [가용성 복제본에 정상 상태의 역할이 없음](https://go.microsoft.com/fwlink/p/?LinkId=220856) 을 참조하세요.  
  
## <a name="possible-causes"></a>가능한 원인  
 이 가용성 복제본의 역할이 비정상 상태에 있습니다. 복제본에 주 역할 또는 보조 역할이 없습니다.  
  
## <a name="possible-solution-information_still_to_come"></a>가능한 해결 방법: Information_still_to_come  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 대시보드 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
