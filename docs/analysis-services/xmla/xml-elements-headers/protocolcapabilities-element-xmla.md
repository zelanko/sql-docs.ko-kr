---
title: ProtocolCapabilities 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 85ddeb22fac03e5ae7f66521ac3ca8a46e210fe7
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38021198"
---
# <a name="protocolcapabilities-element-xmla"></a>ProtocolCapabilities 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  SOAP 요청 메시지의 SOAP 헤더를 사용 하 여 Analysis Services 인스턴스와 클라이언트 응용 프로그램 간의 프로토콜 기능을 식별 합니다.  
  
 **Namespace** `http://schemas.microsoft.com/analysisservices/2003/engine`  
  
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
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[기능](../../../analysis-services/xmla/xml-elements-properties/capability-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 합니다 **ProtocolCapabilities** 요소를 사용 하면 클라이언트 응용 프로그램 이진 XML 또는 압축 지원과 같은 프로토콜 기능을 사용 하 여 협상 하는 데는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 언제 든 지 인스턴스. 프로토콜 협상에는 다음과 같은 단계가 포함됩니다.  
  
1.  클라이언트 응용 프로그램이 SOAP 헤더의 일부로 **ProtocolCapabilities** 요소를 포함하는 SOAP 요청을 전송하여 해당 프로토콜 기능을 식별합니다.  
  
2.  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스가 SOAP 요청을 받고 처리합니다.  
  
3.  경우는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스를 동일한 프로토콜 기능이 요청으로, 인스턴스를 동일한 포함 하는 SOAP 응답을 보내고 **ProtocolCapabilities** 요소가 SOAP 요청에서 전송 되었으며 프로토콜 성공적으로 협상 합니다. 그렇지 않으면 프로토콜이 성공적으로 협상되지 않으며 인스턴스가 SOAP 오류를 반환합니다.  
  
 프로토콜 기능을 얼마나 클라이언트 응용 프로그램을 성공적으로 협상 후 및 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스가 사용 하 여 특정 프로토콜 명시적 또는 암시적 세션 인지에 따라 다릅니다.  
  
-   명시적 세션은 하나를 사용 하 여 만든 합니다 [BeginSession](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md) 헤더 요소입니다. 명시적 세션의 경우 협상된 프로토콜은 클라이언트 응용 프로그램에서 새로운 **ProtocolCapabilities** 요소를 보내거나 세션이 종료될 때까지 사용됩니다.  
  
-   암시적 세션은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 의해 생성되며 클라이언트 응용 프로그램에서 SOAP 요청을 전송할 때 명시적으로 지정하지 않은 세션입니다. 암시적 세션의 경우 협상된 프로토콜은 SOAP 요청이 완료될 때까지만 사용됩니다.  
  
 프로토콜 기능은 명시적으로 협상될 필요가 없습니다. 즉 클라이언트 응용 프로그램은 SOAP 요청의 일부로 **ProtocolCapabilities** 요소를 포함하지 않아도 됩니다. SOAP 요청에 포함 되어 있지 않으면를 **ProtocolCapabilities** 요소는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스는 SOAP 요청과 동일한 형식을 사용 하 여 응답 합니다.  
  
## <a name="see-also"></a>참고자료
 [연결 및 세션 관리 &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [헤더 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
