---
title: "ManufacturingFirstMonth 요소 (ASSL) | Microsoft Docs"
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
apiname: ManufacturingFirstMonth Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ManufacturingFirstMonth
helpviewer_keywords: ManufacturingFirstMonth element
ms.assetid: 3b2fb440-662b-4d88-a133-1e098b9c8169
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c97e22a886bac40463dc3cac320e9260494bc35e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="manufacturingfirstmonth-element-assl"></a>ManufacturingFirstMonth 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]에 대 한 첫 번째 제조 월을 정의 [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<TimeBinding>  
   ...  
   <ManufacturingFirstMonth>...</ManufacturingFirstMonth>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Integer(1부터 12까지, 여기서 1은 1월이고 12는 12월)|  
|기본값|**1**|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **ManufacturingFirstMonth** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.TimeBinding>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
