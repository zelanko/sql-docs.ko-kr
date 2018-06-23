---
title: AllowedRowsExpression 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: ec24b11d-d11e-4369-a619-7e41a3c46159
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 99a340f2bbeb1e5d61a20b4031beeade9fbcc5c7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079851"
---
# <a name="allowedrowsexpression-element-assl"></a>AllowedRowsExpression 요소(ASSL)
  부모 요소의 내용을 정의하며 부울 형식의 DAX(Data Analysis Expression)를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CellPermission> <!-- or StandardAction -->  
   ...  
   <Expression>...</Expression>  
   ...  
</CellPermission>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CellPermission](../objects/cellpermission-element-assl.md), [StandardAction](../data-type/action-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 에 대 한는 `CellPermission` 요소는 `Expression` 요소에서 나타내는 권한에 해당 하는 셀을 식별 하는 MDX 논리 식을 포함는 [액세스](access-element-assl.md) 의 요소는 `CellPermission` 요소입니다. `Expression` 요소의 `CellPermission` 요소 값이 빈 경우 `CellPermission` 요소는 무시됩니다.  
  
 `StandardAction` 요소의 경우 `Expression` 요소는 동작 내용을 나타내는 MDX 식을 포함합니다. `Expression` 요소의 `StandardAction` 요소 값이 빈 경우 `StandardAction` 요소는 무시됩니다.  
  
 AMO(Analysis Management Object) 개체 모델에서 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.CellPermission> 및 <xref:Microsoft.AnalysisServices.StandardAction>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  