---
description: sys.pdw_materialized_view_mappings (Transact-sql)
title: sys.pdw_materialized_view_mappings (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest
ms.openlocfilehash: 5d09d97fe51acec8466bcff8f64c3edfbc9316e2
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97642398"
---
# <a name="syspdw_materialized_view_mappings-transact-sql"></a>sys.pdw_materialized_view_mappings (Transact-sql)  

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Object_id 하 여 구체화 된 뷰를 내부 개체 이름과 연결 합니다.

열 physical_name 및 object_id이 카탈로그 뷰에 대 한 키를 구성 합니다.
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|physical_name |**nvarchar (36)**|구체화 된 뷰의 물리적 이름입니다.|  
|object_id  |**int**|구체화 된 뷰의 개체 ID입니다. [Sys. objects (transact-sql)](./sys-objects-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)를 참조 하세요.| 

## <a name="permissions"></a>사용 권한

VIEW DATABASE STATE 권한이 필요합니다.
  
## <a name="see-also"></a>참고 항목

[구체화된 뷰로 성능 조정](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-materialized-view-as-select-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-materialized-view-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[EXPLAIN &#40;Transact-SQL&#41;](../../t-sql/queries/explain-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](./sys-pdw-materialized-view-column-distribution-properties-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](./sys-pdw-materialized-view-distribution-properties-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[Azure Synapse Analytics 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Azure Synapse Analytics에서 지원되는 시스템 뷰](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Azure Synapse Analytics에서 지원되는 T-SQL 문](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)