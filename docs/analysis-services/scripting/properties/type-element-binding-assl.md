---
title: 요소 (바인딩) (ASSL)를 입력 합니다. | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 84f0df7ee525ae338ef9ba4279c5c19b410ff0b1
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="type-element-binding-assl"></a>Type 요소(바인딩)(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  특성 바인딩의 유형을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AttributeBinding> <!-- or CubeAttributeBinding -->  
   ...  
   <Type>...</Type>  
   ...  
</AttributeBinding>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md), [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*모두*|모든 수준|  
|*Key*|멤버 키|  
|*이름*|멤버 이름|  
|*Value*|멤버 값|  
|*번역*|멤버 번역|  
|*UnaryOperator*|단항 연산자|  
|*SkippedLevels*|건너뛴 수준|  
|*CustomRollup*|사용자 지정 롤업 수식|  
|*CustomRollupProperties*|사용자 지정 롤업 속성|  
  
 부모에 해당 하는 요소 **형식** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.AttributeBinding> 및 <xref:Microsoft.AnalysisServices.CubeAttributeBinding>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Binding 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
