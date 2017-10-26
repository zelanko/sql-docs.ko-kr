---
title: E Element (Dimension) (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Type Element (Dimension)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 6a2798b1-26c7-49d8-b556-e681c69d9574
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 868851d8eeeb72b4d35a7568a93c5ea7467d8204
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*일반*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **Type**의 일부 값(예: *Accounts*)은 특정 동작을 결정합니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*일반*|차원이 일반 차원입니다.|  
|*Time*|차원이 시간 차원입니다.<br /><br /> 참고:이 값은 차원이 시간 차원에 고유한 기능을 지원함 나타냅니다.|  
|*Geography*|차원이 지리적 특성을 포함합니다.|  
|*조직*|차원이 조직적 특성을 포함합니다.|  
|*BillOfMaterials*|차원이 제품 구성 정보(BOM) 특성을 포함합니다.|  
|*계정*|차원이 계정 관련 특성을 포함합니다.<br /><br /> 참고:이 값은 차원이 계정 차원과 관련 된 기능을 지원함 나타냅니다.|  
|*고객*|차원이 고객 관련 특성을 포함합니다.|  
|*제품*|차원이 제품 관련 특성을 포함합니다.|  
|*시나리오*|차원이 시나리오 관련 특성을 포함합니다.|  
|*정량*|차원이 정량 특성을 포함합니다.|  
|*유틸리티*|차원이 유틸리티 특성을 포함합니다.|  
|*통화*|차원이 통화 특성을 포함합니다.|  
|*속도*|차원이 환율 특성을 포함합니다.|  
|*채널*|차원이 채널 특성을 포함합니다.|  
|*프로 모션*|차원이 홍보 행사 관련 특성을 포함합니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **형식** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.DimensionType>합니다.  
  
 부모에 해당 하는 요소 **형식** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Dimension>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

