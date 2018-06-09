---
title: CellData 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ab164b2326cedfaf32100d7354f40684c41a8255
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34574125"
---
# <a name="celldata-element-xmla"></a>CellData 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  [MDDataSet](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) 데이터 형식을 사용하는 [root](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) 요소에 포함된 셀 데이터를 나타내는 Cell 요소의 컬렉션을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">  
   ...  
   <CellData>  
      <Cell>...</Cell>  
   </CellData>  
</root>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[root](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|자식 요소|[Cell](../../../analysis-services/xmla/xml-elements-properties/cell-element-mddataset-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 부모 root 요소에서 **Axes** 요소는 **CellData** 요소 다음에 나타나고, 각 셀에 대한 셀 속성 값을 포함하는 **Cell** 요소의 컬렉션이 다차원 데이터 집합에 반환됩니다.  
  
## <a name="see-also"></a>참고자료
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
