---
title: Exception 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e5b9847f1328fb0f0c7b6c1503708ca0b75b585c
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="exception-element-xmla"></a>Exception 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  예외가 반환 되었음을 나타냅니다는 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 또는 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드를 호출 합니다.  
  
 **Namespace** `http://schemas.microsoft.com/analysisservices/2003/exception`  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<root>  
   ...  
   <Exception />  
   ...  
</root>  
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
|부모 요소|[루트](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **Discover** 메서드 호출 또는 **Execute** 메서드 호출의 단일 XMLA 명령을 실행하는 중에 메서드나 명령이 완료되지 못하게 하는 오류가 발생하면 해당 명령 또는 메서드에 대한 **root** 요소에 **Exception** 요소와 **Messages** 요소가 포함됩니다. **Exception** 요소는 메서드 또는 명령이 실행되지 못하게 하는 오류가 발생했음을 나타내며 **Messages** 요소는 오류 목록 또는 해당 오류와 관련된 경고 메시지를 포함합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [요소를 메시지 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md)   
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
