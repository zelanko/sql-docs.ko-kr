---
title: Parameter 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5ca615a3ca71d025d95fc56c2d4ec8253b7ce2ba
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="parameter-element-xmla"></a>Parameter 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드에서 사용되는 매개 변수의 이름 및 값을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Parameters>  
...  
   <Parameter>  
      <Name>...</Name>  
      <Value>...</Value>  
   </Parameter>  
...  
</Parameters>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[매개 변수](../../../analysis-services/xmla/xml-elements-properties/parameters-element-xmla.md)|  
|자식 요소|[Name](../../../analysis-services/xmla/xml-elements-properties/name-element-parameter-xmla.md), [Value](../../../analysis-services/xmla/xml-elements-properties/value-element-parameter-xmla.md)|  
  
## <a name="remarks"></a>주의  
 일부 XMLA(XML for Analysis) 명령(예: [Process](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) 명령)은 추가 정보를 요청할 수도 있습니다. **Parameter** 요소는 XMLA 명령에 대한 청크 정보를 포함한 추가 정보를 제공하는 메커니즘을 제공합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
