---
title: "(MDX) 간단한 예에서 쿼리 및 Slicer 축 사용 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- slicer axis
- query axis [MDX]
ms.assetid: 85bcb26f-5971-4153-b334-61f8d8b475b5
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5e3dd069c68623f9f0cc5f4fa90a06ca9a3568e1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-query-and-slicer-axes---using-axes-in-a-simple-example"></a>MDX 쿼리 및 Slicer 축-축을 사용 하 여 간단한 예제
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]이 항목에 제시 된 간단한 예제를 지정 하 고 쿼리 및 slicer 축을 사용 하는 기본적인 방법을 설명 합니다.  
  
## <a name="the-cube"></a>큐브  
 Route 및 Time이라는 두 개의 간단한 차원을 가진 TestCube라는 이름의 큐브가 있는 경우 각 차원은 Route 및 Time으로 명명된 한 개의 사용자 계층만 가집니다. 큐브의 측정값은 Measures 차원의 일부이므로 이 큐브에는 모두 3개의 차원이 있습니다.  
  
## <a name="the-query"></a>쿼리  
 쿼리는 Packages 측정값을 경로와 횟수를 기준으로 비교할 수 있는 매트릭스를 제공합니다.  
  
 다음 MDX 쿼리 예에서 Route와 Time 계층은 쿼리 축이며 Measures 차원은 slicer 축입니다. [Members](../../../mdx/members-set-mdx.md) 함수는 MDX가 계층 또는 수준의 멤버를 사용하여 집합을 만들 것임을 나타냅니다. **Members** 함수를 사용하면 MDX 쿼리에서 특정 계층 또는 수준의 각 멤버를 명시적으로 지정할 필요가 없습니다.  
  
```  
SELECT  
   { Route.nonground.Members } ON COLUMNS,  
   { Time.[1st half].Members } ON ROWS  
FROM TestCube  
WHERE ( [Measures].[Packages] )  
```  
  
## <a name="the-results"></a>결과  
 결과는 COLUMNS와 ROWS 축 차원의 각 교차 위치에서 Packages 측정값을 보여 주는 표입니다. 다음 표에서는 이 표의 모양을 보여 줍니다.  
  
||air|sea|  
|-|---------|---------|  
|1st quarter|60|50|  
|2nd quarter|45|45|  
  
## <a name="see-also"></a>관련 항목:  
 [쿼리 축의 내용 지정&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)   
 [Slicer 축의 내용 지정&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)  
  
  
