---
title: ReportFormatParameter 요소 (ASSL) | Microsoft Docs
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
- ReportFormatParameter Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReportFormatParameter
helpviewer_keywords:
- ReportFormatParameter element
ms.assetid: 064a8683-c44b-4261-be4d-32226d3d3119
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dfcc98e3abe60296e7ee28b57bc54fe89f5c2abe
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37245583"
---
# <a name="reportformatparameter-element-assl"></a>ReportFormatParameter 요소(ASSL)
  이름 및 지정 하는 매개 변수의 값을 포함 하는 방법을 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 보고서가 런타임에 서식이 지정 됩니다.  
  
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
|부모 요소|[ReportFormatParameters](../collections/reportformatparameters-element-assl.md)|  
|자식 요소|[Name](../properties/name-element-assl.md), [Value](../properties/value-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 하는 요소가 `ReportFormatParameter` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ReportAction>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ReportAction 데이터 형식 &#40;ASSL&#41;](../data-type/action-data-type-assl.md)   
 [Action 요소 &#40;ASSL&#41;](action-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
