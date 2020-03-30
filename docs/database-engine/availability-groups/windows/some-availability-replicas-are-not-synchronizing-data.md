---
title: 데이터를 동기화하지 않는 가용성 복제본
description: Always On 가용성 그룹에 있는 하나 이상의 가용성 복제본이 주 복제본과 데이터를 동기화하지 않는 경우 가능한 원인 및 해결 방법입니다.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.agp4synchronizing.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 3db6a569-e942-4321-a0dd-c4ab002087c8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 66ebb11535fe2eecc6495b8c5e194d286ecc88ed
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74822586"
---
# <a name="some-availability-replicas-are-not-synchronizing-data"></a>일부 가용성 복제본에서 데이터 동기화가 수행되지 않음
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>소개  
  
|||  
|-|-|  
|**정책 이름**|가용성 복제본 데이터 동기화 상태|  
|**문제점**|일부 가용성 복제본에서 데이터 동기화가 수행되지 않음|  
|**범주**|**경고**|  
|**패싯**|가용성 그룹|  
  
## <a name="description"></a>Description  
 이 정책은 가용성 그룹에 있는 모든 가용성 복제본의 데이터 동기화 상태를 롤업하여 가용성 복제본의 동기화가 작동 중이 아닌지 확인합니다. 데이터 동기화 상태가 NOT SYNCRONIZING인 가용성 복제본이 있으면 정책이 비정상 상태입니다.  
  
 데이터 동기화 상태가 NOT SYNCRONIZING인 가용성 복제본이 없으면 정책이 정상 상태입니다.  
  
> [!NOTE]  
>  이 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]릴리스의 경우 가능한 원인 및 해결 방법은 TechNet Wiki의 [일부 가용성 복제본에서 데이터 동기화가 수행되지 않음](https://go.microsoft.com/fwlink/p/?LinkId=220852) 을 참조하세요.  
  
## <a name="possible-causes"></a>가능한 원인  
 이 가용성 그룹에서 하나 이상의 보조 복제본이 NOT SYNCHRONIZING 동기화 상태에 있으며 주 복제본에서 데이터를 받고 있지 않습니다.  
  
## <a name="possible-solution"></a>가능한 해결 방법  
 가용성 복제본 정책 상태를 사용하여 상태가 NOT SYNCHROINIZING인 가용성 복제본을 찾은 다음 해당 가용성 복제본에서 문제를 해결합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 대시보드 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
