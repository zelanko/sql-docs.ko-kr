---
title: "쿼리 저장소를 사용하여 성능 모니터링 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Query Store
- Query Store, described
ms.assetid: e06344a4-22a5-4c67-b6c6-a7060deb5de6
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5785d0283be2fe40b5010f6f9373f9a2ea81554a
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="monitoring-performance-by-using-the-query-store"></a>쿼리 저장소를 사용하여 성능 모니터링
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 저장소 기능을 통해 사용자는 쿼리 계획 선택 및 성능에 대한 정보를 얻을 수 있습니다. 쿼리 계획 변경으로 인해 발생하는 성능 차이를 신속하게 찾을 수 있도록 하여 성능 문제 해결을 간소화합니다. 쿼리 저장소는 쿼리, 계획 및 런타임 통계의 기록을 자동으로 캡처하고 사용자 검토를 위해 보관합니다. 데이터를 기간별로 구분하여 데이터베이스 사용 패턴을 파악하고 서버에서 쿼리 계획 변경이 발생한 시기를 이해할 수 있게 해줍니다. 쿼리 저장소는 [ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md) 옵션을 사용하여 구성할 수 있습니다. 
  
 Azure SQL 데이터베이스의 쿼리 저장소 작업에 대한 자세한 내용은 [Azure SQL 데이터베이스에서 쿼리 저장소 작업](https://azure.microsoft.com/documentation/articles/sql-database-operate-query-store/)을 참조하세요.  
  
##  <a name="Enabling"></a> Enabling the Query Store  
 새 데이터베이스에서는 기본적으로 쿼리 저장소가 활성 상태가 아닙니다.  
  
#### <a name="use-the-query-store-page-in-management-studio"></a>Management Studio에서 쿼리 저장소 페이지 사용  
  
1.  개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
    > [!NOTE]  
    >  최소한 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 의 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]버전이 필요합니다.  
  
2.  **데이터베이스 속성** 대화 상자에서 **쿼리 저장소** 페이지를 선택합니다.  
  
3.  **작업 모드(요청)** 상자에서 **On**을 선택합니다.  
  
#### <a name="use-transact-sql-statements"></a>Transact-SQL 문 사용  
  
1.  **ALTER DATABASE** 문을 사용하여 쿼리 저장소를 사용하도록 설정합니다. 예를 들어  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET QUERY_STORE = ON;  
    ```  
  
     쿼리 저장소와 관련된 구문 옵션에 대한 자세한 내용은 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.  
  
> [!NOTE]  
>  **마스터** 또는 **tempdb** 데이터베이스에 대해서는 쿼리 저장소를 사용하도록 설정할 수 없습니다.  
 
  
##  <a name="About"></a> 쿼리 저장소에 있는 정보  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 특정 쿼리에 대한 실행 계획은 일반적으로 통계 변경, 스키마 변경, 인덱스 생성/삭제 등과 같은 여러 이유로 인해 시간에 따라 변경됩니다. 프로시저 캐시(캐시된 쿼리 계획이 저장되는 위치)에는 최신 실행 계획만 저장됩니다. 또한 메모리 부족으로 인해 계획 캐시에서 계획이 제거됩니다. 따라서 실행 계획 변경으로 인한 쿼리 성능 저하는 간단한 문제가 아니며 해결하는 데 시간이 걸릴 수 있습니다.  
  
 쿼리 저장소에서는 쿼리당 여러 실행 계획을 유지하므로 쿼리 프로세서가 쿼리에 대해 특정 실행 계획을 사용하도록 하는 정책을 적용할 수 있습니다. 이를 계획 강제 적용이라고 합니다. 쿼리 저장소의 계획 강제 적용은 [USE PLAN](../../t-sql/queries/hints-transact-sql-query.md) 쿼리 힌트와 유사한 메커니즘을 사용하여 제공되지만 사용자 응용 프로그램을 변경할 필요는 없습니다. 계획 강제 적용은 계획 변경으로 인한 쿼리 성능 저하를 짧은 시간 내에 해결할 수 있습니다.  
  
 쿼리 저장소 기능을 사용하는 일반적인 시나리오는 다음과 같습니다.  
  
-   이전 쿼리 계획을 적용하여 계획 성능 저하를 빠르게 찾고 해결합니다. 실행 계획 변경으로 최근에 성능이 저하된 쿼리를 수정합니다.  
  
-   지정된 기간 내에 쿼리가 실행된 횟수를 확인하여 DBA의 성능 리소스 문제 해결을 지원합니다.  
  
-   실행 시간, 메모리 사용 등을 기준으로 이전 *x* 시간 동안의 상위 *n* 개 쿼리를 식별합니다.  
  
-   지정된 쿼리에 대한 쿼리 계획의 기록을 감사합니다.  
  
-   특정 데이터베이스에 대한 리소스(CPU, I/O 및 메모리) 사용 패턴을 분석합니다.  
  
 쿼리 저장소에는 실행 계획 정보를 유지하는 **계획 저장소** 와 실행 통계 정보를 유지하기 위한 **런타임 통계 저장소** 라는 두 가지 저장소가 포함되어 있습니다. 쿼리 저장소에서 쿼리에 대해 저장할 수 있는 고유한 계획의 수는 **max_plans_per_query** 구성 옵션으로 제한됩니다. 성능 향상을 위해 두 저장소에 비동기적으로 정보가 기록됩니다. 공간 사용을 최소화하기 위해 런타임 통계 저장소의 런타임 실행 통계는 고정된 기간 동안 집계됩니다. 이러한 저장소의 정보는 쿼리 저장소 카탈로그 뷰를 쿼리하여 볼 수 있습니다.  
  
 다음 쿼리는 쿼리 저장소의 쿼리 및 계획에 대한 정보를 반환합니다.  
  
```  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
 
  
##  <a name="Regressed"></a> Use the Regressed Queries Feature  
 쿼리 저장소를 사용하도록 설정한 후 개체 탐색기 창의 데이터베이스 부분을 새로 고쳐 **쿼리 저장소** 섹션을 추가합니다.  
  
 ![개체 탐색기의 쿼리 저장소 트리](../../relational-databases/performance/media/objectexplorerquerystore.PNG "개체 탐색기의 쿼리 저장소 트리")  
  
 **재발된 쿼리** 를 선택하여 **에서** 재발된 쿼리 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]창을 엽니다. 재발된 쿼리 창에는 쿼리 저장소의 쿼리 및 계획이 표시됩니다. 위쪽의 드롭다운 상자를 사용하여 다양한 기준에 따라 쿼리를 선택할 수 있습니다. 계획을 선택하면 그래픽 쿼리 계획이 표시됩니다. 단추를 사용하여 원본 쿼리를 보고, 쿼리 계획을 강제 적용 및 적용 취소하고 표시를 새로 고칠 수 있습니다.  
  
 ![개체 탐색기에서 이전 상태로 되돌려진 쿼리](../../relational-databases/performance/media/objectexplorerregressedqueries.PNG "개체 탐색기에서 이전 상태로 되돌려진 쿼리")  
  
 계획을 강제 적용하려면 쿼리 및 계획을 선택한 다음 **계획 강제 적용**을 클릭합니다. 쿼리 계획 기능으로 저장하고 쿼리 계획 캐시에 아직 보존되어 있는 계획만 강제 적용할 수 있습니다.  
 
  
##  <a name="Options"></a> Configuration Options  
 OPERATION_MODE  
 READ_WRITE(기본값) 또는 READ_ONLY일 수 있습니다.  
  
 CLEANUP_POLICY(STALE_QUERY_THRESHOLD_DAYS)  
 STALE_QUERY_THRESHOLD_DAYS 인수를 구성하여 쿼리 저장소에 데이터를 보존할 일수를 지정합니다. 기본값은 30입니다. [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic 버전의 경우 기본값은 7일입니다.
  
 DATA_FLUSH_INTERVAL_SECONDS  
 쿼리 저장소에 기록된 데이터가 디스크에 유지되는 빈도를 결정합니다. 성능 최적화를 위해 쿼리 저장소에서 수집한 데이터는 디스크에 비동기적으로 기록됩니다. 이 비동기 전송이 발생하는 빈도는 DATA_FLUSH_INTERVAL_SECONDS를 통해 구성됩니다. 기본값은 900(15분)입니다.  
  
 MAX_STORAGE_SIZE_MB  
 쿼리 저장소의 최대 크기를 구성합니다. 쿼리 저장소의 데이터가 MAX_STORAGE_SIZE_MB 제한에 도달하는 경우 쿼리 저장소에서는 자동으로 상태를 읽기/쓰기에서 읽기 전용으로 변경하고 새 데이터 수집을 중지합니다.  기본값은 100Mb입니다. [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium Edition의 경우 기본값은 1Gb이고, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic Edition의 경우 기본값은 10Mb입니다.
  
 INTERVAL_LENGTH_MINUTES  
 런타임 실행 통계 데이터가 쿼리 저장소로 집계되는 간격을 결정합니다. 공간 사용을 최적화하기 위해 런타임 통계 저장소의 런타임 실행 통계는 고정된 기간 동안 집계됩니다. 이 고정된 기간은 INTERVAL_LENGTH_MINUTES를 통해 구성됩니다. 기본값은 60입니다. 
  
 SIZE_BASED_CLEANUP_MODE  
 총 데이터 양이 최대 크기에 가까워졌을 때 정리 프로세스를 자동으로 활성화할지의 여부를 제어합니다. AUTO(기본값) 또는 OFF일 수 있습니다.  
  
 QUERY_CAPTURE_MODE  
 쿼리 저장소가 모든 쿼리 또는 실행 횟수 및 리소스 소비량에 따른 관련 쿼리를 캡처하거나 새 쿼리 추가 및 현재 쿼리 추적을 중지할지의 여부를 지정합니다. ALL(모든 쿼리 캡처), AUTO(자주 발생하지 않은 쿼리 및 컴파일/실행 기간이 의미 없는 쿼리 무시) 또는 NONE(새 쿼리 캡처 중지)일 수 있습니다. Azure SQL 데이터베이스에서 AUTO인 동안 SQL Server 2016의 기본값은 ALL입니다.
  
 max_plans_per_query  
 각 쿼리에 대하여 유지되는 계획의 수를 나타내는 정수입니다. 기본값은 200입니다.  
  
 **sys.database_query_store_options** 뷰를 쿼리하여 쿼리 저장소의 현재 옵션을 확인할 수 있습니다. 값에 대한 자세한 내용은 [sys을 참조하세요.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)을 참조하세요.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 옵션을 설정하는 방법에 대한 자세한 내용은 [옵션 관리](#OptionMgmt)를 참조하세요.  
 
  
##  <a name="Related"></a> Related Views, Functions, and Procedures  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 을(를) 통해 또는 다음 뷰 및 프로시저를 사용하여 쿼리 저장소를 보고 관리할 수 있습니다.  
  
-   [sys.fn_stmt_sql_handle_from_sql_stmt&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
### <a name="query-store-catalog-views"></a>쿼리 저장소 카탈로그 뷰  
 7개의 카탈로그 뷰에 쿼리 저장소에 대한 정보가 표시됩니다.  
  
-   [sys.database_query_store_options&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)  
  
-   [sys.query_context_settings&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)  
  
-   [sys.query_store_plan&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)  
  
-   [sys.query_store_query&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)  
  
-   [sys.query_store_query_text&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)  
  
-   [sys.query_store_runtime_stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)  
  
-   [sys.query_store_runtime_stats_interval&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)  
  
### <a name="query-store-stored-procedures"></a>쿼리 저장소 저장 프로시저  
 6개의 저장 프로시저로 쿼리 저장소를 구성합니다.  
  
-   [sp_query_store_flush_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)  
  
-   [sp_query_store_reset_exec_stats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)  
  
-   [sp_query_store_force_plan&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)  
  
-   [sp_query_store_unforce_plan&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)  
  
-   [sp_query_store_remove_plan&#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)  
  
-   [sp_query_store_remove_query&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)  
 
  
##  <a name="Scenarios"></a> 주요 사용 시나리오  
  
###  <a name="OptionMgmt"></a> Option Management  
 이 섹션에서는 쿼리 저장소 기능 자체를 관리하는 데 대한 지침을 제공합니다.  
  
 **쿼리 저장소가 현재 활성 상태인가요?**  
  
 쿼리 저장소는 데이터를 사용자 데이터베이스 내에 저장하며 이 때문에 쿼리 저장소에는 크기 제한( **MAX_STORAGE_SIZE_MB**로 구성)이 있습니다. 쿼리 저장소의 데이터가 이 제한에 도달하면 쿼리 저장소는 자동으로 상태를 읽기/쓰기에서 읽기 전용으로 변경하고 새 데이터 수집을 중지합니다.  
  
 쿼리 저장소가 현재 활성 상태인지, 및 현재 런타임 통계를 수집하는지의 여부를 정하려면 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md) to determine if 쿼리 저장소가 현재 활성 상태인지, 및 현재 런타임 통계를 수집하는지의 여부를 정하려면 Store is currently active, and whether it is currently collects runtime stats or not.  
  
```  
SELECT actual_state, actual_state_desc, readonly_reason,   
    current_storage_size_mb, max_storage_size_mb  
FROM sys.database_query_store_options;  
```  
  
 쿼리 저장소 상태는 actual_state 열에 의해 결정됩니다. 원하는 상태와 다른 경우 readonly_reason 열에서 자세한 정보를 확인할 수 있습니다.   
쿼리 저장소의 크기가 할당량을 초과하면 기능 readon_only 모드로 전환됩니다.  
  
 **쿼리 저장소 옵션 가져오기**  
  
 쿼리 저장소 상태에 대한 자세한 정보를 찾으려면 사용자 데이터베이스에서 다음을 실행합니다.  
  
```  
SELECT * FROM sys.database_query_store_options;  
```  
  
 **쿼리 저장소 간격 설정**  
  
 쿼리 런타임 통계를 집계하는 간격(기본값은 60분)을 재정의할 수 있습니다.  
  
```  
ALTER DATABASE <database_name>   
SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 15);  
```  
  
 임의의 값을 사용할 수는 없고 1, 5, 10, 15, 30, 60 및 1440분 중에서 하나를 사용해야 합니다.  
  
 간격에 대한 새 값은 **sys.database_query_store_options** 뷰를 통해 노출됩니다.  
  
 **쿼리 저장소 공간 사용량**  
  
 현재 쿼리 저장소 크기를 확인하려면 데이터베이스에서 다음 문의 실행을 제한합니다.  
  
```  
SELECT current_storage_size_mb, max_storage_size_mb   
FROM sys.database_query_store_options;  
```  
  
 쿼리 저장소 저장 공간이 꽉 차는 경우 다음 문을 사용하여 저장소를 확장합니다.  
  
```  
ALTER DATABASE <database_name>   
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <new_size>);  
```  
  
 **모든 쿼리 저장소 옵션 설정**  
  
 단일 ALTER DATABASE 문 사용하여 여러 쿼리 저장소 옵션을 한 번에 설정할 수 있습니다.  
  
```  
ALTER DATABASE <database name>   
SET QUERY_STORE (  
    OPERATION_MODE = READ_WRITE,  
    CLEANUP_POLICY =   
    (STALE_QUERY_THRESHOLD_DAYS = 30),  
    DATA_FLUSH_INTERVAL_SECONDS = 3000,  
    MAX_STORAGE_SIZE_MB = 500,  
    INTERVAL_LENGTH_MINUTES = 15,  
    SIZE_BASED_CLEANUP_MODE = AUTO,  
    QUERY_CAPTURE_MODE = AUTO,  
    MAX_PLANS_PER_QUERY = 1000  
);  
```  
  
 **공간 정리**  
  
 데이터베이스 생성 중 쿼리 저장소 내부 테이블이 PRIMARY 파일 그룹에 만들어지며 해당 구성은 나중에 변경할 수 없습니다. 공간이 부족한 경우 다음 문을 사용하여 이전 쿼리 저장소 데이터를 지울 수 있습니다.  
  
```  
ALTER DATABASE <db_name> SET QUERY_STORE CLEAR;  
```  
  
 또는 임시 쿼리 데이터는 쿼리 최적화 및 계획 분석과 관련성이 적고 공간만 많이 차지하므로 임시 쿼리 데이터만 지울 수도 있습니다.  
  
 **임시 쿼리 삭제** 한번만 실행되고 24시간 이상 지난 쿼리를 삭제합니다.  
  
```  
DECLARE @id int  
DECLARE adhoc_queries_cursor CURSOR   
FOR   
SELECT q.query_id  
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q   
    ON q.query_text_id = qt.query_text_id  
JOIN sys.query_store_plan AS p   
    ON p.query_id = q.query_id  
JOIN sys.query_store_runtime_stats AS rs   
    ON rs.plan_id = p.plan_id  
GROUP BY q.query_id  
HAVING SUM(rs.count_executions) < 2   
AND MAX(rs.last_execution_time) < DATEADD (hour, -24, GETUTCDATE())  
ORDER BY q.query_id ;  
  
OPEN adhoc_queries_cursor ;  
FETCH NEXT FROM adhoc_queries_cursor INTO @id;  
WHILE @@fetch_status = 0  
    BEGIN   
        PRINT @id  
        EXEC sp_query_store_remove_query @id  
        FETCH NEXT FROM adhoc_queries_cursor INTO @id  
    END   
CLOSE adhoc_queries_cursor ;  
DEALLOCATE adhoc_queries_cursor;  
```  
  
 더 이상 중요하지 않은 데이터를 지우는 다른 논리를 사용하여 프로시저를 직접 정의할 수 있습니다.  
  
 위의 예제에서는 필요 없는 데이터를 제거하는 **sp_query_store_remove_query** 확장 저장 프로시저를 사용합니다. 또한, 다음을 사용 가능:  
  
-   **sp_query_store_reset_exec_stats** – 지정된 계획에 대한 런타임 통계를 지웁니다.  
  
-   **sp_query_store_remove_plan** – 단일 계획을 제거합니다.  
 
  
###  <a name="Peformance"></a> Performance Auditing and Troubleshooting  
 쿼리 저장소는 쿼리 실행 전반에서 컴파일 및 런타임 메트릭 기록을 유지하여 사용자가 작업에 대한 질문을 할 수 있습니다.  
  
 **마지막 *n*개 쿼리가 데이터베이스에서 실행되었나요?**  
  
```  
SELECT TOP 10 qt.query_sql_text, q.query_id,   
    qt.query_text_id, p.plan_id, rs.last_execution_time  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
ORDER BY rs.last_execution_time DESC;  
```  
  
 **각 쿼리에 대한 실행 수는 몇 개입니까?**  
  
```  
SELECT q.query_id, qt.query_text_id, qt.query_sql_text,   
    SUM(rs.count_executions) AS total_execution_count  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
GROUP BY q.query_id, qt.query_text_id, qt.query_sql_text  
ORDER BY total_execution_count DESC;  
```  
  
 **지난 1 시간 내에 평균 실행 시간이 가장 긴 쿼리 수는 몇 개입니까?**  
  
```  
SELECT TOP 10 rs.avg_duration, qt.query_sql_text, q.query_id,  
    qt.query_text_id, p.plan_id, GETUTCDATE() AS CurrentUTCTime,   
    rs.last_execution_time   
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
WHERE rs.last_execution_time > DATEADD(hour, -1, GETUTCDATE())  
ORDER BY rs.avg_duration DESC;  
```  
  
 **지난 24시간 동안 평균 물리적 IO 읽기가 가장 큰 쿼리 수 및 해당하는 평균 행 수 및 실행 수는 몇 개입니까?**  
  
```  
SELECT TOP 10 rs.avg_physical_io_reads, qt.query_sql_text,   
    q.query_id, qt.query_text_id, p.plan_id, rs.runtime_stats_id,   
    rsi.start_time, rsi.end_time, rs.avg_rowcount, rs.count_executions  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi   
    ON rsi.runtime_stats_interval_id = rs.runtime_stats_interval_id  
WHERE rsi.start_time >= DATEADD(hour, -24, GETUTCDATE())   
ORDER BY rs.avg_physical_io_reads DESC;  
```  
  
 **여러 계획을 사용하는 쿼리는 무엇입니까?** 이러한 쿼리는 계획 선택 변경으로 인한 재발을 일으킬 수 있으므로 특히 흥미롭습니다. 다음 쿼리는 이러한 쿼리와 함께 모든 계획을 식별합니다.  
  
```  
WITH Query_MultPlans  
AS  
(  
SELECT COUNT(*) AS cnt, q.query_id   
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q  
    ON qt.query_text_id = q.query_text_id  
JOIN sys.query_store_plan AS p  
    ON p.query_id = q.query_id  
GROUP BY q.query_id  
HAVING COUNT(distinct plan_id) > 1  
)  
  
SELECT q.query_id, object_name(object_id) AS ContainingObject,   
    query_sql_text, plan_id, p.query_plan AS plan_xml,  
    p.last_compile_start_time, p.last_execution_time  
FROM Query_MultPlans AS qm  
JOIN sys.query_store_query AS q  
    ON qm.query_id = q.query_id  
JOIN sys.query_store_plan AS p  
    ON q.query_id = p.query_id  
JOIN sys.query_store_query_text qt   
    ON qt.query_text_id = q.query_text_id  
ORDER BY query_id, plan_id;  
```  
  
 **최근에 성능이 저하된 쿼리(다른 시점과 비교)는 무엇입니까?** 다음 쿼리 예제는 지난 48 시간에 계획 선택 변경으로 인해 실행 시간이 두 배가 된 모든 쿼리를 반환합니다. 쿼리에서는 모든 런타임 통계 간격을 나란히 비교합니다.  
  
```  
SELECT   
    qt.query_sql_text,   
    q.query_id,   
    qt.query_text_id,   
    rs1.runtime_stats_id AS runtime_stats_id_1,  
    rsi1.start_time AS interval_1,   
    p1.plan_id AS plan_1,   
    rs1.avg_duration AS avg_duration_1,   
    rs2.avg_duration AS avg_duration_2,  
    p2.plan_id AS plan_2,   
    rsi2.start_time AS interval_2,   
    rs2.runtime_stats_id AS runtime_stats_id_2  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p1   
    ON q.query_id = p1.query_id   
JOIN sys.query_store_runtime_stats AS rs1   
    ON p1.plan_id = rs1.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi1   
    ON rsi1.runtime_stats_interval_id = rs1.runtime_stats_interval_id   
JOIN sys.query_store_plan AS p2   
    ON q.query_id = p2.query_id   
JOIN sys.query_store_runtime_stats AS rs2   
    ON p2.plan_id = rs2.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi2   
    ON rsi2.runtime_stats_interval_id = rs2.runtime_stats_interval_id  
WHERE rsi1.start_time > DATEADD(hour, -48, GETUTCDATE())   
    AND rsi2.start_time > rsi1.start_time   
    AND p1.plan_id <> p2.plan_id  
    AND rs2.avg_duration > 2*rs1.avg_duration  
ORDER BY q.query_id, rsi1.start_time, rsi2.start_time;  
```  
  
 계획 선택 변경과 관련된 성능 저하뿐 아니라 성능 저하를 모두 확인하려면 이전 쿼리에서 `AND p1.plan_id <> p2.plan_id` 조건을 제거하면 됩니다.  
  
 **최근에 성능이 저하된 쿼리(최근 및 기록 실행 비교)는 무엇입니까?** 다음 쿼리는 실행 기간을 기준으로 쿼리 실행을 비교합니다. 이 특정 예제의 쿼리는 최근 기간(1시간) 및 기록 기간(어제)의 실행을 비교하고 `additional_duration_workload`를 초래한 쿼리를 식별합니다. 이 메트릭은 최근 평균 실행 기간과 기록 평균 실행 간의 차이에 최근 실행 수를 곱한 값으로 계산됩니다. 이 값은 실제로 기록에 비해 최근 실행으로 초래된 추가 기간을 나타냅니다.  
  
```  
--- "Recent" workload - last 1 hour  
DECLARE @recent_start_time datetimeoffset;  
DECLARE @recent_end_time datetimeoffset;  
SET @recent_start_time = DATEADD(hour, -1, SYSUTCDATETIME());  
SET @recent_end_time = SYSUTCDATETIME();  
  
--- "History" workload  
DECLARE @history_start_time datetimeoffset;  
DECLARE @history_end_time datetimeoffset;  
SET @history_start_time = DATEADD(hour, -24, SYSUTCDATETIME());  
SET @history_end_time = SYSUTCDATETIME();  
  
WITH  
hist AS  
(  
    SELECT   
        p.query_id query_id,   
        CONVERT(float, SUM(rs.avg_duration*rs.count_executions)) total_duration,   
        SUM(rs.count_executions) count_executions,  
        COUNT(distinct p.plan_id) num_plans   
     FROM sys.query_store_runtime_stats AS rs  
        JOIN sys.query_store_plan p ON p.plan_id = rs.plan_id  
    WHERE  (rs.first_execution_time >= @history_start_time   
               AND rs.last_execution_time < @history_end_time)  
        OR (rs.first_execution_time \<= @history_start_time   
               AND rs.last_execution_time > @history_start_time)  
        OR (rs.first_execution_time \<= @history_end_time   
               AND rs.last_execution_time > @history_end_time)  
    GROUP BY p.query_id  
),  
recent AS  
(  
    SELECT   
        p.query_id query_id,   
        CONVERT(float, SUM(rs.avg_duration*rs.count_executions)) total_duration,   
        SUM(rs.count_executions) count_executions,  
        COUNT(distinct p.plan_id) num_plans   
    FROM sys.query_store_runtime_stats AS rs  
        JOIN sys.query_store_plan p ON p.plan_id = rs.plan_id  
    WHERE  (rs.first_execution_time >= @recent_start_time   
               AND rs.last_execution_time < @recent_end_time)  
        OR (rs.first_execution_time \<= @recent_start_time   
               AND rs.last_execution_time > @recent_start_time)  
        OR (rs.first_execution_time \<= @recent_end_time   
               AND rs.last_execution_time > @recent_end_time)  
    GROUP BY p.query_id  
)  
SELECT   
    results.query_id query_id,  
    results.query_text query_text,  
    results.additional_duration_workload additional_duration_workload,  
    results.total_duration_recent total_duration_recent,  
    results.total_duration_hist total_duration_hist,  
    ISNULL(results.count_executions_recent, 0) count_executions_recent,  
    ISNULL(results.count_executions_hist, 0) count_executions_hist   
FROM  
(  
    SELECT  
        hist.query_id query_id,  
        qt.query_sql_text query_text,  
        ROUND(CONVERT(float, recent.total_duration/  
                   recent.count_executions-hist.total_duration/hist.count_executions)  
               *(recent.count_executions), 2) AS additional_duration_workload,  
        ROUND(recent.total_duration, 2) total_duration_recent,   
        ROUND(hist.total_duration, 2) total_duration_hist,  
        recent.count_executions count_executions_recent,  
        hist.count_executions count_executions_hist     
    FROM hist   
        JOIN recent   
            ON hist.query_id = recent.query_id   
        JOIN sys.query_store_query AS q   
            ON q.query_id = hist.query_id  
        JOIN sys.query_store_query_text AS qt   
            ON q.query_text_id = qt.query_text_id      
) AS results  
WHERE additional_duration_workload > 0  
ORDER BY additional_duration_workload DESC  
OPTION (MERGE JOIN);  
```  
 
  
###  <a name="Stability"></a> Maintaining Query Performance Stability  
 여러 번 실행되는 쿼리의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 다른 계획을 사용하여 리소스 사용률 및 기간이 달라짐을 알 수 있습니다. 쿼리 저장소를 사용하면 쿼리 성능이 저하되는 시기를 확인하고 관심 있는 기간 내에 최적의 계획을 결정할 수 있습니다. 그런 다음 향후 쿼리 실행에 해당하는 최적의 계획을 적용할 수 있습니다.  
  
 또한 자동으로 매개 변수화되거나 수동으로 매개 변수화되는 매개 변수를 사용하여 일관성이 없는 쿼리 성능도 식별할 수 있습니다. 여러 계획 중에 대부분의 매개 변수 값에 대해 빠르고 최적화된 계획을 식별하고 해당 계획을 강제 적용할 수 있습니다. 이를 통해 다양한 사용자 시나리오에 대해 예측 가능한 성능을 유지할 수 있습니다.  
  
 **쿼리에 대 한 계획 강제 적용(강제 적용 정책 적용)** 특정 쿼리에 계획을 ;강제 적용하는 경우 쿼리를 실행할 때마다 강제 적용된 계획이 실행됩니다.  
  
```  
EXEC sp_query_store_force_plan @query_id = 48, @plan_id = 49;  
```  
  
 **sp_query_store_force_plan** 을 사용할 경우 쿼리 저장소에서 해당 쿼리에 대한 계획으로 기록된 계획만 강제로 적용할 수 있습니다. 즉, 쿼리 저장소가 활성 상태일 때 해당 쿼리를 실행하는 데 이미 사용된 계획만 쿼리에 사용할 수 있습니다.  
  
 **쿼리에 대한 계획 강제 적용 제거** 다시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램 사용하여 최적의 쿼리 계획을 계산하려면 **sp_query_store_unforce_plan** 을 사용하여 쿼리에 대해 선택한 계획의 강제 적용을 취소합니다.  
  
```  
EXEC sp_query_store_unforce_plan @query_id = 48, @plan_id = 49;  
```  
 
  
## <a name="see-also"></a>관련 항목:  
 [쿼리 저장소에 대한 모범 사례](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [메모리 내 OLTP와 쿼리 저장소 사용](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)   
 [쿼리 저장소 사용 시나리오](../../relational-databases/performance/query-store-usage-scenarios.md)   
 [쿼리 저장소에서 데이터를 수집하는 방법](../../relational-databases/performance/how-query-store-collects-data.md)   
 [쿼리 저장소 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [쿼리 저장소 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [성능 모니터링 및 튜닝 도구](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)   
 [작업 모니터 열기&#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)   
 [활성 쿼리 통계](../../relational-databases/performance/live-query-statistics.md)   
 [작업 모니터](../../relational-databases/performance-monitor/activity-monitor.md)   
 [sys.database_query_store_options&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)  
 [Azure SQL 데이터베이스에서 쿼리 저장소 작업](https://azure.microsoft.com/documentation/articles/sql-database-operate-query-store/) 
  

