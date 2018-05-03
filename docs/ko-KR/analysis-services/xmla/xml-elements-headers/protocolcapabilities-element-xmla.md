---
title: ProtocolCapabilities 요소 (XMLA) | Microsoft Docs
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
- ProtocolCapabilities Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.protocolcapabilities
- http://schemas.microsoft.com/analysisservices/2003/engine#ProtocolCapabilities
- urn:schemas-microsoft-com:xml-analysis#ProtocolCapabilities
helpviewer_keywords:
- ProtocolCapabilities element
ms.assetid: f923896a-3f32-46a3-9543-388c30b3465d
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9ac69f255b3ca09802876adb96bcfac4c9804e2a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="protocolcapabilities-element-xmla"></a>ProtocolCapabilities 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  SOAP 요청 메시지의 SOAP 헤더를 사용 하 여의 인스턴스 간의 프로토콜 기능을 식별 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 클라이언트 응용 프로그램 및입니다.  
  
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
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[기능](../../../analysis-services/xmla/xml-elements-properties/capability-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **ProtocolCapabilities** 요소를 사용 하면 클라이언트 응용 프로그램에 이진 XML 또는 압축 지원과 같은 프로토콜 기능 협상 하는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 언제 든 지 인스턴스. 프로토콜 협상에는 다음과 같은 단계가 포함됩니다.  
  
1.  클라이언트 응용 프로그램이 SOAP 헤더의 일부로 **ProtocolCapabilities** 요소를 포함하는 SOAP 요청을 전송하여 해당 프로토콜 기능을 식별합니다.  
  
2.  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스가 SOAP 요청을 받고 처리합니다.  
  
3.  경우는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 요청 된 것과 동일한 프로토콜 기능이, 인스턴스가 동일한를 포함 하는 SOAP 응답을 보냅니다 **ProtocolCapabilities** 요소가 SOAP 요청에서 전송 및 프로토콜 되었습니다. 성공적으로 협상 합니다. 그렇지 않으면 프로토콜이 성공적으로 협상되지 않으며 인스턴스가 SOAP 오류를 반환합니다.  
  
 성공적으로 협상 프로토콜을 클라이언트 응용 프로그램 시간 후 및 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에서 특정 프로토콜을 사용 하는 세션 명시적 또는 암시적 인지에 따라 달라 집니다.  
  
-   명시적 세션의 하나를 사용 하 여 만든이 [BeginSession](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md) 헤더 요소입니다. 명시적 세션의 경우 협상된 프로토콜은 클라이언트 응용 프로그램에서 새로운 **ProtocolCapabilities** 요소를 보내거나 세션이 종료될 때까지 사용됩니다.  
  
-   암시적 세션은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 의해 생성되며 클라이언트 응용 프로그램에서 SOAP 요청을 전송할 때 명시적으로 지정하지 않은 세션입니다. 암시적 세션의 경우 협상된 프로토콜은 SOAP 요청이 완료될 때까지만 사용됩니다.  
  
 프로토콜 기능은 명시적으로 협상될 필요가 없습니다. 즉 클라이언트 응용 프로그램은 SOAP 요청의 일부로 **ProtocolCapabilities** 요소를 포함하지 않아도 됩니다. SOAP 요청에 포함 되어 있지 않으면는 **ProtocolCapabilities** 요소는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스는 동일한 형식을 사용 하 여 SOAP 요청에 응답 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [관리 연결 및 세션 & #40; XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [헤더 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
