---
title: CellInfo 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- CellInfo Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cellinfo
- http://schemas.microsoft.com/analysisservices/2003/engine#CellInfo
- urn:schemas-microsoft-com:xml-analysis#CellInfo
helpviewer_keywords:
- CellInfo element
ms.assetid: 8b6420f1-e9a7-4975-b580-1439fa11f5ca
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fda3576bb50314c28dd01474e576ff2b5b333cb8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37176390"
---
# <a name="cellinfo-element-xmla"></a>CellInfo 요소(XMLA)
  부모에 의해 포함 된 셀 메타 데이터를 나타냅니다 [OlapInfo](olapinfo-element-xmla.md) 요소입니다.  
  
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[OlapInfo](olapinfo-element-xmla.md)|  
|자식 요소|하나 이상의 셀 속성 정의|  
  
## <a name="remarks"></a>Remarks  
 `CellInfo` 요소는 `root` 데이터 형식을 사용하여 `MDDataSet` 요소에 의해 반환되는 다차원 데이터 집합 내에 포함된 셀에 대한 셀 속성의 컬렉션을 포함합니다. `CellInfo` 요소의 각 셀 속성은 각각 `name` 특성과 `type` 특성을 사용하여 별도의 XML 요소에 의해 정의됩니다. 셀 속성의 `name` 특성은 XML 요소로 표현되는 OLAP용 OLE DB 셀 속성의 이름에 해당하며 `type` 특성은 셀 속성의 XML 데이터 형식을 나타냅니다. XML 요소의 이름은 `CellData` 요소의 `root` 요소에 포함된 셀에 대한 셀 속성의 값을 식별하는 데 사용됩니다.  
  
 다음은 셀 속성 정의의 구문입니다.  
  
```  
<CellPropertyDefinition name="string" type"string" />  
```  
  
 DISCOVER_PROPERTIES 요청 유형을 사용 하 여 사용 가능한 속성 및 해당 값을 가져올 수 있습니다는 `Discover` 메서드. `PropertyList` 요소에 나열되는 속성에 순서를 지정할 필요는 없습니다.  
  
 공급자는 필요에 따라 `AxisInfo` 또는 `CellInfo` 섹션의 개별 멤버나 셀 속성에 대해 기본값을 지정할 수 있습니다. 속성에 항상 또는 거의 항상 같은 값이 지정되는 경우 기본값은 보다 작은 결과를 제공할 수 있습니다. 속성에 대 한 기본값을 나타내기 위해에`Default` 셀 속성 정의 요소 중 하나의 자식 요소로 요소를 지정할 수도 있습니다. 따라서 결과에 멤버나 셀 속성이 없으면 지정된 기본값이 셀 속성의 값이 됩니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 VALUE, FORMATTED_VALUE 및 FORMAT_STRING 셀 속성이 `CellInfo` 요소에서 표현되는 방법을 보여 줍니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
