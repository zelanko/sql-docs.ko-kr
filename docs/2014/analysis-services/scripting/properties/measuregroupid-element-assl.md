---
title: MeasureGroupID 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MeasureGroupID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroupID
helpviewer_keywords:
- MeasureGroupID element
ms.assetid: 3b075f86-dbbc-4285-8d2d-61fa722181c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b4eb43414e0fd7da783f4a1ac588c4851e3c9bd9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083635"
---
# <a name="measuregroupid-element-assl"></a>MeasureGroupID 요소(ASSL)
  연결 된 [MeasureGroup](../objects/group-element-assl.md) 부모 요소, 바인딩 또는 아웃오브 라인 바인딩을 사용 하 여 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ManyToManyMeasureGroupDimension> <!-- or MeasureGroupAttributeBinding, MeasureGroupBinding, PerspectiveMeasureGroup -->  
   ...  
   <MeasureGroupID>...</MeasureGroupID>  
   ...  
</ManyToManyMeasureGroupDimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|없음|  
|카디널리티||  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ManyToManyMeasureGroupDimension](../data-type/dimension-data-type-assl.md)하십시오 [MeasureGroupAttributeBinding](../data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)하십시오 [MeasureGroupBinding](../data-type/binding-data-type-assl.md), [PerspectiveMeasureGroup](../data-type/perspectivemeasuregroup-data-type-assl.md)|  
  
|자식 요소-상위 항목 또는 부모|카디널리티|  
|------------------------------------------|-----------------|  
|[ManyToManyMeasureGroupDimension](../data-type/dimension-data-type-assl.md)|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
|[MeasureGroupAttributeBinding](../data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)하십시오 [MeasureGroupBinding](../data-type/binding-data-type-assl.md) 고 [PerspectiveMeasureGroup](../data-type/perspectivemeasuregroup-data-type-assl.md)|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="remarks"></a>Remarks  
 AMO(Analysis Management Objects) 개체 모델에서 `MeasureGroupID`의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.ManyToManyMeasureGroupDimension>, <xref:Microsoft.AnalysisServices.MeasureGroupBinding> 및 <xref:Microsoft.AnalysisServices.PerspectiveMeasureGroup>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
