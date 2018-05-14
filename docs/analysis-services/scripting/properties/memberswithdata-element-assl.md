---
title: MembersWithData 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a8e777d22a6e87fa111f5c3fead76b0ed24b854e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="memberswithdata-element-assl"></a>MembersWithData 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  비-리프 멤버에 대한 데이터 멤버를 부모 특성에 표시할지 여부를 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <MembersWithData>...</MembersWithData>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*옵션만 지원*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 값은 **MembersWithData** 요소 부모 특성에만 사용 됩니다 (의 값 즉,는 [사용량](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) 의 요소는 **DimensionAttribute** 부모 요소 로 설정 되어 *부모*) 비-리프 멤버에 대 한 데이터 멤버를 부모 특성의 표시 여부를 결정 합니다. 데이터 멤버에 대한 자세한 내용은 [부모-자식 계층의 특성](../../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md)을 참조하세요.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*NonLeafDataHidden*|비-리프 데이터가 숨겨집니다.|  
|*옵션만 지원*|비-리프 데이터가 표시됩니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **MembersWithData** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MembersWithData>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [MembersWithDataCaption 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/memberswithdatacaption-element-assl.md)   
 [DimensionAttribute 데이터 형식 &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
