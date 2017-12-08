---
title: "return 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
apiname: return Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.return
- http://schemas.microsoft.com/analysisservices/2003/engine#return
- urn:schemas-microsoft-com:xml-analysis#return
helpviewer_keywords: return element
ms.assetid: 3cfe8b74-fec3-4987-a74a-5f731444e024
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6fb9f422df762c370f800cdc6f6dcef799d3fa77
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="return-element-xmla"></a>return 요소(XMLA)
  반환 된 정보를 포함 한 [DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md) 요소에 대 한 응답에는 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드 호출 또는 [ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md) 요소에 대 한 응답에는 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드 호출 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DiscoverResponse> <!-- or ExecuteResponse -->  
   <return>  
      <root>...</root>  
      <!-- or -->  
      <results>...</results> <!-- ExecuteResponse only -->  
   </return>  
</DiscoverResponse>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md), [ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)|  
|자식 요소|아래 표를 참조 합니다.|  
  
|상위 항목|자식 요소|  
|--------------|--------------------|  
|[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)|[루트](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|[ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)|[루트](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) 또는 [결과](../../../analysis-services/xmla/xml-elements-properties/results-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **반환** 에서 반환 된 데이터를 포함 하는 요소는 **Discover** 및 **Execute** 메서드. 일반적으로 **반환** 하나를 포함 하는 요소 **루트** 성공적인에서 반환 된 데이터를 포함 하는 요소 **Discover** 또는 **Execute** 메서드 호출 또는 XML for Analysis (XMLA) 예외는 실패 한 메서드 호출에서 반환 합니다. 경우는 **Execute** 메서드에 포함 되어는 **일괄 처리** 여러 작업을 수행 하는 명령을 **반환** 요소를 포함 한 **결과** 차례로 하나를 포함 하는 요소 **루트** 실행에서 성공 또는 실패 한 각 명령에 대 한 요소는 **일괄 처리** 명령입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
