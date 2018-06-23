---
title: SQL Server, Workload Group Stats 개체 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Workload Group Stats object
- 'SQLServer: Workload Group Stats'
ms.assetid: ca20e4f6-50ec-4456-900d-87d280fde2b3
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 98dfc36dc69f8b913b9b1b5939522429d585854b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36183768"
---
# <a name="sql-server-workload-group-stats-object"></a>SQL Server, Workload Group Stats 개체
  SQLServer:Workload Group Stats 개체는 리소스 관리자 작업 그룹 통계에 대한 정보를 보고하는 성능 카운터를 포함합니다.  
  
 각 활성 작업 그룹은 리소스 관리자 작업 그룹 이름과 동일한 인스턴스 이름으로 SQLServer:Workload Group Stats 성능 개체의 인스턴스를 만듭니다. 다음 표에서는 이 인스턴스에서 지원하는 카운터에 대해 설명합니다.  
  
|카운터 이름|Description|  
|------------------|-----------------|  
|Queued requests|선택을 기다리면서 큐에 대기 중인 요청의 현재 개수입니다. GROUP_MAX_REQUESTS 한도에 도달한 후 스로틀이 발생할 경우 이 카운트는 0일 수 없습니다.|  
|Active requests|현재 작업 그룹에서 현재 실행 중인 요청 수로, 그룹 ID로 필터링된 sys.dm_exec_requests의 행 개수와 동일해야 합니다.|  
|Requests completed/sec|현재 작업 그룹에서 완료된 요청 수입니다. 이 숫자는 누적됩니다.|  
|CPU usage %|현재 작업 그룹에 있는 모든 요청에 의한 CPU 대역폭 사용량으로, 컴퓨터를 기준으로 측정되고 시스템에 있는 모든 CPU를 기준으로 평균화됩니다. 이 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에 사용할 수 있는 CPU 양이 변경되면 그에 따라 변경됩니다. 이 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에 전달되는 CPU를 기준으로는 평균화되지 않습니다.|  
|Max request CPU time (ms)|작업 그룹에서 현재 실행 중인 요청에 의해 사용되는 최대 CPU 시간(밀리초)입니다.|  
|Blocked requests|현재 작업 그룹에 있는 차단된 요청의 현재 수로, 작업 특성을 결정하는 데 사용할 수 있습니다.|  
|Reduced memory grants/sec|이상적인 초당 메모리 부여 양보다 줄어든 쿼리 수입니다.|  
|Max request memory grant (KB)|쿼리를 위한 최대 메모리 부여 값(KB)입니다.|  
|Query optimizations/sec|현재 작업 그룹에서 초당 발생한 쿼리 최적화의 수로, 작업 특성을 결정하는 데 사용할 수 있습니다.|  
|Suboptimal plans/sec|현재 작업 그룹에서 초당 생성되는 만족스럽지 못한 계획의 수입니다.|  
|Active parallel threads|병렬 스레드 사용량의 현재 개수입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](monitor-resource-usage-system-monitor.md)   
 [SQLServer, Resource Pool Stats 개체](sql-server-resource-pool-stats-object.md)   
 [Resource Governor](../resource-governor/resource-governor.md)  
  
  