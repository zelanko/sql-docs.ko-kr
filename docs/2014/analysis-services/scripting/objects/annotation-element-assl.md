---
title: Annotation 요소 (ASSL) | Microsoft Docs
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
- Annotation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Annotation
helpviewer_keywords:
- Annotation element
ms.assetid: 7d75291a-47b4-498a-8ba4-3d093b8513b2
caps.latest.revision: 43
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0453688aab37831c54bad3080a34409b078740bf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304503"
---
# <a name="annotation-element-assl"></a>Annotation 요소(ASSL)
  ASSL(Analysis Services Scripting Language) 스키마를 확장하는 데 사용되는 요소를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Annotations>  
   <Annotation>  
      <Name>...</Name>  
      <Visibility>...</Visibility>  
      <Value>...</Value>  
   </Annotation>  
</Annotations >  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[주석](../collections/annotations-element-assl.md)|  
|자식 요소|[이름을](../properties/name-element-assl.md)하십시오 [값](../properties/value-element-assl.md), [표시 유형](../properties/visibility-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 `Annotation` 요소는 복합 데이터 형식을 정의하는 데만 사용되는 개체를 제외한 모든 개체에 ASSL 스키마 확장성을 제공합니다. `Value` 요소의 `Annotation` 요소는 다음 규칙에 따라 ASSL 이외의 모든 XML 네임스페이스에서 유효한 XML을 포함할 수 있습니다.  
  
-   XML은 요소만 포함할 수 있습니다.  
  
-   각 요소 이름은 고유해야 합니다. `Name` 요소의 `Annotation` 요소 값은 대상 네임스페이스를 참조하는 것이 좋습니다.  
  
 이러한 규칙은 `Annotation` 요소 내용이 DSO(의사 결정 지원 개체)와 같은 다른 인터페이스를 통해 이름/값 쌍 집합으로 표시되기 위해 반드시 필요합니다.  
  
 자식 요소로 묶이지 않은 `Annotation` 요소 내 주석 및 공백은 그대로 유지되지 않습니다. 또한 모든 요소는 읽기/쓰기 전용이어야 하며 읽기 전용 요소는 무시됩니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Annotation>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
