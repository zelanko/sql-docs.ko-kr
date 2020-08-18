---
description: sys.xml_schema_attributes(Transact-SQL)
title: sys.xml_schema_attributes (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c5f1eab66cd09f1d52c5e675761c691801baf67e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88400419"
---
# <a name="sysxml_schema_attributes-transact-sql"></a>sys.xml_schema_attributes(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Symbol_space** 특성 인 XML 스키마 구성 요소별 **행을 반환 합니다.**  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**|--|[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)에서 상속 됩니다.|  
|**is_default_fixed**|**bit**|1 = 기본값이 고정 값입니다. XML 인스턴스에서 이 값을 무시할 수 없습니다.<br /><br /> 0 = 기본값이 특성에 대한 고정 값이 아닙니다. (기본값)|  
|**must_be_qualified**|**bit**|1 = 특성의 네임스페이스를 명시적으로 한정해야 합니다.<br /><br /> 0 = 특성의 네임스페이스를 암시적으로 한정할 수 있습니다. (기본값)|  
|**default_value**|**nvarchar**<br /><br /> **(4000)**|특성의 기본값입니다. 기본값을 제공하지 않으면 NULL입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Xml 스키마 &#40;XML 형식 시스템&#41; 카탈로그 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
