---
title: 고유하게 컴파일된 저장 프로시저의 성능 모니터링
description: 고유하게 컴파일된 저장 프로시저 및 고유하게 컴파일된 다른 T-SQL 모듈의 성능을 모니터링하는 방법을 알아봅니다.
ms.custom: seo-dt-2019
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 55548cb2-77a8-4953-8b5a-f2778a4f13cf
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a94d8534dfe028db0d98b8dc2ff585cd7d083026
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86484324"
---
# <a name="monitoring-performance-of-natively-compiled-stored-procedures"></a>고유하게 컴파일된 저장 프로시저의 성능 모니터링

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  이 문서에서는 고유하게 컴파일된 저장 프로시저 및 고유하게 컴파일된 다른 T-SQL 모듈의 성능을 모니터링하는 방법에 대해 설명합니다.  
  
## <a name="using-extended-events"></a>확장 이벤트 사용  
 **sp_statement_completed** 확장 이벤트를 사용하여 쿼리 실행을 추적할 수 있습니다. 이 이벤트로 확장 이벤트 세션을 만들고, 필요에 따라 고유하게 컴파일된 특정 저장 프로시저의 object_id에 대해 필터를 사용하면 각 쿼리 실행 후에 확장 이벤트가 발생합니다. 확장 이벤트에 의해 보고되는 CPU 시간 및 기간은 쿼리에 사용된 CPU 양과 실행 시간을 나타냅니다. 많은 CPU 시간을 사용하는 고유하게 컴파일된 저장 프로시저에는 성능 문제가 있을 수 있습니다.  
  
**line_number**는 확장 이벤트의 **object_id**와 함께 쿼리를 조사하는 데 사용될 수 있습니다. 다음 쿼리를 사용하여 프로시저 정의를 검색할 수 있습니다. 줄 번호를 사용하여 정의 내에서 쿼리를 식별할 수 있습니다.  
  
```sql  
SELECT [definition]
FROM sys.sql_modules
WHERE object_id=object_id;
```  
    
## <a name="using-data-management-views-and-query-store"></a>데이터 관리 뷰 및 쿼리 저장소 사용
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서는 프로시저 수준 및 쿼리 수준 모두에서 고유하게 컴파일된 저장 프로시저에 대한 실행 통계 수집을 지원합니다. 실행 통계 수집은 성능에 미치는 영향 때문에 기본적으로 설정되지 않습니다.  

실행 통계는 [쿼리 저장소](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)에서와 마찬가지로 시스템 뷰 [sys.dm_exec_procedure_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) 및 [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)에 반영됩니다.

## <a name="procedure-level-execution-statistics"></a>프로시저 수준 실행 통계

**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : [sys.sp_xtp_control_proc_exec_stats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md)를 사용하여 프로시저 수준의 고유하게 컴파일된 저장 프로시저에 대한 통계 수집을 활성화하거나 비활성화할 수 있습니다.  다음 명령문을 사용하면 현재 인스턴스에 있는 고유하게 컴파일된 모든 T-SQL 모듈에 대한 프로시저 수준 실행 통계 수집을 활성화할 수 있습니다.

```sql
EXEC sys.sp_xtp_control_proc_exec_stats 1
```

**[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]** 및 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : [데이터베이스 범위 구성](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 옵션 `XTP_PROCEDURE_EXECUTION_STATISTICS`를 사용하여 프로시저 수준의 고유하게 컴파일된 저장 프로시저에 대한 통계 수집을 활성화하거나 비활성화할 수 있습니다. 다음 명령문을 사용하면 현재 데이터베이스에 있는 고유하게 컴파일된 모든 T-SQL 모듈에 대한 프로시저 수준 실행 통계 수집을 활성화할 수 있습니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET XTP_PROCEDURE_EXECUTION_STATISTICS = ON;
```

## <a name="query-level-execution-statistics"></a>쿼리 수준 실행 통계

**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : [sys.sp_xtp_control_query_exec_stats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md)를 사용하여 쿼리 수준의 고유하게 컴파일된 저장 프로시저에 대한 통계 수집을 활성화하거나 비활성화할 수 있습니다.  다음 명령문을 사용하면 현재 인스턴스에 있는 고유하게 컴파일된 모든 T-SQL 모듈에 대한 쿼리 수준 실행 통계 수집을 활성화할 수 있습니다.

```sql
EXEC sys.sp_xtp_control_query_exec_stats 1
```

**[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]** 및 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : [데이터베이스 범위 구성](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 옵션 `XTP_QUERY_EXECUTION_STATISTICS`를 사용하여 명령문 수준의 고유하게 컴파일된 저장 프로시저에 대한 통계 수집을 활성화하거나 비활성화할 수 있습니다. 다음 명령문을 사용하면 현재 데이터베이스에 있는 고유하게 컴파일된 모든 T-SQL 모듈에 대한 쿼리 수준 실행 통계 수집을 활성화할 수 있습니다.

```sql
ALTER DATABASE SCOPED CONFIGURATION SET XTP_QUERY_EXECUTION_STATISTICS = ON;
```

## <a name="sample-queries"></a>샘플 쿼리

 통계를 수집한 후 고유하게 컴파일된 저장 프로시저에 대한 실행 통계에서 [sys.dm_exec_procedure_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)를 사용하여 프로시저를 쿼리하고 [sys.dm_exec_query_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)를 사용하여 쿼리를 쿼리할 수 있습니다.  
 
  
 다음 쿼리에서는 통계 컬렉션 후 현재 데이터베이스에서 고유하게 컴파일된 저장 프로시저에 대한 실행 통계 및 프로시저 이름을 반환합니다.  

```sql
SELECT object_id, object_name(object_id) AS 'object name',
       cached_time, last_execution_time, execution_count,
       total_worker_time, last_worker_time,
       min_worker_time, max_worker_time,
       total_elapsed_time, last_elapsed_time,
       min_elapsed_time, max_elapsed_time
FROM sys.dm_exec_procedure_stats
WHERE database_id = DB_ID()
      AND object_id IN (SELECT object_id FROM sys.sql_modules WHERE uses_native_compilation = 1)
ORDER BY total_worker_time desc;
```

다음 쿼리에서는 쿼리 텍스트와 함께 현재 데이터베이스에서 통계가 수집된 고유하게 컴파일된 저장 프로시저의 코든 쿼리에 대한 실행 통계(전체 작업자 시간을 기준으로 정렬됨)도 내림차순으로 반환합니다.  

```sql
SELECT st.objectid,
        OBJECT_NAME(st.objectid) AS 'object name',
        SUBSTRING(
            st.text,
            (qs.statement_start_offset/2) + 1,
            ((qs.statement_end_offset-qs.statement_start_offset)/2) + 1
            ) AS 'query text',
        qs.creation_time, qs.last_execution_time, qs.execution_count,
        qs.total_worker_time, qs.last_worker_time, qs.min_worker_time, 
        qs.max_worker_time, qs.total_elapsed_time, qs.last_elapsed_time,
        qs.min_elapsed_time, qs.max_elapsed_time
FROM sys.dm_exec_query_stats qs
CROSS APPLY sys.dm_exec_sql_text(sql_handle) st
WHERE database_id = DB_ID()
      AND object_id IN (SELECT object_id FROM sys.sql_modules WHERE uses_native_compilation = 1)
ORDER BY total_worker_time desc;
```

## <a name="query-execution-plans"></a>쿼리 실행 계획

 고유하게 컴파일된 저장 프로시저는 SHOWPLAN_XML(예상 실행 계획)을 지원합니다. 예상 실행 계획을 사용하여 쿼리 계획을 검사하면 잘못된 계획 문제를 모두 찾을 수 있습니다. 잘못된 계획의 일반적인 이유는 다음과 같습니다.  
  
-   프로시저를 만들기 전에 통계가 업데이트되지 않았습니다.  
  
-   누락된 인덱스  
  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 실행하여 Showplan XML을 가져옵니다.  
  
```sql  
SET SHOWPLAN_XML ON  
GO  
EXEC my_proc   
GO  
SET SHOWPLAN_XML OFF  
GO  
```  
  
 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 프로시저 이름을 선택하고 **예상 실행 계획 표시**를 클릭합니다.  
  
 고유하게 컴파일된 저장 프로시저의 예상 실행 계획은 프로시저의 쿼리에 대한 쿼리 연산자 및 식을 보여 줍니다. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 에서는 고유하게 컴파일된 저장 프로시저에 대한 일부 SHOWPLAN_XML 특성을 지원하지 않습니다. 예를 들어 쿼리 최적화 프로그램 비용 계산과 관련된 특성은 프로시저에 대한 SHOWPLAN_XML의 일부가 아닙니다.  
  
## <a name="see-also"></a>참고 항목  
 [고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
