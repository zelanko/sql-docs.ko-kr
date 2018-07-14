---
title: Slice 요소 (ASSL) | Microsoft Docs
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
- Slice Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Slice
helpviewer_keywords:
- Slice element
ms.assetid: 2c8c4107-c641-4724-bfa5-0c47e0ec8888
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 299f84167ec64c4bdd795c56a608e76f61d348b0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37178890"
---
# <a name="slice-element-assl"></a>Slice 요소(ASSL)
  파티션에 포함된 조각을 정의하는 MDX(Multidimensional Expressions) 식을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Partition>  
      ...  
   <Slice>...</Slice>  
   ...  
</Partition>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[파티션](../objects/partition-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Slice` 요소는 파티션이 정보를 저장하는 큐브 부분을 식별하는 MDX 튜플 식 또는 집합 식을 포함합니다. MDX 식은 비슷합니다는 [StrToSet](/sql/mdx/strtoset-mdx) MDX 함수와 CONSTRAINED 키워드를 사용 하 여에 식을 MDX 또는 사용자 정의 함수를 포함할 수 없습니다.  
  
 부모에 해당 하는 요소가 `Slice` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Partition>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
