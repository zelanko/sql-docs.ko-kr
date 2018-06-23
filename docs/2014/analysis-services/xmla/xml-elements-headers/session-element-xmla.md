---
title: Session 요소 (XMLA) | Microsoft Docs
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
- Session Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.session
- http://schemas.microsoft.com/analysisservices/2003/engine#Session
- urn:schemas-microsoft-com:xml-analysis#Session
helpviewer_keywords:
- Session element
ms.assetid: 884ed090-968e-41d3-97e5-6d12787467da
caps.latest.revision: 15
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 4be4778be16da0271e2f46643a165864d679e8ff
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092731"
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="attributes"></a>특성  
  
|attribute|Description|  
|---------------|-----------------|  
|SessionId|사용될 세션을 식별하는 필수 `String` 특성입니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 GUID(Globally Unique Identifier)를 사용하여 세션을 식별합니다.|  
  
## <a name="remarks"></a>Remarks  
 `Session` 헤더 요소는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에서 명시적으로 시작된 기존 세션을 식별합니다. `Session` 요소는 다음 메시지 유형에서 SOAP 헤더의 일부입니다.  
  
-   포함 하는 SOAP 응답은 [BeginSession](session-element-xmla.md) SOAP 헤더 요소입니다.  
  
-   실행할 세션을 식별 하는 SOAP 요청에서 [Discover](../xml-elements-methods-discover.md) 또는 [Execute](../xml-elements-methods-execute.md) 메서드.  
  
 세션 식별자는 세션이 계속 유효한 상태로 유지됨을 보장하지 않습니다. `Session` 요소에 지정된 세션은 만료될 수 있습니다. 예를 들어 세션의 시간이 초과되거나 세션 관련 연결이 끊어지면 세션이 만료될 수 있습니다. 세션이 만료되어 더 이상 유효하지 않으면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]는 세션을 종료하고 현재 처리 중인 모든 트랜잭션을 롤백합니다. 더 이상 유효하지 않은 세션 식별자로 전송된 모든 SOAP 메시지는 지정된 세션을 찾을 수 없다는 SOAP 오류와 함께 실패합니다.  
  
 `Session` 요소가 SOAP 요청의 일부로 전송되지 않으면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스는 `Discover` 또는 `Execute` 메서드 호출 기간 동안 세션을 암시적으로 시작한 다음 메서드 호출이 완료되면 해당 세션을 종료합니다.  
  
## <a name="see-also"></a>관련 항목  
 [EndSession 요소 &#40;XMLA&#41;](endsession-element-xmla.md)   
 [연결 및 세션 관리 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [헤더 &#40;XMLA&#41;](xml-elements-headers.md)  
  
  