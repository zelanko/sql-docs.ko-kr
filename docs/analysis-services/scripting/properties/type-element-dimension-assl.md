---
title: E Element (Dimension) (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3af3168c39f685702154bb7c76435bd1d241a642
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="type-element-dimension-assl"></a>Type 요소(Dimension)(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|기본값|*Regular*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[차원](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **Type**의 일부 값(예: *Accounts*)은 특정 동작을 결정합니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*Regular*|차원이 일반 차원입니다.|  
|*Time*|차원이 시간 차원입니다.<br /><br /> 참고:이 값은 차원이 시간 차원에 고유한 기능을 지원함 나타냅니다.|  
|*지리*|차원이 지리적 특성을 포함합니다.|  
|*조직*|차원이 조직적 특성을 포함합니다.|  
|*BillOfMaterials*|차원이 제품 구성 정보(BOM) 특성을 포함합니다.|  
|*계정*|차원이 계정 관련 특성을 포함합니다.<br /><br /> 참고:이 값은 차원이 계정 차원과 관련 된 기능을 지원함 나타냅니다.|  
|*고객*|차원이 고객 관련 특성을 포함합니다.|  
|*제품*|차원이 제품 관련 특성을 포함합니다.|  
|*시나리오*|차원이 시나리오 관련 특성을 포함합니다.|  
|*정량*|차원이 정량 특성을 포함합니다.|  
|*유틸리티*|차원이 유틸리티 특성을 포함합니다.|  
|*Currency*|차원이 통화 특성을 포함합니다.|  
|*속도*|차원이 환율 특성을 포함합니다.|  
|*채널*|차원이 채널 특성을 포함합니다.|  
|*홍보 행사*|차원이 홍보 행사 관련 특성을 포함합니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **형식** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.DimensionType>합니다.  
  
 부모에 해당 하는 요소 **형식** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Dimension>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
