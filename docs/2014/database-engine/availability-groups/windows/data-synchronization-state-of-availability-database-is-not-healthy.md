---
title: 가용성 데이터베이스의 데이터 동기화 상태가 정상이 아님 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.arp3datasynchealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 4fd003e7-808e-4b0e-b28a-47d9f2616f06
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1aa901fe3230a76af3127af41630b075414d77a6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096879"
---
# <a name="data-synchronization-state-of-availability-database-is-not-healthy"></a>가용성 데이터베이스의 데이터 동기화 상태가 정상이 아님
    
## <a name="introduction"></a>소개  
  
|||  
|-|-|  
|**정책 이름**|가용성 데이터베이스 데이터 동기화 상태|  
|**문제점**|가용성 데이터베이스의 데이터 동기화 상태가 정상이 아님|  
|**범주**|**경고**|  
|**패싯**|가용성 데이터베이스|  
  
## <a name="description"></a>Description  
 이 정책은 가용성 복제본에서 모든 가용성 데이터베이스("데이터베이스 복제본"이라고도 함)의 데이터 동기화 상태를 롤업합니다. 예상되는 데이터 동기화 상태가 아닌 데이터베이스 복제본이 있으면 정책이 비정상 상태입니다. 그렇지 않으면 정책은 정상 상태입니다.  
  
> [!NOTE]  
>  이 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]릴리스의 경우 가능한 원인 및 해결 방법에 대한 자세한 내용은 TechNet Wiki의 [일부 가용성 데이터베이스의 데이터 동기화 상태가 정상이 아님](http://go.microsoft.com/fwlink/p/?LinkId=220858) 을 참조하세요.  
  
## <a name="possible-causes"></a>가능한 원인  
 이 가용성 데이터베이스의 데이터 동기화 상태가 정상이 아닙니다. 비동기 커밋 가용성 복제본에서 모든 가용성 데이터베이스는 SYNCHRONIZING 상태여야 합니다. 동기 커밋 복제본에서 모든 가용성 데이터베이스는 SYNCHRONIZED 상태에 있어야 합니다.  
  
## <a name="possible-solution"></a>가능한 해결 방법  
 데이터베이스 복제본 정책을 사용하여 비정상 데이터 동기화 상태의 데이터베이스 복제본을 찾은 다음 해당 데이터베이스 복제본에서 이 문제를 해결합니다.  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 대시보드 사용&#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
