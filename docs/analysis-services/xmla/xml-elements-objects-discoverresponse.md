---
title: "DiscoverResponse 요소 (XMLA) | Microsoft Docs"
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
- DiscoverResponse Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#DiscoverResponse
- microsoft.xml.analysis.discoverresponse
- urn:schemas-microsoft-com:xml-analysis#DiscoverResponse
helpviewer_keywords:
- DiscoverResponse element
ms.assetid: 20e10a82-dbd1-4ead-b92d-f84b4b2f10c6
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8d2483f4a610d1234277f5c686e71eb37266d124
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="xml-elements---objects---discoverresponse"></a>XML 요소 개체-DiscoverResponse
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
 [ExecuteResponse 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-objects-executeresponse.md)   
 [개체 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-objects.md)  
  
  
