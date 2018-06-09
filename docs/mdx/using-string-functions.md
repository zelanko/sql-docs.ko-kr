---
title: 문자열 함수를 사용 하 여 | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6e151d06d086569b16fcdf1dc3570f9b220dfcd6
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743832"
---
# <a name="using-string-functions"></a>문자열 함수 사용


  문자열 함수는 MDX의 거의 모든 개체에서 사용할 수 있습니다. 문자열 함수는 저장 프로시저에서 개체를 문자열 표현으로 변환하는 데 사용되며 값을 반환하기 위해 개체에 대한 문자열 식을 계산할 때도 사용됩니다.  
  
 가장 널리 사용 되는 문자열 함수는 **이름** 및 **Uniquename**합니다. 이러한 함수는 각각 개체의 이름과 고유 이름을 반환합니다. 이러한 함수는 대개 함수가 반환하는 멤버를 찾기 위해 계산을 디버깅할 때 사용됩니다.  
  
## <a name="examples"></a>예  
 다음 예제 쿼리에서는 이러한 함수를 사용하는 방법을 보여 줍니다.  
  
 `WITH`  
  
 `//Returns the name of the current Product on rows`  
  
 `MEMBER [Measures].[ProductName] AS [Product].[Product].CurrentMember.Name`  
  
 `//Returns the uniquename of the current Product on rows`  
  
 `MEMBER [Measures].[ProductUniqueName] AS [Product].[Product].CurrentMember.Uniquename`  
  
 `//Returns the name of the Product dimension`  
  
 `MEMBER [Measures].[ProductDimensionName] AS [Product].Name`  
  
 `SELECT  {[Measures].[ProductName],[Measures].[ProductUniqueName],[Measures].[ProductDimensionName]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 **생성** 함수 집합의 각 멤버에서 문자열 함수를 실행 하 고 다음 결과 연결에 사용할 수 있습니다. 또한 이 함수는 계산을 디버깅할 때 유용할 수 있습니다. 사용자는 이 함수를 사용하여 집합의 내용을 시각화할 수 있습니다. 다음 예에서는 이 함수를 이러한 방식으로 사용하는 방법을 보여 줍니다.  
  
 `WITH`  
  
 `//Returns the names of the current Product and its ancestors up to the All Member`  
  
 `MEMBER [Measures].[AncestorNames] AS`  
  
 `GENERATE(`  
  
 `ASCENDANTS([Product].[Product Categories].CurrentMember)`  
  
 `, [Product].[Product Categories].CurrentMember.Name, ", ")`  
  
 `SELECT`  
  
 `{[Measures].[AncestorNames]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product Categories].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 많이 사용되는 또 다른 문자열 함수 그룹은 개체의 고유 이름을 포함하는 문자열 또는 개체로 계산되는 식을 개체 자체로 캐스팅하는 함수입니다. 다음 예제 쿼리에서 방법을 보여 줍니다 방법을 **StrToMember** 및 **StrToSet** 함수가 작업을 수행 합니다.  
  
 `SELECT`  
  
 `{StrToMember("[Measures].[Inter" + "net Sales Amount]")}`  
  
 `ON COLUMNS,`  
  
 `StrToSet("{`  
  
 `[Product].[Product Categories].[Category].&[3],`  
  
 `[Product].[Product Categories].[Product].&[477],`  
  
 `[Product].[Product Categories].[Product].&[788],`  
  
 `[Product].[Product Categories].[Product].&[708],`  
  
 `[Product].[Product Categories].[Product].&[711]`  
  
 `}")`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
> [!NOTE]  
>  **StrToMember** 및 **StrToSet** 주의 하 여 함수를 사용 해야 합니다. 이러한 함수를 계산 정의 내에 사용할 때 쿼리 성능이 저하될 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [생성 &#40;MDX&#41;](../mdx/generate-mdx.md)   
 [이름 &#40;MDX&#41;](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [함수 &#40;MDX 구문&#41;](../mdx/functions-mdx-syntax.md)   
 [저장된 프로시저를 사용 하 여 &#40;MDX&#41;](../mdx/using-stored-procedures-mdx.md)   
 [StrToMember &#40;MDX&#41;](../mdx/strtomember-mdx.md)   
 [StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md)  
  
  
