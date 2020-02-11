---
title: sys. xml_schema_attributes (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xml_schema_attributes_TSQL
- xml_schema_attributes
- sys.xml_schema_attributes_TSQL
- sys.xml_schema_attributes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_attributes catalog view
ms.assetid: dd0c98aa-5e72-4df6-96d9-482786c8dbb1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1d9c4ebe7b997ae9ba72249bd431b37ff0fee2f2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037414"
---
# <a name="sysxml_schema_attributes-transact-sql"></a>sys.xml_schema_attributes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Symbol_space** 특성 인 XML 스키마 구성 요소별 **행을 반환 합니다.**  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<상속 된 열>**|--|[Xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)에서 상속 됩니다.|  
|**is_default_fixed**|**bit**|1 = 기본값이 고정 값입니다. XML 인스턴스에서 이 값을 무시할 수 없습니다.<br /><br /> 0 = 기본값이 특성에 대한 고정 값이 아닙니다. (기본값)|  
|**must_be_qualified**|**bit**|1 = 특성의 네임스페이스를 명시적으로 한정해야 합니다.<br /><br /> 0 = 특성의 네임스페이스를 암시적으로 한정할 수 있습니다. (기본값)|  
|**default_value**|**nvarchar**<br /><br /> **(4000)**|특성의 기본값입니다. 기본값을 제공하지 않으면 NULL입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Xml 스키마 &#40;XML 형식 시스템&#41; 카탈로그 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
