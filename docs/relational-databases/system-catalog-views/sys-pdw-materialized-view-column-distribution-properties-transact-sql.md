---
title: sys. pdw_materialized_view_column_distribution_properties (Transact-sql)
ms.custom: seo-dt-2019
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 934b1ed84aa7391ad8cf47e463dd38b37408ec00
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401658"
---
# <a name="syspdw_materialized_view_column_distribution_properties-transact-sql"></a>sys. pdw_materialized_view_column_distribution_properties (Transact-sql) 

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

구체화 된 뷰에서 열에 대 한 분포 정보를 표시 합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|object_id|**int**|열이 속한 개체의 ID입니다. |  
|column_id|**int**|열의 ID입니다.|  
|distribution_ordinal|**tinyint**|0 = 배포 열이 아닙니다.</br> 1 = SQL Data Warehouse이 열을 사용 하 여 구체화 된 뷰를 배포 합니다.|
 
## <a name="permissions"></a>권한 

VIEW DATABASE STATE 권한이 필요합니다.

## <a name="see-also"></a>참고 항목

[구체화 된 뷰로 성능 조정](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[구체화 된 뷰를 CREATE &#40;Transact-sql&#41;를 선택 합니다.](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[ALTER 구체화 된 뷰 &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[Transact-sql&#41;&#40;설명](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[pdw_materialized_view_distribution_properties &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[pdw_materialized_view_mappings &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-sql&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Azure SQL Data Warehouse에서 지원 되는 시스템 뷰](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Azure SQL Data Warehouse에서 지원되는 T-SQL 문](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
