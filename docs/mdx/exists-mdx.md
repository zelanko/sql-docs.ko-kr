---
title: Exists (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: Exists function
ms.assetid: 1e1d93b5-5be6-421c-b82b-839538ea50b1
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: e84cc419442fdd5435d926b247e5cf9d27c919e0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="exists-mdx"></a>Exists(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 첫 번째 집합에 있는 튜플 중 지정된 두 번째 집합에 있는 하나 이상의 튜플과 함께 존재하는 튜플의 집합을 반환합니다. 이 함수는 AUTOEXIST에서 자동으로 수행되는 작업을 수동으로 수행합니다. 에 대 한 자세한 내용은 존재에 대 한 참조 [MDX &#40;의 주요 개념 Analysis Services &#41; ](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md).  
  
 경우 선택적 \<측정값 그룹 이름 > 함수는 지정 된 측정값 그룹의 팩트 테이블의 행을 연결 하는 튜플 및 두 번째 집합에서 하나 이상의 튜플과 함께 존재 하는 튜플을 반환 제공 됩니다.  
  
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
  
## <a name="remarks"></a>주의  
  
1.  Null 값을 포함 하는 측정값이 포함 된 측정값 그룹 행에 영향을 **Exists** MeasureGroupName 인수가 지정 된 경우. 이 Exists 폼과 Nonempty 함수 간에는 다음과 같은 차이가 있습니다. 이 측정값의 NullProcessing 속성이 Preserve로 설정된 경우 큐브의 해당 부분에 대해 쿼리가 실행되면 측정값은 Null 값을 표시합니다. NonEmpty는 항상 Null 측정값이 있는 집합에서 튜플을 제거하는 반면, MeasureGroupName 인수를 사용하는 Exists는 측정값이 Null인 경우에도 연결된 측정값 그룹이 있는 튜플을 필터링하지 않습니다.  
  
2.  경우 *MeasureGroupName* 매개 변수는 사용, 참조 된 측정값 그룹에 측정값을 볼 수 있는지 여부를; 참조 된 측정값 그룹에 측정값이 없으면 볼 수 없는 경우 EXISTS는 항상 빈 집합을의 값에 관계 없이 반환 결과에 따라 달라 집니다 *Set_Expression1* 및 *Set_Expression2*합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)   
 [크로스 조인 &#40; Mdx&#41;](../mdx/crossjoin-mdx.md)   
 [NonEmptyCrossjoin &#40; Mdx&#41;](../mdx/nonemptycrossjoin-mdx.md)   
 [비어 있지 않은 &#40; Mdx&#41;](../mdx/nonempty-mdx.md)   
 [IsEmpty &#40; Mdx&#41;](../mdx/isempty-mdx.md)  
  
  
