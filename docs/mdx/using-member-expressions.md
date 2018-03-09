---
title: "멤버 식을 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- members [MDX], expressions
- expressions [MDX], members
ms.assetid: 63c7af49-8bea-47c5-9566-a961f77d2a3d
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: bc1574fc06eeaa032fb68d395106721fc33ec699
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="using-member-expressions"></a>멤버 식 사용
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  멤버 식은 멤버 식별자, 멤버 함수 또는 멤버로 변환될 수 있는 식을 포함합니다.  
  
 멤버 식별자의 형식은 여러 가지일 수 있습니다. 가장 간단한 형식의 멤버 식별자는 멤버 이름으로 구성됩니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
SELECT Amount ON 0  
FROM [Adventure Works]  
  
```  
  
 그러나 서로 다른 계층에 이름이 같은 멤버가 여러 개 있는 경우 쿼리에서 반환할 멤버를 확인할 수 있는 방법은 없습니다. 예를 들어 다음 쿼리는 이름이 [CY 2004]인 멤버의 데이터를 요청합니다. 쿼리가 성공적으로 실행되지만 Adventure Works 큐브에 해당 이름의 멤버가 6개 이상 있습니다.  
  
```  
SELECT [CY 2004] ON 0  
FROM [Adventure Works]  
  
```  
  
 따라서 가장 신뢰할 수 있는 형식의 멤버 식별자는 큐브에서 특정 멤버를 식별하는 멤버의 고유 이름입니다. Analysis Services에서는 여러 가지 방법으로 고유 이름을 생성할 수 있지만 고유 이름은 항상 최소 두 개의 식별자인 차원 이름과 멤버 이름 또는 멤버 키로 구성됩니다. 고유 이름은 다음 형식으로 나타납니다.  
  
```  
  
Dimension_Name  
.[Hierarchy_Name.] [[{Member_Name | &Member_Key}.]... ] {Member_Name | &Member_Key}  
  
```  
  
 다음은 Adventure Works 큐브에서 가져온 멤버 고유 이름의 몇 가지 예입니다.  
  
```  
[Measures].[Amount]  
[Date].[Calendar Year].&[2004]  
[Date].[Calendar].[Calendar Quarter].&[2004]&[1]  
[Employee].[Employees].&[112]  
[Product].[Product Categories].[All Products]  
  
```  
  
 멤버를 반환하는 여러 MDX 함수가 있습니다. 전체 목록을 보려면 참조 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
> [!NOTE]  
>  멤버 이름과 멤버 키에 대 한 자세한 내용은 참조 [멤버, 튜플 및 집합 &#40; 사용 Mdx&#41; ](../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md).  
  
## <a name="see-also"></a>관련 항목:  
 [식 &#40; Mdx&#41;](../mdx/expressions-mdx.md)  
  
  
