---
title: DMV를 사용하여 뷰의 사용 통계 및 성능 확인
description: DMV를 사용하여 뷰의 사용 통계 및 성능 확인
manager: craigg
author: MashaMSFT
ms.author: mathoma
ms.date: 09/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.openlocfilehash: 1ac9c72ecee9beee66ea190b3acf233a0e4bc753
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618411"
---
# <a name="use-dmvs-to-determine-usage-statistics-and-performance-of-views"></a>DMV를 사용하여 뷰의 사용 통계 및 성능 확인

이 문서에서는 데이터베이스 개체에서 **뷰를 사용하는 쿼리 성능**에 대한 정보를 가져오는 데 사용하는 방법 및 스크립트에 대해 설명합니다. 이러한 스크립트의 목적은 데이터베이스 내에 있는 다양한 뷰의 사용 및 성능 표시기를 제공하는 것입니다. 

## <a name="sysdmexecqueryoptimizerinfo"></a>Sys.dm_exec_query_optimizer_info

DMV [sys.dm_exec_query_optimizer_info](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-optimizer-info-transact-sql)는 SQL Server 쿼리 최적화 프로그램에서 수행한 최적화에 대한 통계를 제공합니다. 이러한 값은 누적되며 SQL Server가 시작될 때 기록을 시작합니다.  

아래의 common_table_expression(CTE)는 이 DMV를 사용하여 뷰를 참조하는 쿼리의 비율과 같은 워크로드 관련 정보를 제공합니다. 이 쿼리에서 반환하는 결과가 자체적으로 성능 문제를 나타내지는 않지만 느리게 작동하는 쿼리에 대한 사용자 불만과 관련이 있는 기본 문제를 나타낼 수 있습니다. 


```SQL
WITH CTE_QO AS
(
  SELECT
    occurrence
  FROM
    sys.dm_exec_query_optimizer_info
  WHERE
    ([counter] = 'optimizations')
),
QOInfo AS
(
  SELECT
    [counter]
    ,[%] = CAST((occurrence * 100.00)/(SELECT occurrence FROM CTE_QO) AS DECIMAL(5, 2))
  FROM
    sys.dm_exec_query_optimizer_info
  WHERE
    [counter] IN ('optimizations'
                  ,'trivial plan'
                  ,'no plan'
                  ,'search 0'
                  ,'search 1'
                  ,'search 2'
                  ,'timeout'
                  ,'memory limit exceeded'
                  ,'insert stmt'
                  ,'delete stmt'
                  ,'update stmt'
                  ,'merge stmt'
                  ,'contains subquery'
                  ,'view reference'
                  ,'remote query'
                  ,'dynamic cursor request'
                  ,'fast forward cursor request'
             )
)
SELECT
  [optimizations] AS [optimizations %]
  ,[trivial plan] AS [trivial plan %]
  ,[no plan] AS [no plan %]
  ,[search 0] AS [search 0 %]
  ,[search 1] AS [search 1 %]
  ,[search 2] AS [search 2 %]
  ,[timeout] AS [timeout %]
  ,[memory limit exceeded] AS [memory limit exceeded %]
  ,[insert stmt] AS [insert stmt %]
  ,[delete stmt] AS [delete stmt]
  ,[update stmt] AS [update stmt]
  ,[merge stmt] AS [merge stmt]
  ,[contains subquery] AS [contains subquery %]
  ,[view reference] AS [view reference %]
  ,[remote query] AS [remote query %]
  ,[dynamic cursor request] AS [dynamic cursor request %]
  ,[fast forward cursor request] AS [fast forward cursor request %]
FROM
  QOInfo
PIVOT (MAX([%]) FOR [counter] 
  IN ([optimizations]
      ,[trivial plan]
      ,[no plan]
      ,[search 0]
      ,[search 1]
      ,[search 2]
      ,[timeout]
      ,[memory limit exceeded]
      ,[insert stmt]
      ,[delete stmt]
      ,[update stmt]
      ,[merge stmt]
      ,[contains subquery]
      ,[view reference]
      ,[remote query]
      ,[dynamic cursor request]
      ,[fast forward cursor request])) AS p;
GO
```
이 쿼리의 결과를 시스템 뷰 [sys.views](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-views-transact-sql)의 결과와 조합하여 쿼리 통계, 쿼리 텍스트 및 캐시된 실행 계획을 식별합니다. 

## <a name="sysviews"></a>Sys.views

아래 CTE는 실행 횟수, 총 실행 시간 및 메모리에서 읽은 페이지 수에 대한 정보를 제공합니다. 이러한 결과를 사용하여 최적화 후보가 될 수 있는 쿼리를 식별할 수 있습니다. 
  
  >[!NOTE]
  > 이 쿼리의 결과는 SQL Server의 버전에 따라 달라질 수 있습니다.  


```SQL
WITH CTE_VW_STATS AS
(
  SELECT
    SCHEMA_NAME(vw.schema_id) AS schemaname
    ,vw.name AS viewname
    ,vw.object_id AS viewid
  FROM
    sys.views AS vw
  WHERE
    (vw.is_ms_shipped = 0)
  INTERSECT
  SELECT
    SCHEMA_NAME(o.schema_id) AS schemaname
    ,o.Name AS name
    ,st.objectid AS viewid
  FROM
    sys.dm_exec_cached_plans cp
  CROSS APPLY
    sys.dm_exec_sql_text(cp.plan_handle) st
  INNER JOIN
    sys.objects o ON st.[objectid] = o.[object_id]
  WHERE
    st.dbid = DB_ID()
)
SELECT
  vw.schemaname
  ,vw.viewname
  ,vw.viewid
  ,DB_NAME(t.databaseid) AS databasename
  ,t.databaseid
  ,t.*
FROM
  CTE_VW_STATS AS vw
CROSS APPLY
  (
    SELECT
      st.dbid AS databaseid
      ,st.text
      ,qp.query_plan
      ,qs.*
    FROM
      sys.dm_exec_query_stats AS qs
    CROSS APPLY
      sys.dm_exec_sql_text(qs.plan_handle) AS st
    CROSS APPLY
      sys.dm_exec_query_plan(qs.plan_handle) AS qp
    WHERE
      (CHARINDEX(vw.schemaname, st.text, 1) > 0)
      AND (st.dbid = DB_ID())
  ) AS t;
GO
```

## <a name="sysdmvexeccachedplans"></a>Sys.dmv_exec_cached_plans

최종 쿼리는 DMV [sys.dmv_exec_cached_plans](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql)를 사용하여 사용하지 않는 뷰에 대한 정보를 제공합니다. 그러나 실행 계획 캐시는 동적이므로 결과는 달라질 수 있습니다. 따라서 이 쿼리를 지속적으로 사용하면서 뷰가 실제로 사용되고 있는지 여부를 확인합니다. 


```SQL
SELECT
  SCHEMA_NAME(vw.schema_id) AS schemaname
  ,vw.name AS name
  ,vw.object_id AS viewid
FROM
  sys.views AS vw
WHERE
  (vw.is_ms_shipped = 0)
EXCEPT
SELECT
  SCHEMA_NAME(o.schema_id) AS schemaname
  ,o.name AS name
  ,st.objectid AS viewid
FROM
  sys.dm_exec_cached_plans cp
CROSS APPLY
  sys.dm_exec_sql_text(cp.plan_handle) st
INNER JOIN
  sys.objects o ON st.[objectid] = o.[object_id]
WHERE
  st.dbid = DB_ID();
GO
```

## <a name="related-external-resources"></a>관련 외부 리소스

- [성능 튜닝을 위한 DMV(동영상 - SQL Saturday Pordenone)](https://www.youtube.com/watch?v=9FQaFwpt3-k)
- [성능 튜닝을 위한 DMV(슬라이드 e 데모 - SQL Saturday Pordenone)](http://www.sqlsaturday.com/589/Sessions/Details.aspx?sid=57409)
- [캡슐 양식으로 SQL Server 튜닝(동영상 - SQL Saturday Parma)](https://vimeo.com/200980883)
- [nutshell에서 SQL Server 튜닝(슬라이드 및 데모 - SQL Saturday Parma)](http://www.sqlsaturday.com/566/Sessions/Details.aspx?sid=53988)
- [SQL Server 동적 관리 뷰를 사용한 성능 튜닝](https://www.red-gate.com/library/performance-tuning-with-sql-server-dynamic-management-views)
- [SQL Server 2016의 가장 중요한 대기 유형](https://channel9.msdn.com/Blogs/MVP-Data-Platform/The-Most-Prominent-Wait-Types-of-your-SQL-Server-2016)
