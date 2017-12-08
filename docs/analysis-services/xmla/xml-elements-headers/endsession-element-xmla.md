---
title: "EndSession 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: EndSession Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#EndSession
- urn:schemas-microsoft-com:xml-analysis#EndSession
- microsoft.xml.analysis.endsession
helpviewer_keywords: EndSession element
ms.assetid: e64f1da4-5c83-40a2-b15e-837f5451bafa
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d58ed65e574fe9055c0a5dd0be1746242e163aa8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="endsession-element-xmla"></a>EndSession 요소(XMLA)
  인스턴스에서 기존 세션을 종료 하려면 SOAP 요청 메시지의 SOAP 헤더를 사용 하 여 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
 **네임스페이스** urn:schemas-microsoft-com:xml-analysis  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <EndSession  
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
|SessionId|종료될 세션을 식별하는 필수 **String** 특성입니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 GUID(Globally Unique Identifier)를 사용하여 세션을 식별합니다.|  
  
## <a name="remarks"></a>주의  
 **EndSession** 헤더 요소는 명시적으로 시작된 된 기존 세션에서 보낸 SOAP 요청의 일부는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스. **EndSession** 헤더 요소가 전송되었지만 여기에 더 이상 유효하지 않은 세션 식별자가 포함된 경우 세션을 찾을 수 없다는 SOAP 오류가 반환됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [BeginSession 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md)   
 [Session 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)   
 [관리 연결 및 세션 &#40; XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [헤더 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
