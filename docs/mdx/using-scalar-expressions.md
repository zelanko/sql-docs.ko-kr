---
title: 스칼라 식을 사용 하 여 | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a80933b1a9845ec2676fba470ed39e06ee7f4ad8
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743902"
---
# <a name="using-scalar-expressions"></a>스칼라 식 사용


  MDX에서 스칼라 식은 계산 시 계산 컨텍스트 내에서 단일 값을 반환하는 MDX 구문의 한 요소입니다.  
  
 스칼라 식은 MDX에 문자열, 숫자 및 날짜 식을 포함합니다.  
  
 일반적으로 스칼라 식은 계산 멤버 정의에 사용됩니다. 계산 멤버는 스칼라 값을 반환해야 합니다. 다음 쿼리에서는 서로 다른 유형의 스칼라 식을 사용하는 Measures 차원의 계산 멤버 예를 보여 줍니다.  
  
 `WITH`  
  
 `MEMBER MEASURES.NumericValue AS 10`  
  
 `MEMBER MEASURES.NumericExpression AS 10 + 10`  
  
 `MEMBER MEASURES.NumericExpressionBasedOnMeasure AS [Measures].[Internet Sales Amount] + 10`  
  
 `MEMBER MEASURES.StringValue AS "10"`  
  
 `MEMBER MEASURES.ConcatenatedString AS "10" + "10"`  
  
 `MEMBER MEASURES.StringFunction AS MEASURES.CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.TodaysDate AS NOW()`  
  
 `SELECT`  
  
 `{MEASURES.NumericValue,MEASURES.NumericExpression,MEASURES.NumericExpressionBasedOnMeasure,`  
  
 `MEASURES.StringValue, MEASURES.ConcatenatedString, MEASURES.StringFunction, MEASURES.TodaysDate}`  
  
 `ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
 계산 측정값 또는 기타 측정값에서 반환할 수 있는 유일한 데이터 형식은 OLE Variant입니다. 따라서 예상하는 동작을 가져오도록 측정값을 특정 유형으로 캐스팅해야 할 경우도 있습니다. 다음 쿼리에서는 이러한 예를 보여 줍니다.  
  
```  
WITH  
//Two calculated measures that return strings  
MEMBER MEASURES.NumericString1 AS "10"  
MEMBER MEASURES.NumericString2 AS "10"  
//In this case, the + operator acts to concatenate the strings  
MEMBER MEASURES.Concatenation AS MEASURES.NumericString1 + MEASURES.NumericString2  
//Casting one value to an integer with the CINT function causes the second measure  
//to be treated as an integer too, so that the + operator now acts to add the values  
MEMBER MEASURES.Addition AS CINT(MEASURES.NumericString1) + MEASURES.NumericString2  
SELECT  
{MEASURES.NumericString1,MEASURES.NumericString2,MEASURES.Concatenation,MEASURES.Addition }  
ON COLUMNS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [식 &#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
