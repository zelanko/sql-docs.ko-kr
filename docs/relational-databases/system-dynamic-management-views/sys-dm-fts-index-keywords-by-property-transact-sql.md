---
title: sys.dm_fts_index_keywords_by_property (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_fts_index_keywords_by_property
- dm_fts_index_keywords_by_property_TSQL
- sys.dm_fts_index_keywords_by_property
- sys.dm_fts_index_keywords_by_property_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], troubleshooting
- search property lists [SQL Server], viewing keywords by property
- full-text search [SQL Server], viewing keywords
- sys.dm_fts_index_keywords_by_property dynamic management view
ms.assetid: fa41e052-a79a-4194-9b1a-2885f7828500
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 603ff2cfed32a6a8ecfb4f55467b697307009822
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmftsindexkeywordsbyproperty-transact-sql"></a>sys.dm_fts_index_keywords_by_property(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  지정된 테이블의 전체 텍스트 인덱스에 있는 속성 관련 내용을 모두 반환합니다. 해당 전체 텍스트 인덱스와 연결된 검색 속성 목록에서 등록한 모든 속성에 속하는 데이터가 모두 여기에 포함됩니다.  
  
 sys.dm_fts_index_keywords_by_property 어떤 내보낸 등록 된 속성 Ifilter를 통해 인덱스 시간 뿐 아니라 각 인덱싱된 문서에서 모든 속성의 정확한 내용을 확인할 수 있는 동적 관리 함수입니다.  
  
 **(속성 관련 내용을 포함)는 모든 문서 수준 콘텐츠를 보려면**  
  
-   [sys.dm_fts_index_keywords_by_document&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
 **상위 수준의 전체 텍스트 인덱스 정보를 보려면**  
  
-   [sys.dm_fts_index_keywords&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
  
> [!NOTE]  
>  검색 속성 목록에 대 한 정보를 참조 하십시오. [검색 속성 목록으로 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.dm_fts_index_keywords_by_property  
(   
    DB_ID('database_name'),   
OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>인수  
 db_id('*database_name*')  
 에 대 한 호출에서 [db_id ()](../../t-sql/functions/db-id-transact-sql.md) 함수입니다. 이 함수는 데이터베이스 이름을 받아서 하 고 지정된 된 데이터베이스를 찾는 데 사용 하는 sys.dm_fts_index_keywords_by_property 데이터베이스 ID를 반환 합니다. *database_name*을 생략하면 현재 데이터베이스 ID가 반환됩니다.  
  
 object_id('*table_name*')  
 에 대 한 호출에서 [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md) 함수입니다. 이 함수는 테이블 이름을 받아서 검사할 전체 텍스트 인덱스가 들어 있는 테이블의 테이블 ID를 반환합니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열|데이터 형식|Description|  
|------------|---------------|-----------------|  
|키워드(keyword)|**nvarchar(4000)**|전체 텍스트 인덱스 내에 저장되는 키워드의 16진수 표현입니다.<br /><br /> 참고: OxFF는 파일 또는 데이터 집합의 끝을 나타내는 특수 문자를 나타냅니다.|  
|display_term|**nvarchar(4000)**|사람이 인식할 수 있는 키워드 형식입니다. 이 형식은 전체 텍스트 인덱스에 저장되는 내부 형식에서 파생됩니다.<br /><br /> 참고: OxFF는 파일 또는 데이터 집합의 끝을 나타내는 특수 문자를 나타냅니다.|  
|column_id|**int**|현재 키워드가 전체 텍스트 인덱싱된 열의 ID입니다.|  
|document_id|**int**|현재 단어가 전체 텍스트 인덱싱된 문서 또는 행의 ID입니다. 이 ID는 해당 문서 또는 행의 전체 텍스트 키 값과 일치합니다.|  
|property_id|**int**|OBJECT_ID에 지정 된 테이블의 전체 텍스트 인덱스에 검색 속성의 내부 속성 ID ('*table_name*') 매개 변수입니다.<br /><br /> 지정된 속성이 검색 속성 목록에 추가되면 전체 텍스트 엔진이 속성을 등록하고 속성 목록에 고유한 내부 속성 ID를 할당합니다. 지정된 검색 속성 목록에 고유한 내부 속성 ID이며 정수입니다. 지정된 속성이 여러 검색 속성 목록에 대해 등록된 경우 검색 속성 목록마다 서로 다른 내부 속성 ID가 할당될 수 있습니다.<br /><br /> 참고: 내부 속성 ID는 검색 속성 목록에 속성을 추가할 때 지정 된 속성 정수 식별자는 다릅니다. 자세한 내용은 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)을 참조하세요.<br /><br /> 속성 id와 속성 이름 간의 연결을 보려면:<br />                    [sys.registered_search_properties&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)|  
  
## <a name="remarks"></a>주의  
 이 동적 관리 뷰에서는 다음과 같은 정보를 확인할 수 있습니다.  
  
-   지정된 DocID에 대해 지정된 속성에 저장되는 내용  
  
-   지정된 속성이 인덱싱된 문서 간에 공통적으로 적용되는 정도  
  
-   지정된 속성이 실제로 문서에 포함되어 있는지 여부. 이 정보는 지정된 검색 속성에 대한 쿼리에서 찾으려는 문서가 반환되지 않는 경우에 유용합니다.  
  
 권장한 대로 전체 텍스트 키 열이 integer 데이터 형식이면 document_id가 기본 테이블의 전체 텍스트 키 값에 직접 매핑됩니다.  
  
 반대로 전체 텍스트 키 열이 integer 이외의 데이터 형식을 사용하면 document_id가 기본 테이블의 전체 텍스트 키를 나타내지 않습니다. 이 경우 dm_fts_index_keywords_by_property에서 반환 되는 기본 테이블의 행을 식별 하려면이 보기에서 반환 된 결과 사용 하 여 조인 [sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)합니다. 이 뷰를 조인하려면 먼저 저장 프로시저의 출력을 임시 테이블에 저장해야 합니다. 그런 다음 dm_fts_index_keywords_by_property의 document_id 열을이 저장된 프로시저에서 반환 된 DocId 열과 조인할 수 있습니다. 한 **타임 스탬프** 에서 자동으로 생성 하는 것이 있기 때문에 열 삽입 시 값 받을 수 없는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 따라서는 **타임 스탬프** 열으로 변환 해야 **varbinary (8)** 열입니다. 다음 예에서는 이 단계를 보여 줍니다. 이 예제에서는 *table_id* 테이블의 id *a s e _* 데이터베이스의 이름 및 *table_name* 테이블의 이름입니다.  
  
```  
USE database_name;  
GO  
CREATE TABLE #MyTempTable   
   (  
      docid INT PRIMARY KEY ,  
      [key] INT NOT NULL  
   );  
DECLARE @db_id int = db_id(N'database_name');  
DECLARE @table_id int = OBJECT_ID(N'table_name');  
INSERT INTO #MyTempTable EXEC sp_fulltext_keymappings @table_id;  
SELECT * FROM sys.dm_fts_index_keywords_by_property   
   ( @db_id, @table_id ) kbd  
   INNER JOIN #MyTempTable tt ON tt.[docid]=kbd.document_id;  
GO  
  
```  
  
## <a name="permissions"></a>Permissions  
 전체 텍스트 인덱스가 적용되는 열에 대한 SELECT 권한 및 CREATE FULLTEXT CATALOG 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Author` 예제 데이터베이스 `Production.Document` 테이블의 전체 텍스트 인덱스에 있는 `AdventureWorks` 속성에서 키워드를 반환합니다. 이 예에서는 별칭 사용 `KWBPOP` 에서 반환 된 테이블에 대 한 **sys.dm_fts_index_keywords_by_property**합니다. 이 예제에서는 내부 조인에서 열을 결합 사용 하 여 [sys.registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md) 및 [sys.fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)합니다.  
  
```  
-- Once the full-text index is configured to support property searching  
-- on the Author property, return any keywords indexed for this property.  
USE AdventureWorks2012;  
GO   
SELECT KWBPOP.* FROM   
   sys.dm_fts_index_keywords_by_property( DB_ID(),   
   object_id('Production.Document') ) AS KWBPOP  
   INNER JOIN  
      sys.registered_search_properties AS RSP ON(   
         (KWBPOP.property_id = RSP.property_id)   
         AND (RSP.property_name = 'Author') )  
   INNER JOIN  
      sys.fulltext_indexes AS FTI ON(   
         (FTI.[object_id] = object_id('Production.Document'))   
         AND (RSP.property_list_id = FTI.property_list_id) );  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)   
 [전체 텍스트 인덱스 성능 향상](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)   
 [sp_fulltext_keymappings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)   
 [sys.dm_fts_index_keywords_by_document &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)   
 [sys.dm_fts_index_keywords &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)   
 [sys.registered_search_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
