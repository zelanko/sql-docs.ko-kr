---
title: Restrictions 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d79e3b88fd428005d1939a90b80b2753137eaf05
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="restrictions-element-xmla"></a>Restrictions 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  제한 열 및 사용 하는 데이터가 포함 된 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드.  
  
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
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
  
## <a name="see-also"></a>참고 항목  
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
