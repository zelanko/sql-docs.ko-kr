---
title: "Session 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Session Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.session
- http://schemas.microsoft.com/analysisservices/2003/engine#Session
- urn:schemas-microsoft-com:xml-analysis#Session
helpviewer_keywords:
- Session element
ms.assetid: 884ed090-968e-41d3-97e5-6d12787467da
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aa1f136ee02b73ab792dae7ee7730a3917dace66
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="session-element-xmla"></a>Session 요소(XMLA)
  인스턴스에서 기존의 명시적 세션을 식별 하는 SOAP 요청 메시지에 SOAP 헤더를 사용 하 여 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
 **네임스페이스** urn:schemas-microsoft-com:xml-analysis  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <Session  
         xmlns="urn:schemas-microsoft-com:xml-analysis"  
         SessionId="string" />  
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
|자식 요소|없음|  
  
## <a name="attributes"></a>특성  
  
|Attribute|설명|  
|---------------|-----------------|  
|SessionId|사용될 세션을 식별하는 필수 **String** 특성입니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 GUID(Globally Unique Identifier)를 사용하여 세션을 식별합니다.|  
  
## <a name="remarks"></a>주의  
 **세션** 헤더 요소에 명시적으로 시작된 된 기존 세션을 식별 하는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스. **Session** 요소는 다음 메시지 유형에서 SOAP 헤더의 일부입니다.  
  
-   포함 하는 SOAP 응답은 [BeginSession](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md) SOAP 헤더 요소입니다.  
  
-   실행할 세션을 식별 하는 SOAP 요청에서 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 또는 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드.  
  
 세션 식별자는 세션이 계속 유효한 상태로 유지됨을 보장하지 않습니다. **Session** 요소에 지정된 세션은 만료될 수 있습니다. 예를 들어 세션의 시간이 초과되거나 세션 관련 연결이 끊어지면 세션이 만료될 수 있습니다. 세션이 만료되어 더 이상 유효하지 않으면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]는 세션을 종료하고 현재 처리 중인 모든 트랜잭션을 롤백합니다. 더 이상 유효하지 않은 세션 식별자로 전송된 모든 SOAP 메시지는 지정된 세션을 찾을 수 없다는 SOAP 오류와 함께 실패합니다.  
  
 경우는 **세션** 요소가 SOAP 요청의 일부로 전송 되지 않으면는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스 기간 동안 세션을 암시적으로 시작 된 **Discover** 또는 **Execute** 메서드 호출에서 한 다음 메서드 호출이 완료 되 면 해당 세션을 종료 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [EndSession 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)   
 [관리 연결 및 세션 &#40; XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [헤더 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  

