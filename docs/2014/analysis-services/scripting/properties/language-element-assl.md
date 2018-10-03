---
title: Language 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Language Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LANGUAGE
helpviewer_keywords:
- Language element
ms.assetid: 4d745d23-6b1f-4a85-97cf-d034cc41356f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2ce2de9ae87ac0c4d22a179f25bbf7ff047e7633
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126068"
---
# <a name="language-element-assl"></a>Language 요소(ASSL)
  부모 요소의 언어 식별자를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cube> <!-- or Database, Dimension, MiningModel, MiningStructure, Translation -->  
   ...  
   <Language>...</Language>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|정수|  
|기본값|없음|  
  
 **카디널리티**  
  
|상위 항목 또는 부모|카디널리티|  
|------------------------|-----------------|  
|[번역](../objects/translation-element-assl.md)|1-1: 한 번만 나타나는 필수 요소입니다.|  
|나머지|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[큐브](../objects/cube-element-assl.md), [데이터베이스](../objects/database-element-assl.md)를 [차원](../objects/dimension-element-assl.md)를 [MiningModel](../objects/miningmodel-element-assl.md)를 [MiningStructure](../objects/miningstructure-element-assl.md), [번역](../objects/translation-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `Language` 요소는 부모 요소에서 사용하는 기본 언어 식별자 또는 `Translation` 요소의 특정 언어 식별자를 포함합니다. 언어는 LCID(로캘 ID) 코드를 사용하여 정의해야 합니다. 예를 들어 영어(미국)를 지정하려면 LCID 1033을 사용합니다.  
  
 AMO(Analysis Management Object) 개체 모델에서 `Language` 요소의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.MiningModel>, <xref:Microsoft.AnalysisServices.MiningStructure> 및 <xref:Microsoft.AnalysisServices.Translation>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
