---
title: UPDATE STATISTICS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- UPDATE STATISTICS
- UPDATE_STATISTICS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- updating statistics
- query optimization statistics [SQL Server], updating
- UPDATE STATISTICS statement
- statistical information [SQL Server], updating
ms.assetid: 919158f2-38d0-4f68-82ab-e1633bd0d308
caps.latest.revision: 74
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 99794bf5f9adc7da4106ebffa7ffc27e6b469cb7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="update-statistics-transact-sql"></a>UPDATE STATISTICS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  테이블 또는 인덱싱된 뷰에 대한 쿼리 최적화 통계를 업데이트합니다. 기본적으로 쿼리 최적화 프로그램은 이미 필요할 때 통계를 업데이트하여 쿼리 계획을 향상시킵니다. 하지만 경우에 따라 사용자가 UPDATE STATISTICS 또는 [sp_updatestats](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md) 저장 프로시저를 사용하여 기본 업데이트 주기보다 더 자주 통계를 업데이트하여 쿼리 성능을 향상시킬 수 있습니다.  
  
 통계를 업데이트하면 쿼리가 최신 통계로 컴파일되지만 쿼리도 다시 컴파일됩니다. 쿼리 계획 향상과 쿼리 재컴파일 소요 시간 간의 성능 균형을 유지해야 하므로 통계를 너무 자주 업데이트하지 않는 것이 좋습니다. 구체적인 성능 균형 유지의 정도는 응용 프로그램에 따라 달라집니다. UPDATE STATISTIC은 통계를 작성하기 위해 tempdb를 사용하여 행 샘플을 정렬할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
UPDATE STATISTICS table_or_indexed_view_name   
    [   
        {   
            { index_or_statistics__name }  
          | ( { index_or_statistics_name } [ ,...n ] )   
                }  
    ]   
    [    WITH   
        [  
            FULLSCAN   
              [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
            | SAMPLE number { PERCENT | ROWS }   
              [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
            | RESAMPLE   
              [ ON PARTITIONS ( { <partition_number> | <range> } [, …n] ) ]  
            | <update_stats_stream_option> [ ,...n ]  
        ]   
        [ [ , ] [ ALL | COLUMNS | INDEX ]   
        [ [ , ] NORECOMPUTE ]   
        [ [ , ] INCREMENTAL = { ON | OFF } ] 
        [ [ , ] MAXDOP = max_degree_of_parallelism ] 
    ] ;  
  
<update_stats_stream_option> ::=  
    [ STATS_STREAM = stats_stream ]  
    [ ROWCOUNT = numeric_constant ]  
    [ PAGECOUNT = numeric_contant ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
UPDATE STATISTICS schema_name . ] table_name   
    [ ( { statistics_name | index_name } ) ]  
    [ WITH   
       {  
              FULLSCAN   
            | SAMPLE number PERCENT   
            | RESAMPLE   
        }  
    ]  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *table_or_indexed_view_name*  
 통계 개체를 포함하는 테이블 또는 인덱싱된 뷰의 이름입니다.  
  
 *index_or_statistics_name*  
 통계를 업데이트할 인덱스 이름 또는 업데이트할 통계의 이름입니다. *index_or_statistics_name*을 지정하지 않으면 쿼리 최적화 프로그램에서 테이블 또는 인덱싱된 뷰에 대한 모든 통계를 업데이트합니다. 여기에는 CREATE STATISTICS 문을 사용하여 생성된 통계, AUTO_CREATE_STATISTICS가 설정되어 생성된 단일 열 통계 및 인덱스에 대해 생성된 통계 등이 포함됩니다.  
  
 AUTO_CREATE_STATISTICS에 대한 자세한 내용은 [ALTER DATABASE SET 옵션 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요. 테이블 또는 뷰에 대한 모든 인덱스를 보려면 [sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)를 사용하면 됩니다.  
  
 FULLSCAN  
 테이블 또는 인덱싱된 뷰에 있는 모든 행을 검색하여 통계를 계산합니다. FULLSCAN과 SAMPLE 100 PERCENT의 결과는 같습니다. FULLSCAN은 SAMPLE 옵션과 함께 사용할 수 없습니다.  
  
 SAMPLE *number* { PERCENT | ROWS }  
 쿼리 최적화 프로그램에서 통계를 업데이트할 때 사용할 테이블이나 인덱싱된 뷰에 있는 행의 비율이나 개수를 대략적으로 지정합니다. PERCENT의 경우 *number*가 0부터 100까지일 수 있고, ROWS의 경우 *number*가 0부터 총 행 수까지일 수 있습니다. 쿼리 최적화 프로그램에서 샘플링하는 실제 행의 비율이나 개수는 지정된 비율이나 개수와 일치하지 않을 수 있습니다. 예를 들어, 쿼리 최적화 프로그램에서는 데이터 페이지의 모든 행을 검색합니다.  
  
 SAMPLE은 기본 샘플링을 기반으로 하는 쿼리 계획이 만족스럽지 못한 특별한 경우에 유용합니다. 대부분의 경우에는 기본적으로 쿼리 최적화 프로그램에서 고품질의 쿼리 계획을 만들기 위해 필요에 따라 샘플링을 사용하고 통계적으로 중요한 샘플 크기를 결정하기 때문에 SAMPLE을 지정할 필요가 없습니다. 
 
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 통계를 작성하는 데이터의 샘플링은 병렬로 수행되어(호환성 수준 130을 사용하는 경우) 통계 컬렉션의 성능이 개선되었습니다. 쿼리 최적화 프로그램은 테이블 크기가 특정 임계값을 초과할 때마다 병렬 샘플 통계를 사용합니다. 
   
 SAMPLE은 FULLSCAN 옵션과 함께 사용할 수 없습니다. SAMPLE과 FULLSCAN을 둘 다 지정하지 않으면 기본적으로 쿼리 최적화 프로그램에서 샘플링된 데이터를 사용하고 샘플 크기를 계산합니다.  
  
 0 PERCENT 또는 0 ROWS로 지정하지 않는 것이 좋습니다. 0 PERCENT 또는 0 ROWS로 지정하면 통계 데이터가 포함되지 않은 빈 통계 개체가 업데이트됩니다.  
  
 대부분의 워크로드에서 전체 검사가 필요하지 않으며 기본 샘플링이 적당합니다.  
그러나 매우 폭 넓은 데이터 배포에 민감한 특정 워크로드의 경우 샘플 크기를 증가시켜야 할 수 있으며 심지어 전체 검사가 필요할 수도 있습니다.  
자세한 내용은 [CSS SQL 에스컬레이션 서비스 블로그](http://blogs.msdn.com/b/psssql/archive/2010/07/09/sampling-can-produce-less-accurate-statistics-if-the-data-is-not-evenly-distributed.aspx)를 참조하세요.  
  
 RESAMPLE  
 가장 최근의 샘플링 주기를 사용하여 각 통계를 업데이트합니다.  
  
 RESAMPLE을 사용하면 전체 테이블 검색이 수행될 수 있습니다. 예를 들어 인덱스에 대한 통계에서는 샘플링 주기에 전체 테이블 검색을 사용합니다. 샘플 옵션(SAMPLE, FULLSCAN, RESAMPLE)을 지정하지 않으면 기본적으로 쿼리 최적화 프로그램에서 데이터를 샘플링하여 샘플 크기를 계산합니다.  

PERSIST_SAMPLE_PERCENT = { ON | OFF }  
**ON**을 선택한 경우 통계는 샘플링 비율을 명시적으로 지정하지 않은 이후 업데이트에 대해 설정된 샘플링 비율을 유지합니다. **OFF**를 선택한 경우 샘플링 비율을 명시적으로 지정하지 않은 이후 업데이트의 통계 샘플링 비율은 기본 샘플링으로 재설정됩니다. 기본값은 **OFF**입니다. 
 
 > [!NOTE]
 > AUTO_UPDATE_STATISTICS가 실행된 경우 유지된 샘플링 비율(사용 가능한 경우)을 사용하거나 사용 가능하지 않은 경우 기본 샘플링 비율을 사용합니다.
 > RESAMPLE 동작은 이 옵션의 영향을 받지 않습니다.
 
 > [!TIP] 
 > [DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md) 및 [sys.dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)는 선택된 통계에 대해 유지되는 샘플 비율 값을 표시합니다.
 
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4부터)에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU1부터)까지.  
 
 ON PARTITIONS ( { \<partition_number> | \<range> } [, …n] ) ] ON PARTITIONS 절에 지정된 파티션에 적용되는 리프 수준 통계를 강제로 다시 계산한 다음, 병합하여 전역 통계를 작성합니다. 서로 다른 샘플링 주기로 작성된 파티션 통계는 병합할 수 없으므로 WITH RESAMPLE이 필요합니다.  
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
 ALL | COLUMNS | INDEX  
 기존의 모든 통계, 하나 이상의 열에 대해 생성된 통계 또는 인덱스에 대해 생성된 통계를 업데이트합니다. 아무 옵션도 지정하지 않은 UPDATE STATISTICS 문은 테이블 또는 인덱싱된 뷰의 모든 통계를 업데이트합니다.  
  
 NORECOMPUTE  
 지정된 통계에 대해 자동 통계 업데이트 옵션인 AUTO_UPDATE_STATISTICS를 비활성화합니다. 이 옵션을 지정하지 않으면 쿼리 최적화 프로그램에서 이 통계 업데이트를 완료하고 이후 업데이트부터 비활성화합니다.  
  
 AUTO_UPDATE_STATISTICS 옵션 동작을 다시 활성화하려면 UPDATE STATISTICS를 NORECOMPUTE 옵션 없이 다시 실행하거나 **sp_autostats**를 실행합니다.  
  
> [!WARNING]  
>  이 옵션을 사용하면 최적이 아닌 쿼리 계획이 생성될 수 있습니다. 이 옵션은 자격 있는 시스템 관리자가 꼭 필요한 경우에만 사용하는 것이 좋습니다.  
  
 AUTO_STATISTICS_UPDATE 옵션에 대한 자세한 내용은 [ALTER DATABASE SET 옵션 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.  
  
 INCREMENTAL = {ON | OFF}  
 **ON**으로 설정된 경우 파티션 통계별로 통계가 다시 작성됩니다. **OFF**로 설정된 경우 통계 트리가 삭제되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 통계를 다시 계산합니다. 기본값은 **OFF**입니다.  
  
 파티션별 통계가 지원되지 않을 경우 오류가 생성됩니다. 다음 통계 유형에 대해서는 증분 통계가 지원되지 않습니다.  
  
-   기본 테이블을 기준으로 파티션 정렬되지 않은 인덱스를 사용하여 작성된 통계입니다.  
-   Always On 읽기 가능한 보조 데이터베이스에 대해 작성된 통계입니다.  
-   읽기 전용 데이터베이스에 대해 작성된 통계입니다.  
-   필터링된 인덱스에 대해 작성된 통계입니다.  
-   뷰에 대해 작성된 통계입니다.  
-   내부 테이블에 대해 작성된 통계입니다.  
-   공간 인덱스 또는 XML 인덱스를 사용하여 작성된 통계입니다.  
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지

MAXDOP = *max_degree_of_parallelism*  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3부터).  
  
 통계 작업 기간 동안 **최대 병렬 처리 수준** 구성 옵션을 재정의합니다. 자세한 내용은 [Configure the max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요. MAXDOP를 사용하여 병렬 계획 실행에 사용되는 프로세서 수를 제한할 수 있습니다. 최대값은 64개입니다.  
  
 *max_degree_of_parallelism*은 다음 중 하나일 수 있습니다.  
  
 1  
 병렬 계획이 생성되지 않습니다.  
  
 \>1  
 병렬 통계 작업에 사용되는 최대 프로세서 수를 현재 시스템 워크로드에 따라 지정된 수 또는 더 적은 수로 제한합니다.  
  
 0(기본값)  
 현재 시스템 작업에 따라 실제 프로세서 수 이하의 프로세서를 사용합니다.  
  
 \<update_stats_stream_option> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  

## <a name="remarks"></a>Remarks  
  
## <a name="when-to-use-update-statistics"></a>UPDATE STATISTICS를 사용하는 경우  
 UPDATE STATISTICS를 사용하는 경우에 대한 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.  

## <a name="limitations-and-restrictions"></a>제한 사항  
* 외부 테이블에 대해서는 통계 업데이트가 지원되지 않습니다. 외부 테이블에 대한 통계를 업데이트하려면 통계를 삭제하고 다시 만듭니다.  
* MAXDOP 옵션은 STATS_STREAM, ROWCOUNT 및 PAGECOUNT 옵션과 호환되지 않습니다.

## <a name="updating-all-statistics-with-spupdatestats"></a>sp_updatestats를 사용하여 모든 통계 업데이트  
 데이터베이스의 모든 사용자 정의 테이블 및 내부 테이블에 대한 통계를 업데이트하는 방법은 저장 프로시저 [sp_updatestats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)를 참조하세요. 예를 들어 다음 명령에서는 sp_updatestats를 호출하여 데이터베이스에 대한 모든 통계를 업데이트합니다.  
  
```sql  
EXEC sp_updatestats;  
```  
  
## <a name="determining-the-last-statistics-update"></a>마지막 통계 업데이트 확인  
 통계가 마지막으로 업데이트된 시점을 확인하려면 [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md) 함수를 사용합니다.  
  
## <a name="pdw--sql-data-warehouse"></a>PDW / SQL Data Warehouse  
 다음 구문은 PDW / SQL Data Warehouse에서 지원되지 않음  
  
```sql  
update statistics t1 (a,b);   
```  
  
```sql  
update statistics t1 (a) with sample 10 rows;  
```  
  
```sql  
update statistics t1 (a) with NORECOMPUTE;  
```  
  
```sql  
update statistics t1 (a) with INCREMENTAL=ON;  
```  
  
```sql  
update statistics t1 (a) with stats_stream = 0x01;  
```  
  
## <a name="permissions"></a>사용 권한  
 테이블이나 뷰에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-update-all-statistics-on-a-table"></a>1. 테이블에 대한 모든 통계 업데이트  
 다음 예제에서는 `SalesOrderDetail` 테이블에서 모든 인덱스에 대한 통계를 업데이트합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Sales.SalesOrderDetail;  
GO  
```  
  
### <a name="b-update-the-statistics-for-an-index"></a>2. 인덱스에 대한 통계 업데이트  
 다음 예에서는 `AK_SalesOrderDetail_rowguid` 테이블의 `SalesOrderDetail` 인덱스에 대한 통계를 업데이트합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Sales.SalesOrderDetail AK_SalesOrderDetail_rowguid;  
GO  
```  
  
### <a name="c-update-statistics-by-using-50-percent-sampling"></a>3. 50퍼센트 샘플링을 사용하여 통계 업데이트  
 다음 예에서는 `Name` 테이블의 `ProductNumber` 및 `Product` 열에 대한 통계를 만든 후 업데이트합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE STATISTICS Products  
    ON Production.Product ([Name], ProductNumber)  
    WITH SAMPLE 50 PERCENT  
-- Time passes. The UPDATE STATISTICS statement is then executed.  
UPDATE STATISTICS Production.Product(Products)   
    WITH SAMPLE 50 PERCENT;  
```  
  
### <a name="d-update-statistics-by-using-fullscan-and-norecompute"></a>4. FULLSCAN 및 NORECOMPUTE를 사용하여 통계 업데이트  
 다음 예에서는 `Products` 테이블의 `Product` 통계를 업데이트하고 `Product` 테이블의 모든 행을 전체 검색하며 `Products` 통계에 대한 자동 통계를 비활성화합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Production.Product(Products)  
    WITH FULLSCAN, NORECOMPUTE;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-update-statistics-on-a-table"></a>5. 테이블에 대한 모든 통계 업데이트  
 다음 예제에서는 `Customer` 테이블에서 `CustomerStats1` 통계를 업데이트합니다.  
  
```sql  
UPDATE STATISTICS Customer ( CustomerStats1 );  
```  
  
### <a name="f-update-statistics-by-using-a-full-scan"></a>6. 전체 검사를 사용하여 통계 업데이트  
 다음 예제에서는 `Customer` 테이블의 모든 행 검사를 기반으로 `CustomerStats1` 통계를 업데이트합니다.  
  
```sql  
UPDATE STATISTICS Customer (CustomerStats1) WITH FULLSCAN;  
```  
  
### <a name="g-update-all-statistics-on-a-table"></a>7. 테이블에 대한 모든 통계 업데이트  
 다음 예제에서는 `Customer` 테이블에서 모든 통계를 업데이트합니다.  
  
```sql  
UPDATE STATISTICS Customer;  
```  
  
## <a name="see-also"></a>참고 항목  
 [통계](../../relational-databases/statistics/statistics.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_updatestats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [STATS_DATE&#40;Transact-SQL&#41;](../../t-sql/functions/stats-date-transact-sql.md)  
 [sys.dm_db_stats_properties&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) [sys.dm_db_stats_histogram&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 
  



