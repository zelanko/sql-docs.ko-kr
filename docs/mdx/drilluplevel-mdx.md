---
title: DrillupLevel (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e00851557b502bda3a98763eff4bac9c3abdccff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62690773"
---
# <a name="drilluplevel-mdx"></a>DrillupLevel(MDX)


  지정한 수준 아래에 있는 집합의 멤버를 드릴업합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DrillupLevel(Set_Expression [ , Level_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Level_Expression*  
 수준을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **DrillupLevel** 지정한 집합에 포함 된 멤버를 기준으로 한 멤버 집합을 계층적으로 구성 하는 함수 반환 합니다. 지정된 집합의 멤버 간 순서는 유지됩니다.  
  
 수준 식이 지정 되는 **DrillupLevel** 함수는 지정 된 수준의 위쪽에 있는 멤버만 검색 하 여 집합을 구성 합니다. 수준 식이 지정되어 있고 지정된 집합에 지정된 수준의 멤버가 표시되지 않는 경우에는 지정된 집합이 반환됩니다.  
  
 수준 식이 지정되지 않은 경우 이 함수는 지정된 집합에서 참조되는 첫 번째 차원의 가장 낮은 수준보다 한 수준 높은 멤버만 검색하여 집합을 구성합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 첫 번째 집합에서 Subcategory 수준의 위쪽에 있는 멤버의 집합을 반환합니다.  
  
```  
SELECT DrillUpLevel   
  ({[Product].[Product Categories].[All Products]  
    ,[Product].[Product Categories].[Subcategory].&[32],  
    [Product].[Product Categories].[Product].&[215]},  
  [Product].[Product Categories].[Subcategory]  
    )  
  ON 0  
  FROM [Adventure Works]  
  WHERE [Measures].[Internet Order Quantity]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
