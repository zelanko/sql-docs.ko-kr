---
title: DefaultScript 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DefaultScript Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DefaultScript
helpviewer_keywords:
- DefaultScript element
ms.assetid: 60716e63-2d64-4774-9ac9-253efe612fa5
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b0a26b8b703636aebb6d3701c5c7c99d24a25ade
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36187287"
---
# <a name="defaultscript-element-assl"></a>DefaultScript 요소(ASSL)
  기본값을 식별 [MdxScript](../objects/mdxscript-element-assl.md) 요소에는 [MdxScripts](../collections/mdxscripts-element-assl.md) 컬렉션입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MdxScript>  
   ...  
   <DefaultScript>...</DefaultScript>  
   ...  
</MdxScript>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|`True`|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MdxScript](../objects/mdxscript-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 한 스크립트에 대해 `DefaultScript`의 값을 `True`로 설정하면 `DefaultScript` 컬렉션의 다른 모든 `False` 요소에 대해 `MdxScript`의 값이 `MdxScripts`로 설정됩니다.  
  
 부모에 해당 하는 요소 `DefaultScript` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MdxScript>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  