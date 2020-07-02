---
title: sys. registered_search_properties (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.registered_search_properties
- registered_search_properties
- sys.registered_search_properties_TSQL
- registered_search_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search properties [SQL Server]
- property searching [SQL Server], viewing registered properties
- search property lists [SQL Server], viewing registered properties
- sys.registered_search_properties catalog view
ms.assetid: 1b9a7a5c-8c05-4819-83c3-7487dd08fcf7
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 09b95722f47442b2d5d749d8ba36888fb9605f58
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717614"
---
# <a name="sysregistered_search_properties-transact-sql"></a>sys.registered_search_properties(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  현재 데이터베이스에서 검색 속성 목록에 있는 각 검색 속성에 대한 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**property_list_id**|**int**|이 속성이 속한 검색 속성 목록의 ID입니다.|  
|**property_set_guid**|**uniqueidentifier**|검색 속성이 속한 속성 집합을 식별하는 GUID(Globally Unique Identifier)입니다.|  
|**property_int_id**|**int**|속성 집합에서 이 검색 속성을 식별하는 정수입니다. **property_int_id** 은 속성 집합 내에서 고유 합니다.|  
|**property_name**|**nvarchar (64)**|검색 속성 목록에서 이 검색 속성을 고유하게 식별하는 이름입니다.<br /><br /> 참고: 속성을 검색 하려면 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 조건자에이 속성 이름을 지정 합니다.|  
|**property_description**|**nvarchar(512)**|속성에 대한 설명입니다.|  
|**property_id**|**int**|**Property_list_id** 값으로 식별 되는 검색 속성 목록에 있는 검색 속성의 내부 속성 ID입니다.<br /><br /> 지정된 속성이 지정된 검색 속성 목록에 추가되면 전체 텍스트 엔진이 속성을 등록하고 속성 목록에 고유한 내부 속성 ID를 할당합니다. 지정된 검색 속성 목록에 고유한 내부 속성 ID이며 정수입니다. 지정된 속성이 여러 검색 속성 목록에 대해 등록된 경우 검색 속성 목록마다 서로 다른 내부 속성 ID가 할당될 수 있습니다.<br /><br /> 참고: 내부 속성 ID는 검색 속성 목록에 속성을 추가할 때 지정 된 속성 정수 식별자와는 다릅니다. 자세한 내용은 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)을 참조하세요.<br /><br /> 전체 텍스트 인덱스에 있는 속성 관련 내용을 모두 보려면 다음을 수행 합니다. <br />                  [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)|  
  
## <a name="remarks"></a>설명  
 검색 속성 목록에 대한 자세한 내용은 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 사용자가 소유하고 있거나 일부 REFERENCE 권한이 부여된 검색 속성 목록에 있는 검색 속성의 경우에만 검색 속성의 메타데이터를 볼 수 있도록 제한됩니다.  
  
> [!NOTE]  
>  검색 속성 목록 소유자는 목록에 대한 REFERENCE 또는 CONTROL 권한을 부여할 수 있습니다. CONTROL 권한을 가진 사용자는 다른 사용자에게 REFERENCE 권한을 부여할 수도 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 등록된 검색 속성의 메타데이터를 모두 나열합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.registered_search_properties;   
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;ALTER 전체 텍스트 인덱스](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [fulltext_indexes &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
