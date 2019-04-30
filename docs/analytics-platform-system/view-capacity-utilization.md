---
title: Analytics Platform System의 용량 사용률을 확인 합니다. | Microsoft Docs
description: Analytics Platform System의 용량 사용률을 확인 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5fe722e6ce3d75f6e271e19d66551ccf951d045f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63243808"
---
# <a name="view-capacity-utilization-in-analytics-platform-system"></a>Analytics Platform System의 용량 사용률 보기
이 항목에서는 SQL Server PDW 어플라이언스의 용량 사용률을 확인 하는 방법에 설명 합니다.  
  
## <a name="to-view-capacity-utilization-by-using-admin-console"></a>관리 콘솔을 사용 하 여 용량 사용률을 보려면  
사용 된 공간을 보려면 관리 콘솔을 열고 클릭 합니다 **저장소** 탭 합니다. 한 **저장소** PDW 영역에 대 한 탭 합니다.  
  
![PDW 관리 콘솔 저장소](./media/view-capacity-utilization/SQL_Server_PDW_AdminConsol_StorageV2.png "SQL_Server_PDW_AdminConsol_StorageV2")  
  
## <a name="to-view-capacity-utilization-by-using-queries"></a>쿼리를 사용 하 여 용량 사용률을 보려면  
경우 노드는 공간이 부족을 이해 하려면 SQL Server PDW 상태 모니터링 시스템 이미 각 노드 내의 모든 볼륨에 대해 사용 가능한 공간을 모니터링 합니다.  
  
볼륨 내에서 사용 가능한 공간이 30% 미만으로 떨어지면 SQL Server PDW에서는 오류가 발생 하는 **경고** 에서 경고 [sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)합니다.  경고에는 사용 가능한 공간이 제공 될 때까지 유지 됩니다.  
  
볼륨 내에서 사용 가능한 공간이 10% 미만으로 떨어질, SQL Server PDW 생성 된 **중요 한** 경고 합니다. 이 데이터베이스를 확장 하는 경우 쿼리가 실패할 수 있으므로 중요 한 간주 됩니다.  
  
볼륨 사용량을 검색 하려면 다음 예제를 참조 하세요.  
  
```sql  
SELECT   
    space.[pdw_node_id] ,  
    space.[node_name] ,  
    MAX(space.[volume_name]) AS 'volume_name' ,  
    MAX(space.[volume_size_mb]) AS 'volume_size_mb' ,  
    MAX(space.[free_space_mb]) AS 'free_space_mb' ,  
   (MAX(space.[volume_size_mb]) - MAX(space.[free_space_mb])) AS 'space_utilized'  
FROM (  
    SELECT   
        s.[pdw_node_id],  
        n.[name] AS [node_name],  
        (CASE WHEN p.property_name = 'volume_name'   
            THEN s.[property_value] ELSE NULL END) AS 'volume_name' ,  
        (CASE WHEN p.property_name = 'volume_size'   
            THEN (CAST(ISNULL(s.[property_value], '0') AS BIGINT)/1024/1024)   
            ELSE 0 END) AS 'volume_size_mb' ,  
        (CASE WHEN p.property_name = 'volume_free_space'   
            THEN (CAST(ISNULL(s.[property_value], '0') AS BIGINT)/1024/1024)   
            ELSE 0 END) AS 'free_space_mb' , s.[component_instance_id]  
    FROM [sys].[dm_pdw_component_health_status] AS s  
        JOIN sys.dm_pdw_nodes AS n   
            ON s.[pdw_node_id] = n.[pdw_node_id]  
        JOIN [sys].[pdw_health_components] AS c   
            ON s.[component_id] = c.[component_id]  
        JOIN [sys].[pdw_health_component_properties] AS p   
            ON s.[property_id] = p.[property_id] AND s.[component_id] = p.[component_id]  
    WHERE  
        c.[Component_name] = 'Volume'  
        AND p.[property_name] IN ('volume_name', 'volume_free_space', 'volume_size')  
    ) AS space  
GROUP BY space.[pdw_node_id] , space.[node_name] , space.[component_instance_id]  
ORDER BY space.[pdw_node_id], MAX(space.[volume_name]);  
```  
  
어플라이언스 노드에서 데이터베이스에서 사용 된 공간을 검색 하려면 다음 예제를 참조 하세요.  
  
```sql  
SELECT   
    [pdw_node_id],   
    [db_name],   
    SUM(CASE WHEN [file_type] = 'DATA' THEN [value_MB] ELSE 0 END) AS [DataSizeMB],  
    SUM(CASE WHEN [file_type] = 'LOG' THEN [value_MB] ELSE 0 END) AS [LogSizeMB],  
    SUM([value_MB]) AS [TotalMB]  
FROM (  
    SELECT   
        pc.[pdw_node_id],   
        RTRIM(pc.[counter_name]) AS [counter_name],   
        ISNULL(d.[name], pc.[instance_name]) AS [db_name],   
        pc.[cntr_value]/1024 AS [value_MB],  
        CASE   
            WHEN [counter_name] LIKE 'Data File(s) Size%'   
            THEN 'DATA'   
            ELSE 'LOG'   
        END AS [file_type]  
    FROM sys.dm_pdw_nodes_os_performance_counters AS pc  
        LEFT JOIN sys.pdw_database_mappings AS dm   
            ON pc.instance_name = dm.physical_name  
        INNER JOIN sys.databases AS d   
            ON d.database_id = dm.database_id  
    WHERE   
        ([counter_name] LIKE 'Log File(s) Size%'  
             OR [counter_name] LIKE 'Data File(s) Size%')  
        AND (d.[name] <> dm.[physical_name]   
             OR pc.[instance_name] = 'tempdb')  
) AS db  
GROUP BY [pdw_node_id], [db_name]  
ORDER BY [db_name], [pdw_node_id];  
```  
  
## <a name="see-also"></a>관련 항목  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->
[어플라이언스 모니터링 &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
