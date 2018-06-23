---
title: 값 요소 (ASSL) | Microsoft Docs
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
- Value Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Value
helpviewer_keywords:
- Value element
ms.assetid: a2fad411-73fd-42df-b4e1-df2cb8454182
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f350c559e78613df5e0a357b8f87dca073e1d248
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093617"
---
# <a name="value-element-assl"></a>Value 요소(ASSL)
  부모 요소의 값을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AlgorithmParameter> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Value>...</Value>  
   ...  
</AlgorithmParameter>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
|상위 항목 또는 부모|데이터 형식|  
|------------------------|---------------|  
|[AlgorithmParameter](../objects/algorithmparameter-element-assl.md)|모든 simpleType|  
|[ServerProperty](../objects/serverproperty-element-assl.md)|모든 simpleType|  
|나머지|String|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AlgorithmParameter](../objects/algorithmparameter-element-assl.md), [주석](../objects/annotation-element-assl.md), [Kpi](../objects/kpi-element-assl.md), [ReportFormatParameter](../objects/reportformatparameter-element-asl.md), [ReportParameter](../objects/reportparameter-element-assl.md), [ServerProperty](../objects/serverproperty-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Value` 요소는 부모 개체와 연결된 값을 포함합니다. `Value` 요소의 필요한 값은 다음 표와 같이 부모 요소에 따라 달라집니다.  
  
|부모 요소|필요한 값|  
|--------------------|--------------------|  
|[AlgorithmParameter](../objects/algorithmparameter-element-assl.md)|알고리즘 매개 변수 값|  
|[주석](../objects/annotation-element-assl.md)|주석 값|  
|[Kpi](../objects/kpi-element-assl.md)|KPI(핵심 성과 지표) 값을 계산하는 데 사용되는 MDX(Multidimensional Expressions) 식|  
|[ReportFormatParameter](../objects/reportformatparameter-element-asl.md)|보고서 형식 매개 변수 값|  
|[ReportParameter](../objects/reportparameter-element-assl.md)|보고서 매개 변수 값을 계산하는 데 사용되는 식|  
|[ServerProperty](../objects/serverproperty-element-assl.md)|현재 실행 중인 인스턴스의 서버 속성 값|  
  
 AMO(Analysis Management Object) 개체 모델에서 `Value`의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.AlgorithmParameter>, <xref:Microsoft.AnalysisServices.Annotation>, <xref:Microsoft.AnalysisServices.Kpi>, <xref:Microsoft.AnalysisServices.ReportParameter> 및 <xref:Microsoft.AnalysisServices.ServerProperty>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  