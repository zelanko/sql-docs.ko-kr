---
title: Multiplicity 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 441e3829-9009-4b32-a8c6-fa580663387f
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 91ecb8a8b7ada49666d2b6144d1ba258a7c26b58
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186831"
---
# <a name="multiplicity-element-assl"></a>Multiplicity 요소(ASSL)
  RelationshipEnd의 특성이 관계의 "일" 쪽인지 "다" 쪽인지를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<RelationshipEnd>  
   ...  
   <Multiplicity>...</Multiplicity>  
   ...  
</RelationshipEnd>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값||  
|카디널리티|1: 한 번만 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[RelationshipEnd](../data-type/relationshipend-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*하나*|기본 키 End입니다.|  
|*많은*|외래 키 End입니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `role`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.Multiplicity>입니다.  
  
  