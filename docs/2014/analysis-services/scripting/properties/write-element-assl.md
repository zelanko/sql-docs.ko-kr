---
title: Write 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Write Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Write element
ms.assetid: d8f7a367-d7bf-4b40-acb4-19c8bc8c6c20
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dd39e3354ee68a2e716e4cfbf50e41e371bf5303
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104253"
---
# <a name="write-element-assl"></a>Write 요소(ASSL)
  에 대 한 데이터 또는 메타 데이터를 쓸 수 있는지 여부를 결정을 지정 [CubeDimensionPermission](../data-type/permission-data-type-assl.md) 하거나 [권한](../data-type/permission-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubeDimensionPermission> <!-- or Permission -->  
   ...  
   <Write>...</Write>  
   ...  
</CubeDimensionPermission>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*없음*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubeDimensionPermission](../objects/cubepermission-element-assl.md), [권한](../data-type/permission-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*없음*|부모 개체의 데이터 또는 메타데이터에 대한 액세스가 허용되지 않습니다.|  
|*허용*|부모 개체의 데이터 및 메타데이터에 대한 쓰기 액세스가 허용됩니다.|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 하는 요소가 `Write` Analysis Management Objects (AMO) 개체 모델 <xref:Microsoft.AnalysisServices.CubeDimensionPermission> 및 <xref:Microsoft.AnalysisServices.Permission>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [큐브 요소 &#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [차원 요소 &#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
