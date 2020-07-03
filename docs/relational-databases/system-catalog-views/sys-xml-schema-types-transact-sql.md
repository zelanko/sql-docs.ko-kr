---
title: sys.xml_schema_types (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_types_TSQL
- xml_schema_types_TSQL
- sys.xml_schema_types
- xml_schema_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_types catalog view
ms.assetid: 441ba49d-f778-4fa1-98c4-ced375a01a34
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c7c3dc90f505f406583f36980ac758033aeb1519
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899968"
---
# <a name="sysxml_schema_types-transact-sql"></a>sys.xml_schema_types(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **T**의 **symbol_space** 형식인 XML 스키마 구성 요소별 행을 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**||[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)에서 열을 상속 합니다.|  
|**is_abstract**|**bit**|1 = 유형이 추상 유형입니다. 이 형식의 요소에 대 한 모든 인스턴스는 **xsi: type** 을 사용 하 여 추상이 아닌 파생 형식을 나타내야 합니다.<br /><br /> 0 = 유형이 추상이 (기본값)|  
|**allows_mixed_content**|**bit**|1 = 혼합된 콘텐츠가 허용됩니다.<br /><br /> 0 = 혼합된 콘텐츠가 허용되지 (기본값)|  
|**is_extension_blocked**|**bit**|1 = **complexType** 정의의 block 특성 또는 상위 요소 정보 항목의 **blockdefault** 특성이 \<schema> "extension" 또는 "#all"로 설정 된 경우 인스턴스에서 형식이 확장 된 대체가 차단 됩니다.<br /><br /> 0 = 확장으로의 대체가 차단되지 않습니다.|  
|**is_restriction_blocked**|**bit**|1 = **complexType** 정의의 block 특성 또는 상위 요소 정보 항목의 **blockdefault** 특성이 \<schema> "restriction" 또는 "#all"로 설정 된 경우 인스턴스에서 형식 제한으로의 대체가 차단 됩니다.<br /><br /> 0 = 제한으로의 대체가 차단되지 (기본값)|  
|**is_final_extension**|**bit**|1 = **complexType** 정의의 최종 특성이 나 상위 요소 정보 항목의 나머지 **기본** 특성이 \<schema> "extension" 또는 "#all"로 설정 된 경우 형식의 확장에의 한 파생이 차단 됩니다.<br /><br /> 0 = 확장이 (기본값)|  
|**is_final_restriction**|**bit**|1 = 단순 또는 **complexType** 정의의 최종 특성이 나 상위 요소 정보 항목의 나머지 **기본** 특성이 \<schema> "restriction" 또는 "#all"로 설정 된 경우 유형의 제한에의 한 파생이 차단 됩니다.<br /><br /> 0 = 제한이 (기본값)|  
|**is_final_list_member**|**bit**|1 = 이 단순 유형은 목록의 항목 유형으로 사용할 수 없습니다.<br /><br /> 0 = 이 유형은 복합 유형이거나 목록 항목 유형으로 사용할 수 (기본값)|  
|**is_final_union_member**|**bit**|1 = 이 단순 유형은 공용 구조체 유형의 멤버 유형으로 사용할 수 없습니다.<br /><br /> 0 = 이 유형은 복합 유형이거나 공용 구조체 멤버 유형으로 사용할 수 (기본값)|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Xml 스키마 &#40;XML 형식 시스템&#41; 카탈로그 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
