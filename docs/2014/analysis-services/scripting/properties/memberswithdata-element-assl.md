---
title: MembersWithData 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MembersWithData Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MembersWithData
helpviewer_keywords:
- MembersWithData element
ms.assetid: 845087a2-b12d-4344-a8be-85ca61155296
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5c0311a774b225234aeb63d4d67680e12b693b0d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184126"
---
# <a name="memberswithdata-element-assl"></a>MembersWithData 요소(ASSL)
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*옵션만 지원*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 값은 `MembersWithData` 요소 부모 특성에만 사용 됩니다 (의 값 즉,는 [사용](usage-element-dimensionattribute-assl.md) 의 요소는 `DimensionAttribute` 로 설정 된 부모 *부모*) 확인 하려면 여부 부모 특성에서 비-리프 멤버에 대 한 데이터 멤버를 표시 합니다. 데이터 멤버에 대한 자세한 내용은 [부모-자식 계층의 특성](../../multidimensional-models/parent-child-dimension-attributes.md)을 참조하세요.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*NonLeafDataHidden*|비-리프 데이터가 숨겨집니다.|  
|*옵션만 지원*|비-리프 데이터가 표시됩니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `MembersWithData`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.MembersWithData>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [MembersWithDataCaption 요소 &#40;ASSL&#41;](caption-element-assl.md)   
 [DimensionAttribute 데이터 형식 &#40;ASSL&#41;](../data-type/dimensionattribute-data-type-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  