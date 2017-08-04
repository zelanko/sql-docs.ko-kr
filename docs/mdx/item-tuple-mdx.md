---
title: "Item (튜플) (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ITEM
dev_langs:
- kbMDX
helpviewer_keywords:
- Item function
ms.assetid: 9ee7af55-d5b5-47c8-a480-ef23878306af
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6e9411f3e4404a29ff0908ff53b0e0fb443b1703
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="item-tuple-mdx"></a>Item(튜플)(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  집합에서 튜플을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Index syntax  
Set_Expression.Item(Index)  
  
String expression syntax  
Set_Expression.Item(String_Expression1 [ ,String_Expression2,...n])  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *String_Expression1*  
 유효한 문자열 식으로서, 일반적으로 문자열로 표현된 튜플입니다.  
  
 *String_Expression2*  
 유효한 문자열 식으로서, 일반적으로 문자열로 표현된 튜플입니다.  
  
 *인덱스*  
 반환할 집합 내의 위치로 특정 튜플을 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>주의  
 **항목** 함수는 지정된 된 집합에서 튜플을 반환 합니다. 세 가지 가능한 방법으로 호출 하 여 **항목** 함수:  
  
-   단일 문자열 식이 지정 된 경우는 **항목** 함수는 지정된 된 튜플을 반환 합니다. 예를 들면 "([2005].Q3, [Store05])"와 같습니다.  
  
-   둘 이상의 문자열 식이 지정 된을 **항목** 함수는 지정 된 좌표로 정의 된 튜플을 반환 합니다. 문자열의 번호는 축의 번호와 일치해야 하며 각 문자열은 고유한 계층을 식별해야 합니다. 예를 들면 "[2005].Q3", "[Store05]"와 같습니다.  
  
-   정수를 지정 하는 경우는 **항목** 함수에 지정 된 0부터 시작 위치에 있는 튜플을 반환 *인덱스*합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 ([1996],Sales)를 반환합니다.  
  
 `{([1996],Sales), ([1997],Sales), ([1998],Sales)}.Item(0)`  
  
 다음 예에서는 수준 식을 사용하고 Australia의 각 State-Province에 대한 Internet Sales Amount와 Australia의 총 Internet Sales Amount에 대한 이 값의 백분율을 반환합니다. 이 예에서는 Item 함수를 사용 하 여 반환한 집합에서 첫 번째 (및 튜플만)을 추출 하는 **상위** 함수입니다.  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   ( [Measures].[Internet Sales Amount],    
      Ancestors   
      ( [Customer].[Customer Geography].CurrentMember,  
        [Customer].[Customer Geography].[Country]  
      ).Item (0)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{ Descendants   
   ( [Customer].[Customer Geography].[Country].&[Australia],  
     [Customer].[Customer Geography].[State-Province], SELF   
   )   
} ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

