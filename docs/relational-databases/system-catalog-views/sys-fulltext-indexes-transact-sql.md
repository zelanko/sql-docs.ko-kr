---
description: sys.fulltext_indexes(Transact-SQL)
title: sys.fulltext_indexes (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_indexes
- fulltext_indexes_TSQL
- sys.fulltext_indexes_TSQL
- sys.fulltext_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_indexes catalog view
- full-text indexes [SQL Server], properties
ms.assetid: 7fc10fdc-370f-4927-bba0-b76108a7508e
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7c9b04a81d537c0b82a7a1bccb76b429d896ba13
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482904"
---
# <a name="sysfulltext_indexes-transact-sql"></a>sys.fulltext_indexes(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  테이블 형식 개체의 각 전체 텍스트 인덱스당 한 개의 행을 포함합니다.  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|이 전체 텍스트 인덱스가 속한 개체의 ID입니다.|  
|**unique_index_id**|**int**|전체 텍스트 인덱스를 행에 연결하는 데 사용되는 고유하고 전체 텍스트가 아닌 해당 인덱스의 ID입니다.|  
|**fulltext_catalog_id**|**int**|전체 텍스트 인덱스가 있는 전체 텍스트 카탈로그의 ID입니다.|  
|**is_enabled**|**bit**|1 = 전체 텍스트 인덱스가 현재 활성화되었습니다.|  
|**change_tracking_state**|**char(1)**|변경 내용 추적의 상태입니다.<br /><br /> M = 수동<br /><br /> A = 자동<br /><br /> O = 추적 안 함|  
|**change_tracking_state_desc**|**nvarchar(60)**|변경 내용 추적 상태에 대한 설명입니다.<br /><br /> MANUAL<br /><br /> AUTO<br /><br /> OFF|  
|**has_crawl_completed**|**bit**|전체 텍스트 인덱스가 완료한 마지막 탐색(채우기)입니다.|  
|**crawl_type**|**char(1)**|현재 또는 마지막 탐색의 유형입니다.<br /><br /> F = 전체 탐색<br /><br /> I = 타임스탬프 기반 증분 탐색<br /><br /> U = 알림 기반 업데이트 탐색<br /><br /> P = 전체 탐색이 일시 중지됨|  
|**crawl_type_desc**|**nvarchar(60)**|현재 또는 마지막 탐색 유형에 대한 설명입니다.<br /><br /> FULL_CRAWL<br /><br /> INCREMENTAL_CRAWL<br /><br /> UPDATE_CRAWL<br /><br /> PAUSED_FULL_CRAWL|  
|**crawl_start_date**|**datetime**|현재 또는 마지막 탐색의 시작 날짜와 시간입니다.<br /><br /> NULL = 없음|  
|**crawl_end_date**|**datetime**|현재 또는 마지막 탐색의 종료 날짜와 시간입니다.<br /><br /> NULL = 없음|  
|**incremental_timestamp**|**binary (8)**|다음 증분 탐색에 사용할 타임스탬프 값입니다.<br /><br /> NULL = 없음|  
|**stoplist_id**|**int**|이 전체 텍스트 인덱스와 연결 된 [중지](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md) 목록의 ID입니다.|  
|**data_space_id**|**int**|이 전체 텍스트 인덱스가 있는 파일 그룹입니다.|  
|**property_list_id**|**int**|이 전체 텍스트 인덱스와 연결된 검색 속성 목록의 ID입니다. NULL은 전체 텍스트 인덱스와 연결된 검색 속성 목록이 없음을 나타냅니다. 이 검색 속성 목록에 대 한 자세한 내용을 보려면 [sys.registered_search_property_lists &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md) 카탈로그 뷰를 사용 하십시오.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="examples"></a>예  
 다음 예에서는 `HumanResources.JobCandidate` 예제 데이터베이스의 `AdventureWorks2012` 테이블에서 전체 텍스트 인덱스를 사용합니다. 이 예에서는 전체 텍스트 인덱스에서 사용하는 중지 목록 ID, 테이블의 개체 ID 및 검색 속성 목록 ID를 반환합니다.  
  
> [!NOTE]  
>  이 전체 텍스트 인덱스를 만드는 코드 예제는 전체 텍스트 [인덱스 만들기 &#40;transact-sql&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)의 "예" 섹션을 참조 하세요.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT object_id, property_list_id, stoplist_id FROM sys.fulltext_indexes  
    where object_id = object_id('HumanResources.JobCandidate');   
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sys.fulltext_index_fragments &#40;](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)   
 [sys.fulltext_index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)   
 [Transact-sql&#41;sys.fulltext_index_catalog_usages &#40;](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)   
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [전체 텍스트 인덱스 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [DROP FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
  
