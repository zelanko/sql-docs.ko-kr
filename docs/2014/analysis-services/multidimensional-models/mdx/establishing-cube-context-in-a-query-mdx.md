---
title: 쿼리 (MDX)에서 큐브 컨텍스트 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cubes [Analysis Services], MDX
- MDX [Analysis Services], cube context
- SELECT statement [MDX]
- Multidimensional Expressions [Analysis Services], cube context
- queries [MDX], cube context
ms.assetid: 79d6a1e8-2825-4eb9-97df-5071aecae8f0
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 972b630aea4ebcc427803e226d27d52f919da4a0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172048"
---
# <a name="establishing-cube-context-in-a-query-mdx"></a>쿼리에 큐브 컨텍스트 설정(MDX)
  모든 MDX 쿼리는 지정된 큐브 컨텍스트 내에서 실행됩니다. 이 컨텍스트는 쿼리 내의 식에 의해 계산되는 멤버를 정의합니다.  
  
 SELECT 문에서 FROM 절은 큐브 컨텍스트를 결정합니다. 이 컨텍스트는 전체 큐브이거나 해당 큐브의 하위 큐브일 수 있습니다. FROM 절을 통해 큐브 컨텍스트를 지정한 경우 추가 함수를 사용하여 해당 큐브를 확장하거나 제한할 수 있습니다.  
  
> [!NOTE]  
>  SCOPE 및 CALCULATE 문을 사용하면 MDX 스크립트 내에서 큐브 컨텍스트를 관리할 수 있습니다. 자세한 내용은 [MDX 스크립팅 기본 사항&#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md)을 참조하세요.  
  
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
  
 MDX SELECT 문의 FROM 절에 대한 자세한 내용은 [SELECT 문&#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)을 참조하세요.  
  
## <a name="refining-the-context"></a>컨텍스트 구체화  
 FROM 절은 단일 큐브 내의 큐브 컨텍스트를 지정하지만 한 번에 하나 이상의 데이터를 사용하는 경우도 있습니다.  
  
 MDX [LookupCube](/sql/mdx/lookupcube-mdx) 함수를 사용하면 큐브 컨텍스트 외부의 다른 큐브에서 데이터를 검색할 수 있습니다. 또한 [Filter](/sql/mdx/filter-mdx) 함수 등을 사용하여 쿼리를 계산할 때 컨텍스트를 임시적으로 제한할 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX 쿼리 기본 사항 &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
