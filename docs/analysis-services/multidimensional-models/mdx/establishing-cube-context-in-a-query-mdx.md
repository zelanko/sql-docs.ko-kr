---
title: "쿼리 (MDX)에서 큐브 컨텍스트 설정 | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cubes [Analysis Services], MDX
- MDX [Analysis Services], cube context
- SELECT statement [MDX]
- Multidimensional Expressions [Analysis Services], cube context
- queries [MDX], cube context
ms.assetid: 79d6a1e8-2825-4eb9-97df-5071aecae8f0
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 08eee9eb06b6e69e5681f5d88ac3f9c7f7a29d27
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="establishing-cube-context-in-a-query-mdx"></a>쿼리에 큐브 컨텍스트 설정(MDX)
  모든 MDX 쿼리는 지정된 큐브 컨텍스트 내에서 실행됩니다. 이 컨텍스트는 쿼리 내의 식에 의해 계산되는 멤버를 정의합니다.  
  
 SELECT 문에서 FROM 절은 큐브 컨텍스트를 결정합니다. 이 컨텍스트는 전체 큐브이거나 해당 큐브의 하위 큐브일 수 있습니다. FROM 절을 통해 큐브 컨텍스트를 지정한 경우 추가 함수를 사용하여 해당 큐브를 확장하거나 제한할 수 있습니다.  
  
> [!NOTE]  
>  SCOPE 및 CALCULATE 문을 사용하면 MDX 스크립트 내에서 큐브 컨텍스트를 관리할 수 있습니다. 자세한 내용은 [MDX 스크립팅 기본 사항&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)을 참조하세요.  
  
## <a name="from-clause-syntax"></a>FROM 절 구문  
 다음 구문은 FROM 절에 대한 설명입니다.  
  
```  
<SELECT subcube clause> ::=  
   Cube_Identifier |   
   (SELECT [  
      * |   
      ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]   
   FROM <SELECT subcube clause> <SELECT slicer axis clause> )  
```  
  
 이 구문에서 `<SELECT subcube clause>` 절은 SELECT 문이 실행되는 큐브 또는 하위 큐브를 설명합니다.  
  
 FROM 절의 간단한 예로는 전체 Adventure Works 예제 큐브에 대해 실행되는 절을 들 수 있습니다. 이러한 FROM 절의 형식은 다음과 같습니다.  
  
```  
FROM [Adventure Works]  
```  
  
 MDX SELECT 문의 FROM 절에 대한 자세한 내용은 [SELECT 문&#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)을 참조하세요.  
  
## <a name="refining-the-context"></a>컨텍스트 구체화  
 FROM 절은 단일 큐브 내의 큐브 컨텍스트를 지정하지만 한 번에 하나 이상의 데이터를 사용하는 경우도 있습니다.  
  
 MDX [LookupCube](../../../mdx/lookupcube-mdx.md) 함수를 사용하면 큐브 컨텍스트 외부의 다른 큐브에서 데이터를 검색할 수 있습니다. 또한 [Filter](../../../mdx/filter-mdx.md) 함수 등을 사용하여 쿼리를 계산할 때 컨텍스트를 임시적으로 제한할 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 쿼리 기본 사항&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
