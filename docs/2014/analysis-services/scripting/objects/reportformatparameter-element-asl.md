---
title: ReportFormatParameter 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7f3dd567a88a76837e13d051988620eb1886ef40
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48188023"
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
|데이터 형식 및 길이|없음|  
|기본값|없음|  
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
  
  
