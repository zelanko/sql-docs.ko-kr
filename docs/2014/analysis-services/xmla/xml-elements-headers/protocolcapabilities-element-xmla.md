---
title: ProtocolCapabilities 요소 (XMLA) | Microsoft Docs
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
- ProtocolCapabilities Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.protocolcapabilities
- http://schemas.microsoft.com/analysisservices/2003/engine#ProtocolCapabilities
- urn:schemas-microsoft-com:xml-analysis#ProtocolCapabilities
helpviewer_keywords:
- ProtocolCapabilities element
ms.assetid: f923896a-3f32-46a3-9543-388c30b3465d
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c4183d90d07a54cf009daec59ca29ca802f2bf67
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37295433"
---
# <a name="protocolcapabilities-element-xmla"></a>ProtocolCapabilities 요소(XMLA)
  SOAP 요청 메시지의 SOAP 헤더를 사용 하 여 인스턴스 간의 프로토콜 기능을 식별 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 클라이언트 응용 프로그램입니다.  
  
 **Namespace** http://schemas.microsoft.com/analysisservices/2003/engine  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <ProtocolCapabilities xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
         <Capability>...</Capability>  
      </ProtocolCapabilities>  
      ...  
   </soap:Header>  
   <soap:Body>  
      ...  
   </soap:Body>  
</soap:Envelope>  
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
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[기능](../xml-elements-properties/capability-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `ProtocolCapabilities` 요소는 클라이언트 응용 프로그램이 언제든지 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스로 이진 XML 또는 압축 지원과 같은 프로토콜 기능을 협상할 수 있게 해 줍니다. 프로토콜 협상에는 다음과 같은 단계가 포함됩니다.  
  
1.  포함 하는 SOAP 요청을 전송 하 여 해당 프로토콜 기능을 식별 하는 클라이언트 응용 프로그램을 `ProtocolCapabilities` 요소의 SOAP 헤더의 일부로.  
  
2.  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스가 SOAP 요청을 받고 처리합니다.  
  
3.  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 요청된 것과 동일한 프로토콜 기능이 있으면 인스턴스가 SOAP 요청에서 전송된 것과 동일한 `ProtocolCapabilities` 요소를 포함하는 SOAP 응답을 보내고 프로토콜이 성공적으로 협상됩니다. 그렇지 않으면 프로토콜이 성공적으로 협상되지 않으며 인스턴스가 SOAP 오류를 반환합니다.  
  
 프로토콜 기능을 얼마나 클라이언트 응용 프로그램을 성공적으로 협상 후 및 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스가 사용 하 여 특정 프로토콜 명시적 또는 암시적 세션 인지에 따라 다릅니다.  
  
-   명시적 세션은 하나를 사용 하 여 만든 합니다 [BeginSession](session-element-xmla.md) 헤더 요소입니다. 명시적 세션의 경우 협상된 된 프로토콜은 클라이언트 응용 프로그램에서 새 보낼 때 까지는 사용 `ProtocolCapabilities` 요소를 보내거나 세션이 종료 됩니다.  
  
-   암시적 세션은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 의해 생성되며 클라이언트 응용 프로그램에서 SOAP 요청을 전송할 때 명시적으로 지정하지 않은 세션입니다. 암시적 세션의 경우 협상된 프로토콜은 SOAP 요청이 완료될 때까지만 사용됩니다.  
  
 프로토콜 기능은 명시적으로 협상될 필요가 없습니다. 즉, 클라이언트 응용 프로그램을 하지 않아도 포함을 `ProtocolCapabilities` SOAP 요청의 일부로 요소입니다. SOAP 요청에 `ProtocolCapabilities` 요소가 포함되지 않은 경우 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스는 SOAP 요청과 동일한 형식을 사용하여 응답합니다.  
  
## <a name="see-also"></a>관련 항목  
 [연결 및 세션 관리 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [헤더 &#40;XMLA&#41;](xml-elements-headers.md)  
  
  
