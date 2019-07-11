---
title: DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: XiaoyuL-Preview
ms.author: xiaoyul
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: e5dc503a06aed58b7e1cb2ae97377d9032355982
ms.sourcegitcommit: e4b241fd92689c2aa6e1f5e625874bd0b807dd01
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2019
ms.locfileid: "67566555"
---
# <a name="dbcc-pdwshowmaterializedviewoverhead-transact-sql-preview"></a>DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD(Transact-SQL)(미리 보기)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서 구체화된 뷰용으로 저장된 기본 테이블에 증분 변경 횟수를 표시합니다. 오버헤드 비율은 TOTAL_ROWS / MAX (1, BASE_VIEW_ROWS)로 계산합니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
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

## <a name="remarks"></a>Remarks

구체화된 뷰의 정의에 있는 기본 테이블을 수정하면 기본 테이블에서 구체화된 뷰의 모든 증분 변경 내용은 유지됩니다.  구체화된 뷰에서 선택하면 클러스터형 columnstore 구조에서 구체화된 뷰가 검색되고 이러한 증분 변경 내용이 적용됩니다.   유지 관리되는 증분 변경 내용 수가 많으면 선택 성능이 저하됩니다.  사용자는 구체화된 뷰를 다시 빌드하여 클러스터형 columnstore 구조를 다시 만들고 모든 증분 변경 내용을 기본 테이블에 통합할 수 있습니다.
  
## <a name="permissions"></a>사용 권한  
  
VIEW DATABASE STATE 권한이 필요합니다.  

## <a name="example"></a>예제  

이 예제에서는 구체화된 뷰에 사용되는 델타 공간을 반환합니다.

```sql
DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD ( "dbo.MyIndexedView" )
```

출력:

|OBJECT_ID|BASE_VIEW_ROWS|TOTAL_ROWS|OVERHEAD_RATIO|
|--------|--------|--------|--------|  
|1234|1|3 |3.0 |

</br>

|OBJECT_ID |BASE_VIEW_ROWS|TOTAL_ROWS|OVERHEAD_RATIO|
|--------|--------|--------|--------|
|4567|0|0|0.0|

</br>

|OBJECT_ID|BASE_VIEW_ROWS|TOTAL_ROWS|OVERHEAD_RATIO|
|--------|--------|--------|--------|
|789|0|2|2.0|

## <a name="see-also"></a>관련 항목:

[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Azure SQL Data Warehouse에서 지원되는 시스템 뷰](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Azure SQL Data Warehouse에서 지원되는 T-SQL 문](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)