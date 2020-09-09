---
description: sys.xml_schema_namespaces(Transact-SQL)
title: sys.xml_schema_namespaces (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_namespaces_TSQL
- sys.xml_schema_namespaces
- xml_schema_namespaces
- xml_schema_namespaces_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_namespaces catalog view
ms.assetid: 3ed42dd6-929a-41de-80e8-d3a0a488bc7a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8709142f4ff0e1db417cb67fdb5ea516400ead82
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545376"
---
# <a name="sysxml_schema_namespaces-transact-sql"></a>sys.xml_schema_namespaces(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  각 XSD 정의 XML 네임스페이스에 대해 행을 반환합니다. **Collection_id**, **namespace_id**및 **collection_id**와 같은 튜플을 고유 **합니다.**  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**xml_collection_id**|**int**|이 네임스페이스를 포함하는 XML 스키마 컬렉션의 ID입니다.|  
|**name**|**nvarchar(4000)**|XML 네임스페이스의 이름입니다. 빈 **이름** 은 대상 네임 스페이스를 나타냅니다.|  
|**xml_namespace_id**|**int**|데이터베이스에서 XML 네임스페이스를 고유하게 식별하는 서수이며 1부터 시작합니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Xml 스키마 &#40;XML 형식 시스템&#41; 카탈로그 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
