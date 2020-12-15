---
description: sys.stats(Transact-SQL)
title: sys. stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 12/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.stats
- stats_TSQL
- sys.stats_TSQL
- stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.stats catalog view
ms.assetid: 42605c80-126f-460a-befb-a0b7482fae6a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a7fab86d3cb05a7b2ce30b6be589c3e7ac1290eb
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97429647"
---
# <a name="sysstats-transact-sql"></a>sys.stats(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스의 테이블, 인덱스 및 인덱싱된 뷰에 대한 각 통계 개체의 행을 포함합니다. 모든 인덱스에는 동일한 이름 및 ID (**index_id** stats_id)를 사용 하는 해당 통계 행이  =  있지만 모든 통계 행에 해당 하는 인덱스가 없습니다.  
  
 카탈로그 뷰 [sys.stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md) 는 데이터베이스의 각 열에 대 한 통계 정보를 제공 합니다. 통계에 대한 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|이 통계가 속한 개체의 ID입니다.|  
|**name**|**sysname**|통계의 이름입니다. 개체 내에서 고유합니다.|  
|**stats_id**|**int**|통계의 ID입니다. 개체 내에서 고유합니다.<br /><br />통계가 인덱스에 해당 하는 경우 *stats_id* 값은 [sys. 인덱스](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 카탈로그 뷰의 *index_id* 값과 동일 합니다.|  
|**auto_created**|**bit**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 자동으로 생성된 통계인지 여부를 나타냅니다.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 자동으로 생성된 통계가 아닙니다.<br /><br /> 1 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 자동으로 생성된 통계입니다.|  
|**user_created**|**bit**|사용자가 만든 통계인지 여부를 나타냅니다.<br /><br /> 0 = 사용자가 만든 통계가 아닙니다.<br /><br /> 1 = 사용자가 만든 통계입니다.|  
|**no_recompute**|**bit**|**NORECOMPUTE** 옵션을 사용 하 여 통계가 생성 되었는지 여부를 나타냅니다.<br /><br /> 0 = **NORECOMPUTE** 옵션을 사용 하 여 통계가 생성 되지 않았습니다.<br /><br /> 1 = **NORECOMPUTE** 옵션을 사용 하 여 통계를 만들었습니다.|  
|**has_filter**|**bit**|0 = 통계에 필터가 없고 모든 행에서 통계가 계산됩니다.<br /><br /> 1 = 통계에 필터가 있고 필터 정의를 충족하는 행에서만 통계가 계산됩니다.|  
|**filter_definition**|**nvarchar(max)**|필터링된 통계에 포함된 행 하위 집합에 대한 식입니다.<br /><br /> NULL = 필터링되지 않은 통계입니다.|  
|**is_temporary**|**bit**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 통계가 임시 통계인지 여부를 나타냅니다. 임시 통계는 읽기 전용 액세스가 가능하도록 설정된 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 보조 데이터베이스를 지원합니다.<br /><br /> 0 = 통계가 임시 통계가 아닙니다.<br /><br /> 1 = 통계가 임시 통계입니다.|  
|**is_incremental**|**bit**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상<br /><br /> 통계를 증분 통계로 만들지 여부를 나타냅니다.<br /><br /> 0 = 통계가 증분되지 않습니다.<br /><br /> 1 = 통계가 증분됩니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 `HumanResources.Employee` 테이블에 대한 모든 통계 및 통계 열을 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT s.name AS statistics_name  
      ,c.name AS column_name  
      ,sc.stats_column_id  
FROM sys.stats AS s  
INNER JOIN sys.stats_columns AS sc   
    ON s.object_id = sc.object_id AND s.stats_id = sc.stats_id  
INNER JOIN sys.columns AS c   
    ON sc.object_id = c.object_id AND c.column_id = sc.column_id  
WHERE s.object_id = OBJECT_ID('HumanResources.Employee');  
```  
  
## <a name="see-also"></a>참고 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [통계](../../relational-databases/statistics/statistics.md)    
 [sys.dm_db_stats_properties&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [Transact-sql&#41;sys.dm_db_stats_histogram &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)   
 [sys.stats_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)
 

 
