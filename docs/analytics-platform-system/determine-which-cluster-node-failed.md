---
title: 실패 한 클러스터 노드 확인
description: 이 문서에서는 클러스터 장애 조치 (failover)가 발생 하 고 클러스터 장애 조치 (failover) 경고가 발생 한 후 실패 한 AP (분석 플랫폼 시스템) 노드의 이름을 확인 하는 방법을 설명 합니다. 클러스터 장애 조치 (failover)의 일부로 문제 해결을 위해 Microsoft에 연결 하기 전에 실패 한 노드의 이름을 결정 해야 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 68ebdb7f17ddee311644e11c48eaa4b586beac74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401204"
---
# <a name="determine-which-cluster-node-failed-for-analytics-platform-system"></a>분석 플랫폼 시스템에 대해 실패 한 클러스터 노드 확인
이 항목에서는 클러스터 장애 조치 (failover)가 발생 하 고 클러스터 장애 조치 (failover) 경고가 발생 한 후 실패 한 AP (분석 플랫폼 시스템) 노드의 이름을 확인 하는 방법에 대해 설명 합니다. 클러스터 장애 조치 (failover)의 일부로 문제 해결을 위해 Microsoft에 연결 하기 전에 실패 한 노드의 이름을 결정 해야 합니다.  
  
## <a name="Background"></a>배경  
SQL Server PDW에서 고가용성을 위해 제어 노드와 계산 노드는 Windows 장애 조치 (failover) 클러스터의 활성 또는 수동 구성 요소로 구성 됩니다. 활성 서버가 심각한 시스템 요청에 응답 하지 못하면 수동 서버가 장애 조치 (failover) 되 고 실패 한 서버의 기능을 수행 합니다.  
  
클러스터 장애 조치 (failover) 후 노드 상태에 대 한 SQL Server PDW 보고 하는 경우 수동 서버의 장애 조치 (failover) 상태가 됩니다. 그러나 실패 한 서버 또는 노드가 아직 온라인 상태 이면 어떤 서버 또는 노드가 실패 했는지 명확 하지 않습니다. 클러스터 오류 문제를 해결 하려면 장애 조치 (failover) 된 노드의 이름을 확인 해야 합니다.  
  
## <a name="AdminConsoleSolution"></a>관리 콘솔 솔루션  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>실패 한 노드의 이름을 찾으려면  
  
1.  관리 콘솔을 엽니다. 관리 콘솔에 대 한 자세한 내용은 [관리 콘솔을 사용 하 여 어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-the-admin-console.md)을 참조 하세요. 장애 조치 (failover)가 발생 한 후에는 **상태** 페이지의 경고 수에 장애 조치 (failover) 이벤트가 포함 됩니다. PDW 지역 및 어플라이언스의 패브릭 영역에 대 한 **상태** 페이지가 있습니다. 각 상태 페이지에는 **경고** 탭이 있습니다. 경고에 대 한 자세한 내용을 보려면 상태 페이지, 경고 탭을 클릭 한 다음 경고를 클릭 합니다.  
  
## <a name="SystemView"></a>시스템 뷰 솔루션  
다음 SQL 문은 [dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md) 시스템 뷰를 사용 하 여 실패 한 서버의 이름을 찾는 방법을 보여 줍니다.  
  
```sql  
SELECT  
SUBSTRING( component_instance_id, 2, charindex(' ', component_instance_id, 1)-2) AS failed_node_name,  
create_time AS failover_time  
FROM sys.dm_pdw_component_health_active_alerts  
WHERE alert_id = 500139  
ORDER BY failed_node_name;  
```  
  
