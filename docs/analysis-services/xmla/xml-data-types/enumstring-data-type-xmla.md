---
title: "EnumString 데이터 형식 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- EnumString Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- EnumString
- urn:schemas-microsoft-com:xml-analysis#EnumString
- http://schemas.microsoft.com/analysisservices/2003/engine#EnumString
helpviewer_keywords:
- EnumString data type
ms.assetid: 9214195e-4539-419b-95ec-b7aa75e033ab
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3209c6fd1546a4b1596eaaf6f4a19049bfc1fa92
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="enumstring-data-type-xmla"></a>EnumString 데이터 형식(XMLA)
  지정된 열거자에 대한 명명된 상수 집합을 나타내는 파생 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<EnumString>...</EnumString>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|**string**|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|없음|  
|파생 요소|없음|  
  
## <a name="remarks"></a>주의  
 XMLA(XML for Analysis)는 열거형을 사용하여 문자열 값을 확인 가능한 설정 집합으로 제한합니다. **EnumString** 은 표준 XML **string** 데이터 형식을 사용합니다. 명명된 상수 각각에 대한 특정 값은 열거자 정의로 지정됩니다. 열거자에 추가 하 여 정의 됩니다는 [DISCOVER_ENUMERATORS](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md) 스키마 행 집합을 사용 하 여 검색할 수 있습니다는 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드에 DISCOVER_ENUMERATORS 요청 유형.  
  
 인스턴스에서 지원 되는 열거자를 설명 하는 다음 표에서 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
|Enumerator|설명|  
|----------------|-----------------|  
|ProviderType|ProviderType 열을 지원는 [DISCOVER_DATASOURCES](../../../analysis-services/schema-rowsets/xml/discover-datasources-rowset.md) 스키마 행 집합에서 반환 될 수 있는 데이터의 유형을 결정 하는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.<br /><br /> 이 열거형에는 XMLA 속성인도 지원 **ProviderType**에서 지 원하는 공급자 유형을 결정 하는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스. 이 열거형은 DISCOVER_DATASOURCES 스키마 행 집합에서도 사용됩니다.<br /><br /> 에 대 한 자세한 내용은 **ProviderType**, 참조 [지원 XMLA 속성 &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|AuthenticationMode|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 액세스하기 위해 전달해야 하는 보안 자격 증명을 결정하는 DISCOVER_DATASOURCES 스키마 행 집합에서 AuthenticationMode 열을 지원합니다.|  
|PropertyAccessType|PropertyAccessType 열을 지원는 [DISCOVER_PROPERTIES](../../../analysis-services/schema-rowsets/xml/discover-properties-rowset.md) XMLA 속성에 사용 가능한 액세스 유형을 결정 하는 스키마 행 집합입니다.|  
|StateSupport|XMLA 속성을 원하는 **StateSupport**에서 지원 되는 상태 유지의 수준을 결정 하는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.<br /><br /> 에 대 한 자세한 내용은 **StateSupport**, 참조 [지원 XMLA 속성 &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|StateActionVerb|SOAP 헤더의 XMLA에서 지원되며 세션을 시작하고, 식별하고, 끝내는 데 사용되는 동사 목록을 포함합니다.<br /><br /> 세션에 대 한 자세한 내용은 참조 [관리 연결 및 세션 &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md).|  
|ResultsetFormat|XMLA 속성을 원하는 **형식**, 반환 되는 데이터의 형식을 결정 하는 [루트](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) 요소입니다.<br /><br /> 에 대 한 자세한 내용은 **형식**, 참조 [지원 XMLA 속성 &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|ResultsetAxisFormat|다차원 데이터를 포함하는 **AxisFormat**요소에서 반환되는 축 정보의 형식을 결정하는 XMLA 속성인 **root** 을 지원합니다.<br /><br /> 에 대 한 자세한 내용은 **a x**, 참조 [지원 XMLA 속성 &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|ResultsetContents|**Content**요소에서 메타데이터가 반환되는지, 아니면 데이터가 반환되는지를 결정하는 XMLA 속성인 **root** 를 지원합니다.<br /><br /> 에 대 한 자세한 내용은 **콘텐츠**, 참조 [지원 XMLA 속성 &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|MDXSupportLevel|XMLA 속성을 원하는 **MDXSupport**에서 사용할 수 있는 MDX (Multidimensional Expressions) 지원의 수준을 나타내는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.<br /><br /> 에 대 한 자세한 내용은 **MDXSupport**, 참조 [지원 XMLA 속성 &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
  
## <a name="see-also"></a>관련 항목:  
 [XML 데이터 형식 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)  
  
  
