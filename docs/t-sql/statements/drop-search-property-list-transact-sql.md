---
title: DROP SEARCH PROPERTY LIST(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP_SEARCH_PROPERTY_LIST_TSQL
- DROP SEARCH PROPERTY LIST
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- DROP SEARCH PROPERTY LIST statement
- search property lists [SQL Server], dropping
- search property lists [SQL Server], deleting
ms.assetid: 7c7ce52a-6b77-4a1c-9abf-d5feb664bea8
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 87dd1a8ed9bdcc6ba0dd76a6fd0f97352811d852
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33067300"
---
# <a name="drop-search-property-list-transact-sql"></a>DROP SEARCH PROPERTY LIST(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  검색 속성 목록이 현재 데이터베이스의 어떠한 전체 텍스트 인덱스와도 연결되지 않은 경우 현재 데이터베이스에서 속성 목록을 삭제합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP SEARCH PROPERTY LIST property_list_name  
;  
```  
  
## <a name="arguments"></a>인수  
 *property_list_name*  
 삭제할 검색 속성 목록의 이름입니다. *property_list_name*은 식별자입니다.  
  
 기존 속성 목록의 이름을 보려면 다음과 같이 [sys.registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md) 카탈로그 뷰를 사용하십시오.  
  
```  
SELECT name FROM sys.registered_search_property_lists;  
```  
  
## <a name="remarks"></a>Remarks  
 데이터베이스의 검색 속성 목록이 전체 텍스트 인덱스와 연결되어 있는 경우에는 해당 목록을 삭제할 수 없으며 삭제하려고 시도하면 실패합니다. 지정된 전체 텍스트 인덱스에서 검색 속성 목록을 삭제하려면 [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) 문을 사용하고 OFF 또는 다른 검색 속성 목록 이름을 사용하여 SET SEARCH PROPERTY LIST 절을 지정합니다.  
  
 **서버 인스턴스에서 속성 목록을 보려면**  
  
-   [sys.registered_search_property_lists&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
 **전체 텍스트 인덱스와 연결된 속성 목록을 보려면**  
  
-   [sys.fulltext_indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
 **전체 텍스트 인덱스에서 속성 목록을 제거하려면**  
  
-   [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
##  <a name="Permissions"></a> Permissions  
 검색 속성 목록에 대한 CONTROL 권한이 필요합니다.  
  
> [!NOTE]  
>  속성 목록 소유자는 목록에 대한 CONTROL 권한을 부여할 수 있습니다. 기본적으로 검색 속성 목록을 만든 사용자가 소유자입니다. [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 소유자를 변경할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `JobCandidateProperties` 데이터베이스에서 `AdventureWorks2012` 속성 목록을 삭제합니다.  
  
```  
DROP SEARCH PROPERTY LIST JobCandidateProperties;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)   
 [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)   
 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.registered_search_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [sys.registered_search_property_lists&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
  
