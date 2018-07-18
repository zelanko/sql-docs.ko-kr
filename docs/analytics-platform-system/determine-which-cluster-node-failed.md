---
title: 실패 한 클러스터 노드-Analytics Platform System 확인 | Microsoft Docs
description: 이 문서에서는 클러스터 장애 조치가 발생 한 후 클러스터 장애 조치 경고를 발생 하지 못한 Analytics Platform System (APS) 노드의 이름을 확인 하는 방법을 설명 합니다. 클러스터 장애 조치가 문제 해결의 일환으로, 문제 해결을 위해 Microsoft에 문의 하기 전에 실패 한 노드의 이름을 결정 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4fd739e55725a3138a22539ef837088f86c8d8b9
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909503"
---
# <a name="determine-which-cluster-node-failed-for-analytics-platform-system"></a>클러스터 확인 Analytics Platform System에 대 한 노드 실패 했습니다.
이 항목에는 클러스터 장애 조치가 발생 한 후 클러스터 장애 조치 경고를 발생 하지 못한 Analytics Platform System (APS) 노드의 이름을 확인 하는 방법을 설명 합니다. 클러스터 장애 조치가 문제 해결의 일환으로, 문제 해결을 위해 Microsoft에 문의 하기 전에 실패 한 노드의 이름을 결정 합니다.  
  
## <a name="Background"></a>배경  
SQL Server PDW에서 고가용성을 위해 제어 노드와 계산 노드 Windows 장애 조치 클러스터의 활성 또는 수동 구성 요소로 구성 됩니다. 중요 한 시스템 요청에 응답 하는 활성 서버가 실패 하면 수동 서버는 장애 조치 하 고 실패 한 서버 기능을 수행 합니다.  
  
클러스터 장애 조치 후 SQL Server PDW 노드 상태를 보고 하는 경우 수동 서버에는 실패 한 상태 위로 그러나이 분명 하지 않습니다는 서버 또는 노드 실패, 실패 한 서버가 아직 온라인 상태인 경우에 특히. 클러스터 오류를 해결 하려면 장애 조치 노드의 이름을 결정 합니다.  
  
## <a name="AdminConsoleSolution"></a>관리 콘솔 솔루션  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>실패 한 노드의 이름을 찾으려면  
  
1.  관리자 콘솔을 엽니다. 관리 콘솔에 대 한 자세한 내용은 참조 하세요. [관리자 콘솔을 사용 하 여 어플라이언스 모니터링 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)합니다. 장애 조치 후 장애 조치 이벤트에 경고 수가 포함 되어는 **상태** 페이지입니다. **상태** 페이지 및 어플라이언스 패브릭 지역 PDW 영역에 대 한 합니다. 각 상태 페이지에는 **경고** 탭 합니다. 경고에 대 한 자세한 내용은 상태 페이지에서 경고 탭을 클릭 하 고 경고를 클릭 합니다.  
  
## <a name="SystemView"></a>시스템 뷰 솔루션  
다음 SQL 문을 사용 하는 방법을 보여 줍니다 합니다 [sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md) 실패 하는 서버의 이름을 찾으려면 시스템 뷰.  
  
```sql  
SELECT  
SUBSTRING( component_instance_id, 2, charindex(' ', component_instance_id, 1)-2) AS failed_node_name,  
create_time AS failover_time  
FROM sys.dm_pdw_component_health_active_alerts  
WHERE alert_id = 500139  
ORDER BY failed_node_name;  
```  
  
