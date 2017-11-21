---
title: "MSSQLSERVER_41030 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 41030 (Database Engine error)
ms.assetid: c85341ae-0fbf-42ae-9275-4cfe678238f0
caps.latest.revision: 6
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e246ec2e406f4bcfb9083875c7111421e967762c
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver41030"></a>MSSQLSERVER_41030
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|41030|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|OPEN_CLUSTER_SUB_KEY|  
|메시지 텍스트|Windows Server 장애 조치(Failover) 클러스터링 레지스트리 하위 키 '%.*ls'을(를) 열지 못했습니다(오류 코드 %d).  부모 키는 클러스터 루트 키입니다.  WSFC 서비스가 실행 중이 아니거나 현재 상태에서 액세스할 수 없거나 지정된 인수가 올바르지 않습니다. 해당 가용성 그룹이 삭제된 경우 이 오류가 발생할 수 있습니다. 이 오류 코드에 대한 자세한 내용은 Windows 개발 설명서의 "시스템 오류 코드"를 참조하십시오.|  
  
## <a name="explanation"></a>설명  
WSFC 클러스터가 제거된 경우 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]과 관련된 모든 레지스트리 키가 제거됩니다.  
  
## <a name="user-action"></a>사용자 동작  
WSFC 클러스터를 다시 만든 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스가 AlwaysOn에 설정된 모든 클러스터 노드에서 AlwaysOn을 해제한 다음 다시 설정합니다. 이 태스크에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
[AlwaysOn 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](~/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
[SQL Server의 WSFC&#40;Windows Server 장애 조치(failover) 클러스터링&#41;](~/sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)  
  

