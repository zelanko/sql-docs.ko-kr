---
title: MemberUniqueNameStyle 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0c79a42cc8958c4c1dfa9ad7174e991a39620ff3
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="memberuniquenamestyle-element-assl"></a>MemberUniqueNameStyle 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  얼마나 고유한 이름을 결정에 포함 된 계층의 멤버에 대해 생성 되는 [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubeDimension>  
   ...  
   <MemberUniqueNameStyle>...</MemberUniqueNameStyle>  
   ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*네이티브*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*네이티브*|인스턴스에서 자동으로 멤버의 고유한 이름을 결정합니다.|  
|*NamePath*|인스턴스에서 각 수준과 멤버의 캡션으로 구성된 복합 이름을 생성합니다.|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **MemberUniqueNameStyle** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CubeDimension>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Cube 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Dimension 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [CubeDimension 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)  
  
  
