---
title: Except (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9ec5eba8f7df7fa7aabd65479fcf08ee7afec9c7
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578295"
---
# <a name="except-mdx-function"></a>Except (MDX) 함수
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  두 집합을 계산하고 첫 번째 집합에서 두 번째 집합에도 존재하는 튜플을 제거합니다. 중복 요소를 유지할 수도 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Except(Set_Expression1, Set_Expression2 [, ALL ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression1*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Set_Expression2*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 경우 **모든** 가 지정 하는 함수는 첫 번째 집합에서 발견 된 중복 요소를 유지 합니다; 두 번째 집합에 있는 중복 제거 됩니다. 멤버는 첫 번째 집합에 나타나는 순서대로 반환됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이 함수의 사용 방법을 보여 줍니다.  
  
```  
   //This query shows the quantity of orders for all products,  
   //with the exception of Components, which are not  
   //sold.  
SELECT   
   [Date].[Month of Year].Children  ON COLUMNS,  
   Except  
      ([Product].[Product Categories].[All].Children ,  
         {[Product].[Product Categories].[Components]}  
      ) ON ROWS  
FROM  
   [Adventure Works]  
WHERE  
   ([Measures].[Order Quantity])  
```  
  
## <a name="see-also"></a>관련 항목  
 [- &#40;제외 하 고&#41; &#40;MDX&#41;](../mdx/except-mdx-operator.md)   
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
