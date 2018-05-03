---
title: 메시지를 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Messages Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Messages
- microsoft.xml.analysis.messages
- urn:schemas-microsoft-com:xml-analysis#Messages
helpviewer_keywords:
- Messages element
ms.assetid: 719d15ff-f18b-4c56-80ba-a9114c0b7d8a
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7c144687245db3c4ed5869d86c74d5848667e745
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="messages-element-xmla"></a>Messages 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  컬렉션을 포함 [메시지](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md) 요소에서의 인스턴스로 반환 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 여는 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 또는 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드 호출 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Resultset>  
   <Messages>  
      <Message>  
   </Messages>  
</Resultset>  
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
|부모 요소|[결과 집합](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|  
|자식 요소|[메시지](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 이 요소는 **Discover** 메서드 호출 또는 **Execute** 메서드 호출 내 단일 XMLA 명령이 성공적으로 완료되었지만 오류 또는 경고가 발생한 경우 사용됩니다. 이러한 경우에는 **메시지** 요소가 추가 되는 [루트](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) 하나 이상 포함 된 다른 모든 요소 뒤 요소 **메시지** 요소입니다. 각 **메시지** 요소가 나타내는 단일 메시지를 오류 또는 경고를 반환한는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
