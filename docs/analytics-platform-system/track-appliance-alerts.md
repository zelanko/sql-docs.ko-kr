---
title: 어플라이언스 경고 추적
description: 분석 플랫폼 시스템에서 어플라이언스 경고를 추적 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 03568666367bf6273f197994f572bbbbd62bb42e
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "74399938"
---
# <a name="track-appliance-alerts-in-analytics-platform-system"></a>분석 플랫폼 시스템에서 어플라이언스 경고 추적
이 항목에서는 관리 콘솔 및 시스템 뷰를 사용 하 여 SQL Server PDW 어플라이언스에서 경고를 추적 하는 방법에 대해 설명 합니다.  
  
## <a name="to-track-appliance-alerts"></a>어플라이언스 경고를 추적 하려면  
SQL Server PDW는 주의가 필요한 하드웨어 및 소프트웨어 문제에 대 한 경고를 생성 합니다. 각 경고에는 문제에 대 한 제목과 설명이 포함 되어 있습니다.  
  
SQL Server PDW는 [dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md) DMV에서 경고를 로깅합니다. 시스템은 제한 시간을 1만로 유지 하 고 제한을 초과 하는 경우 가장 오래 된 경고를 먼저 삭제 합니다.  
  
### <a name="view-alerts-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 경고 보기  
PDW 지역 및 어플라이언스의 패브릭 영역에 대 한 **경고** 탭이 있습니다. 장애 조치 (failover)가 발생 한 후에는 장애 조치 (failover) 이벤트가 페이지의 경고 수에 포함 됩니다. PDW 지역 및 어플라이언스의 패브릭 영역에 대 한 페이지가 있습니다. 각 상태 페이지에는 탭이 있습니다. 경고에 대 한 자세한 내용을 보려면 **상태** 페이지, **경고** 탭을 클릭 한 다음 경고를 클릭 합니다.  
  
![PDW 관리 콘솔 경고](./media/track-appliance-alerts/SQL_Server_PDW_AdminConsole_AlertsV2.png "SQL_Server_PDW_AdminConsole_AlertsV2")  
  
**경고** 페이지에서 다음을 수행 합니다.  
  
-   경고 기록을 보려면 **경고 기록 검토** 링크를 클릭 합니다.  
  
-   경고 구성 요소와 현재 속성 값을 보려면 경고 행을 클릭 합니다.  
  
-   경고를 발생 시킨 노드에 대 한 세부 정보를 보려면 노드 이름을 클릭 합니다.  
  
### <a name="view-alerts-by-using-the-system-views"></a>시스템 뷰를 사용 하 여 경고 보기  
시스템 뷰를 사용 하 여 경고를 보려면 [dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)를 쿼리 합니다. 이 DMV는 수정 되지 않은 경고를 표시 합니다. 심사 경고 및 오류에 대 한 도움말을 보려면 [dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md) DMV를 사용 하십시오.  
  
다음 예는 현재 경고를 표시 하는 일반적인 쿼리입니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->
[어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](appliance-monitoring.md)  
  
