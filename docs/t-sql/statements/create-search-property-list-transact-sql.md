---
title: "검색 속성 목록 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_SEARCH_PROPERTY_LIST_TSQL
- CREATE SEARCH
- CREATE_SEARCH_TSQL
- CREATE_SEARCH_PROPERTY_TSQL
- CREATE SEARCH PROPERTY
- CREATE SEARCH PROPERTY LIST
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], creating
- CREATE SEARCH PROPERTY LIST statement
ms.assetid: 5440cbb8-3403-4d27-a2f9-8e1f5a1bc12b
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b055be4f948b62553ddbabb40613971a0e5619d8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-search-property-list-transact-sql"></a>CREATE SEARCH PROPERTY LIST(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  새로운 검색 속성 목록을 만듭니다. 검색 속성 목록은 전체 텍스트 인덱스에 포함할 하나 이상의 검색 속성을 지정하는 데 사용됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CREATE SEARCH PROPERTY LIST new_list_name  
   [ FROM [ database_name. ] source_list_name ]  
   [ AUTHORIZATION owner_name ]  
;  
```  
  
## <a name="arguments"></a>인수  
 *new_list_name*  
 새 검색 속성 목록 이름입니다. *new_list_name* 은 최대 128 자의 식별자입니다. *new_list_name* 현재 데이터베이스의 모든 속성 목록에서 고유 해야 하며 식별자에 대 한 규칙을 따라야 합니다. *new_list_name* 전체 텍스트 인덱스를 만들 때 사용 됩니다.  
  
 *database_name*  
 속성 목록에 지정 된 있는 데이터베이스의 이름인 *source_list_name* 있는 합니다. 지정 하지 않으면 *database_name* 현재 데이터베이스에 대 한 기본값입니다.  
  
 *a s e _* 기존 데이터베이스의 이름을 지정 해야 합니다. 현재 연결에 대 한 로그인에 지정 된 데이터베이스의 기존 사용자 ID와 연결 되어 있어야 *database_name*합니다. 필요한 있어야 [권한을](#Permissions) 데이터베이스에 있습니다.  
  
 *source_list_name*  
 새 속성 목록에서 기존 속성 목록을 복사 하 여 만들어지도록 지정 *database_name*합니다. 경우 *source_list_name* CREATE SEARCH PROPERTY LIST 실패 오류가 발생 하 여 존재 하지 않습니다. 검색 속성 *source_list_name* 상속 *new_list_name*합니다.  
  
 권한 부여 *owner_name*  
 속성 목록을 소유할 사용자 또는 역할 이름을 지정합니다. *owner_name* 는 현재 사용자가 멤버, 또는 현재 사용자 대 한 IMPERSONATE 권한이 있어야 하는 역할의 이름 이어야 합니다. *owner_name*합니다. 값을 지정하지 않으면 현재 사용자에게 소유권이 부여됩니다.  
  
> [!NOTE]  
>  사용 하 여 소유자를 변경할 수는 [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] 문.  
  
## <a name="remarks"></a>주의  
  
> [!NOTE]  
>  속성에 대 한 정보는 일반적으로 참조 [검색 속성 목록으로 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)합니다.  
  
 기본적으로 새 검색 속성 목록은 비어 있으므로 검색 속성 목록을 변경하여 하나 이상의 검색 속성을 수동으로 추가해야 합니다. 또는 기존 검색 속성 목록을 복사할 수 있습니다. 이 경우 새 목록이 해당 원본의 검색 속성을 상속하지만 새 목록을 변경하여 검색 속성을 추가하거나 제거할 수 있습니다. 다음 번 전체 채우기를 수행할 당시의 검색 속성 목록의 속성이 전체 텍스트 인덱스에 포함됩니다.  
  
 다음 조건에서는 CREATE SEARCH PROPERTY LIST 문이 실패합니다.  
  
-   데이터베이스를 지정 하는 경우 *database_name* 존재 하지 않습니다.  
  
-   으로 지정한 목록이 경우 *source_list_name* 존재 하지 않습니다.  
  
-   올바른 사용 권한이 없을 경우  
  
 **추가 하거나 목록에서 속성을 제거 하려면**  
  
-   [ALTER SEARCH PROPERTY LIST&#40;Transact-SQL&#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)  
  
-   **속성 목록을 삭제 하려면**  
  
-   [DROP SEARCH PROPERTY LIST&#40;Transact-SQL&#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)  
  
##  <a name="Permissions"></a> 사용 권한  
 현재 데이터베이스에서 CREATE FULLTEXT CATALOG 권한이 필요하고 원본 속성 목록을 복사하는 데이터베이스에 대한 REFERENCES 권한이 필요합니다.  
  
> [!NOTE]  
>  목록을 전체 텍스트 인덱스와 연결하려면 REFERENCES 권한이 필요합니다. 속성을 추가 및 제거하거나 목록을 삭제하려면 CONTROL 권한이 필요합니다. 속성 목록 소유자는 목록에 대한 REFERENCES 또는 CONTROL 권한을 부여할 수 있습니다. CONTROL 권한을 가진 사용자는 다른 사용자에게 REFERENCES 권한을 부여할 수도 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-an-empty-property-list-and-associating-it-with-an-index"></a>1. 빈 속성 목록을 만들고 인덱스와 연결  
 다음 예에서는 `DocumentPropertyList`라는 새 검색 속성 목록을 만듭니다. 이 예제에서는 다음 사용 하 여는 [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) 문을의 전체 텍스트 인덱스와 새 속성 목록 연결에 `Production.Document` 테이블에 `AdventureWorks` 채우기를 시작 하지 않고 데이터베이스입니다.  
  
> [!NOTE]  
>  이 검색 속성 목록에 몇 가지 미리 정의 된, 잘 알려진 검색 속성을 추가 하는 예제를 참조 하세요. [ALTER SEARCH PROPERTY list&#40; Transact SQL &#41; ](../../t-sql/statements/alter-search-property-list-transact-sql.md). 목록에 검색 속성을 추가한 후에는 데이터베이스 관리자가 다른 ALTER FULLTEXT INDEX 문을 START FULL POPULATION 절과 함께 사용해야 합니다.  
  
```  
CREATE SEARCH PROPERTY LIST DocumentPropertyList;  
GO  
USE AdventureWorks2012;  
ALTER FULLTEXT INDEX ON Production.Document   
   SET SEARCH PROPERTY LIST DocumentPropertyList  
   WITH NO POPULATION;   
GO   
```  
  
### <a name="b-creating-a-property-list-from-an-existing-one"></a>2. 기존 속성 목록을 사용하여 속성 목록 만들기  
 다음 예에서는 예 1에서 만든 목록 `JobCandidateProperties`로 새 검색 속성 목록 `DocumentPropertyList`를 만듭니다. 기존 목록은 `AdventureWorks2012` 데이터베이스에서 전체 텍스트 인덱스와 연결되어 있습니다. 그런 다음 이 예에서는 ALTER FULLTEXT INDEX 문을 사용하여 새 속성 목록을 `HumanResources.JobCandidate` 데이터베이스에 있는 `AdventureWorks2012` 테이블의 전체 텍스트 인덱스와 연결합니다. 이 ALTER FULLTEXT INDEX 문이 전체 채우기를 시작합니다. 전체 채우기는 SET SEARCH PROPERTY LIST 절의 기본 동작입니다.  
  
```  
CREATE SEARCH PROPERTY LIST JobCandidateProperties 
FROM AdventureWorks2012.DocumentPropertyList;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate   
   SET SEARCH PROPERTY LIST JobCandidateProperties;  
GO  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER SEARCH PROPERTY list&#40; Transact SQL &#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)   
 [DROP SEARCH PROPERTY list&#40; Transact SQL &#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)   
 [sys.registered_search_properties&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [sys.registered_search_property_lists&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [sys.dm_fts_index_keywords_by_property&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [검색 속성의 속성 집합 GUID 및 속성 정수 ID찾기](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md)  
  
  

