---
title: Except (MDX) | Microsoft Docs
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
f1_keywords: EXCEPT
dev_langs: kbMDX
helpviewer_keywords: Except function
ms.assetid: 5d832c82-1e6d-4308-9c26-7edb8afe11dd
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 9e6f07d27d51e06a31def5ae6dd1ca9967dc6d57
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
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
  
## <a name="remarks"></a>주의  
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
  
## <a name="see-also"></a>관련 항목:  
 [-&#40; 제외 하 고 &#41; &#40; Mdx&#41;](../mdx/except-mdx-operator.md)   
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
