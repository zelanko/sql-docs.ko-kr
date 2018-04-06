---
title: Restrictions 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Restrictions Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Restrictions
- http://schemas.microsoft.com/analysisservices/2003/engine#Restrictions
- microsoft.xml.analysis.restrictions
helpviewer_keywords:
- Restrictions element
ms.assetid: e745ce13-b468-4372-a6f0-0da3d772dda3
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 704906a3b42557feace9c75ce5f2702be553ff08
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="restrictions-element-xmla"></a>Restrictions 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]제한 열 및 사용 하는 데이터가 포함 된 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Discover>  
...  
   <Restrictions>  
      <RestrictionList>...</RestrictionList>  
   </Restrictions>  
...  
</Discover>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[검색](../../../analysis-services/xmla/xml-elements-methods-discover.md)|  
|자식 요소|[RestrictionList](../../../analysis-services/xmla/xml-elements-properties/restrictionlist-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **제한** 제한 열 및 검색 정보를 제한 하는 데 사용 되는 데이터 요소를 나타내는 **Discover** 메서드.  
  
## <a name="example"></a>예제  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <RequestType>DISCOVER_PROPERTIES</RequestType>  
   <Restrictions>  
      <RestrictionList xmlns="urn:schemas-microsoft-com:xml-analysis">  
         <PropertyName>Catalog</PropertyName>  
      </RestrictionList>  
   </Restrictions>  
   <Properties />  
</Discover>  
```  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
