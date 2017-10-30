---
title: "(나누기) (MDX) | Microsoft Docs"
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
- /
dev_langs:
- kbMDX
helpviewer_keywords:
- / (divide)
- divide operator (/)
ms.assetid: 42b7d3ea-234d-41b3-a849-f457be6d7972
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c980a9505ab69cd521edf5e72d3cd99028b4070b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="divide---mdx-operator-reference"></a>나누기-MDX 연산자 참조
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  한 수를 다른 수로 나누는 산술 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>매개 변수  
 *피제수*  
 숫자 값을 반환하는 유효한 MDX 식입니다.  
  
 *제 수*  
 숫자 값을 반환하는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 우선 순위가 더 높은 매개 변수의 데이터 형식을 갖는 값입니다.  
  
## <a name="remarks"></a>주의  
 반환 되는 실제 값은 **/ (나누기)** 연산자의은 첫째 식 둘째 식으로 나누어 나온 몫을 나타냅니다.  
  
 두 식이 모두 동일한 데이터 형식으로 되어 있거나 식 하나가 암시적으로 다른 식의 데이터 형식으로 변환될 수 있어야 합니다. 경우 *Divisor* 는 오류가 발생 된 null 값을 계산 합니다. 두 *Divisor* 및 *피제수* 평가 연산자를 null 값으로 null 값을 반환 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이 연산자의 사용 방법을 보여 줍니다.  
  
```  
-- This query returns the freight cost per user,  
-- for products, averaged by month.   
With Member [Measures].[Freight Per Customer] as  
    [Measures].[Internet Freight Cost]  
    /   
    [Measures].[Customer Count]  
  
SELECT   
    [Ship Date].[Calendar].[Calendar Year] Members ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Freight Per Customer])  
```  
  
 0이 아닌 값 또는 Null이 아닌 값을 0 또는 Null로 나누면 쿼리 결과에 "1.#INF" 값으로 표시되는 Infinity 값을 반환합니다. 대부분의 경우 이러한 상황을 방지하기 위해 0으로 나누기를 검사해야 합니다. 다음 예에서는 이러한 방법을 보여 줍니다.  
  
 `//Returns 1.#INF when Internet Sales Amount is zero or null`  
  
 `Member [Measures].[Reseller to Internet Ratio] AS`  
  
 `[Measures].[Reseller Sales Amount]`  
  
 `/`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `//Traps the division by zero scenario and returns null instead of 1.#INF`  
  
 `Member [Measures].[Reseller to Internet Ratio With Error Handling] AS`  
  
 `IIF([Measures].[Internet Sales Amount]=0, NULL,`  
  
 `[Measures].[Reseller Sales Amount]`  
  
 `/`  
  
 `[Measures].[Internet Sales Amount])`  
  
 `SELECT`  
  
 `{[Measures].[Reseller to Internet Ratio],[Measures].[Reseller to Internet Ratio With Error Handling]} ON 0,`  
  
 `[Product].[Category].[Category].Members ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 `WHERE([Date].[Calendar].[Calendar Year].&[2001])`  
  
## <a name="see-also"></a>관련 항목:  
 [IIf &#40; Mdx&#41;](../mdx/iif-mdx.md)   
 [MDX 연산자 참조 &#40; Mdx&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

