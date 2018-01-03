---
title: UPDATE STATISTICS (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATE STATISTICS
- UPDATE_STATISTICS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- updating statistics
- query optimization statistics [SQL Server], updating
- UPDATE STATISTICS statement
- statistical information [SQL Server], updating
ms.assetid: 919158f2-38d0-4f68-82ab-e1633bd0d308
caps.latest.revision: "74"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b619b3cf7ea50fb87e18fd96e8a85a2a231d21f5
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="update-statistics-transact-sql"></a>UPDATE STATISTICS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  테이블 또는 인덱싱된 뷰에 대한 쿼리 최적화 통계를 업데이트합니다. 기본적으로 쿼리 최적화 통계를 업데이트; 쿼리 계획을 개선 하기 위해 필요에 따라 UPDATE STATISTICS 또는 저장된 프로시저를 사용 하 여 쿼리 성능을 향상 수 하는 경우에 따라 [sp_updatestats](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md) 기본 업데이트 보다 더 자주 통계를 업데이트 합니다.  
  
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
 테이블 또는 인덱싱된 뷰의 통계 개체를 포함 하는 이름이입니다.  
  
 *index_or_statistics_name*  
 통계를 업데이트할 인덱스 이름 또는 업데이트할 통계의 이름입니다. 경우 *index_or_statistics_name* 를 지정 하지 않으면 쿼리 최적화 프로그램이 테이블 또는 인덱싱된 뷰에 대 한 모든 통계를 업데이트 합니다. 여기에는 CREATE STATISTICS 문을 사용하여 생성된 통계, AUTO_CREATE_STATISTICS가 설정되어 생성된 단일 열 통계 및 인덱스에 대해 생성된 통계 등이 포함됩니다.  
  
 AUTO_CREATE_STATISTICS에 대 한 자세한 내용은 참조 [ALTER DATABASE SET 옵션 &#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md). 테이블 또는 뷰에 대 한 모든 인덱스를 보려면 사용할 수 있습니다 [sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)합니다.  
  
 FULLSCAN  
 테이블 또는 인덱싱된 뷰에 있는 모든 행을 검색하여 통계를 계산합니다. FULLSCAN과 SAMPLE 100 PERCENT의 결과는 같습니다. FULLSCAN은 SAMPLE 옵션과 함께 사용할 수 없습니다.  
  
 샘플 *번호* {%| 행을 (를)  
 쿼리 최적화 프로그램에서 통계를 업데이트할 때 사용할 테이블이나 인덱싱된 뷰에 있는 행의 비율이나 개수를 대략적으로 지정합니다. Percent의 경우 *번호* 에서 100 사이 행에 대 한 일 수 있습니다 *번호* 총 행 수를 0에서 일 수 있습니다. 쿼리 최적화 프로그램에서 샘플링하는 실제 행의 비율이나 개수는 지정된 비율이나 개수와 일치하지 않을 수 있습니다. 예를 들어, 쿼리 최적화 프로그램에서는 데이터 페이지의 모든 행을 검색합니다.  
  
 SAMPLE은 기본 샘플링을 기반으로 하는 쿼리 계획이 만족스럽지 못한 특별한 경우에 유용합니다. 대부분의 경우에는 기본적으로 쿼리 최적화 프로그램에서 고품질의 쿼리 계획을 만들기 위해 필요에 따라 샘플링을 사용하고 통계적으로 중요한 샘플 크기를 결정하기 때문에 SAMPLE을 지정할 필요가 없습니다. 
 
부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], 통계 컬렉션의 성능 향상을 위해 호환성 수준 130을 사용 하는 경우 통계를 만들 데이터 샘플링 병렬로 수행 됩니다. 테이블 크기는 특정 임계값을 초과 될 때마다 쿼리 최적화 프로그램에서 병렬 샘플 통계를 사용 합니다. 
   
 SAMPLE은 FULLSCAN 옵션과 함께 사용할 수 없습니다. SAMPLE과 FULLSCAN을 둘 다 지정하지 않으면 기본적으로 쿼리 최적화 프로그램에서 샘플링된 데이터를 사용하고 샘플 크기를 계산합니다.  
  
 0 PERCENT 또는 0 ROWS로 지정하지 않는 것이 좋습니다. 0 PERCENT 또는 0 ROWS로 지정하면 통계 데이터가 포함되지 않은 빈 통계 개체가 업데이트됩니다.  
  
 대부분의 작업에 대 한 전체 검색 필요 하지 않습니다. 및 기본 샘플링 것이 좋습니다.  
그러나 다양 한 데이터 배포에 영향을 받는 특정 작업 부하는 증가 된 샘플 크기 또는 전체 검색도 필요할 수 있습니다.  
자세한 내용은 참조는 [CSS SQL 에스컬레이션 Services 블로그](http://blogs.msdn.com/b/psssql/archive/2010/07/09/sampling-can-produce-less-accurate-statistics-if-the-data-is-not-evenly-distributed.aspx)합니다.  
  
 RESAMPLE  
 가장 최근의 샘플링 주기를 사용하여 각 통계를 업데이트합니다.  
  
 RESAMPLE을 사용하면 전체 테이블 검색이 수행될 수 있습니다. 예를 들어 인덱스에 대한 통계에서는 샘플링 주기에 전체 테이블 검색을 사용합니다. 샘플 옵션(SAMPLE, FULLSCAN, RESAMPLE)을 지정하지 않으면 기본적으로 쿼리 최적화 프로그램에서 데이터를 샘플링하여 샘플 크기를 계산합니다.  

PERSIST_SAMPLE_PERCENT = {ON | OFF}  
때 **ON**, 통계 샘플링 비율을 명시적으로 지정 하지 않으면 후속 업데이트에 대 한 집합 샘플링 백분율을 그대로 유지 됩니다. 때 **OFF**, 통계 샘플링 비율 샘플링 비율을 명시적으로 지정 하지 않은 이후의 업데이트에서 기본 샘플링을 다시 설정 될 됩니다. 기본값은 **OFF**합니다. 
 
 > [!NOTE]
 > AUTO_UPDATE_STATISTICS를 실행 하면 사용 가능한 경우 지속형된 샘플링 비율을 사용 하거나 그렇지 않은 경우 기본 샘플링 비율을 사용 합니다.
 > RESAMPLE 동작이이 옵션의 영향을 받지 않습니다.
 
 > [!TIP] 
 > [DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md) 및 [sys.dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) 선택한 통계에 대 한 지속형된 샘플 백분율 값을 표시 합니다.
 
 **에 적용 됩니다**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4)를 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (부터는 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU1).  
 
 ON PARTITIONS ({ \<partition_number > | \<범위 >} [, … n]) ] 리프 수준 통계를 다시 계산한 다음 전역 통계 구축 하기 위해 병합 ON PARTITIONS 절에 지정 된 파티션에 적용 되도록 합니다. 서로 다른 샘플링 주기로 작성된 파티션 통계는 병합할 수 없으므로 WITH RESAMPLE이 필요합니다.  
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 ALL | COLUMNS | INDEX  
 기존의 모든 통계, 하나 이상의 열에 대해 생성된 통계 또는 인덱스에 대해 생성된 통계를 업데이트합니다. 아무 옵션도 지정하지 않은 UPDATE STATISTICS 문은 테이블 또는 인덱싱된 뷰의 모든 통계를 업데이트합니다.  
  
 NORECOMPUTE  
 지정된 통계에 대해 자동 통계 업데이트 옵션인 AUTO_UPDATE_STATISTICS를 비활성화합니다. 이 옵션을 지정하지 않으면 쿼리 최적화 프로그램에서 이 통계 업데이트를 완료하고 이후 업데이트부터 비활성화합니다.  
  
 AUTO_UPDATE_STATISTICS 옵션 동작을 다시 설정, NORECOMPUTE 옵션 없이 UPDATE STATISTICS를 다시 실행 또는 실행 하려면 **sp_autostats**합니다.  
  
> [!WARNING]  
>  이 옵션을 사용하면 최적이 아닌 쿼리 계획이 생성될 수 있습니다. 이 옵션은 자격 있는 시스템 관리자가 꼭 필요한 경우에만 사용하는 것이 좋습니다.  
  
 AUTO_STATISTICS_UPDATE 옵션에 대 한 자세한 내용은 참조 하세요. [ALTER DATABASE SET 옵션 &#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 INCREMENTAL = {ON | OFF}  
 때 **ON**, 파티션 통계 별로 통계가 다시 만들어집니다. 때 **OFF**, 통계 트리가 삭제 되 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 통계를 다시 계산 합니다. 기본값은 **OFF**합니다.  
  
 파티션별 통계가 지원되지 않을 경우 오류가 생성됩니다. 다음 통계 유형에 대해서는 증분 통계가 지원되지 않습니다.  
  
-   기본 테이블을 기준으로 파티션 정렬되지 않은 인덱스를 사용하여 작성된 통계입니다.  
  
-   Always On 읽기 가능한 보조 데이터베이스에 대해 작성된 통계입니다.  
  
-   읽기 전용 데이터베이스에 대해 작성된 통계입니다.  
  
-   필터링된 인덱스에 대해 작성된 통계입니다.  
  
-   뷰에 대해 작성된 통계입니다.  
  
-   내부 테이블에 대해 작성된 통계입니다.  
  
-   공간 인덱스 또는 XML 인덱스를 사용하여 작성된 통계입니다.  
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 \<update_stats_stream_option >[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="remarks"></a>주의  
  
## <a name="when-to-use-update-statistics"></a>UPDATE STATISTICS를 사용하는 경우  
 UPDATE STATISTICS를 사용 하는 경우에 대 한 자세한 내용은 참조 [통계](../../relational-databases/statistics/statistics.md)합니다.  
  
## <a name="updating-all-statistics-with-spupdatestats"></a>sp_updatestats를 사용하여 모든 통계 업데이트  
 데이터베이스의 모든 사용자 정의 테이블 및 내부 테이블에 대한 통계를 업데이트하는 방법은 저장 프로시저 [sp_updatestats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)를 참조하세요. 예를 들어 다음 명령에서는 sp_updatestats를 호출하여 데이터베이스에 대한 모든 통계를 업데이트합니다.  
  
```sql  
EXEC sp_updatestats;  
```  
  
## <a name="determining-the-last-statistics-update"></a>마지막 통계 업데이트 확인  
 통계가 마지막으로 업데이트된 시점을 확인하려면 [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md) 함수를 사용합니다.  
  
## <a name="pdw--sql-data-warehouse"></a>PDW / SQL 데이터 웨어하우스  
 다음 구문을 PDW에서 지원 되지 않습니다 / SQL 데이터 웨어하우스  
  
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
  
## <a name="permissions"></a>Permissions  
 테이블이나 뷰에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-update-all-statistics-on-a-table"></a>1. 테이블에 대한 모든 통계 업데이트  
 모든 인덱스에 대 한 통계를 업데이트 하는 다음 예제는 `SalesOrderDetail` 테이블입니다.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-update-statistics-on-a-table"></a>5. 테이블에 대 한 통계를 업데이트 합니다.  
 다음 예에서는 업데이트 된 `CustomerStats1` 에 대 한 통계는 `Customer` 테이블입니다.  
  
```sql  
UPDATE STATISTICS Customer ( CustomerStats1 );  
```  
  
### <a name="f-update-statistics-by-using-a-full-scan"></a>6. 전체 검색을 사용 하 여 통계를 업데이트 합니다.  
 다음 예에서는 업데이트 된 `CustomerStats1` 에 있는 행의 모든 검색 기준으로 통계는 `Customer` 테이블입니다.  
  
```sql  
UPDATE STATISTICS Customer (CustomerStats1) WITH FULLSCAN;  
```  
  
### <a name="g-update-all-statistics-on-a-table"></a>7. 테이블에 대한 모든 통계 업데이트  
 모든 통계를 업데이트 하는 다음 예제는 `Customer` 테이블입니다.  
  
```sql  
UPDATE STATISTICS Customer;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [통계](../../relational-databases/statistics/statistics.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_updatestats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [STATS_DATE &#40; Transact SQL &#41;](../../t-sql/functions/stats-date-transact-sql.md)  
 [sys.dm_db_stats_properties&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) [sys.dm_db_stats_histogram&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 
  



