---
title: sys. dm_fts_index_keywords_by_document (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_keywords_by_document_TSQL
- dm_fts_index_keywords_by_document_TSQL
- sys.dm_fts_index_keywords_by_document
- dm_fts_index_keywords_by_document
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], troubleshooting
- sys.dm_fts_index_keywords_by_document dynamic management function
- full-text search [SQL Server], viewing keywords
ms.assetid: 793b978b-c8a1-428c-90c2-a3e49d81b5c9
author: pmasl
ms.author: pelopes
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 86ab3a31f53f480713ae27a70bfe59d3817af017
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68078557"
---
# <a name="sysdm_fts_index_keywords_by_document-transact-sql"></a>sys.dm_fts_index_keywords_by_document(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  지정된 테이블에 연결된 전체 텍스트 인덱스의 문서 수준 내용에 대한 정보를 반환합니다.  
  
 sys.dm_fts_index_keywords_by_document는 동적 관리 함수입니다.  
  
 **상위 수준의 전체 텍스트 인덱스 정보를 보려면**  
  
-   [sys.dm_fts_index_keywords&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
  
 **문서 속성과 관련된 속성 수준 내용에 대한 정보를 보려면**  
  
-   [sys.dm_fts_index_keywords_by_property&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.dm_fts_index_keywords_by_document  
(   
    DB_ID('database_name'),     OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>인수  
 db_id ('*database_name*')  
 [DB_ID ()](../../t-sql/functions/db-id-transact-sql.md) 함수에 대 한 호출입니다. 이 함수는 데이터베이스 이름을 받아서 데이터베이스 ID를 반환합니다. 이 ID는 지정된 데이터베이스를 찾기 위해 sys.dm_fts_index_keywords_by_document에 사용됩니다. 
  *database_name*을 생략하면 현재 데이터베이스 ID가 반환됩니다.  
  
 object_id ('*table_name*')  
 [OBJECT_ID ()](../../t-sql/functions/object-id-transact-sql.md) 함수에 대 한 호출입니다. 이 함수는 테이블 이름을 받아서 검사할 전체 텍스트 인덱스가 들어 있는 테이블의 테이블 ID를 반환합니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열|데이터 형식|Description|  
|------------|---------------|-----------------|  
|키워드(keyword)|**nvarchar(4000)**|전체 텍스트 인덱스 내에 저장되는 키워드의 16진수 표현입니다.<br /><br /> 참고: OxFF는 파일이 나 데이터 집합의 끝을 나타내는 특수 문자를 나타냅니다.|  
|display_term|**nvarchar(4000)**|사람이 인식할 수 있는 키워드 형식입니다. 이 형식은 전체 텍스트 인덱스에 저장되는 내부 형식에서 파생됩니다.<br /><br /> 참고: OxFF는 파일이 나 데이터 집합의 끝을 나타내는 특수 문자를 나타냅니다.|  
|column_id|**int**|현재 키워드가 전체 텍스트 인덱싱된 열의 ID입니다.|  
|document_id|**int**|현재 단어가 전체 텍스트 인덱싱된 문서 또는 행의 ID입니다. 이 ID는 해당 문서 또는 행의 전체 텍스트 키 값과 일치합니다.|  
|occurrence_count|**int**|**Document_id**로 표시 되는 문서 또는 행에서 현재 키워드의 발생 횟수입니다. '*Search_property_name*'를 지정 하면 occurrence_count은 문서 또는 행 내의 지정 된 검색 속성에 현재 키워드의 발생 횟수만 표시 합니다.|  
  
## <a name="remarks"></a>설명  
 sys.dm_fts_index_keywords_by_document에서 반환하는 정보는 특히 다음을 확인하는 데 유용합니다.  
  
-   전체 텍스트 인덱스에 포함된 총 키워드 수  
  
-   키워드가 특정 문서 또는 행에 포함되어 있는지 여부  
  
-   모든 전체 텍스트 인덱스에서 키워드가 나타나는 횟수  
  
     ([SUM](../../t-sql/functions/sum-transact-sql.md)(**occurrence_count**) WHERE **키워드**=*keyword_value* )  
  
-   지정된 문서 또는 행에서 키워드가 나타나는 횟수  
  
-   지정된 문서 또는 행에 포함된 키워드 수  
  
 sys.dm_fts_index_keywords_by_document에서 제공하는 정보를 사용하여 특정 문서 또는 행에 속한 모든 키워드를 검색할 수도 있습니다.  
  
 권장한 대로 전체 텍스트 키 열이 integer 데이터 형식이면 document_id가 기본 테이블의 전체 텍스트 키 값에 직접 매핑됩니다.  
  
 반대로 전체 텍스트 키 열이 integer 이외의 데이터 형식을 사용하면 document_id가 기본 테이블의 전체 텍스트 키를 나타내지 않습니다. 이 경우 dm_fts_index_keywords_by_document에서 반환 하는 기본 테이블의 행을 식별 하려면 [sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)에서 반환 된 결과와이 뷰에 조인 해야 합니다. 이 뷰를 조인하려면 먼저 저장 프로시저의 출력을 임시 테이블에 저장해야 합니다. 그런 다음 dm_fts_index_keywords_by_document의 document_id 열을 이 저장 프로시저에서 반환된 DocId 열과 조인할 수 있습니다. **타임 스탬프** 열은에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]자동으로 생성 되기 때문에 삽입 시 값을 받을 수 없습니다. 따라서 **timestamp** 열을 **varbinary (8)** 열로 변환 해야 합니다. 다음 예에서는 이 단계를 보여 줍니다. 이 예에서 *table_id* 은 테이블의 id 이며, *database_name* 은 데이터베이스의 이름이 고 *table_name* 는 테이블의 이름입니다.  
  
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
SELECT * FROM sys.dm_fts_index_keywords_by_document   
   ( @db_id, @table_id ) kbd  
   INNER JOIN #MyTempTable tt ON tt.[docid]=kbd.document_id;  
GO  
  
```  
  
## <a name="permissions"></a>사용 권한  
 전체 텍스트 인덱스가 적용되는 열에 대한 SELECT 권한 및 CREATE FULLTEXT CATALOG 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-displaying-full-text-index-content-at-the-document-level"></a>A. 문서 수준의 전체 텍스트 인덱스 내용 표시  
 다음 예에서는 `HumanResources.JobCandidate` 예제 데이터베이스의 `AdventureWorks2012` 테이블에 문서 수준의 전체 텍스트 인덱스 내용을 표시합니다.  
  
> [!NOTE]  
>  `HumanResources.JobCandidate` [TRANSACT-SQL&#41;&#40;전체 텍스트 인덱스 만들기 ](../../t-sql/statements/create-fulltext-index-transact-sql.md)에서 테이블에 대해 제공 된 예를 실행 하 여이 인덱스를 만들 수 있습니다.  
  
```  
SELECT * FROM sys.dm_fts_index_keywords_by_document(db_id('AdventureWorks'),   
object_id('HumanResources.JobCandidate'));  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;전체 텍스트 검색 및 의미 체계 검색 동적 관리 뷰 및 함수 &#40;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)   
 [dm_fts_index_keywords &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)   
 [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [Transact-sql&#41;sp_fulltext_keymappings &#40;](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)   
 [전체 텍스트 인덱스 성능 향상](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)  
  
  
