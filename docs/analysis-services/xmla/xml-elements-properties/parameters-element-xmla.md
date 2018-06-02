---
title: Parameters 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 68366f03168b7c7c434f05e88f512401248c1124
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34576065"
---
# <a name="parameters-element-xmla"></a>Parameters 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  [Execute](../../../analysis-services/xmla/xml-elements-properties/parameter-element-xmla.md) 메서드에서 사용하는 [Parameter](../../../analysis-services/xmla/xml-elements-methods-execute.md) 요소의 컬렉션을 포함합니다.  
  
 **Namespace:** `urn:schemas-microsoft-com:xml-analysis`  
  
## <a name="syntax"></a>구문  
  
```  
  
<Execute>  
...  
   <Parameters>  
      <Parameter>...</Parameter>  
   </Parameters>  
...  
</Execute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[실행](../../../analysis-services/xmla/xml-elements-methods-execute.md)|  
|자식 요소|[매개 변수](../../../analysis-services/xmla/xml-elements-properties/parameter-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 일부 XMLA(XML for Analysis) 명령(예: [Process](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) 명령)은 추가 정보를 요청할 수도 있습니다. **Parameters** 요소는 XMLA 명령에 대한 청크 정보를 포함한 추가 정보를 제공하는 메커니즘을 제공합니다.  
  
 XMLA 명령이 **Parameters** 요소를 사용하지 않는 경우 **Execute** 메서드를 호출할 때 이 요소를 생략할 수 있습니다.  
  
## <a name="see-also"></a>참고자료
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
