---
title: "스칼라 식을 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- scalar expressions
- expressions [MDX], scalar
ms.assetid: 4678b675-8fbd-4e5b-a519-d4cd1bb8c46a
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 67966680e10b35064c65a91f8b8da22a00fb17c4
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="using-scalar-expressions"></a>스칼라 식 사용
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="see-also"></a>관련 항목:  
 [식 &#40; Mdx&#41;](../mdx/expressions-mdx.md)  
  
  

