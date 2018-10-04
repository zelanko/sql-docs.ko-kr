---
title: Expression 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Expression Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Expression
helpviewer_keywords:
- Expression element
ms.assetid: a9491b21-5279-4531-b6a5-9e8022060dd8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d7801b94d30e0b0c4baa62dd861146ee89fb3717
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48173913"
---
# <a name="expression-element-assl"></a>Expression 요소(ASSL)
  부모 요소의 내용을 정의하는 MDX(Multidimensional Expressions) 식을 포함합니다.  
  
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
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CellPermission](../objects/cellpermission-element-assl.md), [StandardAction](../data-type/action-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 에 대 한는 `CellPermission` 요소를 `Expression` 요소에서 나타내는 권한에 해당 하는 셀을 식별 하는 MDX 논리 식을 포함 합니다 [액세스](access-element-assl.md) 요소의 `CellPermission` 요소. `Expression` 요소의 `CellPermission` 요소 값이 빈 경우 `CellPermission` 요소는 무시됩니다.  
  
 `StandardAction` 요소의 경우 `Expression` 요소는 동작 내용을 나타내는 MDX 식을 포함합니다. `Expression` 요소의 `StandardAction` 요소 값이 빈 경우 `StandardAction` 요소는 무시됩니다.  
  
 AMO(Analysis Management Object) 개체 모델에서 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.CellPermission> 및 <xref:Microsoft.AnalysisServices.StandardAction>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
