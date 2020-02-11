---
title: 단항 연산자 | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9ec9ac3eef28c4deae08d577487599575852c132
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68893550"
---
# <a name="unary-operators"></a>단항 연산자


  MDX의 단항 연산자는 숫자 식의 음수 값 또는 양수 값을 반환하는 등의 단일 피연산자에 대한 연산을 수행합니다.  
  
 다음 표에서는 MDX가 지원하는 단항 연산자를 나열합니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|[-(음수)](../mdx/negative-mdx.md)|숫자 식의 음수 값을 반환합니다.|  
|[+(양수)](../mdx/positive-mdx.md)|숫자 식의 양수 값을 반환합니다.|  
  
 다음 예에서는 음수 측정 값을 반환하는 단항 연산자의 사용 방법을 설명합니다.  
  
```  
WITH   
   MEMBER [Measures].[NegDiscountAmount] AS  
   -[Measures].[Discount Amount]  
SELECT   
   {[Measures].[Discount Amount],[Measures].[NegDiscountAmount]} on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
 또한 MDX는 특수 단항 연산자를 사용 하 여 [RollupChildren](../mdx/rollupchildren-mdx.md) 함수에서 수행 하는 집계 작업을 결정 합니다. 이러한 특수 단항 연산자에 대 한 자세한 내용은 [차원에 사용자 지정 집계 추가](https://docs.microsoft.com/analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [연산자 &#40;MDX 구문&#41;](../mdx/operators-mdx-syntax.md)  
  
  
