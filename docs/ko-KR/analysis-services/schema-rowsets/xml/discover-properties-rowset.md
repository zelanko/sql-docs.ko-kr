---
title: DISCOVER_PROPERTIES 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DISCOVER_PROPERTIES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_PROPERTIES rowset
ms.assetid: 3e2b50e2-3855-4091-8b02-4968e8e57d4c
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f37cf116c4d31dbd63ba13b575a91fa042350863
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="discoverproperties-rowset"></a>DISCOVER_PROPERTIES 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  지정된 데이터 원본에 대해 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA(XML for Analysis) 공급자에서 지원하는 표준 및 공급자별 속성에 대한 정보와 값 목록을 반환합니다. 지원되지 않는 속성은 반환된 결과 집합에 나열되지 않습니다.  
  
 호출 하는 경우는 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드는 **DISCOVER_PROPERTIES** 열거 값은 [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) 요소는 **Discover** 메서드가 반환 되는 **DISCOVER_PROPERTIES** 행 집합.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_PROPERTIES** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|형식|길이|Description|  
|-----------------|----------|------------|-----------------|  
|**propertyName**|**DBTYPE_WSTR**||속성의 이름입니다.|  
|**PropertyDescription**|**DBTYPE_WSTR**||속성의 지역화 가능한 텍스트 설명입니다. **NULL**을 반환할 수 있습니다.|  
|**PropertyType**|**DBTYPE_WSTR**||속성의 XML 데이터 형식입니다.<br /><br /> **NULL**을 반환할 수 있습니다.|  
|**PropertyAccessType**|**DBTYPE_WSTR**||속성에 대한 액세스입니다. 값은 **Read**, **Write**또는 **ReadWrite**일 수 있습니다.|  
|**IsRequired**|**DBTYPE_BOOL**||속성이 필요한지 여부를 나타내는 부울입니다.<br /><br /> 속성이 필요하면 True이고, 필요하지 않으면 False입니다.<br /><br /> **NULL**을 반환할 수 있습니다.|  
|**Value**|**DBTYPE_WSTR**||속성의 현재 값입니다.<br /><br /> **NULL**을 반환할 수 있습니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **DISCOVER_PROPERTIES** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**propertyName**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>관련 항목:  
 [XML for Analysis 스키마 행 집합](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
