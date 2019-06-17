---
title: sys.xml_schema_components (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xml_schema_components
- sys.xml_schema_components_TSQL
- sys.xml_schema_components
- xml_schema_components_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_components catalog view
ms.assetid: 70142d3a-f8b5-4ee2-8287-3935f0f67aa2
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
ms.openlocfilehash: 7066592f665309cfbe476c3ff8f05ab57306deef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "64945921"
---
# <a name="sysxmlschemacomponents-transact-sql"></a>sys.xml_schema_components(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 XML 스키마 구성 요소에 대해 행을 반환합니다. 쌍 (**collection_id**를 **namespace_id**) 포함 된 네임 스페이스에 복합 외래 키입니다. 명명 된 구성 요소에 대 한 값 **symbol_space**를 **이름**를 **scoping_xml_component_id**를 **is_qualified**,  **xml_namespace_id**하십시오 **xml_collection_id** 고유 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|데이터베이스에 있는 XML 스키마 구성 요소의 고유 ID입니다.|  
|**xml_collection_id**|**int**|해당 구성 요소의 네임스페이스를 포함하는 XML 스키마 컬렉션의 ID입니다.|  
|**xml_namespace_id**|**int**|컬렉션 내의 XML 네임스페이스 ID입니다.|  
|**is_qualified**|**bit**|1 = 이 구성 요소에 명시적 네임스페이스 한정자가 있습니다.<br /><br /> 0 = 구성 요소가 로컬 범위 구성 요소입니다. 이 예에서 쌍 **namespace_id**를 **collection_id**, "없는 네임 스페이스"를 참조 **targetNamespace**합니다.<br /><br /> 와일드카드 구성 요소의 경우 이 값이 1과 같습니다.|  
|**name**|**nvarchar**<br /><br /> **(4000)**|XML 스키마 구성 요소의 고유 이름입니다. 구성 요소 이름이 없으면 NULL입니다.|  
|**symbol_space**|**char(1)**|이 기호 이름이 고유한의 공간에 따라 **종류**:<br /><br /> N = 없음<br /><br /> T = 유형<br /><br /> E = 요소<br /><br /> M = 모델 그룹<br /><br /> A = 특성<br /><br /> G = 특성 그룹|  
|**symbol_space_desc**|**nvarchar**<br /><br /> **(60)**|이 기호 이름이 고유한의 공간의 설명에 따라 **종류**:<br /><br /> 없음<br /><br /> TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP|  
|**kind**|**char(1)**|XML 스키마 구성 요소의 종류입니다.<br /><br /> N = 모든 유형(특수 기본 제공 구성 요소)<br /><br /> Z = 모든 단순 유형(특수 기본 제공 구성 요소)<br /><br /> P = 기본 유형(기본 제공 유형)<br /><br /> S = 단순 유형<br /><br /> L = 목록 유형<br /><br /> U = 공용 구조체 유형<br /><br /> C = 복합 단순 유형(단순 유형에서 파생됨)<br /><br /> K = 복합 유형<br /><br /> E = 요소<br /><br /> M = 모델 그룹<br /><br /> W = 요소 와일드카드<br /><br /> A = 특성<br /><br /> G = 특성 그룹<br /><br /> V = 특성 와일드카드|  
|**kind_desc**|**nvarchar**<br /><br /> **(60)**|XML 스키마 구성 요소의 종류에 대한 설명입니다.<br /><br /> ANY_TYPE<br /><br /> ANY_SIMPLE_TYPE<br /><br /> PRIMITIVE_TYPE<br /><br /> SIMPLE_TYPE<br /><br /> LIST_TYPE<br /><br /> UNION_TYPE<br /><br /> COMPLEX_SIMPLE_TYPE<br /><br /> COMPLEX_TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ELEMENT_WILDCARD<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP<br /><br /> ATTRIBUTE_WILDCARD|  
|**derivation**|**char(1)**|파생 유형에 대한 파생 방법입니다.<br /><br /> N = 없음(파생되지 않음)<br /><br /> X = 확장<br /><br /> R = 제한<br /><br /> S = 대체|  
|**derivation_desc**|**nvarchar**<br /><br /> **(60)**|파생 유형의 파생 방법에 대한 설명입니다.<br /><br /> 없음<br /><br /> EXTENSION<br /><br /> RESTRICTION<br /><br /> SUBSTITUTION|  
|**base_xml_component_id**|**int**|이 구성 요소가 파생된 원래 구성 요소의 ID입니다. 없으면 NULL입니다.|  
|**scoping_xml_component_id**|**int**|범위 지정 구성 요소의 고유 ID입니다. 없으면 NULL입니다(전역 범위).|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 스키마 &#40;XML 형식 시스템&#41; 카탈로그 뷰 &#40;SQL 트랜잭션&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
