---
title: "간단한 예에서 쿼리 및 Slicer 축 사용(MDX) | Microsoft Docs"
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
  - "slicer 축"
  - "쿼리 축 [MDX]"
ms.assetid: 85bcb26f-5971-4153-b334-61f8d8b475b5
caps.latest.revision: 11
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 간단한 예에서 쿼리 및 Slicer 축 사용(MDX)
  이 항목에 제시된 예에서는 쿼리 및 slicer 축을 지정 및 사용하는 기본적인 방법을 설명합니다.  
  
## 큐브  
 Route 및 Time이라는 두 개의 간단한 차원을 가진 TestCube라는 이름의 큐브가 있는 경우 각 차원은 Route 및 Time으로 명명된 한 개의 사용자 계층만 가집니다. 큐브의 측정값은 Measures 차원의 일부이므로 이 큐브에는 모두 3개의 차원이 있습니다.  
  
## 쿼리  
 쿼리는 Packages 측정값을 경로와 횟수를 기준으로 비교할 수 있는 매트릭스를 제공합니다.  
  
 다음 MDX 쿼리 예에서 Route와 Time 계층은 쿼리 축이며 Measures 차원은 slicer 축입니다. [Members](../../../mdx/members-set-mdx.md) 함수는 MDX가 계층 또는 수준의 멤버를 사용하여 집합을 만들 것임을 나타냅니다. **Members** 함수를 사용하면 MDX 쿼리에서 특정 계층 또는 수준의 각 멤버를 명시적으로 지정할 필요가 없습니다.  
  
```  
SELECT  
   { Route.nonground.Members } ON COLUMNS,  
   { Time.[1st half].Members } ON ROWS  
FROM TestCube  
WHERE ( [Measures].[Packages] )  
```  
  
## 결과  
 결과는 COLUMNS와 ROWS 축 차원의 각 교차 위치에서 Packages 측정값을 보여 주는 표입니다. 다음 표에서는 이 표의 모양을 보여 줍니다.  
  
||air|sea|  
|-|---------|---------|  
|1st quarter|60|50|  
|2nd quarter|45|45|  
  
## 관련 항목:  
 [쿼리 축의 내용 지정&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/specifying-the-contents-of-a-query-axis-mdx.md)   
 [Slicer 축의 내용 지정&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/specifying-the-contents-of-a-slicer-axis-mdx.md)  
  
  