---
title: Actions 요소 (ASSL) | Microsoft Docs
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
- Actions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Actions
helpviewer_keywords:
- Actions element
ms.assetid: 100a4209-2c22-4902-a8ca-f2bd99bf8fbb
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 583f265b0fb45b22cd0f6b3d20b577276d70ae92
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37183230"
---
# <a name="actions-element-assl"></a>Actions 요소(ASSL)
  에 대 한 작업의 컬렉션을 포함 한 [큐브](../objects/cube-element-assl.md) 또는 [관점](../objects/perspective-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cube> <!-- or Perspective -->  
   ...  
   <Actions>  
      <Action xsi:type="DrillThroughAction">...</Action> <!-- ancestor: Cube -->  
      <Action xsi:type="ReportAction">...</Action> <!-- ancestor: Cube -->  
      <Action xsi:type="StandardAction">...</Action> <!-- ancestor: Cube -->  
      <!-- or -->  
      <Action xsi:type="PerspectiveAction">...</Action> <!-- ancestor: Perspective -->  
      </Actions>  
      ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음(컬렉션)|  
|기본값|없음(컬렉션)|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[큐브](../objects/cube-element-assl.md), [관점](../objects/perspective-element-assl.md)|  
  
|상위 항목 또는 부모|자식 요소|  
|------------------------|--------------------|  
|[큐브](../data-type/action-data-type-assl.md)하십시오 [ReportAction](../data-type/reportaction-data-type-assl.md), [StandardAction](../data-type/standardaction-data-type-assl.md)|  
|[큐브 뷰](../data-type/perspectiveaction-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 AMO(Analysis Management Objects) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ActionCollection> 및 <xref:Microsoft.AnalysisServices.PerspectiveActionCollection>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [컬렉션 &#40;ASSL&#41;](collections-assl.md)  
  
  
