---
title: 어플라이언스 알림-분석 플랫폼 시스템 추적 | Microsoft Docs
description: 분석 플랫폼 시스템에서 경고를 기기를 추적 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 82803e6f20e4a710f317e2e7a541c4a1c72ed08d
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539273"
---
# <a name="track-appliance-alerts-in-analytics-platform-system"></a>분석 플랫폼 시스템에 기기 경고 추적
이 경고는 SQL Server PDW 어플라이언스를 추적 하는 관리 콘솔 및 시스템 뷰를 사용 하는 방법을 설명 합니다.  
  
## <a name="to-track-appliance-alerts"></a>기기 경고를 추적 하려면  
SQL Server PDW 하드웨어 및 소프트웨어 주의가 필요한 문제에 대 한 경고를 만듭니다. 각 경고에는 제목 및 문제에 대 한 설명을 포함합니다.  
  
경고를 기록 하는 SQL Server PDW는 [sys.dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md) DMV 합니다. 시스템 경고 10, 000 개로 제한을 유지 하며 제한을 초과 하는 가장 오래 된 경고를 먼저 삭제 합니다.  
  
### <a name="view-alerts-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 경고 보기  
한 **경고** HDI 영역 PDW 영역에 대 한 어플라이언스의 패브릭 지역에 대 한 탭 합니다. 장애 조치가 발생 한 후 페이지에는 경고의 수에 장애 조치 이벤트가 포함 됩니다. HDI 영역 PDW 영역에 대 한 어플라이언스의 패브릭 지역에 대 한 페이지가 있습니다. 각 상태 페이지 탭을 있습니다. 경고에 대 한 자세한 내용을 보려면, 클릭는 **상태** 페이지는 **경고** 탭을 클릭 한 다음 경고를 클릭 합니다.  
  
![PDW 관리 콘솔 경고](./media/track-appliance-alerts/SQL_Server_PDW_AdminConsole_AlertsV2.png "SQL_Server_PDW_AdminConsole_AlertsV2")  
  
에 **경고** 페이지:  
  
-   경고 내역을 보려면 클릭는 **검토 경고 기록** 링크 합니다.  
  
-   경고 구성 요소와 현재 속성 값을 보려면 경고 행을 클릭 합니다.  
  
-   경고를 발생 시키는 노드에 대 한 세부 정보를 보려면 노드 이름을 클릭 합니다.  
  
### <a name="view-alerts-by-using-the-system-views"></a>시스템 뷰를 사용 하 여 경고 보기  
시스템 뷰를 사용 하 여 경고를 보려면 쿼리 [sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)합니다. 이 DMV는 수정 되지 경고를 표시 합니다. 에 대 한 심사 경고 및 오류 도움말을 사용 하 여는 [sys.dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md) DMV 합니다.  
  
다음 예제는 현재 경고를 보고 하는 일반적인 쿼리 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->
[어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](appliance-monitoring.md)  
  
