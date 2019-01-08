---
title: 가용성 그룹이 오프라인 상태임 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp2online.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 093c5208-bf7a-49f4-a546-72b48197cadf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 35d8f9cdda7c3b85c77d290f9c793640705438e9
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359715"
---
# <a name="availability-group-is-offline"></a>가용성 그룹이 오프라인 상태임
    
## <a name="introduction"></a>소개  
  
|||  
|-|-|  
|**정책 이름**|가용성 그룹 온라인 상태|  
|**문제점**|가용성 그룹이 오프라인 상태임|  
|**범주**|**심각**|  
|**패싯**|가용성 그룹|  
  
## <a name="description"></a>Description  
 이 정책은 가용성 그룹의 온라인 또는 오프라인 상태를 확인합니다. 가용성 그룹의 클러스터 리소스가 오프라인이거나 가용성 그룹에 주 복제본이 없으면 정책이 비정상 상태이며 경고가 발생합니다.  
  
 가용성 그룹의 클러스터 리소스가 온라인이고 가용성 그룹에 주 복제본이 있으면 정책 상태가 정상입니다.  
  
> [!NOTE]  
>  이 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]릴리스의 경우 가능한 원인 및 해결 방법에 대한 자세한 내용은 TechNet Wiki에서 [가용성 그룹이 오프라인 상태임](https://go.microsoft.com/fwlink/p/?LinkId=220850) 을 참조하세요.  
  
## <a name="possible-causes"></a>가능한 원인  
 이 문제는 주 복제본을 호스팅하는 서버 인스턴스에 장애가 있거나 WSFC(Windows Server 장애 조치(Failover) 클러스터) 가용성 그룹 리소스가 오프라인 상태가 되어 발생할 수 있습니다. 다음과 같은 경우 가용성 그룹이 오프라인 상태가 될 수 있습니다.  
  
-   가용성 그룹이 자동 장애 조치(Failover) 모드로 구성되지 않은 경우. 주 복제본을 사용할 수 없게 되고 가용성 그룹에 있는 모든 복제본의 역할이 RESOLVING이 됩니다.  
  
    -   주 복제본 인스턴스 서비스가 다운되거나 응답하지 않는 경우  
  
    -   가용성 그룹에 클러스터와의 연결 문제가 있는 경우  
  
-   가용성 그룹이 자동 장애 조치(Failover) 모드로 구성되었지만 성공적으로 완료되지 않은 경우  
  
    -   자동 장애 조치(Failover) 중 대상 복제본에서 주 복제본 준비 상태 검사가 실패하고 새 주 복제본이 될 수 있는 복제본이 없는 경우  
  
-   클러스터의 가용성 그룹 리소스가 오프라인 상태가 되는 경우  
  
    -   종속 클러스터 리소스에 심각한 문제가 발생하여 오프라인이 되는 경우. 종속 리소스가 온라인 상태가 될 때까지 가용성 그룹 리소스도 오프라인 상태가 됩니다.  
  
    -   클러스터의 심각한 문제로 인해 가용성 그룹 리소스가 해제된 경우  
  
-   가용성 그룹에 대해 자동, 수동 또는 강제 장애 조치(Failover)가 진행 중인 경우  
  
## <a name="possible-solutions"></a>가능한 해결 방법  
 이 문제에 대한 해결 방법은 다음과 같습니다.  
  
-   주 복제본의 SQL Server 인스턴스가 다운된 경우 서버를 다시 시작한 다음 가용성 그룹이 정상 상태로 복구되는지 확인합니다.  
  
-   자동 장애 조치(Failover)가 실패한 것으로 보이면 복제본의 데이터베이스가 이전에 알려진 주 복제본과 동기화되었는지 확인한 다음 주 복제본으로 장애 조치(Failover)를 수행합니다. 데이터베이스가 동기화되지 않은 경우 데이터 손실이 가장 적은 복제본을 선택한 다음 장애 조치(Failover) 모드로 복구합니다.  
  
-   SQL Server 인스턴스가 정상으로 보이지만 클러스터의 리소스가 오프라인 상태인 경우 장애 조치(Failover) 클러스터 관리자를 사용하여 클러스터 상태 또는 서버의 다른 클러스터 문제를 검사합니다. 장애 조치(Failover) 클러스터 관리자를 사용하여 가용성 그룹 리소스의 온라인 전환을 시도해 볼 수도 있습니다.  
  
-   장애 조치(Failover)가 진행 중인 경우 해당 장애 조치가 완료될 때까지 기다립니다.  
  
## <a name="see-also"></a>관련 항목:  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 대시보드 사용&#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
