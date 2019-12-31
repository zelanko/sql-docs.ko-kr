---
title: 어플라이언스 상태 모니터링
description: 관리 콘솔을 사용 하거나 병렬 데이터 웨어하우스 동적 관리 뷰를 직접 쿼리하여 분석 플랫폼 시스템 어플라이언스의 상태를 모니터링 하는 방법입니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b99123f81fcdddd74dc72d485d97e428ca59ed84
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400989"
---
# <a name="monitor-appliance-health-state"></a>어플라이언스 상태 모니터링
이 문서에서는 관리 콘솔을 사용 하거나 병렬 데이터 웨어하우스 동적 관리 뷰를 직접 쿼리하여 분석 플랫폼 시스템 어플라이언스의 상태를 모니터링 하는 방법을 설명 합니다. 
  
## <a name="to-monitor-the-appliance-state"></a>어플라이언스 상태를 모니터링 하려면  
시스템 관리자는 관리 콘솔 또는 SQL Server PDW Dmv (동적 관리 뷰)를 사용 하 여 노드, 구성 요소 및 소프트웨어의 전체 계층 구조를 검색할 수 있습니다. 다음 다이어그램은 SQL Server PDW 모니터를 구성 하는 구성 요소에 대 한 높은 수준의 이해를 제공 합니다.  
  
![모니터링 개요](./media/monitor-appliance-health-state/SQL_Server_PDW_Monitoring_Overview.png "SQL_Server_PDW_Monitoring_Overview")  
  
### <a name="monitor-component-status-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 구성 요소 상태 모니터링  
관리 콘솔을 사용 하 여 구성 요소 상태를 검색 하려면:  
  
1.  **어플라이언스 상태** 탭을 클릭 합니다.  
  
2.  어플라이언스 상태 페이지에서 특정 노드를 클릭 하 여 노드 세부 정보를 봅니다.  
  
    ![PDW 관리 콘솔 상태](./media/monitor-appliance-health-state/SQL_Server_PDW_AdminConsol_State.png "SQL_Server_PDW_AdminConsol_State")  
  
### <a name="monitor-component-status-by-using-system-views"></a>시스템 뷰를 사용 하 여 구성 요소 상태 모니터링  
시스템 뷰를 사용 하 여 구성 요소 상태를 검색 하려면 [dm_pdw_component_health_status](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)를 사용 합니다. 예를 들어 다음 쿼리는 모든 구성 요소에 대 한 상태를 검색 합니다.  
  
```sql  
SELECT   
   s.[pdw_node_id],  
   n.[name] as [node_name],  
   n.[address] ,  
   g.[group_id] ,  
   g.[group_name] ,  
   c.[component_id] ,  
   c.[component_name] ,  
   s.[component_instance_id] ,   
   p.[property_name] ,  
   s.[property_value] ,  
   s.[update_time]  
FROM [sys].[dm_pdw_component_health_status] AS s  
JOIN sys.dm_pdw_nodes AS n   
   ON s.[pdw_node_id] = n.[pdw_node_id]  
JOIN [sys].[pdw_health_components] AS c   
   ON s.[component_id] = c.[component_id]  
JOIN [sys].[pdw_health_component_groups] AS g   
   ON c.[group_id] = g.[group_id]  
JOIN [sys].[pdw_health_component_properties] AS p   
   ON s.[property_id] = p.[property_id] AND s.[component_id] = p.[component_id]  
WHERE p.property_name = 'Status'  
ORDER BY  
   s.[pdw_node_id],  
   g.[group_name] ,   
   s.[component_instance_id] ,  
   c.[component_name] ,   
   p.[property_name];  
```  
  
Status 속성에 대해 반환 될 수 있는 값은 다음과 같습니다.  
  
-   확인  
  
-   않음  
  
-   위험  
  
-   Unknown  
  
-   지원되지 않음  
  
-   연결 불가  
  
-   복구가  
  
모든 구성 요소의 속성을 모두 보려면 `WHERE  p.property_name = 'Status'` 절을 제거 합니다.  
  
**[Update_time]** 열은 SQL Server PDW 상태 에이전트에서 구성 요소를 마지막으로 폴링한 시간을 보여 줍니다.  
  
> [!CAUTION]  
> 구성 요소가 5 분 이상 폴링 되지 않은 경우 문제를 조사 해야 합니다. 소프트웨어 하트 비트에 대 한 문제를 나타내는 경고가 있을 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](appliance-monitoring.md)  
  
