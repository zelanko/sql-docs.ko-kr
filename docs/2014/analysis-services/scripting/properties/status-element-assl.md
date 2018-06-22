---
title: Status 요소 (ASSL) | Microsoft Docs
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
- Status Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Status
helpviewer_keywords:
- Status element
ms.assetid: 4938465e-7876-43e2-9d03-70dcc9b7b749
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fd27525f6a0a7457a3fd6a3f63f102b1f6ae7bf4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082547"
---
# <a name="status-element-assl"></a>Status 요소(ASSL)
  에 대 한 상태 표시를 반환 하는 MDX (Multidimensional Expressions) 식을 포함 한 [Kpi](../objects/kpi-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Kpi>  
   ...  
   <Status>...</Status>  
   ...  
</Kpi>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Kpi](../objects/kpi-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Status` 요소는 MDX 식을 포함합니다.  
  
 부모에 해당 하는 요소 `Status` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Kpi>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  