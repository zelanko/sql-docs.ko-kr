---
title: 고유하게 컴파일된 저장 프로시저의 성능 모니터링 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 55548cb2-77a8-4953-8b5a-f2778a4f13cf
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9b8d6f35f8dedeb4539dc8299ca32f6566beb03f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161957"
---
# <a name="monitoring-performance-of-natively-compiled-stored-procedures"></a>고유하게 컴파일된 저장 프로시저의 성능 모니터링
  이 항목에서는 고유하게 컴파일된 저장 프로시저의 성능을 모니터링하는 방법에 대해 설명합니다.  
  
## <a name="using-extended-events"></a>확장 이벤트 사용  
 `sp_statement_completed` 확장 이벤트를 사용하여 쿼리 실행을 추적할 수 있습니다. 이 이벤트로 확장 이벤트 세션을 만들면(필요에 따라 고유하게 컴파일된 특정 저장 프로시저의 object_id에 대해 필터 사용) 각 쿼리 실행 후에 확장 이벤트가 발생합니다. 확장 이벤트에 의해 보고되는 CPU 시간 및 기간은 쿼리에 사용된 CPU 양과 실행 시간을 나타냅니다. 많은 CPU 시간을 사용하는 고유하게 컴파일된 저장 프로시저에는 성능 문제가 있을 수 있습니다.  
  
 확장 이벤트의 `line_number`와 함께 `object_id`를 사용하여 쿼리를 조사할 수 있습니다. 다음 쿼리를 사용하여 프로시저 정의를 검색할 수 있습니다. 줄 번호를 사용하여 정의 내에서 쿼리를 식별할 수 있습니다.  
  
```sql  
select [definition] from sys.sql_modules where object_id=object_id  
```  
  
 에 대 한 자세한 내용은 합니다 `sp_statement_completed` 확장 이벤트를 참조 하세요 [이벤트를 발생 시킨 문을 검색 하는 방법을](https://blogs.msdn.com/b/extended_events/archive/2010/05/07/making-a-statement-how-to-retrieve-the-t-sql-statement-that-caused-an-event.aspx)합니다.  
  
## <a name="using-data-management-views"></a>데이터 관리 뷰 사용  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 프로시저 수준 및 쿼리 수준 모두에서 고유하게 컴파일된 저장 프로시저에 대한 실행 통계 수집을 지원합니다. 실행 통계 수집은 성능에 미치는 영향 때문에 기본적으로 설정되지 않습니다.  
  
 [sys.sp_xtp_control_proc_exec_stats&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql)를 사용하여 고유하게 컴파일된 저장 프로시저에 대한 통계 수집을 설정하고 해제할 수 있습니다.  
  
 통계 수집이 [sys.sp_xtp_control_proc_exec_stats&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql)를 사용하여 설정된 경우 [sys.dm_exec_procedure_stats&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql)를 사용하여 고유하게 컴파일된 저장 프로시저의 성능을 모니터링할 수 있습니다.  
  
 통계 수집이 [sys.sp_xtp_control_query_exec_stats&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql)를 사용하여 설정된 경우 [sys.dm_exec_query_stats&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)를 사용하여 고유하게 컴파일된 저장 프로시저의 성능을 모니터링할 수 있습니다.  
  
 컬렉션의 시작 부분에서 통계 컬렉션을 설정합니다. 그런 다음 고유하게 컴파일된 저장 프로시저를 실행합니다. 컬렉션의 끝 부분에서 통계 컬렉션의 설정을 해제합니다. 그런 다음 DMV에서 반환되는 실행 통계를 분석합니다.  
  
 통계를 수집한 후 고유하게 컴파일된 저장 프로시저에 대한 실행 통계에서 [sys.dm_exec_procedure_stats&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql)를 사용하여 프로시저를 쿼리하고 [sys.dm_exec_query_stats&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)를 사용하여 쿼리를 쿼리할 수 있습니다.  
  
> [!NOTE]  
>  고유하게 컴파일된 저장 프로시저에 대해 통계 컬렉션을 설정하면 작업자 시간이 밀리초 단위로 수집됩니다. 쿼리가 밀리초 미만 단위로 실행되는 경우 값은 0이 됩니다. 고유하게 컴파일된 저장 프로시저의 경우 1초 미만이 소요되는 실행이 많으면 **total_worker_time** 이 정확하지 않을 수 있습니다.  
  
 다음 쿼리에서는 통계 컬렉션 후 현재 데이터베이스에서 고유하게 컴파일된 저장 프로시저에 대한 실행 통계 및 프로시저 이름을 반환합니다.  
  
```sql  
select object_id,  
       object_name(object_id) as 'object name',  
       cached_time,  
       last_execution_time,  
       execution_count,  
       total_worker_time,  
       last_worker_time,  
       min_worker_time,  
       max_worker_time,  
       total_elapsed_time,  
       last_elapsed_time,  
       min_elapsed_time,  
       max_elapsed_time   
from sys.dm_exec_procedure_stats  
where database_id=db_id() and object_id in (select object_id   
from sys.sql_modules where uses_native_compilation=1)  
order by total_worker_time desc  
```  
  
 다음 쿼리에서는 쿼리 텍스트와 함께 현재 데이터베이스에서 통계가 수집된 고유하게 컴파일된 저장 프로시저의 코든 쿼리에 대한 실행 통계(전체 작업자 시간을 기준으로 정렬됨)도 내림차순으로 반환합니다.  
  
```sql  
select st.objectid,   
       object_name(st.objectid) as 'object name',   
       SUBSTRING(st.text, (qs.statement_start_offset/2) + 1, ((qs.statement_end_offset-qs.statement_start_offset)/2) + 1) as 'query text',   
       qs.creation_time,  
       qs.last_execution_time,  
       qs.execution_count,  
       qs.total_worker_time,  
       qs.last_worker_time,  
       qs.min_worker_time,  
       qs.max_worker_time,  
       qs.total_elapsed_time,  
       qs.last_elapsed_time,  
       qs.min_elapsed_time,  
       qs.max_elapsed_time  
from sys.dm_exec_query_stats qs cross apply sys.dm_exec_sql_text(sql_handle) st  
where  st.dbid=db_id() and st.objectid in (select object_id   
from sys.sql_modules where uses_native_compilation=1)  
order by qs.total_worker_time desc  
```  
  
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
  
## <a name="see-also"></a>관련 항목  
 [고유하게 컴파일된 저장 프로시저](natively-compiled-stored-procedures.md)  
  
  
