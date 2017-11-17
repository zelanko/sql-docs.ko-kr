---
title: ALTER SEARCH PROPERTY LIST (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SEARCH_PROPERTY_TSQL
- ALTER_SEARCH_PROPERTY_LIST_TSQL
- ALTER SEARCH PROPERTY LIST
- ALTER SEARCH PROPERTY
- ALTER_SEARCH_TSQL
- ALTER SEARCH
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], altering
- ALTER SEARCH PROPERTY LIST statement
ms.assetid: 0436e4a8-ca26-4d23-93f1-e31e2a1c8bfb
caps.latest.revision: 55
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c93a8382bec0746ae3cfb8f43485da53a06184f0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-search-property-list-transact-sql"></a>ALTER SEARCH PROPERTY LIST(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  지정된 검색 속성 목록에 대해 지정한 검색 속성을 추가하거나 삭제합니다.  
  
## <a name="syntax"></a>구문  
  
```  
ALTER SEARCH PROPERTY LIST list_name  
{  
   ADD 'property_name'  
     WITH   
      (   
          PROPERTY_SET_GUID = 'property_set_guid'  
        , PROPERTY_INT_ID = property_int_id  
      [ , PROPERTY_DESCRIPTION = 'property_description' ]  
      )  
 | DROP 'property_name'   
}  
;  
```  
  
## <a name="arguments"></a>인수  
 *list_name*  
 변경할 속성 목록 이름입니다. *list_name* 식별자입니다.  
  
 기존 속성 목록의 이름을 사용 하 여는 [sys.registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md) 카탈로그 뷰를 다음과 같이 합니다.  
  
```  
SELECT name FROM sys.registered_search_property_lists;  
```  
  
 ADD  
 으로 지정 된 속성 목록에 지정 된 검색 속성을 추가 *list_name*합니다. 속성이 검색 속성 목록에 등록 됩니다. 새로 추가한 속성을 속성 검색에 사용하려면 연결된 전체 텍스트 인덱스가 다시 채워져야 합니다. 자세한 내용은 [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)를 참조하세요.  
  
> [!NOTE]  
>  지정된 된 검색 속성을 검색 속성 목록에 추가 하려면 해당 속성 집합 GUID를 제공 해야 합니다 (*같이 property_set_guid*) 및 속성 정수 ID (*property_int_id*). 자세한 내용은 이 항목의 뒷부분에 나오는 "속성 설정 GUID 및 식별자 가져오기"를 참조하십시오.  
  
 *property_name*  
 전체 텍스트 쿼리에서 속성을 식별하는 데 사용할 이름을 지정합니다. *property_name* 속성 집합 내의 속성을 고유 하 게 식별 해야 합니다. 속성 이름은 내부에 공백을 포함할 수 있습니다. 최대 길이 *property_name* 는 256 자입니다. 이 이름은 작성자나 집 주소와 같은 친숙 한 이름을 나 수 속성의 Windows 정식 이름 같은 **System.Author** 또는 **System.Contact.HomeAddress**합니다.  
  
 개발자에 대 한 사용자가 지정한 값을 사용 해야 합니다 *property_name* 속성을 식별 하는 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 조건자입니다. 따라서 지정된 된 속성에 정의 된 속성을 의미 있게 나타내는 값을 지정 해야 하는 속성 추가 설정 된 경우 GUID (*같이 property_set_guid*) 및 속성의 식별자 (*property_int _id*). 속성 이름에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
 현재 데이터베이스의 검색 속성 목록에 현재 존재 하는 속성의 이름을 보려면를 사용 하 여는 [sys.registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md) 카탈로그 뷰를 다음과 같이 합니다.  
  
```  
SELECT property_name FROM sys.registered_search_properties;  
```  
  
 같이 PROPERTY_SET_GUID ='*같이 property_set_guid*'  
 속성이 속한 속성 집합의 식별자를 지정합니다. 이 식별자는 GUID(Globally Unique Identifier)입니다. 이 값을 가져오는 방법은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
 속성을 보려면 사용 하 여 현재 데이터베이스의 검색 속성 목록에 있는 속성의 GUID를 설정의 [sys.registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md) 카탈로그 뷰를 다음과 같이 합니다.  
  
```  
SELECT property_set_guid FROM sys.registered_search_properties;  
```  
  
 PROPERTY_INT_ID =*property_int_id*  
 속성 집합에서 속성을 식별하는 정수를 지정합니다. 이 값을 가져오는 방법은 "주의"를 참조하십시오.  
  
 현재 데이터베이스의 검색 속성 목록에 있는 속성의 정수 식별자를 보려면 사용 하 여는 [sys.registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md) 카탈로그 뷰를 다음과 같이 합니다.  
  
```  
SELECT property_int_id FROM sys.registered_search_properties;  
```  
  
> [!NOTE]  
>  값의 조합은 *같이 property_set_guid* 및 *property_int_id* 검색 속성 목록에서 고유 해야 합니다. 기존의 조합을 추가하려는 경우 ALTER SEARCH PROPERTY LIST 작업이 실패하고 오류가 발생합니다. 즉, 지정된 속성에 대해 이름을 한 개만 정의할 수 있습니다.  
  
 PROPERTY_DESCRIPTION ='*property_description*'  
 속성의 사용자 정의 설명을 지정합니다. *property_description* 설명은 최대 512 자의 문자열입니다. 이 옵션은 선택 사항입니다.  
  
 DROP  
 지정된 된 속성으로 지정 된 속성 목록에서 삭제 *list_name*합니다. 속성을 삭제하면 속성의 등록이 취소되므로 더 이상 검색할 수 없습니다.  
  
## <a name="remarks"></a>주의  
 전체 텍스트 인덱스마다 검색 속성 목록이 하나만 있을 수 있습니다.  
  
 지정된 검색 속성에 대해 쿼리를 사용하려면 해당 속성을 전체 텍스트 인덱스의 검색 속성 목록에 추가하고 인덱스를 다시 채워야 합니다.  
  
 속성을 지정할 때는 다음 예와 같이 PROPERTY_SET_GUID, PROPERTY_INT_ID 및 PROPERTY_DESCRIPTION 절을 순서에 관계없이 괄호 안에 쉼표로 구분된 목록으로 정렬합니다.  
  
```  
ALTER SEARCH PROPERTY LIST CVitaProperties  
ADD 'System.Author'   
WITH (   
      PROPERTY_DESCRIPTION = 'Author or authors of a given document.',  
      PROPERTY_SET_GUID   = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9',   
      PROPERTY_INT_ID = 4   
      );  
```  
  
> [!NOTE]  
>  이 예에서는 속성 이름 `System.Author`를 사용합니다. 이 이름은 Windows Vista에 도입된 정식 속성 이름(Windows 정식 이름)의 개념과 비슷합니다.  
  
## <a name="obtaining-property-values"></a>속성 값 가져오기  
 해당 속성 집합 GUID 및 속성 정수 ID를 사용하여 전체 텍스트 검색이 검색 속성을 전체 텍스트 인덱스에 매핑합니다. Microsoft에서 정의 된 속성에 대 한 이러한를 가져오는 방법에 대 한 정보를 참조 하십시오. [찾을 속성 집합 Guid 및 Property Integer IDs for Search Properties](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md)합니다. ISV(Independent Software Vendor)에서 정의한 속성에 대한 자세한 내용은 해당 공급업체의 설명서를 참조하십시오.  
  
## <a name="making-added-properties-searchable"></a>추가한 속성을 검색 가능하도록 설정  
 검색 속성 목록에 검색 속성을 추가하면 속성이 등록됩니다. 새로 추가한 속성에 즉시 지정할 수 있습니다 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 쿼리 합니다. 그러나 연결된 전체 텍스트 인덱스를 다시 채워야 새로 추가한 속성의 속성 범위 전체 텍스트 쿼리가 문서를 반환합니다. 예를 들어 다음 속성 범위 쿼리에서 새로 추가 된 속성을 *new_search_property*, 대상 테이블에 연결 된 전체 텍스트 인덱스는 문서를 반환 합니다 (*table_name*) 다시 채워야 합니다.  
  
```  
SELECT column_name  
FROM table_name  
WHERE CONTAINS( PROPERTY( column_name, 'new_search_property' ), 
               'contains_search_condition');  
GO   
```  
  
 전체 채우기를 시작 하려면 다음을 사용 하 여 [ALTER FULLTEXT index&#40; Transact SQL &#41; ](../../t-sql/statements/alter-fulltext-index-transact-sql.md) 문:  
  
```  
USE database_name;  
GO  
ALTER FULLTEXT INDEX ON table_name START FULL POPULATION;  
GO  
```  
  
> [!NOTE]  
>  검색 속성 목록에 남아 있는 속성만 전체 텍스트 쿼리에 사용할 수 있으므로 속성 목록에서 속성이 삭제된 후에는 다시 채울 필요가 없습니다.  
  
## <a name="related-references"></a>관련 참조  
 **속성 목록을 만들려면**  
  
-   [CREATE SEARCH PROPERTY LIST&#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)  
  
 **속성 목록을 삭제 하려면**  
  
-   [DROP SEARCH PROPERTY LIST&#40;Transact-SQL&#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)  
  
 **추가 하거나 전체 텍스트 인덱스에서 속성 목록을 제거 하려면**  
  
-   [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
 **전체 텍스트 인덱스 채우기를 실행 하려면**  
  
-   [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
##  <a name="Permissions"></a> 사용 권한  
 속성 목록에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-adding-a-property"></a>1. 속성 추가  
 다음 예에서는 `Title`, `Author` 및 `Tags`와 같은 여러 속성을 `DocumentPropertyList`라는 속성 목록에 추가합니다.  
  
> [!NOTE]  
>  만드는 예제를 보려면 `DocumentPropertyList` 속성 목록 참조 [CREATE SEARCH PROPERTY LIST &#40; Transact SQL &#41; ](../../t-sql/statements/create-search-property-list-transact-sql.md).  
  
```  
ALTER SEARCH PROPERTY LIST DocumentPropertyList  
   ADD 'Title'   
   WITH ( PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9', PROPERTY_INT_ID = 2,   
      PROPERTY_DESCRIPTION = 'System.Title - Title of the item.' );  
  
ALTER SEARCH PROPERTY LIST DocumentPropertyList   
    ADD 'Author'  
   WITH ( PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9', PROPERTY_INT_ID = 4,   
      PROPERTY_DESCRIPTION = 'System.Author - Author or authors of the item.' );  
  
ALTER SEARCH PROPERTY LIST DocumentPropertyList   
    ADD 'Tags'  
   WITH ( PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9', PROPERTY_INT_ID = 5,   
      PROPERTY_DESCRIPTION = 
          'System.Keywords - Set of keywords (also known as tags) assigned to the item.' );  
```  
  
> [!NOTE]  
>  제공된 검색 속성 목록을 속성 범위 쿼리에 사용하려면 먼저 이 목록을 전체 텍스트 인덱스와 연결해야 합니다. 이 위해 사용 하 여 프로그램 [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) 문을 SET SEARCH PROPERTY LIST 절을 지정 합니다.  
  
### <a name="b-dropping-a-property"></a>2. 속성 삭제  
 다음 예에서는 `Comments` 속성 목록에서 `DocumentPropertyList` 속성을 삭제합니다.  
  
```  
ALTER SEARCH PROPERTY LIST DocumentPropertyList  
DROP 'Comments' ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SEARCH PROPERTY list&#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)   
 [DROP SEARCH PROPERTY list&#40; Transact SQL &#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)   
 [sys.registered_search_properties&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [sys.registered_search_property_lists&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [sys.dm_fts_index_keywords_by_property&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [검색 속성의 속성 집합 GUID 및 속성 정수 ID찾기](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md)  
  
  

