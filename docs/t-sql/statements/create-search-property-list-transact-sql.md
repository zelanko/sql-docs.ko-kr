---
description: CREATE SEARCH PROPERTY LIST(Transact-SQL)
title: CREATE SEARCH PROPERTY LIST(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_SEARCH_PROPERTY_LIST_TSQL
- CREATE SEARCH
- CREATE_SEARCH_TSQL
- CREATE_SEARCH_PROPERTY_TSQL
- CREATE SEARCH PROPERTY
- CREATE SEARCH PROPERTY LIST
- sql13.swb.spl.newsearchpropertylist.f1
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], creating
- CREATE SEARCH PROPERTY LIST statement
ms.assetid: 5440cbb8-3403-4d27-a2f9-8e1f5a1bc12b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 22ae11a8e37109e7ba90e2b02e9e4351510f9ae7
ms.sourcegitcommit: 5f3e0eca9840db20038f0362e5d88a84ff3424af
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92344079"
---
# <a name="create-search-property-list-transact-sql"></a>CREATE SEARCH PROPERTY LIST(Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  새로운 검색 속성 목록을 만듭니다. 검색 속성 목록은 전체 텍스트 인덱스에 포함할 하나 이상의 검색 속성을 지정하는 데 사용됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
CREATE SEARCH PROPERTY LIST new_list_name  
   [ FROM [ database_name. ] source_list_name ]  
   [ AUTHORIZATION owner_name ]  
;  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *new_list_name*  
 새 검색 속성 목록 이름입니다. *new_list_name* 은 최대 128자의 식별자입니다. *new_list_name* 은 목록에서 고유해야 하며 식별자 규칙을 따릅니다. *new_list_name* 은 전체 텍스트 인덱스를 만들 때 사용합니다.  
  
 *database_name*  
 *source_list_name* 에 지정된 속성 목록이 있는 데이터베이스의 이름입니다. *database_name* 을 지정하지 않으면 기본적으로 현재 데이터베이스가 됩니다.  
  
 *database_name* 은 기존 데이터베이스 이름을 지정해야 합니다. 현재 연결의 로그인은 *database_name* 에 지정된 데이터베이스의 기존 사용자 ID와 연결되어야 합니다. 데이터베이스에 대한 필수 [사용 권한](#Permissions)도 있어야 합니다.  
  
 *source_list_name*  
 *database_name* 에서 기존 속성 목록을 복사하여 새로운 속성 목록을 만들도록 지정합니다. *source_list_name* 이 없으면 CREATE SEARCH PROPERTY LIST가 실패하고 오류가 발생합니다. *source_list_name* 의 검색 등록 정보는 *new_list_name* 에 의해 상속됩니다.  
  
 AUTHORIZATION *owner_name*  
 속성 목록을 소유할 사용자 또는 역할 이름을 지정합니다. *owner_name* 은 현재 사용자가 멤버로 속한 역할의 이름이어야 합니다. 그렇지 않으면 현재 사용자가 *owner_name* 에 대한 IMPERSONATE 권한이 있어야 합니다. 값을 지정하지 않으면 현재 사용자에게 소유권이 부여됩니다.  
  
> [!NOTE]  
>  [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 소유자를 변경할 수 있습니다.  
  
## <a name="remarks"></a>설명  
  
> [!NOTE]  
>  일반적으로 속성 목록에 대한 자세한 내용은 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)을 참조하세요.  
  
 기본적으로 새 검색 속성 목록은 비어 있으므로 검색 속성 목록을 변경하여 하나 이상의 검색 속성을 수동으로 추가해야 합니다. 또는 기존 검색 속성 목록을 복사할 수 있습니다. 이 경우 새 목록이 해당 원본의 검색 속성을 상속하지만 새 목록을 변경하여 검색 속성을 추가하거나 제거할 수 있습니다. 다음 번 전체 채우기를 수행할 당시의 검색 속성 목록의 속성이 전체 텍스트 인덱스에 포함됩니다.  
  
 다음 조건에서는 CREATE SEARCH PROPERTY LIST 문이 실패합니다.  
  
-   *database_name* 으로 지정한 데이터베이스가 없을 경우  
  
-   *source_list_name* 으로 지정한 목록이 없을 경우  
  
-   올바른 사용 권한이 없을 경우  
  
 **목록에서 속성을 추가하거나 제거하려면**  
  
-   [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)  
  
-   **속성 목록을 삭제하려면**  
  
-   [DROP SEARCH PROPERTY LIST&#40;Transact-SQL&#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)  
  
##  <a name="permissions"></a><a name="Permissions"></a> 권한  
 현재 데이터베이스에서 CREATE FULLTEXT CATALOG 권한이 필요하고 원본 속성 목록을 복사하는 데이터베이스에 대한 REFERENCES 권한이 필요합니다.  
  
> [!NOTE]  
>  목록을 전체 텍스트 인덱스와 연결하려면 REFERENCES 권한이 필요합니다. 속성을 추가 및 제거하거나 목록을 삭제하려면 CONTROL 권한이 필요합니다. 속성 목록 소유자는 목록에 대한 REFERENCES 또는 CONTROL 권한을 부여할 수 있습니다. CONTROL 권한을 가진 사용자는 다른 사용자에게 REFERENCES 권한을 부여할 수도 있습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-creating-an-empty-property-list-and-associating-it-with-an-index"></a>A. 빈 속성 목록을 만들고 인덱스와 연결  
 다음 예에서는 `DocumentPropertyList`라는 새 검색 속성 목록을 만듭니다. 그런 다음, 이 예에서는 채우기를 시작하지 않고 [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) 문을 사용하여 새 속성 목록을 `AdventureWorks` 데이터베이스에 있는 `Production.Document` 테이블의 전체 텍스트 인덱스와 연결합니다.  
  
> [!NOTE]  
>  이 검색 속성 목록에 미리 정의되고 잘 알려진 검색 속성을 여러 개 추가하는 예에 대해서는 [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)을 참조하세요. 목록에 검색 속성을 추가한 후에는 데이터베이스 관리자가 다른 ALTER FULLTEXT INDEX 문을 START FULL POPULATION 절과 함께 사용해야 합니다.  
  
```sql 
CREATE SEARCH PROPERTY LIST DocumentPropertyList;  
GO  
USE AdventureWorks2012;  
ALTER FULLTEXT INDEX ON Production.Document   
   SET SEARCH PROPERTY LIST DocumentPropertyList  
   WITH NO POPULATION;   
GO   
```  
  
### <a name="b-creating-a-property-list-from-an-existing-one"></a>B. 기존 속성 목록을 사용하여 속성 목록 만들기  
 다음 예에서는 예 1에서 만든 목록 `JobCandidateProperties`로 새 검색 속성 목록 `DocumentPropertyList`를 만듭니다. 기존 목록은 `AdventureWorks2012` 데이터베이스에서 전체 텍스트 인덱스와 연결되어 있습니다. 그런 다음 이 예에서는 ALTER FULLTEXT INDEX 문을 사용하여 새 속성 목록을 `HumanResources.JobCandidate` 데이터베이스에 있는 `AdventureWorks2012` 테이블의 전체 텍스트 인덱스와 연결합니다. 이 ALTER FULLTEXT INDEX 문이 전체 채우기를 시작합니다. 전체 채우기는 SET SEARCH PROPERTY LIST 절의 기본 동작입니다.  
  
```sql  
CREATE SEARCH PROPERTY LIST JobCandidateProperties 
FROM AdventureWorks2012.DocumentPropertyList;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate   
   SET SEARCH PROPERTY LIST JobCandidateProperties;  
GO
```  
  
## <a name="see-also"></a>관련 항목  
 [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)   
 [DROP SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)   
 [sys.registered_search_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [검색 속성의 속성 집합 GUID 및 속성 정수 ID찾기](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md)  
  
  
