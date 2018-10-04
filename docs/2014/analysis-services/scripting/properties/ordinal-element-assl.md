---
title: Ordinal 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 87957fdfa3adf85081c0a2ca6a6539917b9f9b81
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198743"
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
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `AttributeBinding` 및 `CubeAttributeBinding` 요소가 합니다 [형식](type-element-binding-assl.md) 속성이 설정 되어 *키* 또는 *번역* 의 컬렉션에 바인딩되는 특성에 바인딩될 수 열을 데이터 원본 뷰. `Ordinal` 요소의 값은 해당 컬렉션에서 `AttributeBinding` 또는 `CubeAttributeBinding`이 참조하는 열을 결정합니다.  
  
 부모에 해당 하는 요소가 `Ordinal` Analysis Management Objects (AMO) 개체 모델 <xref:Microsoft.AnalysisServices.AttributeBinding> 및 <xref:Microsoft.AnalysisServices.CubeAttributeBinding>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
