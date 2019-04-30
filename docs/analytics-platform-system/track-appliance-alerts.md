---
title: Analytics Platform System-어플라이언스 경고 추적 | Microsoft Docs
description: 분석 플랫폼 시스템 어플라이언스 경고 추적 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f38f76975290538a35203ddbbed84b9354285edc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156995"
---
# <a name="track-appliance-alerts-in-analytics-platform-system"></a>분석 플랫폼 시스템에서 어플라이언스 경고 추적
이 항목에서는 SQL Server PDW 어플라이언스에에서 경고를 추적 하는 관리 콘솔과 시스템 뷰를 사용 하는 방법을 설명 합니다.  
  
## <a name="to-track-appliance-alerts"></a>어플라이언스 경고 추적  
SQL Server PDW 하드웨어 및 소프트웨어 주의가 필요한 문제에 대 한 경고를 만듭니다. 각 경고에는 제목 및 문제에 대 한 설명을 포함합니다.  
  
SQL Server PDW 경고를 기록 합니다 [sys.dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md) DMV 합니다. 시스템 경고 10,000 개로 제한 하며 제한을 초과 하는 경우 가장 오래 된 경고를 먼저 삭제 합니다.  
  
### <a name="view-alerts-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 경고 보기  
**경고** PDW 영역에 대 한 및 어플라이언스 패브릭 영역에 대 한 탭 합니다. 장애 조치 후 장애 조치 이벤트 페이지에서 경고의 개수에 포함 됩니다. PDW 영역에 대 한 및 어플라이언스 패브릭 영역에는 페이지가 제공 됩니다. 각 상태 페이지에는 탭 합니다. 경고에 대 한 자세한 내용은 다음을 클릭 합니다 **상태** 페이지를 **경고** 탭을 선택한 다음 경고를 클릭 합니다.  
  
![PDW 관리 콘솔 경고](./media/track-appliance-alerts/SQL_Server_PDW_AdminConsole_AlertsV2.png "SQL_Server_PDW_AdminConsole_AlertsV2")  
  
에 **경고** 페이지:  
  
-   경고 내역을 보려면 클릭 합니다 **검토 경고 기록** 링크 합니다.  
  
-   경고 구성 요소 및 해당 현재 속성 값을 보려면 경고 행을 클릭 합니다.  
  
-   경고를 발생 시키는 노드에 대 한 세부 정보를 보려면 노드 이름을 클릭 합니다.  
  
### <a name="view-alerts-by-using-the-system-views"></a>시스템 뷰를 사용 하 여 경고 보기  
시스템 뷰를 사용 하 여 경고를 보려면 쿼리 [sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)합니다. 이 DMV는 수정 되지 않은 경고를 표시 합니다. 심사 경고 및 오류를 사용 하 여 도움말을 사용 합니다 [sys.dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md) DMV 합니다.  
  
다음 예제는 현재 경고 보기에 대 한 일반적인 쿼리 합니다.  
  
```sql  
SELECT   
    aa.[pdw_node_id],  
    n.[name] AS [node_name],  
    g.[group_name] ,  
    c.[component_name] ,  
    aa.[component_instance_id] ,   
    a.[alert_name] ,  
    a.[state] ,  
    a.[severity] ,  
    aa.[current_value] ,  
    aa.[previous_value] ,  
    aa.[create_time] ,  
    a.[description]   
FROM [sys].[dm_pdw_component_health_active_alerts] AS aa  
    INNER JOIN sys.dm_pdw_nodes AS n   
        ON aa.[pdw_node_id] = n.[pdw_node_id]  
    INNER JOIN [sys].[pdw_health_components] AS c   
        ON aa.[component_id] = c.[component_id]  
    INNER JOIN [sys].[pdw_health_component_groups] AS g   
        ON c.[group_id] = g.[group_id]  
    INNER JOIN [sys].[pdw_health_alerts] AS a   
        ON aa.[alert_id] = a.[alert_id] and aa.[component_id] = c.[component_id]  
ORDER BY  
    a.alert_id ,  
    aa.[pdw_node_id];  
```  
  
## <a name="see-also"></a>관련 항목  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->
[어플라이언스 모니터링 &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
