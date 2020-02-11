---
title: CurrentMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 374a38d07c3174e799d01199e20e822f85deed13
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892918"
---
# <a name="currentmember-mdx"></a>CurrentMember(MDX)


  반복하는 동안 지정된 계층을 따라 현재 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Hierarchy_Expression.CurrentMember  
```  
  
## <a name="arguments"></a>인수  
 *Hierarchy_Expression*  
 계층을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 계층 멤버 집합에서 반복하는 동안 반복의 각 단계에서 작업이 수행되는 대상 멤버가 현재 멤버입니다. **Currentmember** 함수는 해당 멤버를 반환 합니다.  
  
> [!IMPORTANT]  
>  차원에 표시 가능한 계층이 하나만 있는 경우 해당 차원 이름은 표시 가능한 유일한 계층으로 확인되므로 해당 계층을 차원 이름이나 계층 이름 중 하나로 참조할 수 있습니다. 예를 들어 `Measures.CurrentMember`는 Measures 차원의 유일한 계층으로 확인되므로 유효한 MDX 식입니다.  
  
## <a name="examples"></a>예  
 다음 쿼리는 **Currentmember** 를 사용 하 여 열, 행 및 조각 축의 계층에서 현재 멤버를 찾는 방법을 보여 줍니다.  
  
 `WITH MEMBER MEASURES.CURRENTDATE AS`  
  
 `[Date].[Calendar].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTPRODUCT AS`  
  
 `[Product].[Product Categories].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTMEASURE AS`  
  
 `MEASURES.CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTCUSTOMER AS`  
  
 `[Customer].[Customer Geography].CURRENTMEMBER.NAME`  
  
 `SELECT`  
  
 `[Product].[Product Categories].[Category].MEMBERS`  
  
 `*`  
  
 `{MEASURES.CURRENTDATE, MEASURES.CURRENTPRODUCT,MEASURES.CURRENTMEASURE, MEASURES.CURRENTCUSTOMER}`  
  
 `ON 0,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Customer].[Customer Geography].[Country].&[Australia])`  
  
 현재 멤버는 쿼리의 축에 사용된 계층에서 변경됩니다. 따라서 축에 사용 되지 않는 동일한 차원의 다른 계층에 있는 현재 멤버도 변경 될 수 있습니다. 이 동작을 ' 자동 존재 ' 라고 하며 자세한 내용은 [MDX &#40;Analysis Services&#41;의 주요 개념 ](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)에서 찾을 수 있습니다. 예를 들어 아래 쿼리에서는 Date 차원의 Calendar Year 계층에 있는 현재 멤버가 Rows 축에 표시되는 Calendar 계층의 현재 멤버와 함께 변경되는 방법을 보여 줍니다.  
  
 `WITH MEMBER MEASURES.CURRENTYEAR AS`  
  
 `[Date].[Calendar Year].CURRENTMEMBER.NAME`  
  
 `SELECT`  
  
 `{MEASURES.CURRENTYEAR}`  
  
 `ON 0,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 **Currentmember** 는 사용 중인 쿼리의 컨텍스트를 인식 하 여 계산 하도록 하는 데 매우 중요 합니다. 다음 예에서는 **놀이 Works** 큐브에서 각 제품의 주문 수량과 범주 및 모델 별로 주문 수량 비율을 반환 합니다. **Currentmember** 함수는 계산 중에 주문 수량이 사용 될 제품을 식별 합니다.  
  
```  
WITH   
   MEMBER [Measures].[Order Percent by Category] AS  
   CoalesceEmpty  
(   
      ([Product].[Product Categories].CurrentMember,  
        Measures.[Order Quantity]) /   
          (  
           Ancestor  
           ( [Product].[Product Categories].CurrentMember,   
             [Product].[Product Categories].[Category]  
           ), Measures.[Order Quantity]  
       ), 0  
   ), FORMAT_STRING='Percent'  
SELECT   
   {Measures.[Order Quantity],  
      [Measures].[Order Percent by Category]} ON COLUMNS,  
{[Product].[Product].Members} ON ROWS  
FROM [Adventure Works]  
WHERE {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
