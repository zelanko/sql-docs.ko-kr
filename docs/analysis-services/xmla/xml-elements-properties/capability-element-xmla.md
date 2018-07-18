---
title: Capability 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
ms.openlocfilehash: dca8f668f64ab8ced157cf817be1f9f8f6390133
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38062981"
---
# <a name="capability-element-xmla"></a>Capability 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모 [ProtocolCapabilities](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md) 머리글 요소에서의 프로토콜 기능에 대한 지원을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ProtocolCapabilities>  
   ...  
   <Capability>...</Capability>  
   ...  
</ProtocolCapabilities>  
```  
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ProtocolCapabilities](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **기능** 요소는 이진 또는 압축과 같은 특정 기능이 포함 된 응용 프로그램에서 지원 되는지 나타냅니다 합니다 **ProtocolCapabilities** 헤더 요소에는 포함 된 Analysis Services의 인스턴스에 의해 또는 SOAP 요청의 SOAP 헤더를 **ProtocolCapabilities** SOAP 응답의 SOAP 헤더에 있습니다. **Capability** 요소의 값은 지원될 기능의 이름입니다.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]는 다음 표에 나열된 기능을 지원합니다.  
  
|기능 이름|Description|  
|---------------------|-----------------|  
|sx|이진 XML 지원|  
|xpress|압축 지원|  
  
## <a name="see-also"></a>참고자료
 [연결 및 세션 관리 &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
