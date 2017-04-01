---
title: "쿼리 범위 셀 계산 만들기(MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WITH 키워드"
  - "쿼리 범위 셀 계산 만들기 [MDX]"
ms.assetid: 45987daa-4400-41e9-add7-2428fd75709b
caps.latest.revision: 30
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 쿼리 범위 셀 계산 만들기(MDX)
  MDX에서 **WITH** 키워드를 사용하여 쿼리 컨텍스트 내의 계산 셀을 설명합니다. **WITH** 키워드는 다음 구문을 가집니다.  
  
```  
WITH CELL CALCULATION Cube_Name.CellCalc_Identifier  String_Expression  
```  
  
 `CellCalc_Identifier` 값은 계산 셀의 이름입니다. `String_Expression` 값에는 직각의 단일 차원 MDX 집합 식 목록이 들어 있습니다. 이들 각각의 집합 식은 다음 테이블에 나열된 범주 중 하나로 확인되어야 합니다.  
  
|범주|Description|  
|--------------|-----------------|  
|빈 집합|빈 집합으로 확인되는 MDX 집합 식입니다. 이 경우 계산 셀의 범위는 전체 큐브입니다.|  
|단일 멤버 집합|단일 멤버로 확인되는 MDX 집합 식입니다.|  
|수준 멤버 집합|단일 수준의 멤버로 확인되는 MDX 집합 식입니다. 이런 집합 식의 한 예가 *Level_Expression*.**Members** MDX 함수입니다. 계산 멤버를 포함하려면 *Level_Expression*.**AllMembers** MDX 함수를 사용합니다. 자세한 내용은 [AllMembers&#40;MDX&#41;](../../../mdx/allmembers-mdx.md)를 참조하세요.|  
|하위 항목 집합|지정된 멤버의 하위 항목으로 확인되는 MDX 집합 식입니다. 이런 집합 식의 한 예가 **Descendants**(*Member_Expression*, *Level_Expresion*, *Desc_Flag*) MDX 함수입니다. 자세한 내용은 [Descendants&#40;MDX&#41;](../../../mdx/descendants-mdx.md)를 참조하세요.|  
  
 `String_Expression` 인수가 차원을 설명하지 않으면 MDX는 계산 하위 큐브를 만들 목적으로 모든 멤버가 포함되는 것으로 가정합니다. 따라서 `String_Expression` 인수가 NULL이면 계산 셀 정의는 전체 큐브에 적용됩니다.  
  
 `MDX_Expression` 인수는 `String_Expression` 인수에 정의된 모든 셀에 대한 셀 값이 되는 MDX 식을 포함합니다.  
  
## 기타 고려 사항  
 MDX는 **CONDITION** 속성으로 지정되는 계산 조건을 한 번만 처리합니다. 이 단 한 번의 처리로 특히 전체 큐브 패스에 대해 중복되는 계산 셀을 통해 여러 계산 셀 정의 평가에 대한 성능이 향상됩니다.  
  
 이런 단일 처리가 발생하는 시기는 계산 셀 정의의 작성 범위에 따라 결정됩니다.  
  
-   전체 범위에서 큐브의 일부로 만들어지는 경우 MDX는 큐브가 처리될 때 계산 조건을 처리합니다. 큐브에서 어떤 방식으로든 셀이 수정되고 그 셀이 계산 셀 정의의 계산 하위 큐브에 포함되는 경우에는 큐브가 다시 처리될 때까지는 셀 조건이 정확하지 않을 수도 있습니다. 예를 들어 셀은 쓰기 저장에서 수정될 수 있습니다. 계산 조건은 큐브를 다시 처리할 때 다시 처리됩니다.  
  
-   세션 범위에서 만들어진 경우 MDX는 세션 중에 문이 실행될 때 계산 조건을 처리합니다. 계산 셀 정의가 전체적으로 만들어지는 경우와 마찬가지로, 셀이 수정되는 경우에는 계산 조건이 계산 셀 정의에 대해 정확하지 않을 수도 있습니다.  
  
-   쿼리 범위에서 만들어진 경우 MDX는 쿼리가 실행될 때 계산 조건을 처리합니다. MDX 쿼리 실행의 짧은 처리 시간 때문에 데이터 대기 시간 문제가 최소화되긴 하지만 셀 수정 문제는 여기서도 적용됩니다.  
  
 한편으로 MDX는 계산 셀 정의에 포함된 셀과 관련된 큐브에 대해 MDX 쿼리를 실행할 때마다 계산 수식을 처리합니다. 작성 범위에 상관없이 이렇게 처리됩니다.  
  
## 관련 항목:  
 [CREATE CELL CALCULATION 문&#40;MDX&#41;](../Topic/CREATE%20CELL%20CALCULATION%20Statement%20\(MDX\).md)  
  
  