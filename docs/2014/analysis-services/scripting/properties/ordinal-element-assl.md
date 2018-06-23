---
title: Ordinal 요소 (ASSL) | Microsoft Docs
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
- Ordinal Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Ordinal
helpviewer_keywords:
- Ordinal element
ms.assetid: 64e68ad5-439c-4c1d-9df4-ee90c56761b4
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9c9328a33db828af8bb7b0b129574d8ba855433e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080939"
---
# <a name="ordinal-element-assl"></a>Ordinal 요소(ASSL)
  키 및 번역과 같은 컬렉션에서 바인딩할 서수를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AttributeBinding> <!-- or CubeAttributeBinding -->  
   ...  
   <Ordinal>...</Ordinal>  
   ...  
</AttributeBinding>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|정수|  
|기본값|`0`|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AttributeBinding](../data-type/binding-data-type-assl.md), [CubeAttributeBinding](../data-type/cubeattributebinding-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `AttributeBinding` 및 `CubeAttributeBinding` 요소가 들어는 [형식](type-element-binding-assl.md) 속성으로 설정 되어 *키* 또는 *번역* 의 컬렉션에 바인딩되는 특성에 바인딩될 수 데이터의 열 원본 뷰를 사용 합니다. `Ordinal` 요소의 값은 해당 컬렉션에서 `AttributeBinding` 또는 `CubeAttributeBinding`이 참조하는 열을 결정합니다.  
  
 부모에 해당 하는 요소 `Ordinal` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.AttributeBinding> 및 <xref:Microsoft.AnalysisServices.CubeAttributeBinding>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  