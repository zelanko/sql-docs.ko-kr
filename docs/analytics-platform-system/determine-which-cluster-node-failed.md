---
title: "클러스터 노드 실패 (분석 플랫폼 시스템) 확인"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e001117-a1b6-4357-bf25-e85aba3f1cf0
caps.latest.revision: "21"
ms.openlocfilehash: 14b68f56a89d5fec57ede1a49be4dedc435353b5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="determine-which-cluster-node-failed"></a>클러스터 노드 실패를 확인 합니다.
이 항목에는 클러스터 장애 조치가 발생 한 것 이며 클러스터 장애 조치 경고가 발생 했습니다 후 실패 한 SQL Server PDW 노드의 이름을 확인 하는 방법을 설명 합니다. 클러스터 장애 조치가 문제 해결의 일환으로, 문제를 해결 하기 위해 Microsoft에 문의 하기 전에 실패 한 노드의 이름을 결정 해야 합니다.  
  
## <a name="Background"></a>배경  
SQL Server PDW에서 고가용성을 위해 컨트롤 노드와 계산 노드는 Windows 장애 조치 클러스터의 활성 또는 수동 구성 요소로 구성 됩니다. 중요 한 시스템 요청에 응답 하는 활성 서버에 실패 하면 수동 서버 장애 조치 되 고 실패 한 서버 기능을 수행 합니다.  
  
클러스터 장애 조치 후 SQL Server PDW 노드 상태를 보고 하는 경우 수동 서버에 오류가 발생 한 동안 상태 있습니다. 그러나 확실 하지는 서버나 노드를 실패, 실패 한 서버가 온라인 상태인 경우에 특히 합니다. 클러스터 실패의 문제를 해결 하려면 장애 조치 노드의 이름을 확인 해야 합니다.  
  
## <a name="AdminConsoleSolution"></a>관리 콘솔 솔루션  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>실패 한 노드의 이름을 찾으려면  
  
1.  관리 콘솔을 엽니다. 관리 콘솔에 대 한 자세한 내용은 참조 하세요. [관리 콘솔 &#40;를 사용 하 여 어플라이언스에 모니터링 분석 플랫폼 시스템 &#41; ](monitor-the-appliance-by-using-the-admin-console.md). 장애 조치 이벤트가 장애 조치가 발생 한 후에 경고의 수에 포함 되는지는 **상태** 페이지. 한 **상태** HDI 영역 PDW 영역에 대 한 어플라이언스의 패브릭 지역에 대 한 페이지입니다. 각 상태 페이지에는 **경고** 탭 합니다. 경고에 대 한 자세한 내용은 상태 페이지에서 경고 탭을 클릭 하 고 경고를 클릭 합니다.  
  
## <a name="SystemView"></a>시스템 뷰 솔루션  
다음 SQL 문을 사용 하는 방법을 보여 줍니다는 [sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md) 실패 하는 서버의 이름을 찾으려면 시스템 뷰.  
  
```sql  
SELECT  
SUBSTRING( component_instance_id, 2, charindex(' ', component_instance_id, 1)-2) AS failed_node_name,  
create_time AS failover_time  
FROM sys.dm_pdw_component_health_active_alerts  
WHERE alert_id = 500139  
ORDER BY failed_node_name;  
```  
  
