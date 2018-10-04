---
title: TargetType 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- TargetType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TargetType
helpviewer_keywords:
- TargetType element
ms.assetid: 2c69ea6e-2af7-435b-9841-86117d5554a7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ed0ca768f075b7cd4249c9d8b021e2ec10d54c46
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099563"
---
# <a name="targettype-element-assl"></a>TargetType 요소(ASSL)
  식별 된 항목 유형을 식별 합니다 [대상](target-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Action>  
   ...  
   <TargetType>...</TargetType>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동작](../objects/action-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*Cube*|동작 대상이 큐브입니다.|  
|*셀*|동작 대상이 하위 큐브입니다.|  
|*설정*|동작 대상이 집합입니다.|  
|*Hierarchy*|동작 대상이 계층입니다.|  
|*Level*|동작 대상이 수준입니다.|  
|*DimensionMembers*|동작 대상이 차원의 멤버입니다.|  
|*HierarchyMembers*|동작 대상이 계층의 멤버입니다.|  
|*LevelMembers*|동작 대상이 수준의 멤버입니다.|  
|*AttributeMembers*|동작 대상이 특성의 멤버입니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `TargetType`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.ActionTargetType>입니다.  
  
 부모에 해당 하는 요소가 `TargetType` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Action>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
