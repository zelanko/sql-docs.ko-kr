---
title: 가용성 복제본이 조인되어 있지 않음 | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.arp4joined.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 9c0d10b1-9e12-430c-83b9-ca2bd0a3afc4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c1143efc4d5a695dd00766d1f78132f7e69adc46
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62815290"
---
# <a name="availability-replica-is-not-joined"></a>가용성 복제본이 조인되어 있지 않습니다.
    
## <a name="introduction"></a>소개  
  
|||  
|-|-|  
|**정책 이름**|가용성 복제본 조인 상태|  
|**문제점**|가용성 복제본이 조인되어 있지 않습니다.|  
|**범주**|**경고**|  
|**패싯**|가용성 복제본|  
  
## <a name="description"></a>Description  
 이 정책은 가용성 복제본의 조인 상태를 확인합니다. 가용성 복제본이 가용성 그룹에 추가되었지만 제대로 조인되지 않은 경우 정책은 비정상 상태입니다. 그렇지 않으면 정책은 정상 상태입니다.  
  
> [!NOTE]  
>  이 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]릴리스에서의 가능한 원인 및 해결 방법은 TechNet Wiki의 [가용성 복제본이 조인되어 있지 않음](https://go.microsoft.com/fwlink/p/?LinkId=220859) 을 참조하세요.  
  
## <a name="possible-causes"></a>가능한 원인  
 보조 복제본이 가용성 그룹에 조인되어 있지 않습니다. 가용성 복제본을 가용성 그룹에 성공적으로 조인하려면 조인 상태가 조인된 독립 실행형 인스턴스(1) 또는 조인된 장애 조치(Failover) 클러스터(2)여야 합니다.  
  
## <a name="possible-solution"></a>가능한 해결 방법  
 Transact-SQL, PowerShell 또는 SQL Server Management Studio를 사용하여 보조 복제본을 가용성 그룹에 조인합니다. 보조 복제본을 가용성 그룹에 조인하는 방법은 [가용성 그룹에 보조 복제본 조인(SQL Server)](https://msdn.microsoft.com/library/ff878473\(en-us,SQL.110\).aspx)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 대시보드 사용&#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
