---
title: 일부 가용성 데이터베이스의 데이터 동기화 상태가 정상이 아님 | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.drp3datasynchealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 89f95d15-33c6-4768-bccd-9dbf8c4f49a9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f9260f9de24d282b3b6ce5c4e46b4572e01aafa9
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51604459"
---
# <a name="data-synchronization-state-of-some-availability-database-is-not-healthy"></a>일부 가용성 데이터베이스의 데이터 동기화 상태가 정상이 아님
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>소개  
  
|||  
|-|-|  
|**정책 이름**|가용성 복제본 데이터 동기화 상태|  
|**문제점**|일부 가용성 데이터베이스의 데이터 동기화 상태가 정상이 아닙니다.|  
|**범주**|**경고**|  
|**패싯**|가용성 복제본|  
  
## <a name="description"></a>설명  
 이 정책은 가용성 데이터베이스("데이터베이스 복제본"이라고도 함)의 데이터 동기화 상태를 확인합니다. 데이터 동기화 상태가 NOT SYNCHRONIZING이거나 동기 커밋 데이터베이스 복제본에 대한 상태가 SYNCHRONIZED 상태가 아닌 경우 정책은 비정상 상태에 있습니다.  
  
> [!NOTE]  
>  이 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]릴리스의 경우 가능한 원인 및 해결 방법은 TechNet Wiki의 [가용성 데이터베이스의 데이터 동기화 상태가 정상이 아님](https://go.microsoft.com/fwlink/p/?LinkId=220863) 을 참조하세요.  
  
## <a name="possible-causes"></a>가능한 원인  
 복제본의 가용성 데이터베이스 중 하나 이상의 상태가 비정상 데이터 동기화 상태입니다. 비동기 커밋 가용성 복제본인 경우 모든 가용성 데이터베이스를 SYNCHRONIZING 상태로 설정해야 합니다. 이 복제본이 동기 커밋 가용성 복제본이면 모든 가용성 데이터베이스가 SYNCHRONIZED 상태에 있어야 합니다. 이 문제는 다음에 의해 발생할 수 있습니다.  
  
-   가용성 복제본의 연결이 끊어졌을 수 있습니다.  
  
-   데이터 이동이 일시 중지되었을 수 있습니다.  
  
-   데이터베이스에 액세스할 수 없는 상태일 수 있습니다.  
  
-   주 복제본이나 보조 복제본의 부하와 네트워크 대기 시간으로 인해 일시적인 지연 문제가 있을 수 있습니다.  
  
## <a name="possible-solution"></a>가능한 해결 방법  
 모든 연결 또는 데이터 이동 일시 중지 문제를 해결합니다. SQL Server Management Studio를 사용하여 이벤트에서 이 문제를 확인하고 데이터베이스 오류를 찾습니다. 특정 오류에 대한 문제 해결 단계를 따릅니다.  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 대시보드 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
