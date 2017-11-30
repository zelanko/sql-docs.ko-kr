---
title: sys.dm_fts_index_keywords (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_fts_index_keywords
- sys.dm_fts_index_keywords
- sys.dm_fts_index_keywords_TSQL
- dm_fts_index_keywords_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.dm_fts_index_keywords dynamic management function
- full-text search [SQL Server], viewing keywords
- troubleshooting [SQL Server], full-text search
ms.assetid: fce7b2a1-7e74-4769-86a8-c77c7628decd
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 903c8f459242fc7f470f71207afd2d5ea3bee23e
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="sysdmftsindexkeywords-transact-sql"></a>sys.dm_fts_index_keywords(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 테이블에 대한 전체 텍스트 인덱스 내용에 관한 정보를 반환합니다.  
  
 **sys.dm_fts_index_keywords** 는 동적 관리 함수입니다.  
  
> [!NOTE]  
>  하위 수준의 전체 텍스트 인덱스 정보를 보려면 사용 하 여는 [sys.dm_fts_index_keywords_by_document](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md) 문서 수준에서 동적 관리 함수입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.dm_fts_index_keywords( DB_ID('database_name'), OBJECT_ID('table_name') )  
```  
  
## <a name="arguments"></a>인수  
 db_id ('*database_name*')  
 에 대 한 호출에서 [db_id ()](../../t-sql/functions/db-id-transact-sql.md) 함수입니다. 이 함수는 데이터베이스 이름을 받아서 데이터베이스 ID를 반환 하 고 있는 **sys.dm_fts_index_keywords** 사용 하 여 지정된 된 데이터베이스를 찾습니다. 경우 *database_name* 은 생략 하면 현재 데이터베이스 ID가 반환 됩니다.  
  
 object_id ('*table_name*')  
 에 대 한 호출에서 [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md) 함수입니다. 이 함수는 테이블 이름을 받아서 검사할 전체 텍스트 인덱스가 들어 있는 테이블의 테이블 ID를 반환합니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**키워드**|**nvarchar(4000)**|전체 텍스트 인덱스에 저장되는 키워드의 16진수 표현입니다.<br /><br /> 참고: OxFF는 파일 또는 데이터 집합의 끝을 나타내는 특수 문자를 나타냅니다.|  
|**display_term**|**nvarchar(4000)**|사람이 인식할 수 있는 키워드 형식입니다. 이 형식은 16진수 형식에서 파생됩니다.<br /><br /> 참고:는 **display_term** OxFF은 "END OF FILE"의 값|  
|**column_id**|**int**|현재 키워드가 전체 텍스트 인덱싱된 열의 ID입니다.|  
|**document_count**|**int**|현재 용어가 들어 있는 문서 또는 행 수입니다.|  
  
## <a name="remarks"></a>주의  
 반환 된 정보 **sys.dm_fts_index_keywords** 무엇 보다도 다음을 찾는 데 유용 합니다.  
  
-   키워드가 전체 텍스트 인덱스에 포함되어 있는지 여부  
  
-   지정된 키워드가 들어 있는 문서 또는 행 수  
  
-   전체 텍스트 인덱스의 가장 일반적인 키워드  
  
    -   **document_count** 각 *keyword_value* 총에 비해 **document_count**, 0xFF의 문서 수입니다.  
  
    -   일반적으로 공통 키워드는 중지 단어로 선언하기에 적합합니다.  
  
> [!NOTE]  
>  **document_count** 반환한 **sys.dm_fts_index_keywords** 에서 반환 되는 수보다 특정 문서에 대 한 덜 정확할 수 있습니다 **sys.dm_fts_index_keywords_by_document** 또는 **CONTAINS** 쿼리 합니다. 잠재적인 부정확성은 1%보다 작을 것으로 예상됩니다. 이 잠재적인 부정확성 때문에 발생할 수 있습니다는 **document_id** 인덱스 조각에 또는 동일한 행에 두 번 이상 나타나면 둘 이상의 행에서 계속 하는 경우에 두 번 계산 될 수 있습니다. 특정 문서에 대 한 보다 정확한 수를 가져오려면 **sys.dm_fts_index_keywords_by_document** 또는 **CONTAINS** 쿼리 합니다.  
  
## <a name="permissions"></a>Permissions  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-displaying-high-level-full-text-index-content"></a>1. 상위 수준의 전체 텍스트 인덱스 내용 표시  
 다음 예에서는 `HumanResources.JobCandidate` 테이블에 상위 수준의 전체 텍스트 인덱스 내용을 표시합니다.  
  
```  
SELECT * FROM sys.dm_fts_index_keywords(db_id('AdventureWorks2012'), object_id('HumanResources.JobCandidate'))  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [전체 텍스트 검색 및 의미 체계 검색 동적 관리 뷰 및 함수 &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)   
 [sys.dm_fts_index_keywords_by_document&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
  
