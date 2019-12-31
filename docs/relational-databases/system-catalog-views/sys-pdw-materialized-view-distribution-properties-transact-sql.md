---
title: sys. pdw_materialized_view_distribution_properties (Transact-sql)
ms.custom: seo-dt-2019
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
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 5dca3564e8e2ccc83f0968d42c636112880f6e56
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401679"
---
# <a name="syspdw_materialized_view_distribution_properties-transact-sql-preview"></a>pdw_materialized_view_distribution_properties (Transact-sql) (미리 보기)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

분포 정보 구체화 뷰를 표시 합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------| 
|object_id|**int**|속성이 지정 된 구체화 된 뷰의 ID입니다.| 
|distribution_policy |**tinyint**|2 = 해시</br>4 = ROUND_ROBIN|  
|distribution_policy_desc |**nvarchar (60)**|해시, ROUND_ROBIN|  
 
## <a name="permissions"></a>권한

VIEW DATABASE STATE 권한이 필요합니다.
 
## <a name="see-also"></a>참고 항목

[구체화 된 뷰를 CREATE &#40;Transact-sql&#41;를 선택 합니다.](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[ALTER 구체화 된 뷰 &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[Transact-sql&#41;&#40;설명](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[pdw_materialized_view_mappings &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-sql&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Azure SQL Data Warehouse에서 지원 되는 시스템 뷰](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Azure SQL Data Warehouse에서 지원되는 T-SQL 문](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
