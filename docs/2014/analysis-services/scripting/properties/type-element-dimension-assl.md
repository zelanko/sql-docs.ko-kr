---
title: E Element (Dimension) (ASSL) | Microsoft Docs
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
- Type Element (Dimension)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 6a2798b1-26c7-49d8-b556-e681c69d9574
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 582d5b2052f2681630c5f0cd86facacd5e7cfc91
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089395"
---
# <a name="type-element-dimension-assl"></a>Type 요소(Dimension)(ASSL)
  차원의 내용에 대한 정보를 제공합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Dimension>  
      ...  
   <Type>...</Type>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*일반*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Dimension](../objects/dimension-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 에 대 한 일부 값 `Type`, 예를 들어 *계정*, 특정 동작을 결정 합니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*일반*|차원이 일반 차원입니다.|  
|*Time*|차원이 시간 차원입니다. **참고:** 이 값은 차원이 시간 차원에 고유한 기능을 지원함을 나타냅니다.|  
|*Geography*|차원이 지리적 특성을 포함합니다.|  
|*조직*|차원이 조직적 특성을 포함합니다.|  
|*BillOfMaterials*|차원이 제품 구성 정보(BOM) 특성을 포함합니다.|  
|*계정*|차원이 계정 관련 특성을 포함합니다. **참고:** 이 값은 차원이 계정 차원과 관련 된 기능을 지원함을 나타냅니다.|  
|*고객*|차원이 고객 관련 특성을 포함합니다.|  
|*제품*|차원이 제품 관련 특성을 포함합니다.|  
|*시나리오*|차원이 시나리오 관련 특성을 포함합니다.|  
|*정량*|차원이 정량 특성을 포함합니다.|  
|*유틸리티*|차원이 유틸리티 특성을 포함합니다.|  
|*통화*|차원이 통화 특성을 포함합니다.|  
|*속도*|차원이 환율 특성을 포함합니다.|  
|*채널*|차원이 채널 특성을 포함합니다.|  
|*프로 모션*|차원이 홍보 행사 관련 특성을 포함합니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `Type`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.DimensionType>입니다.  
  
 부모에 해당 하는 요소 `Type` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Dimension>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  