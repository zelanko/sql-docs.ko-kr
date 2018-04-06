---
title: 요소 (ASSL) 기본 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Default Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DEFAULT
helpviewer_keywords:
- Default element
ms.assetid: 02c1844c-51fb-44fe-aafb-001e53ad293c
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 598c483bce16630e2f07d3edc575324fe5804596
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="default-element-assl"></a>Default 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]결정 여부는 [DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md) 이 기본 드릴스루 동작 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DrillThroughAction>  
   ...  
   <Default>...</Default  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|**False**|  
|카디널리티|0-1: 한 번만 나타나는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **기본** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.DrillThroughAction>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
