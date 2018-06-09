---
title: 메시지를 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 21bb83be0940b806c071f305d75826ab65330c15
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34575595"
---
# <a name="messages-element-xmla"></a>Messages 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  컬렉션을 포함 [메시지](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md) 하 여 Analysis Services의 인스턴스에서 반환 된 요소는 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 또는 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드를 호출 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Resultset>  
   <Messages>  
      <Message>  
   </Messages>  
</Resultset>  
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
|부모 요소|[결과 집합](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|  
|자식 요소|[메시지](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 이 요소는 **Discover** 메서드 호출 또는 **Execute** 메서드 호출 내 단일 XMLA 명령이 성공적으로 완료되었지만 오류 또는 경고가 발생한 경우 사용됩니다. 이러한 경우에는 **메시지** 요소가 추가 되는 [루트](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) 하나 이상 포함 된 다른 모든 요소 뒤 요소 **메시지** 요소입니다. 각 **메시지** 요소가 나타내는 단일 메시지를 오류 또는 경고를 반환한는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.  
  
## <a name="see-also"></a>참고자료
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
