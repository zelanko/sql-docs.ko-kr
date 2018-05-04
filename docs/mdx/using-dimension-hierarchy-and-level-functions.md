---
title: 차원, 계층 및 수준 함수를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- dimensions [Analysis Services], functions
- level functions [MDX]
- hierarchy functions [MDX]
ms.assetid: e730f65a-1798-4094-9acf-2739e2505d52
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: ee0b18ebe3b72da6d417763be12f2d803eaf9c8c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-dimension-hierarchy-and-level-functions"></a>차원, 계층 구조, 수준 함수 사용
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  차원, 계층 및 수준 함수는 Analysis Services에서 사용되는 다차원 구조를 탐색하는 데 유용합니다. 일반적으로 이 함수들은 차원, 계층 또는 수준의 멤버에 관한 정보를 가져오는 작업에 다른 함수와 함께 사용됩니다.  
  
 사용 하는 방법을 보여 주는 다음 예제는 **합니다. 차원**, **합니다. 계층 구조**, 및 **합니다. 수준** 함수:  
  
 `WITH`  
  
 `MEMBER MEASURES.DIMENSIONNAME AS [Date].[Calendar].CURRENTMEMBER.DIMENSION.NAME`  
  
 `MEMBER MEASURES.HIERARCHYNAME AS [Date].[Calendar].CURRENTMEMBER.HIERARCHY.NAME`  
  
 `MEMBER MEASURES.LEVELNAME AS [Date].[Calendar].LEVEL.NAME`  
  
 `SELECT`  
  
 `{MEASURES.DIMENSIONNAME, MEASURES.HIERARCHYNAME, MEASURES.LEVELNAME}`  
  
 `ON Columns,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목:  
 [차원 &#40;MDX&#41;](../mdx/dimension-mdx.md)   
 [함수 &#40;MDX 구문&#41;](../mdx/functions-mdx-syntax.md)   
 [계층 구조 &#40;MDX&#41;](../mdx/hierarchy-mdx.md)   
 [수준 &#40;MDX&#41;](../mdx/level-mdx.md)  
  
  
