---
title: BeginSession 요소 (XMLA) | Microsoft Docs
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
- BeginSession Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#BeginSession
- urn:schemas-microsoft-com:xml-analysis#BeginSession
- microsoft.xml.analysis.beginsession
helpviewer_keywords:
- BeginSession element
ms.assetid: 49873a97-58d7-42a9-ab7f-e045e2856737
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cf272ae8221b66f7ac8390fab900d22d6b8aaf87
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37285829"
---
# <a name="beginsession-element-xmla"></a>BeginSession 요소(XMLA)
  SOAP 요청 메시지의 SOAP 헤더를 사용 하 여 인스턴스에서 새 세션을 시작할 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
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
 `BeginSession` 헤더 요소는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스로 보내는 SOAP 요청의 일부이며 해당 인스턴스에서 새 세션을 명시적으로 시작합니다. SOAP 응답에서 반환 된 SOAP 헤더를 포함 한 [세션](session-element-xmla.md) 새 세션을 식별 하는 요소입니다. 이 새 세션 식별자는 후속 SOAP 요청에서 `Session` 헤더 요소를 사용하여 저장 및 전송됩니다.  
  
 `BeginSession` 헤더 요소가 전송되지 않으면 세션은 명시적으로 시작되지 않습니다. 세션이 명시적으로 시작되지 않으면 해당 세션의 트랜잭션을 관리할 수 없습니다. Analysis (XMLA) 명령에 대 한 다음 XML을 사용할 수 없습니다는 즉,: [BeginTransaction](../xml-elements-commands/begintransaction-element-xmla.md)하십시오 [CommitTransaction](../xml-elements-commands/committransaction-element-xmla.md), 및 [RollbackTransaction](../xml-elements-commands/rollbacktransaction-element-xmla.md)합니다. 암시적으로 시작된 세션에서 실행되는 모든 XMLA 메서드 및 명령은 원자성 트랜잭션으로 간주됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [EndSession 요소 &#40;XMLA&#41;](endsession-element-xmla.md)   
 [Session 요소 &#40;XMLA&#41;](session-element-xmla.md)   
 [연결 및 세션 관리 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [헤더 &#40;XMLA&#41;](xml-elements-headers.md)  
  
  
