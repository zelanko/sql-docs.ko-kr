---
title: RefreshPolicy 요소 (ASSL) | Microsoft Docs
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
- RefreshPolicy Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RefreshPolicy
helpviewer_keywords:
- RefreshPolicy element
ms.assetid: f4c36280-1a39-4f1c-a3ab-fbeb81742d6d
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6d2dc0549eb8151f93c817e9e59bc1a8990fac87
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36078639"
---
# <a name="refreshpolicy-element-assl"></a>RefreshPolicy 요소(ASSL)
  빈도 결정 차원 또는 측정값 그룹의 동적 부분 (에 지정 된 대로 [지 속성](persistence-element-assl.md) 요소)의 변경 사항을 검사 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionBinding> <!-- or MeasureGroupBinding -->  
   ...  
   <RefreshPolicy>...</RefreshPolicy>  
   ...  
</DimensionBinding>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
|상위 항목 또는 부모|기본값|  
|------------------------|-------------------|  
|[DimensionBinding](../data-type/binding-data-type-assl.md)|*ByQuery*|  
|[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|InclusionThresholdSetting|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionBinding](../data-type/binding-data-type-assl.md), [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*ByQuery*|모든 쿼리에서 원본 데이터가 변경되었는지 검사합니다.|  
|*ByInterval*|원본 데이터에서 지정 된 간격에 변경 내용에 대 한 검사만 [RefreshInterval](refreshinterval-element-assl.md)합니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `RefreshPolicy`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.RefreshPolicy>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Persistence 요소 &#40;ASSL&#41;](persistence-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  