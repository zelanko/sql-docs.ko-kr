---
title: sys.xml_schema_elements (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_elements
- sys.xml_schema_elements_TSQL
- xml_schema_elements
- xml_schema_elements_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_elements catalog view
ms.assetid: 190ed0cd-0c5e-4607-9db4-9e77cacf17d7
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e4d329881c8e895b7f2f1a3b06080b869218a93e
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sysxmlschemaelements-transact-sql"></a>sys.xml_schema_elements(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  형식이 XML 스키마 구성 요소의 각 행을 반환 **symbol_space** 의 **E**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<열을 상속 >**|**--**|열을 상속 [sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)합니다.|  
|**is_default_fixed**|**bit**|1 = 기본값이 고정 값입니다. XML 인스턴스에서 이 값을 무시할 수 없습니다.<br /><br /> 0 = 기본값이 요소에 대해 고정 값이 않습니다(기본값).|  
|**is_abstract**|**bit**|1 = 요소가 추상적이며 인스턴스 문서에서 사용할 수 없습니다. 인스턴스 문서에 요소의 대체 그룹 멤버가 나타나야 합니다.<br /><br /> 0 = 요소가 추상적이지 않습니다(기본값).|  
|**is_nillable**|**bit**|1 = 요소가 nillable입니다.<br /><br /> 0 = 요소가 nillable이 (기본값)|  
|**must_be_qualified**|**bit**|1 = 요소가 명시적으로 정규화된 네임스페이스여야 합니다.<br /><br /> 0 = 요소가 암시적으로 정규화된 네임스페이스여야 (기본값)|  
|**is_extension_blocked**|**bit**|1 = 확장 유형 인스턴스로의 대체가 차단됩니다.<br /><br /> 0 = 확장 유형으로의 대체가 (기본값)|  
|**is_restriction_blocked**|**bit**|1 = 제한 유형 인스턴스로의 대체가 차단됩니다.<br /><br /> 0 = 제한 유형으로의 대체가 (기본값)|  
|**is_substitution_blocked**|**bit**|1 = 대체 그룹 인스턴스를 사용할 수 없습니다.<br /><br /> 0 = 대체 그룹으로의 대체가 (기본값)|  
|**is_final_extension**|**bit**|1 = 확장 유형 인스턴스로의 대체가 허용되지 않습니다.<br /><br /> 0 = 확장 유형 인스턴스에서 대체가 (기본값)|  
|**is_final_restriction**|**bit**|1 = 제한 유형 인스턴스로의 대체가 허용되지 않습니다.<br /><br /> 0 = 제한 유형 인스턴스에서 대체가 (기본값)|  
|**default_value**|**nvarchar (4000)**|요소의 기본값입니다. 기본값을 제공하지 않으면 NULL입니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 스키마 &#40; XML 유형 시스템 &#41; 카탈로그 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
