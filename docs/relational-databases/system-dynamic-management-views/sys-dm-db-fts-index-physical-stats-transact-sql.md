---
description: sys.dm_db_fts_index_physical_stats(Transact-SQL)
title: sys.dm_db_fts_index_physical_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3884a802e2eca87cb829bfa5e906155675080922
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97328478"
---
# <a name="sysdm_db_fts_index_physical_stats-transact-sql"></a>sys.dm_db_fts_index_physical_stats(Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  연결된 전체 텍스트 또는 의미 체계 인덱스가 있는 각 테이블의 전체 텍스트 또는 의미 체계 인덱스에 대해 행을 하나씩 반환합니다.  
  
||||  
|-|-|-|  
|**열 이름**|**Type**|**설명**|  
|**object_id**|int|인덱스를 포함하는 테이블의 개체 ID입니다.|  
|**fulltext_index_page_count**|**bigint**|추출의 논리적 크기(인덱스 페이지의 수)입니다.|  
|**keyphrase_index_page_count**|**bigint**|추출의 논리적 크기(인덱스 페이지의 수)입니다.|  
|**similarity_index_page_count**|**bigint**|추출의 논리적 크기(인덱스 페이지의 수)입니다.|  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 자세한 내용은 [의미 체계 검색 관리 및 모니터링](../../relational-databases/search/manage-and-monitor-semantic-search.md)을 참조 하세요.  
  
## <a name="metadata"></a>메타데이터  
 의미 체계 인덱싱의 상태에 대한 자세한 내용을 보려면 다음 동적 관리 뷰를 쿼리합니다.  
  
-   [sys.dm_fts_index_population&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="permissions"></a>사용 권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
SQL Database Basic, S0 및 S1 서비스 목적과 탄력적 풀의 데이터베이스에 대해서는 `Server admin` 또는 `Azure Active Directory admin` 계정이 필요 합니다. 다른 모든 SQL Database 서비스 목표에서 `VIEW DATABASE STATE` 사용 권한은 데이터베이스에서 필요 합니다.   

## <a name="examples"></a>예제  
 다음 예에서는 연결된 전체 텍스트 또는 의미 체계 인덱스가 있는 모든 테이블에서 각 전체 텍스트 또는 의미 체계 인덱스의 논리적 크기를 쿼리하는 방법을 보여 줍니다.  
  
```  
SELECT * FROM sys.dm_db_fts_index_physical_stats;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [의미 체계 검색 관리 및 모니터링](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
  
  
