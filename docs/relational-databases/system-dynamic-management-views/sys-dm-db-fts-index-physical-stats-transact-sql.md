---
title: sys.dm_db_fts_index_physical_stats (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_fts_index_physical_stats_TSQL
- dm_db_fts_index_physical_stats
- dm_db_fts_index_physical_stats_TSQL
- sys.dm_db_fts_index_physical_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_fts_index_physical_stats dynamic management view
ms.assetid: 997c3278-3630-47f6-ada3-190b6c16ce0e
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 952f07e7112b316e9109e0761deecf99f694306a
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34464139"
---
# <a name="sysdmdbftsindexphysicalstats-transact-sql"></a>sys.dm_db_fts_index_physical_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  연결된 전체 텍스트 또는 의미 체계 인덱스가 있는 각 테이블의 전체 텍스트 또는 의미 체계 인덱스에 대해 행을 하나씩 반환합니다.  
  
||||  
|-|-|-|  
|**열 이름**|**형식**|**설명**|  
|**object_id**|int|인덱스를 포함하는 테이블의 개체 ID입니다.|  
|**fulltext_index_page_count**|**bigint**|추출의 논리적 크기(인덱스 페이지의 수)입니다.|  
|**keyphrase_index_page_count**|**bigint**|추출의 논리적 크기(인덱스 페이지의 수)입니다.|  
|**similarity_index_page_count**|**bigint**|추출의 논리적 크기(인덱스 페이지의 수)입니다.|  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 자세한 내용은 참조 [검색 관리 및 모니터링 의미 체계](../../relational-databases/search/manage-and-monitor-semantic-search.md)합니다.  
  
## <a name="metadata"></a>메타데이터  
 의미 체계 인덱싱의 상태에 대한 자세한 내용을 보려면 다음 동적 관리 뷰를 쿼리합니다.  
  
-   [sys.dm_fts_index_population&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="permissions"></a>Permissions

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   

## <a name="examples"></a>예  
 다음 예에서는 연결된 전체 텍스트 또는 의미 체계 인덱스가 있는 모든 테이블에서 각 전체 텍스트 또는 의미 체계 인덱스의 논리적 크기를 쿼리하는 방법을 보여 줍니다.  
  
```  
SELECT * FROM sys.dm_db_fts_index_physical_stats;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [의미 체계 검색 관리 및 모니터링](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
  
  
