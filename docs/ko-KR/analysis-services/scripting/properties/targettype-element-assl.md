---
title: TargetType 요소 (ASSL) | Microsoft Docs
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
- TargetType Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TargetType
helpviewer_keywords:
- TargetType element
ms.assetid: 2c69ea6e-2af7-435b-9841-86117d5554a7
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 67c53bb07cfb9144869ce759af25b42b12478107
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="targettype-element-assl"></a>TargetType 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  식별 된 항목의 유형을 식별 된 [대상](../../../analysis-services/scripting/properties/target-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Action>  
   ...  
   <TargetType>...</TargetType>  
   ...  
</Action>  
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
|부모 요소|[동작](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*Cube*|동작 대상이 큐브입니다.|  
|*셀*|동작 대상이 하위 큐브입니다.|  
|*설정*|동작 대상이 집합입니다.|  
|*계층 구조*|동작 대상이 계층입니다.|  
|*Level*|동작 대상이 수준입니다.|  
|*DimensionMembers*|동작 대상이 차원의 멤버입니다.|  
|*HierarchyMembers*|동작 대상이 계층의 멤버입니다.|  
|*LevelMembers*|동작 대상이 수준의 멤버입니다.|  
|*AttributeMembers*|동작 대상이 특성의 멤버입니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **TargetType** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ActionTargetType>합니다.  
  
 부모에 해당 하는 요소 **TargetType** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Action>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
