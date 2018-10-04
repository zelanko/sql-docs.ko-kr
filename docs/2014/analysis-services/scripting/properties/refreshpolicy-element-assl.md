---
title: RefreshPolicy 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6322c725a0c4b339425b9cc9e10aa6596c9fc34c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48144433"
---
# <a name="refreshpolicy-element-assl"></a>RefreshPolicy 요소(ASSL)
  빈도 결정 차원 또는 측정값 그룹의 동적 부분 (지정 된 대로 합니다 [지 속성](persistence-element-assl.md) 요소) 변경 내용을 확인 하는 합니다.  
  
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
|[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|없음|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionBinding](../data-type/binding-data-type-assl.md), [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*ByQuery*|모든 쿼리에서 원본 데이터가 변경되었는지 검사합니다.|  
|*ByInterval*|원본 데이터는 으로만 변경 사항을 검사 하 여 지정 된 간격 [RefreshInterval](refreshinterval-element-assl.md)합니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `RefreshPolicy`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.RefreshPolicy>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Persistence 요소 &#40;ASSL&#41;](persistence-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
