---
title: 일부 가용성 복제본에서 데이터 동기화가 수행되지 않음 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp4synchronizing.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 3db6a569-e942-4321-a0dd-c4ab002087c8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0fb7d422687d0bc956937b30bae261b28edb3931
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53351479"
---
# <a name="some-availability-replicas-are-not-synchronizing-data"></a>일부 가용성 복제본에서 데이터 동기화가 수행되지 않음
    
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
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 대시보드 사용&#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
