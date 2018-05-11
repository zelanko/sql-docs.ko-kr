---
title: ID 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 950b8a9221580ad359f10ebf5a43dcda66da009b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="id-element-xmla"></a>ID 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모 실행할 잠금을 식별 [잠금](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) 또는 [잠금 해제](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Lock> <!-- or Unlock>  
   ...  
   <ID>...</ID>  
   ...  
</Lock>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[잠금](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md), [잠금 해제](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **ID** 요소는 잠금을 식별 하는 데 사용 전역 고유 식별자 (GUID)를 포함 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Object 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [Mode 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md)   
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
