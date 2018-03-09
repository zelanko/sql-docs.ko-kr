---
title: sys.column_xml_schema_collection_usages (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- column_xml_schema_collection_usages_TSQL
- sys.column_xml_schema_collection_usages
- column_xml_schema_collection_usages
- sys.column_xml_schema_collection_usages_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.column_xml_schema_collection_usages catalog view
ms.assetid: 4fd1ec7f-b9dc-4ddb-ab3a-0d59ab05ad20
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4a0f522a4d243951f7d415cec516d644e163a968
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="syscolumnxmlschemacollectionusages-transact-sql"></a>sys.column_xml_schema_collection_usages(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XML 스키마에서 유효성을 검사하는 각 열에 대해 하나의 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|이 열이 속해 있는 개체의 ID입니다.|  
|**column_id**|**int**|열의 ID입니다. 개체 내에서 고유합니다.|  
|**xml_collection_id**|**int**|열의 유효성을 검사하는 XML 스키마 네임스페이스를 포함하는 컬렉션의 ID입니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 스키마 &#40; XML 유형 시스템 &#41; 카탈로그 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
