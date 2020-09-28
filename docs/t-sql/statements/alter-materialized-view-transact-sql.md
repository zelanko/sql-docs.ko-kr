---
description: ALTER MATERIALIZED VIEW(Transact-SQL)
title: ALTER MATERIALIZED VIEW(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: jrasnick
ms.technology: data-warehouse
ms.topic: language-reference
f1_keywords:
- ALTER_VIEW_TSQL
- ALTER VIEW
dev_langs:
- TSQL
helpviewer_keywords:
- indexed views [SQL Server], modifying
- views [SQL Server], modifying
- modifying views
- ALTER VIEW statement
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 3dd2ed6aab24741144c8c96c1db29079b46b16c5
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2020
ms.locfileid: "91379638"
---
# <a name="alter-materialized-view-transact-sql"></a>ALTER MATERIALIZED VIEW(Transact-SQL)  

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

이전에 만든 구체화된 뷰를 수정합니다. ALTER VIEW는 종속된 저장 프로시저 또는 트리거에 영향을 주지 않으며 사용 권한을 변경하지 않습니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
ALTER MATERIALIZED VIEW [ schema_name . ] view_name
{
      REBUILD | DISABLE
}
[;]
```  
  
## <a name="arguments"></a>인수

 *schema_name*     
 뷰가 속한 스키마의 이름입니다.  
  
 *view_name*     
 변경할 구체화된 뷰입니다.  
  
*REBUILD*   
구체화된 뷰를 다시 시작합니다.

*DISABLE*   
메타데이터 및 사용 권한을 유지하면서 구체화된 뷰의 유지 관리를 일시 중단합니다.사용 안 함 상태의 구체화된 뷰에 대한 모든 쿼리는 기본 테이블을 확인합니다.
  
## <a name="permissions"></a>사용 권한

테이블이나 뷰에 대한 ALTER 권한이 필요합니다.
  
## <a name="examples"></a>예제

이 예제에서는 구체화된 뷰를 사용하지 않도록 설정하고 일시 중단 모드에 둡니다.
  
```sql
ALTER MATERIALIZED VIEW My_Indexed_View DISABLE;  
```  
  
이 예제에서는 구체화된 뷰를 다시 작성하여 다시 시작합니다.  
  
```sql
ALTER MATERIALIZED VIEW My_Indexed_View REBUILD;  
```  
  
## <a name="see-also"></a>참고 항목

[구체화된 뷰로 성능 조정](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[[!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[[!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]에서 지원되는 시스템 뷰](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[[!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]에서 지원되는 T-SQL 문](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
