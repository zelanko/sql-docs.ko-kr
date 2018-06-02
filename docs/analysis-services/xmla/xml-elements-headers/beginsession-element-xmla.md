---
title: BeginSession 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 34bdcfb37eaf5e2f960b7ea282c2628eca91916f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34574845"
---
# <a name="beginsession-element-xmla"></a>BeginSession 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  SOAP 요청 메시지의 SOAP 헤더를 사용 하 여 Analysis Services의 인스턴스에서 새 세션을 시작 합니다.  
  
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
  
## <a name="remarks"></a>Remarks  
 **BeginSession** 헤더 요소는 SOAP 요청에 전송의 일부는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스 및 명시적으로 인스턴스에서 새 세션을 시작 합니다. SOAP 응답에서 반환 되는 SOAP 헤더를 포함 한 [세션](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md) 새 세션을 식별 하는 요소입니다. 이 새 세션 식별자는 후속 SOAP 요청에서 **Session** 헤더 요소를 사용하여 저장 및 전송됩니다.  
  
 **BeginSession** 헤더 요소가 전송되지 않으면 세션은 명시적으로 시작되지 않습니다. 세션이 명시적으로 시작되지 않으면 해당 세션의 트랜잭션을 관리할 수 없습니다. 즉, Analysis (XMLA) 명령에 대 한 다음과 같은 XML를 사용할 수 없습니다: [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md), [CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md), 및 [RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)합니다. 암시적으로 시작된 세션에서 실행되는 모든 XMLA 메서드 및 명령은 원자성 트랜잭션으로 간주됩니다.  
  
## <a name="see-also"></a>참고자료
 [EndSession 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)   
 [Session 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)   
 [연결 및 세션 관리 &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [헤더 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
