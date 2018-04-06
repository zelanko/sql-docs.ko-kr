---
title: ReportFormatParameter 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ReportFormatParameter Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ReportFormatParameter
helpviewer_keywords:
- ReportFormatParameter element
ms.assetid: 064a8683-c44b-4261-be4d-32226d3d3119
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 23927f3f832509ddc64e07941be89449dd8a063f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="reportformatparameter-element---asl"></a>ReportFormatParameter 요소-ASL
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]이름 및 지정 하는 매개 변수 값을 포함 방법을 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 보고서가 런타임에 서식이 지정 됩니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ReportFormatParameters>  
   <ReportFormatParameter>  
      <Name>...</Name>  
      <Value>...</Value>  
   </ReportFormatParameter>  
</ReportFormatParameters>  
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
|부모 요소|[ReportFormatParameters](../../../analysis-services/scripting/collections/reportformatparameters-element-assl.md)|  
|자식 요소|[Name](../../../analysis-services/scripting/properties/name-element-assl.md), [Value](../../../analysis-services/scripting/properties/value-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **ReportFormatParameter** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ReportAction>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ReportAction 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)   
 [Action 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/action-element-assl.md)   
 [개체 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
