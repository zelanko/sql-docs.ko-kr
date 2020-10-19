---
description: CREATE MATERIALIZED VIEW AS SELECT(Transact-SQL)
title: CREATE MATERIALIZED VIEW AS SELECT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: data-warehouse
ms.topic: language-reference
f1_keywords:
- CREATE VIEW
- VIEW_TSQL
- VIEW
- CREATE_VIEW_TSQL
- SCHEMABINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table creation [SQL Server], CREATE VIEW
- views [SQL Server], creating
- CREATE VIEW statement
- updatable partitioned views
- tables [SQL Server], virtual
- updatable views
- modifying partitioned views
- virtual tables [SQL Server]
- number of columns per view
- partitioned views [SQL Server], creating
- WITH ENCRYPTION clause
- WITH CHECK OPTION clause
- partitioned views [SQL Server], modifying
- partitioned views [SQL Server], replication
- distributed partitioned views [SQL Server]
- views [SQL Server], indexed views
- maximum number of columns per view
ms.assetid: aecc2f73-2ab5-4db9-b1e6-2f9e3c601fb9
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: cda76ce52f9b14c732cb4effb95c3ff523dd460b
ms.sourcegitcommit: 9122251ab8bbd46ea3c699e741d6842c995195fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2020
ms.locfileid: "91847343"
---
# <a name="create-materialized-view-as-select-transact-sql"></a>CREATE MATERIALIZED VIEW AS SELECT(Transact-SQL)  

[!INCLUDE [Azure Synapse Analytics](../../includes/applies-to-version/asa.md)]

이 문서에서는 솔루션 개발을 위한 [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]의 CREATE MATERIALIZED VIEW AS SELECT T-SQL 문에 대해 설명합니다. 코드 예제도 제공합니다.

구체화된 뷰는 뷰 정의 쿼리에서 반환되는 데이터를 유지하고 기본 테이블에서 데이터가 변경될 때 자동으로 업데이트됩니다.   간단한 유지 관리 작업을 제공하면서 복잡한 쿼리(일반적으로 조인 및 집계를 사용한 쿼리)의 성능을 향상시킵니다.   실행 계획 자동 일치 기능을 사용할 경우 최적화 프로그램에서 뷰의 대체를 고려할 때 쿼리에서 구체화된 뷰를 참조할 필요가 없습니다.  이 기능을 통해 데이터 엔지니어는 쿼리를 변경하지 않고도 쿼리 응답 시간을 개선하기 위한 메커니즘으로 구체화된 뷰를 구현할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
CREATE MATERIALIZED VIEW [ schema_name. ] materialized_view_name
    WITH (  
      <distribution_option>
    )
    AS <select_statement>
[;]

<distribution_option> ::=
    {  
        DISTRIBUTION = HASH ( distribution_column_name )  
      | DISTRIBUTION = ROUND_ROBIN  
    }

<select_statement> ::=
    SELECT select_criteria
```

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]
  
## <a name="arguments"></a>인수

*schema_name*     
 뷰가 속한 스키마의 이름입니다.  
  
*materialized_view_name*   
뷰의 이름입니다. 뷰 이름은 반드시 식별자에 적용되는 규칙을 준수해야 합니다. 뷰 소유자 이름을 지정하는 것은 선택 사항입니다.  

*배포 옵션*     
HASH 및 ROUND_ROBIN 배포만 지원됩니다.

*select_statement*   
구체화된 뷰 정의의 SELECT 목록은 다음의 두 가지 조건 중 하나 이상을 충족 해야 합니다.
- SELECT 목록이 집계 함수를 포함합니다.
- GROUP BY가 구체화된 뷰 정의에서 사용되고 GROUP BY의 모든 열이 SELECT 목록에 포함됩니다.  GROUP BY 절에는 최대 32개 열을 사용할 수 있습니다.

구체화된 뷰 정의의 SELECT 목록에는 집계 함수가 필요합니다.  지원되는 집계 함수에는 MAX, MIN, AVG, COUNT, COUNT_BIG, SUM, VAR, STDEV가 포함됩니다.

MIN/MAX 집계가 구체화된 뷰 정의의 SELECT 목록에 사용될 경우 다음과 같은 요구 사항이 적용됩니다.
 
- FOR_APPEND가 필요합니다.  예를 들면 다음과 같습니다.
  ```sql 
  CREATE MATERIALIZED VIEW mv_test2  
  WITH (distribution = hash(i_category_id), FOR_APPEND)  
  AS
  SELECT MAX(i.i_rec_start_date) as max_i_rec_start_date, MIN(i.i_rec_end_date) as min_i_rec_end_date, i.i_item_sk, i.i_item_id, i.i_category_id
  FROM syntheticworkload.item i  
  GROUP BY i.i_item_sk, i.i_item_id, i.i_category_id
  ```

- 참조되는 기본 테이블에서 UPDATE 또는 DELETE가 나올 경우 구체화된 뷰가 사용하지 않도록 설정됩니다.  INSERT에는 이 제한이 적용되지 않습니다.  구체화된 뷰를 다시 사용하도록 설정하려면 REBUILD를 사용하여 ALTER MATERIALIZED VIEW를 실행합니다.
  
## <a name="remarks"></a>설명

Azure Data Warehouse의 구체화된 뷰는 SQL Server의 인덱싱된 뷰와 비슷합니다.구체화된 뷰는 집계 함수를 지원한다는 점을 제외하고, 인덱싱된 뷰와 거의 같은 제한을 공유합니다([인덱싱된 뷰 만들기](/sql/relational-databases/views/create-indexed-views)에서 자세한 내용 참조).   

>[!Note]
>CREATE MATERIALIZED VIEW는 COUNT, DISTINCT, COUNT(DISTINCT 식) 또는 COUNT_BIG(DISTINCT 식)을 지원하지 않지만, Synapse SQL 최적화 프로그램이 사용자 쿼리의 집계를 기존의 구체화된 뷰와 일치하도록 자동으로 다시 작성할 수 있으므로 해당 함수를 포함하는 SELECT 쿼리가 성능 향상을 위해 구체화된 뷰를 활용할 수 있습니다.  자세한 내용은 이 문서의 예제 섹션을 참조하세요. 

APPROX_COUNT_DISTINCT는 CREATE MATERIALIZED VIEW AS SELECT에서 지원되지 않습니다.

구체화된 뷰는 CLUSTERED COLUMNSTORE INDEX만 지원합니다. 

구체화된 뷰는 다른 뷰를 참조할 수 없습니다.  

DDM 열이 구체화된 뷰의 일부가 아닌 경우에도 DDM(동적 데이터 마스킹)이 포함된 테이블에는 구체화된 뷰를 만들 수 없습니다.  테이블 열이 활성 구체화된 뷰 또는 사용할 수 없는 구체화된 뷰의 일부인 경우 이 열에는 DDM을 추가할 수 없습니다.  

행 수준 보안이 사용되는 테이블에는 구체화된 뷰를 만들 수 없습니다.

구체화된 뷰는 분할된 테이블에서 만들 수 있습니다.  구체화된 뷰 기본 테이블에서 파티션 분할/병합은 지원되고 파티션 전환은 지원되지 않습니다.  
 
ALTER TABLE SWITCH는 구체화된 뷰에서 참조되는 테이블에서 지원되지 않습니다. ALTER TABLE SWITCH를 사용하기 전에 구체화된 뷰를 사용하지 않도록 설정하거나 삭제합니다. 다음 시나리오에서 구체화된 뷰를 만들려면 새 열을 구체화된 뷰에 추가해야 합니다.

|시나리오|구체화된 뷰에 추가할 새 열|의견|  
|-----------------|---------------|-----------------|
|COUNT_BIG()이 구체화된 뷰 정의의 SELECT 목록에 없습니다.| COUNT_BIG (*) |구체화된 뷰를 만들면 자동으로 추가됩니다.  추가적인 조치가 필요하지 않습니다.|
|사용자가 구체화된 뷰 정의의 SELECT 목록에서 SUM(a)을 지정하며, ‘a’는 null 허용 식입니다. |COUNT_BIG (a) |사용자가 구체화된 뷰 정의에서 수동으로 식 ‘a’를 추가해야 합니다.|
|사용자가 구체화된 뷰 정의의 SELECT 목록에서 AVG(a)를 지정합니다. 여기서 ‘a’는 식입니다.|SUM(a), COUNT_BIG(a)|구체화된 뷰를 만들면 자동으로 추가됩니다.  추가적인 조치가 필요하지 않습니다.|
|사용자가 구체화된 뷰 정의의 SELECT 목록에서 STDEV(a)를 지정합니다. 여기서 ‘a’는 식입니다.|SUM(a), COUNT_BIG(a), SUM(square(a))|구체화된 뷰를 만들면 자동으로 추가됩니다.  추가적인 조치가 필요하지 않습니다. |
| | | |

만들어진 구체화된 뷰는 SQL Server Management Studio에서 [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)] 인스턴스의 views 폴더 아래에 표시됩니다.

사용자는 [SP_SPACEUSED](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql?view=azure-sqldw-latest) 및 [DBCC PDW_SHOWSPACEUSED](/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql?view=azure-sqldw-latest)를 실행하여 구체화된 뷰에서 사용되는 공간을 확인할 수 있습니다.  

구체화된 뷰는 DROP VIEW를 통해 삭제할 수 있습니다.  ALTER MATERIALIZED VIEW를 사용하여 구체화된 뷰를 사용하지 않도록 설정하거나 다시 작성할 수 있습니다.   

EXPLAIN 계획과 SQL Server Management Studio의 그래픽 예상 실행 계획은 쿼리 최적화 프로그램이 쿼리 실행을 위해 구체화된 뷰를 고려하는지 여부를 나타냅니다. 또한 SQL Server Management Studio의 그래픽 예상 실행 계획은 쿼리 최적화 프로그램이 쿼리 실행을 위해 구체화된 뷰를 고려하는지 여부를 나타냅니다.

SQL 문이 새 구체화된 뷰로 인해 개선될 수 있는지 확인하려면 `EXPLAIN` 명령과 `WITH_RECOMMENDATIONS`를 실행합니다.  자세한 내용은 [EXPLAIN (Transact-SQL)](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)을 참조하세요.

## <a name="permissions"></a>사용 권한

뷰를 만드는 스키마에 대한 1) REFERENCES 및 CREATE VIEW 권한 또는 2) CONTROL 권한이 필요합니다. 

## <a name="example"></a>예제
A. 이 예제에서는 쿼리가 CREATE MATERIALIZED VIEW에서 지원되지 않는 COUNT(DISTINCT 식) 등의 함수를 사용하는 경우에도 Synapse SQL 최적화 프로그램이 성능 향상을 위해 자동으로 구체화된 뷰를 사용하여 쿼리를 실행하는 방식을 보여 줍니다. 완료하는 데 몇 초 정도 걸렸던 쿼리가 사용자 쿼리를 변경하지 않고도 이제 1초 이내에 완료됩니다.   

``` sql 

-- Create a table with ~536 million rows
create table t(a int not null, b int not null, c int not null) with (distribution=hash(a), clustered columnstore index);

insert into t values(1,1,1);

declare @p int =1;
while (@P < 30)
    begin
    insert into t select a+1,b+2,c+3 from t;  
    select @p +=1;
end

-- A SELECT query with COUNT_BIG (DISTINCT expression) took multiple seconds to complete and it reads data directly from the base table a. 
select a, count_big(distinct b) from t group by a;

-- Create two materialized views, not using COUNT_BIG(DISTINCT expression).
create materialized view V1 with(distribution=hash(a)) as select a, b from dbo.t group by a, b;

-- Clear all cache.

DBCC DROPCLEANBUFFERS;
DBCC freeproccache;

-- Check the estimated execution plan in SQL Server Management Studio.  It shows the SELECT query is first step (GET operator) is to read data from the materialized view V1, not from base table a.
select a, count_big(distinct b) from t group by a;

-- Now execute this SELECT query.  This time it took sub-second to complete because Synapse SQL engine automatically matches the query with materialized view V1 and uses it for faster query execution.  There was no change in the user query.

DECLARE @timerstart datetime2, @timerend datetime2;
SET @timerstart = sysdatetime();

select a, count_big(distinct b) from t group by a;

SET @timerend = sysdatetime()
select DATEDIFF(ms,@timerstart,@timerend);

```

  
## <a name="see-also"></a>참고 항목

[구체화된 뷰로 성능 조정](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)      
[DROP VIEW](/sql/t-sql/statements/drop-view-transact-sql?view=azure-sqldw-latest)  
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[[!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Azure [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]에서 지원되는 시스템 뷰](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Azure [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]에서 지원되는 T-SQL 문](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
