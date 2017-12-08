---
title: "추세 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Trend Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Trend
helpviewer_keywords: Trend element
ms.assetid: d1d92d10-a181-4402-aacb-c0b2adc96bba
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6a784b274e5971f0846c0ee3739cce75e70b2276
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="trend-element-assl"></a>Trend 요소(ASSL)
  에 대 한 추세 표시를 반환 하는 MDX (Multidimensional Expressions) 식을 포함 한 [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Kpi>  
   ...  
   <Trend>...</Trend>  
   ...  
</Kpi>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **Trend** 요소는 결과가 -1과 1 사이의 숫자인 MDX 식을 포함합니다.  
  
 부모에 해당 하는 요소 **추세** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Kpi>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
