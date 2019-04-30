---
title: Crossjoin (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b68dafa89f8285f532fc6e92e80f9741be239f65
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63248262"
---
# <a name="crossjoin-mdx"></a>Crossjoin(MDX)


  하나 이상의 집합에 대한 교차곱을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Standard syntax  
Crossjoin(Set_Expression1 ,Set_Expression2 [,...n] )  
  
Alternate syntax  
Set_Expression1 * Set_Expression2 [* ...n]  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression1*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Set_Expression2*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **Crossjoin** 이상 지정 된 집합 또는 함수 2의 교차곱을 반환 합니다. 결과 집합에서 튜플의 순서는 집합의 조인 순서 및 해당 멤버의 순서에 따라 달라집니다. 예를 들어 경우 첫 번째 집합은 구성의 {x1, x2,..., x*n*}, 고 두 번째 집합이 {y1, y2,..., y*n*}, 이러한 집합의 교차곱은:  
  
 {(x1, y1), (x1, y2),...,(x1, y*n*), (x2, y1), (x2, y2),...,  
  
 (x2, y*n*),..., (x*n*, y1), (x*n*, y2),..., (xn, y*n*)}  
  
> [!IMPORTANT]  
>  크로스 조인의 집합이 동일한 차원에 있는 다른 특성 계층의 튜플로 구성된 경우 이 함수는 실제로 존재하는 튜플만 반환합니다. 자세한 내용은 [9a43-81a1af7eb36c"&gt;key Concepts in MDX &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)합니다.  
  
## <a name="examples"></a>예  
 다음 쿼리에서는 쿼리의 Columns 및 Rows 축에서 Crossjoin 함수를 사용하는 간단한 예를 보여 줍니다.  
  
 `SELECT`  
  
 `[Customer].[Country].Members *`  
  
 `[Customer].[State-Province].Members`  
  
 `ON 0,`  
  
 `Crossjoin(`  
  
 `[Date].[Calendar Year].Members,`  
  
 `[Product].[Category].[Category].Members)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE Measures.[Internet Sales Amount]`  
  
 다음 예에서는 동일한 차원에서 서로 다른 계층을 크로스 조인할 때 발생하는 자동 필터링을 보여 줍니다.  
  
 `SELECT`  
  
 `Measures.[Internet Sales Amount]`  
  
 `ON 0,`  
  
 `//Only the dates in Calendar Years 2003 and 2004 will be returned here`  
  
 `Crossjoin(`  
  
 `{[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]},`  
  
 `[Date].[Date].[Date].Members)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 다음 세 개의 예에서는 동일한 결과, 즉 미국 내의 주에 대한 주별 인터넷 판매 금액(Internet Sales Amount)을 반환합니다. 처음 두 개의 예에서는 두 개의 크로스 조인 구문을 사용하고, 세 번째 예에서는 WHERE 절을 사용하여 동일한 정보를 반환하는 방법을 보여 줍니다.  
  
### <a name="example-1"></a>예제 1  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
       [Customer].[State-Province].Members  
   ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
### <a name="example-2"></a>예제 2  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
### <a name="example-3"></a>예 3  
  
```  
SELECT   
   [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
