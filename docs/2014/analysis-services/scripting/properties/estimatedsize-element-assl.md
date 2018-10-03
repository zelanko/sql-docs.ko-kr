---
title: EstimatedSize 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- EstimatedSize Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EstimatedSize
helpviewer_keywords:
- EstimatedSize element
ms.assetid: a9c63a22-d424-4f27-a186-5372f7b0224d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8ce5a46547488bb81e0ad50890e3588259bad4c8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048513"
---
# <a name="estimatedsize-element-assl"></a>EstimatedSize 요소(ASSL)
  부모 요소의 읽기 전용 예상 크기(바이트)를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Database> <!-- or MeasureGroup, Partition -->  
   ...  
   <EstimatedSize>...</EstimatedSize>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Long|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[데이터베이스](../objects/database-element-assl.md)하십시오 [MeasureGroup](../objects/group-element-assl.md), [파티션](../objects/partition-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 AMO(Analysis Management Object) 개체 모델에서 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.MeasureGroup> 및 <xref:Microsoft.AnalysisServices.Partition>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
