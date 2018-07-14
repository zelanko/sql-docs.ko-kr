---
title: DiscoverResponse 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DiscoverResponse Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#DiscoverResponse
- microsoft.xml.analysis.discoverresponse
- urn:schemas-microsoft-com:xml-analysis#DiscoverResponse
helpviewer_keywords:
- DiscoverResponse element
ms.assetid: 20e10a82-dbd1-4ead-b92d-f84b4b2f10c6
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 61552da233cdcd405fc9d0e07ecc93e186295422
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180816"
---
# <a name="discoverresponse-element-xmla"></a>DiscoverResponse 요소(XMLA)
  인스턴스에서 반환한 정보를 포함 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 대 한 응답을 [Discover](xml-elements-methods-discover.md) 메서드를 호출 합니다.  
  
 **네임스페이스** urn:schemas-microsoft-com:xml-analysis  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DiscoverResponse>  
   <return>  
</DiscoverResponse>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[반환](xml-elements-properties/return-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `DiscoverResponse` 요소는 `Discover` 메서드에 대한 SOAP 응답의 본문 내에 있는 최상위 요소입니다.  
  
## <a name="see-also"></a>관련 항목  
 [ExecuteResponse 요소 &#40;XMLA&#41;](xml-elements-objects-executeresponse.md)   
 [개체 &#40;XMLA&#41;](xml-elements-objects.md)  
  
  
