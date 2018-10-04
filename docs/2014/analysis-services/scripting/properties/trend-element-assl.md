---
title: Trend 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Trend Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Trend
helpviewer_keywords:
- Trend element
ms.assetid: d1d92d10-a181-4402-aacb-c0b2adc96bba
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0d5aa3fb1c7e078a34b7b75cbf89c0e88e29e07c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048723"
---
# <a name="trend-element-assl"></a>Trend 요소(ASSL)
  추세 표시를 반환 하는 MDX (Multidimensional Expressions) 식을 포함 한 [Kpi](../objects/kpi-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Kpi>  
   ...  
   <Trend>...</Trend>  
   ...  
</Kpi>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Kpi](../objects/kpi-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `Trend` 요소는 결과가 -1과 1 사이의 숫자인 MDX 식을 포함합니다.  
  
 부모에 해당 하는 요소가 `Trend` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Kpi>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
