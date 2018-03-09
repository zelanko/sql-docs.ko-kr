---
title: "RefreshPolicy 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: RefreshPolicy Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: RefreshPolicy
helpviewer_keywords: RefreshPolicy element
ms.assetid: f4c36280-1a39-4f1c-a3ab-fbeb81742d6d
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2f2d8598e588f65799df46a3b5e60c2f027f8861
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="refreshpolicy-element-assl"></a>RefreshPolicy 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]빈도 결정 차원 또는 측정값 그룹의 동적 부분 (에 지정 된 대로 [지 속성](../../../analysis-services/scripting/properties/persistence-element-assl.md) 요소)의 변경 사항을 검사 합니다.  
  
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
|기본값|아래 표를 참조 합니다.|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
|상위 항목 또는 부모|기본값|  
|------------------------|-------------------|  
|[DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)|*ByQuery*|  
|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|InclusionThresholdSetting|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*ByQuery*|모든 쿼리에서 원본 데이터가 변경되었는지 검사합니다.|  
|*ByInterval*|원본 데이터에서 지정 된 간격에 변경 내용에 대 한 검사만 [RefreshInterval](../../../analysis-services/scripting/properties/refreshinterval-element-assl.md)합니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **RefreshPolicy** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.RefreshPolicy>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Persistence 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/persistence-element-assl.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
