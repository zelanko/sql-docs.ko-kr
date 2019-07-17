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
ms.openlocfilehash: 781c03283c39ab5ec100ba7f7d83b3cbe19a7c19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139179"
---
# <a name="exists-mdx"></a>Exists(MDX)


  지정된 첫 번째 집합에 있는 튜플 중 지정된 두 번째 집합에 있는 하나 이상의 튜플과 함께 존재하는 튜플의 집합을 반환합니다. 이 함수는 AUTOEXIST에서 자동으로 수행되는 작업을 수동으로 수행합니다. 에 대 한 자동에 대 한 자세한 내용은 참조 하세요 [9a43-81a1af7eb36c"&gt;key Concepts in MDX &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)합니다.  
  
 경우 선택적 \<측정값 그룹 이름 >을 제공 하면 하나 이상의 튜플의 갖는 튜플에 존재 하는 두 번째 집합에서 지정 된 측정값 그룹의 팩트 테이블의 행을 연결 된 있는 튜플을 반환 합니다.  
  
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
  
1.  Null 값을 포함 하는 측정값을 사용 하 여 측정값 그룹 행에 기여 **Exists** MeasureGroupName 인수가 지정 된 경우. Exists의이 폼과 Nonempty 함수 간의 차이입니다:이 측정값의 NullProcessing 속성이 Preserve로이 경우 측정값; 큐브의 해당 부분에 대해 쿼리를 실행할 때 Null 값이 표시 됩니다 비어 있지 않은 MeasureGroupName 인수를 사용 하는 Exists 측정 값이 null 인 경우에 연관 된 측정값 그룹 행이 있는 튜플을 필터링 하지 것입니다 하지만 Null 측정값이 있는 집합에서 튜플을 제거 항상 됩니다.  
  
2.  하는 경우 *MeasureGroupName* 매개 변수는 사용, 참조 된 측정값 그룹에 측정값을 볼 수 있는지 여부를; 참조 된 측정값 그룹에 측정값이 없으면 표시 경우 EXISTS는 항상 반환 결과에 따라 달라 집니다는 빈 집합의 값에 관계 없이 *Set_Expression1* 하 고 *Set_Expression2*합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 & #40; Mdx& #41;](../mdx/mdx-function-reference-mdx.md)   
 [Crossjoin &#40;MDX&#41;](../mdx/crossjoin-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)   
 [비어 있지 않은 &#40;MDX&#41;](../mdx/nonempty-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)  
  
  
