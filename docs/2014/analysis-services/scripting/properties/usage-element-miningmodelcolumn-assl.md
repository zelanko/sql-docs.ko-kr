---
title: Usage 요소 (MiningModelColumn) (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Usage Element (MiningModelColumn)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Usage
helpviewer_keywords:
- Usage element
ms.assetid: 435a857e-37a9-434e-9de1-354f1ff2993f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 220f59e5e342f61f30d0f94bc9f9728982105986
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48090308"
---
# <a name="usage-element-miningmodelcolumn-assl"></a>Usage 요소(MiningModelColumn)(ASSL)
  에 대해 설명 하는 방법을 부모에 연결된 된 열 [MiningStructure](../objects/miningstructure-element-assl.md) 사용 됩니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningModelColumn>  
   ...  
   <Usage>...</Usage>  
   ...  
</MiningModelColumn>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*키*|열이 키 열입니다.|  
|*입력*|열이 입력 열입니다.|  
|*Predict*|열이 예측 열입니다.|  
|*PredictOnly*|열이 예측 열 전용입니다.|  
|*없음*|열이 모델에서 사용되지 않습니다. **경고:** Usage 값이 "None" 인 경우 Analysis Services 보내지 않도록 모든 값 서버에 기본적으로; 따라서 사용 특성은 요청/응답에 포함 되지 않습니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `Usage`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.MiningModelColumnUsages>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
