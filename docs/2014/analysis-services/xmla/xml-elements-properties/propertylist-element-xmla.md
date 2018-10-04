---
title: PropertyList 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- PropertyList Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#PropertyList
- microsoft.xml.analysis.propertylist
- urn:schemas-microsoft-com:xml-analysis#PropertyList
helpviewer_keywords:
- PropertyList element
ms.assetid: 58e63bd9-8aac-438d-adba-1868b4d123f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d3eb6da43b5487efa93f3901c866a1183e77d978
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48068913"
---
# <a name="propertylist-element-xmla"></a>PropertyList 요소(XMLA)
  Analysis (XMLA) 속성에서 사용 하는 for XML의 컬렉션을 포함 합니다 [Discover](../xml-elements-methods-discover.md) 하 고 [Execute](../xml-elements-methods-execute.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Properties>  
   <PropertyList>  
      <!-- Zero or more XMLA properties -->  
   </PropertyList>  
</Properties>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Properties](properties-element-xmla.md)|  
|자식 요소|XMLA 속성(주의 참조)|  
  
## <a name="remarks"></a>Remarks  
 `PropertyList` 요소는 XMLA 속성의 컬렉션을 포함 합니다. 사용자는 각 속성을 사용하여 `Discover` 또는 `Execute` 메서드의 일부 요소를 제어함으로써 데이터 원본에 연결하는 데 필요한 정보를 정의하거나, 결과 집합의 반환 형식을 지정하거나, 데이터의 서식을 지정할 로캘을 지정할 수 있습니다. 각 XMLA 속성은 `PropertyList` 요소는 별도 XML 요소로 정의 됩니다. XML 속성의 값은 XML 요소에 포함된 데이터이며, XML 속성의 이름은 XML 요소 이름과 일치합니다.  
  
 DISCOVER_PROPERTIES 요청 유형을 사용 하 여 사용 가능한 속성 및 해당 값을 가져올 수 있습니다는 `Discover` 메서드. `PropertyList` 요소에 나열되는 속성에 순서를 지정할 필요는 없습니다.  
  
 지원 되는 XMLA 속성에 대 한 자세한 내용은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]를 참조 하십시오 [지원 되는 XMLA 속성 &#40;XMLA&#41;](propertylist-element-supported-xmla-properties.md).  
  
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
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
