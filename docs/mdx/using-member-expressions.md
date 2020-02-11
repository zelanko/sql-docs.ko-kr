---
title: 멤버 식 사용 | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8d40d6a3b6cacb65cf1463b0eeb8b29e59e079e4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68893511"
---
# <a name="using-member-expressions"></a>멤버 식 사용


  멤버 식은 멤버 식별자, 멤버 함수 또는 멤버로 변환될 수 있는 식을 포함합니다.  
  
 멤버 식별자의 형식은 여러 가지일 수 있습니다. 가장 간단한 형식의 멤버 식별자는 멤버 이름으로 구성됩니다. 다음은 그 예입니다.  
  
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
  
 멤버를 반환하는 여러 MDX 함수가 있습니다. 전체 목록은 mdx [함수 참조 &#40;mdx](../mdx/mdx-function-reference-mdx.md) 를 참조 하세요&#41;  
  
> [!NOTE]  
>  멤버 이름 및 멤버 키에 대 한 자세한 내용은 [MDX&#41;&#40;멤버, 튜플 및 집합 작업 ](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [MDX &#40;식&#41;](../mdx/expressions-mdx.md)  
  
  
