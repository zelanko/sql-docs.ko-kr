---
title: RequestType 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 63c1a838d74745b5ef51f73b51e34c95e08a81ff
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37994795"
---
# <a name="requesttype-element-xmla"></a>RequestType 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  반환 된 메타 데이터의 형식을 결정 합니다 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Discover>  
   ...  
   <RequestType>...</RequestType>  
   ...  
</Discover>  
```  
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[검색](../../../analysis-services/xmla/xml-elements-methods-discover.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **RequestType** 요소는 스키마 행 집합을 결정 합니다 **검색** 메서드 데이터를 반환 합니다. 이 열거형은 Analysis Services에서 지 원하는 스키마 행 집합의 이름으로 제한 합니다. 스키마 행 집합에 대 한 자세한 내용은 참조 하세요. [Analysis Services 스키마 행 집합](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)합니다.  
  
> [!NOTE]  
>  합니다 **RequestType** 요소는 스키마 행 집합 이름만 열거 합니다. 스키마 행 집합 GUID를 사용하면 오류가 발생합니다.  
  
## <a name="see-also"></a>참고자료
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
