---
title: sys. stats_columns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 12/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- stats_columns_TSQL
- stats_columns
- sys.stats_columns
- sys.stats_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.stats_columns catalog view
ms.assetid: 93414d07-97e9-4501-8577-f35b8d68fbe9
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6abf636a371047f344861f09affaa1dd9f7d82de
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68108970"
---
# <a name="sysstats_columns-transact-sql"></a>sys.stats_columns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  에는 각 열에 대 한 행이 포함 되어 **있습니다.**  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|이 열이 속한 개체의 ID입니다.|  
|**stats_id**|**int**|이 열이 속한 통계의 ID입니다.<br /><br />통계가 인덱스에 해당 하는 경우 *stats_id* 값은 [sys. 인덱스](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 카탈로그 뷰의 *index_id* 값과 동일 합니다.|  
|**stats_column_id**|**int**|stats 열 집합 내의 1부터 시작하는 서수입니다.|  
|**column_id**|**int**|**Sys. columns**열의 ID입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리에 대한 질문과 대답](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
 [통계](../../relational-databases/statistics/statistics.md)    
 [dm_db_stats_properties &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [dm_db_stats_histogram &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)   
 [sys.stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)  
  
  
