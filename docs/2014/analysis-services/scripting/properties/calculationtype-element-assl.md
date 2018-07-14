---
title: CalculationType 요소 (ASSL) | Microsoft Docs
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
- CalculationType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CalculationType
helpviewer_keywords:
- CalculationType element
ms.assetid: b974b3d3-fbf7-4d77-8f6e-4e05a258fe84
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 24e8f95af2ab7eb8be754eb2d1c7de96fee91ea7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37275939"
---
# <a name="calculationtype-element-assl"></a>CalculationType 요소(ASSL)
  연결에 정의 된 계산 유형을 설명 [CalculationProperty](../objects/calculationproperty-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CalculationProperty>  
   ...  
   <CalculationType>...</CalculationType>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CalculationProperty](../objects/calculationproperty-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*멤버*|계산 속성이 계산 멤버 정의에 적용됩니다.|  
|*설정*|계산 속성이 명명된 집합 정의에 적용됩니다.|  
|*셀*|계산 속성이 계산 셀 정의에 적용됩니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `CalculationType`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.CalculationType>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [CalculationProperties 요소 &#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [MdxScript 요소 &#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [MdxScripts 요소 &#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
