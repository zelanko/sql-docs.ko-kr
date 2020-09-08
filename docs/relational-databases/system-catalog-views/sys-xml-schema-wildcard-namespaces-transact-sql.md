---
description: sys.xml_schema_wildcard_namespaces(Transact-SQL)
title: sys.xml_schema_wildcard_namespaces (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xml_schema_wildcard_namespaces_TSQL
- xml_schema_wildcard_namespaces
- sys.xml_schema_wildcard_namespaces_TSQL
- sys.xml_schema_wildcard_namespaces
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_wildcard_namespaces catalog view
ms.assetid: a3caa932-41c7-48a9-9b2d-ff090afbb66b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ea04c90be9d3fb597c912e74de8c97ad12100e4f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89519276"
---
# <a name="sysxml_schema_wildcard_namespaces-transact-sql"></a>sys.xml_schema_wildcard_namespaces(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  XML 스키마 와일드카드의 각 열거된 네임스페이스에 대해 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|이 문이 적용될 XML 스키마 구성 요소(와일드카드)의 ID입니다.|  
|**namespace**|**nvarchar(4000)**|XML 와일드카드에서 사용하는 네임스페이스의 이름이나 URI입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Xml 스키마 &#40;XML 형식 시스템&#41; 카탈로그 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
