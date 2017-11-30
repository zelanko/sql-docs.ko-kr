---
title: Dimension (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: Dimension
dev_langs: kbMDX
helpviewer_keywords: Dimension function
ms.assetid: 0e3ce539-1d34-45ca-8342-67796e11b730
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ecf8801b32ffc559d1ba51c51e0a361236451f06
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="dimension-mdx"></a>Dimension(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 멤버, 수준 또는 계층을 포함하고 있는 계층을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Hierarchy syntax  
Hierarchy_Expression.Dimension  
  
Level syntax  
Level_Expression.Dimension  
  
Member syntax  
Member_Expression.Dimension  
  
```  
  
## <a name="arguments"></a>인수  
 *Hierarchy_Expression*  
 계층을 반환하는 유효한 MDX 식입니다.  
  
 *Level_Expression*  
 수준을 반환하는 유효한 MDX 식입니다.  
  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
### <a name="examples"></a>예  
 다음 예제에서는 **차원** 와 함께에서 함수는 **이름** 함수를 지정된 된 멤버의 계층 이름을 반환 합니다.  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Name  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
 다음 예에서는 Dimension 함수와 Levels 및 Count 함수를 함께 사용하여 지정된 멤버가 들어 있는 계층의 수준 수를 반환합니다.  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
 다음 예제에서는 **차원** 와 함께에서 함수는 **멤버** 및 **Count** 지정 된 멤버가 들어 있는 계층의 멤버 수를 반환 하는 함수, 합니다.  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Count &#40; 계층 수준 &#41; &#40; Mdx&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Count &#40; 설정 &#41; &#40; Mdx&#41;](../mdx/count-set-mdx.md)   
 [수준 &#40; Mdx&#41;](../mdx/levels-mdx.md)   
 [멤버 &#40; 설정 &#41; &#40; Mdx&#41;](../mdx/members-set-mdx.md)   
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
