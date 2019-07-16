---
title: sys.xml_schema_types (TRANSACT-SQL) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a78730509cc1f9eeec83b8d9ff9cb0917e0ed99
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060436"
---
# <a name="sysxmlschematypes-transact-sql"></a>sys.xml_schema_types(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  형식인 XML 스키마 구성 요소 마다 한 행을 반환 **symbol_space** 의 **T**합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**\<열을 상속 >**||열을 상속 [sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)합니다.|  
|**is_abstract**|**bit**|1 = 유형이 추상 유형입니다. 이 형식의 요소의 모든 인스턴스를 사용 해야 합니다 **xsi: type** 추상이 아닌 파생된 형식을 나타내는입니다.<br /><br /> 0 = 유형이 추상이 (기본값)|  
|**allows_mixed_content**|**bit**|1 = 혼합된 콘텐츠가 허용됩니다.<br /><br /> 0 = 혼합된 콘텐츠가 허용되지 (기본값)|  
|**is_extension_blocked**|**bit**|1 =의 블록 특성이 때 인스턴스 형식의 확장으로의 대체가 차단 됩니다 합니다 **complexType** 정의 또는 **blockDefault** 부모의 특성 \<스키마 > 요소 정보 항목은 "extension" 또는 "#all"로 설정 됩니다.<br /><br /> 0 = 확장으로의 대체가 차단되지 않습니다.|  
|**is_restriction_blocked**|**bit**|1 =의 블록 특성이 때 인스턴스 형식의 제한으로의 대체가 차단 됩니다 합니다 **complexType** 정의 또는 **blockDefault** 부모의 특성 \<스키마 > 요소 정보 항목 "restriction" 또는 "#all"로 설정 됩니다.<br /><br /> 0 = 제한으로의 대체가 차단되지 (기본값)|  
|**is_final_extension**|**bit**|1 = 파생 형식의 확장으로 경우 차단 됩니다 final 특성에는 **complexType** 정의 또는 **finalDefault** 부모의 특성 \<스키마 > 요소 정보 항목은 "extension" 또는 "#all"로 설정 됩니다.<br /><br /> 0 = 확장이 (기본값)|  
|**is_final_restriction**|**bit**|1 = 제한 유형 파생 경우 차단 됩니다 final 특성에 단순 또는 **complexType** 정의 또는 **finalDefault** 부모의 특성 \<스키마 > 요소 정보 항목 "restriction" 또는 "#all"로 설정 됩니다.<br /><br /> 0 = 제한이 (기본값)|  
|**is_final_list_member**|**bit**|1 = 이 단순 유형은 목록의 항목 유형으로 사용할 수 없습니다.<br /><br /> 0 = 이 유형은 복합 유형이거나 목록 항목 유형으로 사용할 수 (기본값)|  
|**is_final_union_member**|**bit**|1 = 이 단순 유형은 공용 구조체 유형의 멤버 유형으로 사용할 수 없습니다.<br /><br /> 0 = 이 유형은 복합 유형이거나 공용 구조체 멤버 유형으로 사용할 수 (기본값)|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 스키마 &#40;XML 형식 시스템&#41; 카탈로그 뷰 &#40;SQL 트랜잭션&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
