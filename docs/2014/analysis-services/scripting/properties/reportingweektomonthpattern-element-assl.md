---
title: ReportingWeekToMonthPattern 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ReportingWeekToMonthPattern Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReportingWeekToMonthPattern
helpviewer_keywords:
- ReportingWeekToMonthPattern element
ms.assetid: 8d7c694d-d5c5-4faa-af78-155779e84fe9
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b90c07018747c7ad04bbd2324bb0bd697f7d774c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172262"
---
# <a name="reportingweektomonthpattern-element-assl"></a>ReportingWeekToMonthPattern 요소(ASSL)
  에 대 한 보고 주-월 패턴 정의 [TimeBinding](../data-type/binding-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<TimeBinding>  
   ...  
   <ReportingWeekToMonthPattern>...</ReportingWeekToMonthPattern>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*445*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[TimeBinding](../data-type/binding-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*445*|및 세 번째 달에 5 주, 두 번째 달에 4 주 분기의 첫 번째 달에 4 주가 있습니다.|  
|*454*|및 세 번째 달에 4 주가 두 번째 달에 5 주 분기의 첫 번째 달에 4 주가 있습니다.|  
|*544*|사분기의 첫 번째 달에 5주, 두 번째 달에 4주, 세 번째 달에 4주가 있습니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `ReportingWeekToMonthPattern`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.ReportingWeekToMonthPattern>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  