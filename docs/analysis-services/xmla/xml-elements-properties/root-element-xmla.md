---
title: root 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 794e33d6270ef9540396fd7d2f38a08ccab4c8d2
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37968385"
---
# <a name="root-element-xmla"></a>root 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  반환 된 결과 포함 합니다 [검색](../../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드 또는 XML for Analysis (XMLA) 명령 사용 하 여 실행 합니다 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<return> <!-- or results-->  
   ...  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">...</root> <!-- for Execute method only -->  
   <!-- or -->  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">...</root>  
   <!-- or -->  
   <root xmlns= xmlns="urn:schemas-microsoft-com:xml-analysis:empty">...</root>  
   ...  
</return>  
```  
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|아래 표를 참조하세요.|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-n: 두 번 이상 나타날 수 있는 필수 요소입니다.|  
  
|상위 항목|데이터 형식|  
|--------------|---------------|  
|[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)|[행 집합](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md), [olapxmla_EmptyResult](../../../analysis-services/xmla/xml-data-types/emptyresult-data-type-xmla.md)|  
|[ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)|[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)하십시오 [행 집합](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md), [olapxmla_EmptyResult](../../../analysis-services/xmla/xml-data-types/emptyresult-data-type-xmla.md)|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[결과](../../../analysis-services/xmla/xml-elements-properties/results-element-xmla.md), [반환](../../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **루트** 요소에서 반환 된 정보를 포함 합니다 [DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md) 요소는 단일 반환 **검색** 메서드 호출 또는 [ ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md) 단일 실행 된 단일 XMLA 명령에서 반환한 요소 **Execute** 메서드를 호출 합니다.  
  
## <a name="see-also"></a>참고자료
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
