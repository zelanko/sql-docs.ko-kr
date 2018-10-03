---
title: Collation 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Collation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Collation
helpviewer_keywords:
- Collation element
ms.assetid: 9b6dbe19-543e-43e6-abe9-1e8b4dfaa275
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 410baddd86da9d6100cd3ef7342501fed955b847
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178073"
---
# <a name="collation-element-assl"></a>Collation 요소(ASSL)
  부모 요소에 사용되는 데이터 정렬을 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Database> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Collation>...</Collation>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[큐브](../objects/cube-element-assl.md), [데이터베이스](../objects/database-element-assl.md)를 [DataItem](../data-type/dataitem-data-type-assl.md)를 [차원](../objects/dimension-element-assl.md)를 [MiningModel](../objects/miningmodel-element-assl.md), [MiningStructure](../objects/miningstructure-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `Collation` 문자열은 LCID(로캘 ID)와 비교 플래그를 밑줄로 구분하여 구성됩니다. 예를 들어 Latin1_General_CI_AS는 허용되는 문자열입니다.  
  
 AMO(Analysis Management Object) 개체 모델에서 `Collation`의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataItem>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.MiningModel> 및 <xref:Microsoft.AnalysisServices.MiningStructure>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
