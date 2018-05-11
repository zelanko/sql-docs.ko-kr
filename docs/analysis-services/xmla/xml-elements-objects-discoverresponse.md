---
title: DiscoverResponse 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b2a581b447831dfb25d345923d4e0e1cbdaf517b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="xml-elements---objects---discoverresponse"></a>XML 요소 개체-DiscoverResponse
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  인스턴스에서 반환한 정보를 포함 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 대 한 응답에는 [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드를 호출 합니다.  
  
 **네임스페이스** urn:schemas-microsoft-com:xml-analysis  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DiscoverResponse>  
   <return>  
</DiscoverResponse>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타날 수 있는 필수 요소.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[반환](../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **DiscoverResponse** 요소에 대 한 SOAP 응답의 본문 내에 있는 최상위 요소는는 **Discover** 메서드.  
  
## <a name="see-also"></a>관련 항목:  
 [ExecuteResponse 요소 &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-objects-executeresponse.md)   
 [개체 &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-objects.md)  
  
  
