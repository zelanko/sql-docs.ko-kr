---
title: CubeInfo 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a1e93de452634e0f97d648e6548357cc040b9aca
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34574115"
---
# <a name="cubeinfo-element-xmla"></a>CubeInfo 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모에 포함 된 큐브 메타 데이터를 포함 [OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<OlapInfo>  
   ...  
   <CubeInfo>  
      <Cube>...</Cube>  
   </CubeInfo>  
   ...  
</OlapInfo>  
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
|부모 요소|[OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)|  
|자식 요소|[Cube](../../../analysis-services/xmla/xml-elements-properties/cube-element-olapinfo-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 **CubeInfo** 요소 하나가 포함 된 **큐브** 다차원 데이터 집합에서 참조 되는 각 큐브에 대 한 요소입니다.  
  
> [!NOTE]  
>  Analysis Services는 단일 반환 **큐브** 이 컬렉션의 요소 때문에 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 여러 큐브는 MDX (Multidimensional Expressions) 언어의 FROM 절에서 참조 하는 문을 지원 하지 않습니다.  
  
## <a name="see-also"></a>참고자료
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
