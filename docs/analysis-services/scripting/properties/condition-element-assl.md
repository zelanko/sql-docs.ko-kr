---
title: "조건 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Condition Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- condition
helpviewer_keywords:
- Condition element
ms.assetid: 9c3cb31c-4aa1-49e4-aeb2-6cab54db0be3
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0f979f051615ef44f713b93736ca20a8913d7bce
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="condition-element-assl"></a>Condition 요소(ASSL)
  결정 하는 MDX (Multidimensional Expressions) 식을 포함 여부는 [동작](../../../analysis-services/scripting/objects/action-element-assl.md) 부모 요소는 대상에 적용 됩니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Action>  
   ...  
   <Condition>...</Condition  
      ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동작](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **조건** 요소는 부울 값으로 계산 되는 MDX 식을 포함 합니다. 식에서 반환 하는 경우 **True**, 하면 **동작** 에 지정 된 대상에 적용 됩니다는 [대상](../../../analysis-services/scripting/properties/target-element-assl.md) 요소입니다. 그렇지 않은 경우는 **동작** 적용 되지 않습니다.  
  
 부모에 해당 하는 요소 **조건** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Action>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

