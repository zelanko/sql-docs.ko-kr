---
title: 가용성 복제본 연결 해제됨 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.agdashboard.arp2connected.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 1a2162d3-54fb-4356-b349-effbdc15a5a4
caps.latest.revision: 10
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: fb94df7f1a442dcb3dc25193a38d055ccc15e446
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186384"
---
# <a name="availability-replica-is-disconnected"></a>가용성 복제본 연결 해제됨
    
## <a name="introduction"></a>소개  
  
|||  
|-|-|  
|**정책 이름**|가용성 복제본 연결 상태|  
|**문제점**|가용성 복제본의 연결이 끊어짐|  
|**범주**|**심각**|  
|**패싯**|가용성 복제본|  
  
## <a name="description"></a>Description  
 이 정책은 가용성 복제본 간의 연결 상태를 확인합니다. 가용성 복제본의 연결 상태가 DISCONNECTED인 경우 정책은 비정상 상태에 있습니다. 그렇지 않으면 정책은 정상 상태입니다.  
  
> [!NOTE]  
>  이 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]릴리스의 경우 가능한 원인 및 해결 방법에 대한 자세한 내용은 TechNet Wiki의 [가용성 복제본의 연결이 끊어짐](http://go.microsoft.com/fwlink/p/?LinkId=220857) 을 참조하세요.  
  
## <a name="possible-causes"></a>가능한 원인  
 보조 복제본이 주 복제본에 연결되어 있지 않습니다. 연결 상태가 DISCONNECTED입니다. 이 문제는 다음에 의해 발생할 수 있습니다.  
  
-   연결 포트가 다른 응용 프로그램과 충돌했을 수 있습니다.  
  
-   암호화 유형 또는 알고리즘이 일치하지 않습니다.  
  
-   연결 끝점이 삭제되었거나 시작되지 않았습니다.  
  
-   전송 연결이 끊어졌습니다.  
  
## <a name="possible-solutions"></a>가능한 해결 방법  
 이 문제에 대한 해결 방법은 다음과 같습니다.  
  
-   주 복제본 및 보조 복제본 인스턴스의 데이터베이스 미러링 끝점 구성을 확인하여 일치하지 않는 구성을 업데이트합니다.  
  
-   포트가 충돌하는 경우 포트 번호를 변경합니다.  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 대시보드 사용&#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  