---
title: Analytics Platform System appliance 상태-모니터링
description: 관리 콘솔을 사용 하 여 또는 병렬 데이터 웨어하우스 동적 관리 뷰를 직접 쿼리하여 분석 플랫폼 시스템 어플라이언스의 상태를 모니터링 하는 방법입니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c69e46ad6a37a17a12c37f83625b5c7f6eaf8078
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960610"
---
# <a name="monitor-appliance-health-state"></a>어플라이언스 성능 상태 모니터
이 문서에서는 관리 콘솔을 사용 하 여 또는 병렬 데이터 웨어하우스 동적 관리 뷰를 직접 쿼리하여 분석 플랫폼 시스템 어플라이언스의 상태를 모니터링 하는 방법에 설명 합니다. 
  
## <a name="to-monitor-the-appliance-state"></a>어플라이언스 상태를 모니터링 하려면  
시스템 관리자 노드, 구성 요소 및 소프트웨어의 전체 계층 구조를 검색할 관리 콘솔 또는 SQL Server PDW 동적 관리 뷰 (Dmv)를 사용할 수 있습니다. 다음 다이어그램은 SQL Server PDW 모니터링 하는 구성 요소에 대 한 높은 수준의 이해를 제공 합니다.  
  
![모니터링 개요](./media/monitor-appliance-health-state/SQL_Server_PDW_Monitoring_Overview.png "SQL_Server_PDW_Monitoring_Overview")  
  
### <a name="monitor-component-status-by-using-the-admin-console"></a>관리 콘솔을 사용 하 여 구성 요소 상태 모니터링  
관리 콘솔을 사용 하 여 구성 요소 상태를 검색:  
  
1.  클릭 합니다 **어플라이언스 상태** 탭 합니다.  
  
2.  어플라이언스 상태 페이지의 노드 세부 정보를 보려면 특정 노드를 클릭 합니다.  
  
    ![PDW 관리 콘솔 상태](./media/monitor-appliance-health-state/SQL_Server_PDW_AdminConsol_State.png "SQL_Server_PDW_AdminConsol_State")  
  
### <a name="monitor-component-status-by-using-system-views"></a>시스템 뷰를 사용 하 여 구성 요소 상태 모니터링  
사용 하 여 시스템 뷰를 사용 하 여 구성 요소 상태를 검색할 [sys.dm_pdw_component_health_status](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)합니다. 예를 들어 다음 쿼리는 모든 구성 요소에 대 한 상태를 검색합니다.  
  
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
  
Status 속성에 대해 반환 되는 가능한 값은:  
  
-   확인  
  
-   중요 하지 않은  
  
-   심각  
  
-   알 수 없음  
  
-   지원되지 않음  
  
-   연결할 수 없음  
  
-   복구할 수 없는  
  
모든 구성 요소에 대 한 모든 속성을 보려면 제거는 `WHERE  p.property_name = 'Status'` 절.  
  
합니다 **[update_time]** 열 구성 요소는 SQL Server PDW 상태 에이전트에서 폴링한 된 마지막 시간을 보여 줍니다.  
  
> [!CAUTION]  
> 5 분 이상; 구성 요소에 폴링 되지 않습니다 하는 경우 문제를 조사 해야 합니다. 소프트웨어 하트 비트를 사용 하 여 문제를 나타내는 경고가 있을 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[어플라이언스 모니터링 &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
