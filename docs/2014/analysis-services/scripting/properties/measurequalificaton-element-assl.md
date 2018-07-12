---
title: MeasureQualificaton 요소 (ASSL) | Microsoft Docs
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
- MeasureQualificaton Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- MeasureQualification element
ms.assetid: 754a037c-f20b-4717-a6e8-12f495e8e3b4
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cb84c39d7d7a3b69ea3c13e43dfda0b331c548e4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37149504"
---
# <a name="measurequalificaton-element-assl"></a>MeasureQualificaton 요소(ASSL)
  측정값에 대 한 접두사 적용 여부를 결정 합니다 [MeasureGroup](../objects/group-element-assl.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MeasureGroup>  
   ...  
   <MeasureQualification>...</MeasureQualification>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*없음*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[측정값 그룹](../objects/group-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*없음*|이 측정값 그룹의 측정값에 접두사가 적용되지 않습니다.|  
|*PrefixMeasureGroup*|이 측정값 그룹에 있는 각 측정값의 고유한 이름 및 캡션에 측정값 그룹 및 공백 하나가 접두사로 적용됩니다.|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 하는 요소가 `MeasureQualification` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MeasureGroup>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [큐브 요소 &#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [차원 요소 &#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [MeasureGroup 요소 &#40;ASSL&#41;](../objects/group-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
