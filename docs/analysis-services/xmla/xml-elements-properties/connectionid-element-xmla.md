---
title: ConnectionID 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0c4aeb71b62ac75647e29bb822e0fd29f05b3722
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="connectionid-element-xmla"></a>ConnectionID 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모를 실행할 활성 연결 식별 [취소](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cancel>  
   ...  
   <ConnectionID>...</ConnectionID>  
   ...  
</Cancel>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|정수|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[취소](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
  
## <a name="see-also"></a>참고 항목  
 [CancelAssociated 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/cancelassociated-element-xmla.md)   
 [SessionID 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/sessionid-element-xmla.md)   
 [SPID 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/spid-element-xmla.md)   
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
