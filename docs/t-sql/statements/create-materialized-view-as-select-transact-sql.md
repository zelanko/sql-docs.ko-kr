---
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
ms.openlocfilehash: 73fcf068c55b28448d87245b380281b461ef36b0
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81633613"
---
# <a name="create-materialized-view-as-select-transact-sql"></a>CREATE MATERIALIZED VIEW AS SELECT(Transact-SQL)  

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

이 문서에서는 솔루션 개발을 위한 Azure SQL Data Warehouse의 CREATE MATERIALIZED VIEW AS SELECT T-SQL 문에 대해 설명합니다. 코드 예제도 제공합니다.

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
 
- FOR_APPEND가 필요합니다.  다음은 그 예입니다.
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

Azure Data Warehouse의 구체화된 뷰는 SQL Server의 인덱싱된 뷰와 비슷합니다.  구체화된 뷰는 집계 함수를 지원한다는 점을 제외하고, 인덱싱된 뷰와 거의 같은 제한을 공유합니다([인덱싱된 뷰 만들기](/sql/relational-databases/views/create-indexed-views)에서 자세한 내용 참조).   

구체화된 뷰는 CLUSTERED COLUMNSTORE INDEX만 지원합니다. 

구체화된 뷰는 다른 뷰를 참조할 수 없습니다.  

DDM 열이 구체화된 뷰의 일부가 아닌 경우에도 DDM(동적 데이터 마스킹)이 포함된 테이블에는 구체화된 뷰를 만들 수 없습니다.  테이블 열이 활성 구체화된 뷰 또는 사용할 수 없는 구체화된 뷰의 일부인 경우 이 열에는 DDM을 추가할 수 없습니다.  

행 수준 보안이 사용되는 테이블에는 구체화된 뷰를 만들 수 없습니다.

구체화된 뷰는 분할된 테이블에서 만들 수 있습니다.  구체화된 뷰 기본 테이블에서 파티션 분할/병합은 지원되고 파티션 전환은 지원되지 않습니다.  
 
ALTER TABLE SWITCH는 구체화된 뷰에서 참조되는 테이블에서 지원되지 않습니다. ALTER TABLE SWITCH를 사용하기 전에 구체화된 뷰를 사용하지 않도록 설정하거나 삭제합니다. 다음 시나리오에서 구체화된 뷰를 만들려면 새 열을 구체화된 뷰에 추가해야 합니다.

|시나리오|구체화된 뷰에 추가할 새 열|주석|  
|-----------------|---------------|-----------------|
|COUNT_BIG()이 구체화된 뷰 정의의 SELECT 목록에 없습니다.| COUNT_BIG (*) |구체화된 뷰를 만들면 자동으로 추가됩니다.  추가적인 조치가 필요하지 않습니다.|
|사용자가 구체화된 뷰 정의의 SELECT 목록에서 SUM(a)을 지정하며, ‘a’는 null 허용 식입니다. |COUNT_BIG (a) |사용자가 구체화된 뷰 정의에서 수동으로 식 ‘a’를 추가해야 합니다.|
|사용자가 구체화된 뷰 정의의 SELECT 목록에서 AVG(a)를 지정합니다. 여기서 ‘a’는 식입니다.|SUM(a), COUNT_BIG(a)|구체화된 뷰를 만들면 자동으로 추가됩니다.  추가적인 조치가 필요하지 않습니다.|
|사용자가 구체화된 뷰 정의의 SELECT 목록에서 STDEV(a)를 지정합니다. 여기서 ‘a’는 식입니다.|SUM(a), COUNT_BIG(a), SUM(square(a))|구체화된 뷰를 만들면 자동으로 추가됩니다.  추가적인 조치가 필요하지 않습니다. |
| | | |

만들고 나면, 구체화된 뷰는 Azure SQL Data Warehouse 인스턴스의 뷰 폴더 아래에 있는 SQL Server Management Studio 내에 표시됩니다.

사용자는 [SP_SPACEUSED](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql?view=azure-sqldw-latest) 및 [DBCC PDW_SHOWSPACEUSED](/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql?view=azure-sqldw-latest)를 실행하여 구체화된 뷰에서 사용되는 공간을 확인할 수 있습니다.  

구체화된 뷰는 DROP VIEW를 통해 삭제할 수 있습니다.  ALTER MATERIALIZED VIEW를 사용하여 구체화된 뷰를 사용하지 않도록 설정하거나 다시 작성할 수 있습니다.   

EXPLAIN 계획과 SQL Server Management Studio의 그래픽 예상 실행 계획은 쿼리 최적화 프로그램이 쿼리 실행을 위해 구체화된 뷰를 고려하는지 여부를 나타냅니다. 또한 SQL Server Management Studio의 그래픽 예상 실행 계획은 쿼리 최적화 프로그램이 쿼리 실행을 위해 구체화된 뷰를 고려하는지 여부를 나타냅니다.

SQL 문이 새 구체화된 뷰로 인해 개선될 수 있는지 확인하려면 `EXPLAIN` 명령과 `WITH_RECOMMENDATIONS`를 실행합니다.  자세한 내용은 [EXPLAIN (Transact-SQL)](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)을 참조하세요.

## <a name="permissions"></a>사용 권한

데이터베이스에는 CREATE VIEW 권한이 필요하고 뷰를 만들 구성표에는 ALTER 권한이 필요합니다. 
  
## <a name="see-also"></a>참고 항목

[구체화된 뷰로 성능 조정](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)      
[DROP VIEW](/sql/t-sql/statements/drop-view-transact-sql?view=azure-sqldw-latest)  
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Azure SQL Data Warehouse에서 지원되는 시스템 뷰](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Azure SQL Data Warehouse에서 지원되는 T-SQL 문](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
