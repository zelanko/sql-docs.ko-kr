---
title: "메모리 내 OLTP와 쿼리 저장소 사용 | Microsoft 문서"
ms.custom: SQL2016_New_Updated
ms.date: 03/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Query Store, in-memory
ms.assetid: aae5ae6d-7c90-4661-a1c5-df704319888a
caps.latest.revision: "10"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 53942f718cdb697db2d7644b39b2c241d715234e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="using-the-query-store-with-in-memory-oltp"></a>메모리 내 OLTP와 쿼리 저장소 사용
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 저장소를 사용하면 메모리 내 OLTP에서 실행 중인 작업에 대한 기본 컴파일 코드의 성능을 모니터링할 수 있습니다.  
컴파일 및 런타임 통계는 디스크 기반 작업과 동일한 방식으로 수집 및 표시됩니다.   
메모리 내 OLTP로 마이그레이션하는 경우 디스크 기반 작업용으로 개발한 사용자 지정 스크립트뿐만 아니라 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 의 쿼리 저장소 보기를 사용하여 진행한 후 마이그레이션할 수 있습니다. 이를 통해 쿼리 저장소 기술에 대한 학습 시간을 단축하고 모든 유형의 작업에 대한 문제를 해결하기 위해 일반적으로 사용할 수 있습니다.  
쿼리 저장소 사용에 대한 일반 정보는 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)을(를) 참조하십시오.  
  
 쿼리 저장소와 메모리 내 OLTP를 사용하기 위해 추가 기능을 구성할 필요가 없습니다. 데이터베이스에서 활성화되면 모든 유형의 작업에 대해 작동합니다.   
그러나 쿼리 저장소와 메모리 내 OLTP를 사용하는 경우 사용자가 알아야 하는 일부 사항이 있습니다.  
  
-   쿼리 저장소를 활성화하면 쿼리, 계획 및 컴파일 시간 통계가 기본적으로 수집됩니다. 그러나 사용자가 [sys.sp_xtp_control_query_exec_stats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md)를 통해 명시적으로 활성화한 경우를 제외하고 런타임 통계 컬렉션은 활성화되지 않습니다.  
  
-   *@new_collection_value*를 0으로 설정한 경우 쿼리 저장소는 영향을 받는 프로시저 또는 전체 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 런타임 통계 수집을 중지합니다.  
  
-   [sys.sp_xtp_control_query_exec_stats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md)로 구성된 값은 유지되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을(를) 다시 시작한 후에는 통계 컬렉션을 확인 후 다시 구성해야 합니다.  
  
-   일반 쿼리 통계 컬렉션에서 사용되는 경우와 같이 작업 실행을 추적하기 위해 쿼리 저장소를 사용하는 경우 성능이 저하될 수 있습니다. 중요한 일부 기본 컴파일 저장 프로시저에 대해서만 통계 컬렉션을 활성화하는 것이 좋습니다.  
  
-   쿼리 및 계획은 첫 번째 기본 컴파일에 캡처 및 저장되고 다시 컴파일될 때마다 업데이트됩니다.  
  
-   모든 기본 저장 프로시저가 컴파일된 후 쿼리 저장소를 활성화하거나 해당 컨텐츠를 지운 경우 수동으로 다시 컴파일해야 쿼리 저장소에 캡처할 수 있습니다. [sp_query_store_remove_query&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md) 또는 [sp_query_store_remove_plan&#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)을 사용하여 쿼리를 수동으로 제거한 경우에도 이 방식이 적용됩니다. [sp_recompile&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md)을 사용하여 프로시저를 강제로 다시 컴파일합니다.  
  
-   쿼리 저장소는 메모리 내 OLTP의 계획 생성 메커니즘을 활용하여 컴파일하는 동안 쿼리 실행 계획을 캡처합니다. 저장된 계획은 의미상 `SET SHOWPLAN_XML ON` 을(를) 사용하여 획득한 것과 같고 한 가지 차이점은 쿼리 저장소의 계획은 개별 문을 기준으로 분할 및 저장된다는 것입니다.  
    
-   혼합 작업이 있는 데이터베이스에서 쿼리 저장소를 실행하는 경우 [sys.query_store_plan&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)의 **is_natively_compiled** 필드를 사용하여 네이티브 코드 컴파일에서 생성된 쿼리 계획을 쉽게 찾을 수 있습니다.  
  
-   쿼리 저장소 캡처 모드(**ALTER TABLE** 문의 *QUERY_CAPTURE_MODE* 매개 변수)는 구성된 값과 관계없이 항상 캡처되므로 기본적으로 컴파일된 모듈에서 쿼리에 영향을 주지 않습니다. 여기에는 `QUERY_CAPTURE_MODE = NONE`설정이 포함됩니다.  
  
-   쿼리 저장소로 캡처된 쿼리 컴파일 기간에는 기본 코드가 생성되기 전 쿼리 최적화에 소요된 시간만 포함됩니다. 보다 정확하게, C 코드 컴파일 시간 및 C 코드를 생성하기 위해 필요한 내부 구조 생성 시간이 포함되지 않습니다.  
  
-   [sys.query_store_runtime_stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md) 내의 메모리 부여 메트릭은 고유하게 컴파일된 쿼리에 대해 채워지지 않습니다. 해당 값은 항상 0입니다. 메모리 부여 열은 avg_query_max_used_memory, last_query_max_used_memory, min_query_max_used_memory, max_query_max_used_memory, 및 stdev_query_max_used_memory입니다.  
  
## <a name="enabling-and-using-query-store-with-in-memory-oltp"></a>쿼리 저장소와 메모리 내 OLTP 활성화 및 사용  
 다음의 간단한 예제는 종단 간 사용자 시나리오에서 쿼리 저장소와 메모리 내 OLTP를 사용하는 방법을 보여줍니다. 이 예제에서는 메모리 내 OLTP용으로 데이터베이스(`MemoryOLTP`)가 활성화된 것으로 가정되었습니다.  
    메모리 최적화 테이블의 필수 구성 요소에 대한 자세한 내용은 [메모리 최적화 테이블 및 고유하게 컴파일된 저장 프로시저 만들기](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)를 참조하세요.  
  
```  
USE MemoryOLTP;  
GO  
  
-- Create a simple memory-optimized table   
CREATE TABLE dbo.Ord  
   (OrdNo INTEGER not null PRIMARY KEY NONCLUSTERED,   
    OrdDate DATETIME not null,   
    CustCode NVARCHAR(5) not null)   
WITH (MEMORY_OPTIMIZED=ON);  
GO  
  
-- Enable Query Store before native module compilation  
ALTER DATABASE MemoryOLTP SET QUERY_STORE = ON;  
GO  
  
-- Create natively compiled stored procedure  
CREATE PROCEDURE dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS   
    BEGIN ATOMIC WITH  
    (TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
    LANGUAGE = N'English')  
  
    DECLARE @OrdDate DATETIME = GETDATE();  
    INSERT INTO dbo.Ord (OrdNo, CustCode, OrdDate)   
        VALUES (@OrdNo, @CustCode, @OrdDate);  
END;  
GO  
  
-- Enable runtime stats collection for queries from dbo.OrderInsert stored procedure  
DECLARE @db_id INT = DB_ID()  
DECLARE @proc_id INT = OBJECT_ID('dbo.OrderInsert');  
DECLARE @collection_enabled BIT;  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1,   
    @database_id = @db_id, @xtp_object_id = @proc_id;  
  
-- Check the state of the collection flag  
EXEC sp_xtp_control_query_exec_stats @database_id = @db_id,   
    @xtp_object_id = @proc_id,   
    @old_collection_value= @collection_enabled output;  
SELECT @collection_enabled AS 'collection status';  
  
-- Execute natively compiled workload  
EXEC dbo.OrderInsert 1, 'A';  
EXEC dbo.OrderInsert 2, 'B';  
EXEC dbo.OrderInsert 3, 'C';  
EXEC dbo.OrderInsert 4, 'D';  
EXEC dbo.OrderInsert 5, 'E';  
  
-- Check Query Store Data  
-- Compile time data  
SELECT q.query_id, plan_id, object_id, query_hash, p.query_plan,  
    p.initial_compile_start_time, p.last_compile_start_time,   
    p.last_execution_time, p.avg_compile_duration,  
    p.last_force_failure_reason, p.force_failure_count  
FROM sys.query_store_query AS q  
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.plan_id  
WHERE q.object_id = OBJECT_ID('dbo.OrderInsert');  
  
-- Get runtime stats  
-- Check count_executions field to verify that runtime statistics   
-- have been collected by the Query Store  
SELECT q.query_id, p.plan_id, object_id, rsi.start_time, rsi.end_time,    
    p.last_force_failure_reason, p.force_failure_count, rs.*  
FROM sys.query_store_query AS q  
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.plan_id  
JOIN sys.query_store_runtime_stats AS rs   
    ON rs.plan_id = p.plan_id  
JOIN sys.query_store_runtime_stats_interval AS rsi   
    ON rs.runtime_stats_interval_id = rsi.runtime_stats_interval_id  
WHERE q.object_id = OBJECT_ID('dbo.OrderInsert');  
```  
  
## <a name="see-also"></a>참고 항목  
 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [메모리 액세스에 최적화된 테이블 및 고유하게 컴파일된 저장 프로시저 만들기](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)   
 [쿼리 저장소에 대한 모범 사례](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [쿼리 저장소 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [쿼리 저장소 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)  
  
  
