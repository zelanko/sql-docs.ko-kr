---
title: OlapInfo 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8bc01149181299fc89613f3c4c9084fd3b7cba6f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="olapinfo-element-xmla"></a>OlapInfo 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  에 포함 된 축 및 셀 메타 데이터를 포함 한 [루트](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) 요소를 사용 하는 [MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) 데이터 형식입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">  
   ...  
   <OlapInfo>  
      <CubeInfo>...</CubeInfo>  
      <AxesInfo>...</AxesInfo>  
      <CellInfo>...</CellInfo>  
   </OlapInfo>  
   ...  
</root>  
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
|부모 요소|[루트](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|자식 요소|[AxesInfo](../../../analysis-services/xmla/xml-elements-properties/axesinfo-element-xmla.md), [CellInfo](../../../analysis-services/xmla/xml-elements-properties/cellinfo-element-xmla.md), [CubeInfo](../../../analysis-services/xmla/xml-elements-properties/cubeinfo-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **OLAPInfo** 섹션은 **루트** 사용 하 여 요소는 **MDDataSet** 데이터 형식을 통해 큐브에 대 한 메타 데이터, 다차원 결과 및 속성이 축 셀의 결과 포함 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
