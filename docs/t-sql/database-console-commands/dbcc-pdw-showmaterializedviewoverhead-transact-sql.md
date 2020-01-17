---
title: DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD(Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 669c6274301c09f260badfb354c8add67ae86791
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401631"
---
# <a name="dbcc-pdw_showmaterializedviewoverhead-transact-sql"></a>DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD(Transact-SQL)  

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서 구체화된 뷰용으로 저장된 기본 테이블에 증분 변경 횟수를 표시합니다. 오버헤드 비율은 TOTAL_ROWS / MAX (1, BASE_VIEW_ROWS)로 계산합니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "|::ref1::|") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문

```
DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD ( " [ schema_name .] materialized_view_name  " )
[;]
```
  
## <a name="arguments"></a>인수

 *schema_name*     
 뷰가 속한 스키마의 이름입니다.

*materialized_view_name*   
구체화된 뷰의 이름입니다.

## <a name="remarks"></a>설명

구체화된 뷰를 기본 테이블의 데이터 변경 내용으로 계속 새로 고치기 위해 데이터 웨어하우스 엔진은 영향을 받는 각 뷰에 추적 행을 추가하여 변경 내용을 반영합니다. 구체화된 뷰에서 선택하면 뷰의 클러스터형 columnstore 인덱스 검색과 증분 변경 내용 적용이 포함됩니다.  사용자가 구체화된 뷰를 다시 빌드할 때까지 추적 행(TOTAL_ROWS-BASE_VIEW_ROWS)은 제거되지 않습니다.  

overhead_ratio는 TOTAL_ROWS/MAX(1, BASE_VIEW_ROWS)로 계산됩니다.  비율이 높으면 SELECT 성능이 저하됩니다.  사용자는 구체화된 뷰를 다시 빌드하여 오버헤드 비율을 줄일 수 있습니다.

## <a name="permissions"></a>사용 권한  
  
VIEW DATABASE STATE 권한이 필요합니다.  

## <a name="examples"></a>예  

### <a name="a-this-example-returns-the-overhead-ratio-of-a-materialized-view"></a>A. 이 예제에서는 구체화된 뷰의 오버헤드 비율을 반환합니다.

```sql
DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD ( "dbo.MyIndexedView" )
```

출력:

|OBJECT_ID|BASE_VIEW_ROWS|TOTAL_ROWS|OVERHEAD_RATIO|
|--------|--------|--------|--------|  
|1234|1|3 |3.0 |

</br>

### <a name="b-this-example-shows-how-the-materialized-view-overhead-increases-as-data-changes-in-base-tables"></a>B. 이 예제에서는 기본 테이블의 데이터가 변경됨에 따라 구체화된 뷰 오버헤드가 증가하는 방식을 보여 줍니다.

테이블 만들기
```sql
CREATE TABLE t1 (c1 int NOT NULL, c2 int not null, c3 int not null)
```
T1에 행 5개 삽입
```sql
INSERT INTO t1 VALUES (1, 1, 1)
INSERT INTO t1 VALUES (2, 2, 2) 
INSERT INTO t1 VALUES (3, 3, 3) 
INSERT INTO t1 VALUES (4, 4, 4) 
INSERT INTO t1 VALUES (5, 5, 5) 
```
구체화된 뷰 MV1 만들기
```sql
CREATE materialized view MV1 
WITH (DISTRIBUTION = HASH(c1))  
AS
SELECT c1, count(*) total_number 
FROM dbo.t1 where c1 < 3
GROUP BY c1  
```
구체화된 뷰에서 선택하면 행 2개가 반환됩니다.

|c1|total_number|
|--------|--------| 
|1|1| 
|2|1|

기본 테이블의 데이터를 변경하기 전에 구체화된 뷰 오버헤드를 확인합니다.
```sql
DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD ("dbo.mv1")
```
출력:

|OBJECT_ID|BASE_VIEW_ROWS|TOTAL_ROWS|OVERHEAD_RATIO|
|--------|--------|--------|--------|  
|587149137|2|2 |1.00000000000000000 |

기본 테이블을 업데이트합니다.  이 쿼리는 동일한 행의 동일한 열을 동일한 값으로 100번 업데이트합니다.  구체화된 뷰 내용은 변경되지 않습니다.
```sql
DECLARE @p int
SELECT @p = 1
WHILE (@p < 101)
BEGIN
UPDATE t1 SET c1 = 1 WHERE c1 = 1
SELECT @p = @p+1
END  
```

구체화된 뷰에서 선택하면 이전과 동일한 결과가 반환됩니다.  

|c1|total_number|
|--------|--------| 
|1|1| 
|2|1|

다음은 DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD(“dbo.mv1”)의 출력입니다.  행 100개가 구체화된 뷰(total_row-base_view_rows)에 추가되었으며 해당 overhead_ratio가 증가했습니다. 

|OBJECT_ID|BASE_VIEW_ROWS|TOTAL_ROWS|OVERHEAD_RATIO|
|--------|--------|--------|--------|  
|587149137|2|102 |51.00000000000000000 |

구체화된 뷰를 다시 빌드한 후에는 증분 데이터 변경 내용에 대한 모든 추적 행이 제거되었으며 뷰 오버헤드 비율이 감소했습니다.  

```sql
ALTER MATERIALIZED VIEW dbo.MV1 REBUILD
go
DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD ("dbo.mv1")
```
출력

|OBJECT_ID|BASE_VIEW_ROWS|TOTAL_ROWS|OVERHEAD_RATIO|
|--------|--------|--------|--------|  
|587149137|2|2 |1.00000000000000000 |

## <a name="see-also"></a>참고 항목

[구체화된 뷰로 성능 조정](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Azure SQL Data Warehouse에서 지원되는 시스템 뷰](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Azure SQL Data Warehouse에서 지원되는 T-SQL 문](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
