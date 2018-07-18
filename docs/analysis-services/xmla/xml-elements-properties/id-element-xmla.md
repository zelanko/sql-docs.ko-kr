---
title: ID 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 18c0a9e1db03ef30b54b788d16223e70bc9e9059
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38037031"
---
# <a name="id-element-xmla"></a>ID 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모를 실행할 잠금을 식별 [잠금](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) 하거나 [Unlock](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Lock> <!-- or Unlock>  
   ...  
   <ID>...</ID>  
   ...  
</Lock>  
```  
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[잠금을](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md), [잠금 해제](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 합니다 **ID** 요소는 잠금을 식별 하는 데는 전역적으로 고유 식별자 (GUID)를 포함 합니다.  
  
## <a name="see-also"></a>참고자료
 [개체 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [Mode 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md)   
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
