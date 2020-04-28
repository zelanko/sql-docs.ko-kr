---
title: Exists (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ba2cef1cfb95319cbe0aff827cb251ff7e2317c2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68893617"
---
# <a name="exists-mdx"></a>Exists(MDX)


  지정된 첫 번째 집합에 있는 튜플 중 지정된 두 번째 집합에 있는 하나 이상의 튜플과 함께 존재하는 튜플의 집합을 반환합니다. 이 함수는 AUTOEXIST에서 자동으로 수행되는 작업을 수동으로 수행합니다. Auto exists에 대 한 자세한 내용은 [MDX의 주요 개념 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)를 참조 하세요.  
  
 선택적인 \<측정값 그룹 이름> 제공 되는 경우이 함수는 두 번째 집합의 튜플이 하나 이상 있고 지정 된 측정값 그룹의 팩트 테이블에 연결 된 행이 있는 튜플을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Exists( Set_Expression1 , Set_Expression2 [, MeasureGroupName] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression1*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Set_Expression2*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *MeasureGroupName*  
 측정값 그룹 이름을 지정하는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>설명  
  
1.  MeasureGroupName 인수가 지정 된 경우 null 값을 포함 하는 측정값이 있는 측정값 그룹 행이 **존재** 합니다. 이 형식의 존재와 비어 있지 않은 함수 간의 차이점입니다. 이러한 측정값의 NullProcessing 속성이 Preserve로 설정 되어 있으면 큐브의 해당 부분에 대해 쿼리를 실행할 때 측정값에 Null 값이 표시 됩니다. 비어 있지 않으면 항상 Null 측정값을 포함 하는 집합에서 튜플을 제거 하는 반면, MeasureGroupName 인수를 사용 하는 경우 측정값은 Null 인 경우에도 연결 된 측정값 그룹 행이 있는 튜플을 필터링 하지 않습니다.  
  
2.  *MeasureGroupName* 매개 변수를 사용 하는 경우 참조 되는 측정값 그룹에 표시 되는 측정값이 있는지 여부에 따라 결과가 달라 집니다. 참조 된 측정값 그룹에 표시 되는 측정값이 없으면 *Set_Expression1* 및 *Set_Expression2*의 값에 관계 없이 항상 빈 집합이 반환 됩니다.  
  
## <a name="examples"></a>예  
 캘리포니아에 거주하는 고객  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Customer].[State-Province].&[CA]&[US]}  
) ON 1   
FROM [Adventure Works]  
  
```  
  
 캘리포니아에 거주하며 제품을 구입한 적이 있는 고객  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Customer].[State-Province].&[CA]&[US]}  
, "Internet Sales") ON 1   
FROM [Adventure Works]  
  
```  
  
 제품을 구입한 적이 있는 고객  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, , "Internet Sales") ON 1   
FROM [Adventure Works]  
  
```  
  
 자전거를 구입한 고객  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Product].[Product Categories].[Category].&[1]}  
, "Internet Sales") ON 1   
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Crossjoin &#40;MDX&#41;](../mdx/crossjoin-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)   
 [비어 있지 않은 &#40;MDX&#41;](../mdx/nonempty-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)  
  
  
