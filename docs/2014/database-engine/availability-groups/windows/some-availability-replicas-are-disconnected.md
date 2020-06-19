---
title: 일부 가용성 복제본의 연결이 해제됨 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp7allconnected.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: aea808be-6f0f-40c2-9aa2-a2a435ec6443
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0ff3efc9f98745154960f18945d806d28043d73c
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936464"
---
# <a name="some-availability-replicas-are-disconnected"></a>일부 가용성 복제본의 연결이 해제됨
    
## <a name="introduction"></a>소개  
  
|||  
|-|-|  
|**정책 이름**|가용성 복제본 연결 상태|  
|**문제점**|일부 가용성 복제본의 연결이 해제됩니다.|  
|**범주**|**Warning**|  
|**패싯에**|가용성 그룹|  
  
## <a name="description"></a>Description  
 이 정책은 모든 가용성 복제본의 연결 상태를 롤업하며 연결이 해제된 가용성 복제본이 있는지 확인합니다. 가용성 복제본의 연결이 해제된 경우 정책은 비정상 상태에 있습니다. 그렇지 않으면 정책은 정상 상태입니다.  
  
> [!NOTE]  
>   이 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]릴리스의 경우 가능한 원인 및 해결 방법에 대한 자세한 내용은 TechNet Wiki의 [일부 가용성 복제본의 연결이 해제됨](https://go.microsoft.com/fwlink/p/?LinkId=220855) 을 참조하십시오.  
  
## <a name="possible-causes"></a>가능한 원인  
 이 가용성 그룹의 하나 이상의 보조 복제본이 주 복제본에 연결되어 있지 않습니다. 연결 상태가 DISCONNECTED입니다.  
  
## <a name="possible-solution"></a>가능한 해결 방법  
 가용성 복제본 정책 상태를 사용하여 DISCONNECTED 상태인 가용성 복제본을 찾은 다음 가용성 복제본에서 문제를 해결합니다.  
  
## <a name="see-also"></a>참고 항목  
 [AlwaysOn 가용성 그룹 &#40;SQL Server 개요&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 대시보드 사용&#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
