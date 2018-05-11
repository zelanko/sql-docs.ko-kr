---
title: BeginSession 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3f369a963c287fd2bf1c2dc82a51bb285088c8b1
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="beginsession-element-xmla"></a>BeginSession 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  SOAP 요청 메시지에서 SOAP 헤더를 사용하여 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]인스턴스에서 새 세션을 시작할 수 있습니다.  
  
 **네임스페이스** urn:schemas-microsoft-com:xml-analysis  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <BeginSession  
         xmlns="urn:schemas-microsoft-com:xml-analysis" />  
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
  
## <a name="remarks"></a>주의  
 **BeginSession** 헤더 요소는 SOAP 요청에 전송의 일부는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스 및 명시적으로 인스턴스에서 새 세션을 시작 합니다. SOAP 응답에서 반환되는 SOAP 헤더에는 새 세션을 식별하는 [Session](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md) 요소가 포함됩니다. 이 새 세션 식별자는 후속 SOAP 요청에서 **Session** 헤더 요소를 사용하여 저장 및 전송됩니다.  
  
 **BeginSession** 헤더 요소가 전송되지 않으면 세션은 명시적으로 시작되지 않습니다. 세션이 명시적으로 시작되지 않으면 해당 세션의 트랜잭션을 관리할 수 없습니다. 즉, [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md), [CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)및 [RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)XMLA(XML for Analysis) 명령을 사용할 수 없습니다. 암시적으로 시작된 세션에서 실행되는 모든 XMLA 메서드 및 명령은 원자성 트랜잭션으로 간주됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [EndSession 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)   
 [Session 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)   
 [관리 연결 및 세션 & #40; XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [헤더 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
