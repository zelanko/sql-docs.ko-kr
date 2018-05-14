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
ms.openlocfilehash: 92e9fa83f19384276abd7401fd809a56187c75b7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
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
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ProtocolCapabilities](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **기능** 요소를 포함 하는 응용 프로그램 이진 또는 압축과 같은 특정 기능이 지원 됨을 나타냅니다는 **ProtocolCapabilities** 헤더 요소에는 인스턴스에서 또는 SOAP 요청의 SOAP 헤더 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 포함는 **ProtocolCapabilities** SOAP 응답의 SOAP 헤더에 헤더 요소입니다. **Capability** 요소의 값은 지원될 기능의 이름입니다.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]는 다음 표에 나열된 기능을 지원합니다.  
  
|기능 이름|설명|  
|---------------------|-----------------|  
|sx|이진 XML 지원|  
|xpress|압축 지원|  
  
## <a name="see-also"></a>관련 항목:  
 [관리 연결 및 세션 & #40; XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
