---
title: sys. dm_fts_index_keywords_position_by_document (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_keywords_position_by_document_TSQL
- dm_fts_index_keywords_position_by_document_TSQL
- dm_fts_index_keywords_position_by_document
- sys.dm_fts_index_keywords_position_by_document
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_index_keywords_position_by_document dynamic management view
ms.assetid: 0d70184f-baa2-411b-a32d-a4c5af890edd
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 04cedd0df5552ee19f7fc98ecdd94ff2d9dc88fb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734558"
---
# <a name="sysdm_fts_index_keywords_position_by_document-transact-sql"></a>sys. dm_fts_index_keywords_position_by_document (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  인덱싱된 문서에서 키워드 위치 정보를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('database_name'),   
OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>인수  
 db_id ('*database_name*')  
 [DB_ID ()](../../t-sql/functions/db-id-transact-sql.md) 함수에 대 한 호출입니다. 이 함수는 데이터베이스 이름을 허용 하 고 데이터베이스 ID를 반환 합니다 .이 ID를 사용 하 여 지정 된 데이터베이스를 찾을 dm_fts_index_keywords_position_by_document.  
  
 object_id ('*table_name*')  
 [OBJECT_ID ()](../../t-sql/functions/object-id-transact-sql.md) 함수에 대 한 호출입니다. 이 함수는 테이블 이름을 받아서 검사할 전체 텍스트 인덱스가 들어 있는 테이블의 테이블 ID를 반환합니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열|데이터 형식|Description|  
|------------|---------------|-----------------|  
|키워드(keyword)|**varbinary(128)**|키워드를 나타내는 이진 문자열입니다.|  
|display_term|**nvarchar(4000)**|사람이 인식할 수 있는 키워드 형식입니다. 이 형식은 전체 텍스트 인덱스에 저장되는 내부 형식에서 파생됩니다.|  
|column_id|**int**|현재 키워드가 전체 텍스트 인덱싱된 열의 ID입니다.|  
|document_id|**bigint**|현재 단어가 전체 텍스트 인덱싱된 문서 또는 행의 ID입니다. 이 ID는 해당 문서 또는 행의 전체 텍스트 키 값과 일치합니다.|  
|position|**int**|문서에서 키워드의 위치입니다.|  
  
## <a name="remarks"></a>설명  
 DMV를 사용 하 여 인덱싱된 문서에서 인덱싱된 단어의 위치를 식별 합니다. 이 DMV를 사용 하 여 dm_fts_index_keywords_by_document 경우 문제를 해결할 수 있습니다 **.** 이러한 단어를 사용 하 여 쿼리를 실행 하는 경우 해당 단어를 사용 하 여 쿼리를 실행 하면 문서가 반환 되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 전체 텍스트 인덱스가 적용되는 열에 대한 SELECT 권한 및 CREATE FULLTEXT CATALOG 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 예제 데이터베이스에 있는 테이블의 전체 텍스트 인덱스에서 키워드를 반환 합니다 `Production.Document` `AdventureWorks` .  
  
```  
USE AdventureWorks2012;  
GO   
  
SELECT * FROM sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('AdventureWorks2012'),  
    OBJECT_ID('AdventureWorks2012.Production.Document')   
);   
GO  
```  
  
 다음 예제 쿼리와 같이 다른 columns_id에 조건자를 추가 하 여 위치를 추가로 격리할 수 있습니다.  
  
```  
SELECT * FROM sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('AdventureWorks2012'),  
    OBJECT_ID('AdventureWorks2012.Production.Document')   
)  
WHERE document_id = 7 AND display_term = 'performance';  
```  
  
## <a name="see-also"></a>참고 항목  
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)   
 [전체 텍스트 인덱스의 성능 향상](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)   
 [Transact-sql&#41;를 &#40;전체 텍스트 검색 및 의미 체계 검색 함수](../../relational-databases/system-functions/full-text-search-and-semantic-search-functions-transact-sql.md)   
 [Transact-sql&#41;전체 텍스트 검색 및 의미 체계 검색 동적 관리 뷰 및 함수 &#40;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Transact-sql&#41;&#40;전체 텍스트 검색 및 의미 체계 검색 저장 프로시저](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [검색 속성 목록을 사용 하 여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.dm_fts_index_keywords_by_document&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
  
