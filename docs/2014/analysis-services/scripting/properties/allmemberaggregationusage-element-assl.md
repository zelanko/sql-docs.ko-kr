---
title: AllMemberAggregationUsage 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AllMemberAggregationUsage Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AllMemberAggregationUsage
helpviewer_keywords:
- AllMemberAggregationUsage element
ms.assetid: 264fe9d8-8e9a-4642-8cee-7c2804126926
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e044340af4ed275af18a3e8dfe788e8a766b542c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074393"
---
# <a name="allmemberaggregationusage-element-assl"></a>AllMemberAggregationUsage 요소(ASSL)
  제어 하는 방법에서 집계 디자이너로 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 집계를 디자인 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubeDimension>  
   ...  
   <AllMemberAggregationUsage>...</AllMemberAggregationUsage>  
   ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*기본값*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubeDimension](../data-type/dimension-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*전체*|큐브의 모든 집계가 All 멤버를 포함해야 합니다.|  
|*없음*|큐브의 어떤 집계도 All 멤버를 포함하지 않아야 합니다.|  
|*무제한*|집계 디자이너에 제한 사항이 지정되지 않습니다.|  
|*기본값*|*Unrestricted*와 같습니다.|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 하는 요소가 `AllMemberAggregationUsage` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CubeDimension>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [큐브 요소 &#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [차원 요소 &#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
