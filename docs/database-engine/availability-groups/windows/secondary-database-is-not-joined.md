---
title: "보조 데이터베이스가 조인되지 않음 | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.agdashboard.drp2joined.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 10817e5e-75fa-42dd-baa2-359bea3ad051
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6041c31fa2c2e015980c8fc8a7875ddd1e53ac13
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="secondary-database-is-not-joined"></a>보조 데이터베이스에 조인되어 있지 않음
    
## <a name="introduction"></a>소개  
  
|||  
|-|-|  
|**정책 이름**|가용성 데이터베이스 조인 상태|  
|**문제점**|보조 데이터베이스가 조인되지 않음|  
|**범주**|**경고**|  
|**패싯**|가용성 데이터베이스|  
  
## <a name="description"></a>설명  
 이 정책은 보조 데이터베이스("보조 데이터베이스 복제본"이라고도 함)의 조인 상태를 확인합니다. 데이터베이스 복제본이 조인되지 않은 경우 정책은 비정상 상태에 있습니다. 그렇지 않으면 정책은 정상 상태입니다.  
  
> [!NOTE]  
>  이 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]릴리스의 경우 가능한 원인 및 해결 방법에 대한 자세한 내용은 TechNet Wiki의 [보조 데이터베이스가 조인되지 않음](http://go.microsoft.com/fwlink/p/?LinkId=220862) 을 참조하세요.  
  
## <a name="possible-causes"></a>가능한 원인  
 보조 데이터베이스가 가용성 그룹에 조인되어 있지 않습니다. 이 보조 데이터베이스의 구성이 완료되지 않았습니다.  
  
## <a name="possible-solution"></a>가능한 해결 방법  
 Transact-SQL, PowerShell 또는 SQL Server Management Studio를 사용하여 보조 복제본을 가용성 그룹에 조인합니다. 보조 복제본을 가용성 그룹에 조인하는 방법은 [가용성 그룹에 보조 복제본 조인(SQL Server)](http://msdn.microsoft.com/library/ff878473\(SQL.110\).aspx)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 대시보드 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  

