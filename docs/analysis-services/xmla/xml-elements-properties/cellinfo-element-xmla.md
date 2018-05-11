---
title: CellInfo 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0919c539bcb284ddde1167303e7060eaa998b44f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="cellinfo-element-xmla"></a>CellInfo 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모에 포함 된 셀 메타 데이터를 나타내는 [OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<OlapInfo>  
   ...  
   <CellInfo>  
      <!-- One or more cell property definitions -->  
   </CellInfo>  
   ...  
</OlapInfo>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)|  
|자식 요소|하나 이상의 셀 속성 정의|  
  
## <a name="remarks"></a>주의  
 **CellInfo** 요소에서 반환 된 다차원 데이터 집합에 포함 된 셀에 대 한 셀 속성의 컬렉션을 포함 한 **루트** 사용 하 여 요소는 **MDDataSet**데이터 형식입니다. 각 셀 속성은 **CellInfo** 요소가 각각 별도 XML 요소에 의해 정의 된는 **이름** 특성 및 **형식** 특성입니다. **이름** XML 요소로 표현 되는 OLAP 셀 속성에 대 한 OLE db 이름에 해당 하는 셀 속성의 특성 및 **형식** 나타내는 셀의 XML 데이터 형식 특성 속성입니다. 에 포함 된 셀에 대 한 셀 속성의 값을 식별 하는 XML 요소의 이름이 사용 됩니다는 **CellData** 의 요소는 **루트** 요소입니다.  
  
 다음은 셀 속성 정의의 구문입니다.  
  
```  
<CellPropertyDefinition name="string" type"string" />  
```  
  
 사용 가능한 속성 및 해당 값은 **Discover** 메서드에 DISCOVER_PROPERTIES 요청 유형을 사용하여 얻을 수 있습니다. **PropertyList** 요소에 나열되는 속성에 순서를 지정할 필요는 없습니다.  
  
 공급자의 개별 멤버나 셀 속성에 대 한 기본값을 선택적으로 지정할 수는 **AxisInfo** 또는 **CellInfo** 섹션. 속성에 항상 또는 거의 항상 같은 값이 지정되는 경우 기본값은 보다 작은 결과를 제공할 수 있습니다. 속성에 대 한 기본값을 나타내기 위해는**기본** 셀 속성 정의 요소 중 하나의 자식 요소로 요소를 지정할 수도 있습니다. 따라서 결과에 멤버나 셀 속성이 없으면 지정된 기본값이 셀 속성의 값이 됩니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 VALUE, FORMATTED_VALUE 및 FORMAT_STRING 셀 속성에 표시 되는 방법을 보여 줍니다.는 **CellInfo** 요소입니다.  
  
```  
<OlapInfo>  
   ...  
      <CellInfo>  
         <Value name="VALUE"></Value>  
         <FmtValue name="FORMATTED_VALUE"></FmtValue>  
         <FormatString name="FORMAT_STRING"></FormatString>  
      </CellInfo>  
</OlapInfo>  
```  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
