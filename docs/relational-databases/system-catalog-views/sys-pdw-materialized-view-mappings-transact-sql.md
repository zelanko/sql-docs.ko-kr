---
title: sys.pdw_materialized_view_mappings (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: XiaoyuL-Preview
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: f4e286a335ca6668c81e6b959bd61605c0ea398a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059391"
---
# <a name="syspdwmaterializedviewmappings-transact-sql-preview"></a>sys.pdw_materialized_view_mappings (TRANSACT-SQL) (미리 보기)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Object_id에서 내부 개체 이름에 구체화 된 뷰를 연결합니다.

열 physical_name 및 object_id이 카탈로그 뷰에 대 한 키를 형성합니다.
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|physical_name |**nvarchar(36)**|구체화 된 뷰에 대 한 물리적 이름입니다.|  
|object_id  |**int**|구체화 된 뷰에 대 한 개체 ID입니다. 참조 [sys.objects (Transact SQL)](/sql/relational-databases/system-catalog-views/sys-objects-transact-sql?view=azure-sqldw-latest)합니다.| 

## <a name="permissions"></a>사용 권한

VIEW DATABASE STATE 권한이 필요합니다.
  
## <a name="see-also"></a>참조

[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Azure SQL Data Warehouse에서 지원되는 시스템 뷰](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Azure SQL Data Warehouse에서 지원되는 T-SQL 문](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements) 