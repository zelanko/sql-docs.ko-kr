---
title: sys.xml_schema_namespaces (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a862eb792087b46c7665c79944475bd7e7e1d3af
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysxmlschemanamespaces-transact-sql"></a>sys.xml_schema_namespaces(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 XSD 정의 XML 네임스페이스에 대해 행을 반환합니다. 튜플은 고유: **collection_id**, **namespace_id**, 및 **collection_id**, 및 **이름**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**xml_collection_id**|**int**|이 네임스페이스를 포함하는 XML 스키마 컬렉션의 ID입니다.|  
|**name**|**nvarchar(4000)**|XML 네임스페이스의 이름입니다. 빈 **이름** 대상 네임 스페이스가 없는 합니다.|  
|**xml_namespace_id**|**int**|데이터베이스에서 XML 네임스페이스를 고유하게 식별하는 서수이며 1부터 시작합니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 스키마 &#40;XML 유형 시스템&#41; 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
