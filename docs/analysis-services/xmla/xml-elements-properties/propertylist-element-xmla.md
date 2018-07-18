---
title: PropertyList 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3e773de16e65aa9c7f1be521214088aa9f06b369
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38036711"
---
# <a name="propertylist-element-xmla"></a>PropertyList 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Analysis (XMLA) 속성에서 사용 하는 for XML의 컬렉션을 포함 합니다 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 하 고 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Properties>  
   <PropertyList>  
      <!-- Zero or more XMLA properties -->  
   </PropertyList>  
</Properties>  
```  
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Properties](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)|  
|자식 요소|XMLA 속성(주의 참조)|  
  
## <a name="remarks"></a>Remarks  
 **PropertyList** 요소는 XMLA 속성의 컬렉션을 포함합니다. 사용자는 각 속성을 사용하여 **Discover** 또는 **Execute** 메서드의 일부 요소를 제어함으로써 데이터 원본에 연결하는 데 필요한 정보를 정의하거나, 결과 집합의 반환 형식을 지정하거나, 데이터의 서식을 지정할 로캘을 지정할 수 있습니다. **PropertyList** 요소의 각 XMLA 속성은 개별 XML 요소로 정의됩니다. XML 속성의 값은 XML 요소에 포함된 데이터이며, XML 속성의 이름은 XML 요소 이름과 일치합니다.  
  
 사용 가능한 속성 및 해당 값은 **Discover** 메서드에 DISCOVER_PROPERTIES 요청 유형을 사용하여 얻을 수 있습니다. **PropertyList** 요소에 나열되는 속성에 순서를 지정할 필요는 없습니다.  
  
 Analysis Services에서 지원 되는 XMLA 속성에 대 한 자세한 내용은 [지원 되는 XMLA 속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)합니다.  
  
## <a name="example"></a>예제  
  
```  
<Properties>  
   <PropertyList>  
      <DataSourceInfo>  
         Provider=MSOLAP;Data Source=local;  
      </DataSourceInfo>  
      <Catalog>  
         Foodmart 2000  
      </Catalog>  
      <Format>  
         Multidimensional  
      </Format>  
   </PropertyList>  
</Properties>  
```  
  
## <a name="see-also"></a>참고자료
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
