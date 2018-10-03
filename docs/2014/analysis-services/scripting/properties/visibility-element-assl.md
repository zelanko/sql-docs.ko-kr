---
title: Visibility 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Visibility Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Visibility
helpviewer_keywords:
- Visibility element
ms.assetid: 59372ebf-af52-4d60-bf9b-bb1644ae9865
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e0ec079bcdfefb84f5d7b9e1ea24b5c16b001f16
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48216633"
---
# <a name="visibility-element-assl"></a>Visibility 요소(ASSL)
  표시 유형을 정의 [주석](../objects/annotation-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Annotation>  
   ...  
   <Visibility>...</Visibility>  
   ...  
</Annotation>  
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
|부모 요소|[주석](../objects/annotation-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*SchemaRowset*|주석이 스키마 행 집합에 표시됩니다.|  
|*없음*|주석이 표시되지 않습니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `Visibility`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.Annotation>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
