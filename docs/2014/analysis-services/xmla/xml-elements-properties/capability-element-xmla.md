---
title: Capability 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Capability Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Capability
- http://schemas.microsoft.com/analysisservices/2003/engine#Capability
- microsoft.xml.analysis.capability
helpviewer_keywords:
- Capability element
ms.assetid: 544a733e-77fc-48a0-8f92-9cd1fdbcf824
caps.latest.revision: 16
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 7fd495ff0abf921b377526f6030d5207d962e1bd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088911"
---
# <a name="capability-element-xmla"></a>Capability 요소(XMLA)
  부모 [ProtocolCapabilities](../xml-elements-headers/protocolcapabilities-element-xmla.md) 머리글 요소에서의 프로토콜 기능에 대한 지원을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ProtocolCapabilities>  
   ...  
   <Capability>...</Capability>  
   ...  
</ProtocolCapabilities>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ProtocolCapabilities](../xml-elements-headers/protocolcapabilities-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Capability` 요소는 이진 또는 압축과 같은 특정 기능이 SOAP 요청의 SOAP 헤더에 `ProtocolCapabilities` 머리글 요소를 포함하는 응용 프로그램에 의해 지원되는지, 아니면 SOAP 응답의 SOAP 헤더에 `ProtocolCapabilities` 머리글 요소를 포함하는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 의해 지원되는지를 나타냅니다. `Capability` 요소의 값은 지원될 기능의 이름입니다.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]는 다음 표에 나열된 기능을 지원합니다.  
  
|기능 이름|Description|  
|---------------------|-----------------|  
|sx|이진 XML 지원|  
|xpress|압축 지원|  
  
## <a name="see-also"></a>관련 항목  
 [연결 및 세션 관리 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  