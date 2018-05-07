---
title: sys.xml_schema_collections (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_collections_TSQL
- sys.xml_schema_collections
- xml_schema_collections
- xml_schema_collections_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_collections catalog view
ms.assetid: f3f7f3dc-029f-4942-ab3c-75fa9814e40f
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 11e9a91fc27b704b54415acfe98a516a2176603a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysxmlschemacollections-transact-sql"></a>sys.xml_schema_collections(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  각 XML 스키마 컬렉션에 대한 행을 반환합니다. XML 스키마 컬렉션은 XSD 정의의 명명된 집합입니다. XML 스키마 컬렉션 자체는 관계형 스키마에 포함되고 스키마 범위 [!INCLUDE[tsql](../../includes/tsql-md.md)] 이름으로 식별됩니다. 튜플은 고유: xml_collection_id, schema_id 및 이름입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|xml_collection_id|**int**|XML 스키마 컬렉션의 ID입니다. 데이터베이스 내에서 고유합니다.|  
|schema_id|**int**|이 XML 스키마 컬렉션을 포함하는 관계형 스키마의 ID입니다.|  
|principal_id|**int**|스키마 소유자와 다른 경우 개별 소유자의 ID입니다. 기본적으로 스키마에 포함된 개체는 스키마 소유자가 소유합니다. 그러나 ALTER AUTHORIZATION 문으로 대체 소유자를 지정하여 소유권을 변경할 수 있습니다.<br /><br /> NULL = 대체 개별 소유자 없음|  
|name|**sysname**|XML 스키마 컬렉션의 이름입니다.|  
|create_date|**datetime**|XML 스키마 컬렉션을 만든 날짜입니다.|  
|modify_date|**datetime**|XML 스키마 컬렉션을 마지막으로 변경한 날짜입니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 스키마 &#40;XML 유형 시스템&#41; 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
