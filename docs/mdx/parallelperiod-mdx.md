---
title: ParallelPeriod (MDX) | Microsoft Docs
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
f1_keywords: PARALLELPERIOD
dev_langs: kbMDX
helpviewer_keywords: ParallelPeriod function
ms.assetid: 9c87f5a6-5694-46f1-9890-bd9705190ea7
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 7ffd7d68192806a30c65d7c446b3907e766401f8
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="parallelperiod-mdx"></a>ParallelPeriod (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 멤버와 상대적 위치가 같은 멤버를 이전 기간에서 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ParallelPeriod( [ Level_Expression [ ,Index [ , Member_Expression ] ] ] )  
```  
  
## <a name="arguments"></a>인수  
 *Level_Expression*  
 수준을 반환하는 유효한 MDX 식입니다.  
  
 *Index*  
 지정한 멤버와의 간격을 나타내는 병렬 기간 수를 지정하는 유효한 숫자 식입니다.  
  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 유사 하지만 [사촌](../mdx/cousin-mdx.md) 함수는 **ParallelPeriod** 함수는 시계열 더욱 긴밀 하 게 관련이 있습니다. **ParallelPeriod** 함수는 지정된 된 수준에서 지정된 된 멤버의 상위 항목, 지정 된 시간 간격의 상위 항목의 형제나 찾아서 마지막 형제의 하위 항목 중 지정된 된 멤버의 병렬 기간을 반환 합니다.  
  
 **ParallelPeriod** 함수는 다음 기본값을 가집니다.  
  
-   기본 멤버 값의 형식 가진 첫 번째 차원에 있는 첫 번째 계층의 현재 구성원은 수준 식과 멤버 식이 모두 지정 하는 경우 *시간* 측정값 그룹에 있습니다.  
  
-   수준 식이 지정 된 경우 표시 되지만 멤버 식이 지정 되지 않은 경우 기본 멤버 값은 *Level_Expression*. **Hierarchy.CurrentMember**합니다.  
  
-   기본 인덱스 값은 1입니다.  
  
-   기본 수준은 지정된 멤버의 부모 수준입니다.  
  
 **ParallelPeriod** 함수는 다음과 같은 MDX 문과 동일 합니다.  
  
 `Cousin(Member_Expression, Ancestor(Member_Expression, Level_Expression) .Lag(Numeric_Expression))`  
  
## <a name="example"></a>예제  
 다음 예에서는 Quarter 수준에 따라 기간 간격을 3으로 하여 2003년 10월에 대한 병렬 기간을 반환합니다. 즉, 2003년 1월을 반환합니다.  
  
```  
SELECT ParallelPeriod ([Date].[Calendar].[Calendar Quarter]  
   , 3  
   , [Date].[Calendar].[Month].[October 2003])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 다음 예에서는 Semester 수준에 따라 기간 간격을 3으로 하여 2003년 10월에 대한 병렬 기간을 반환합니다. 즉, 2002년 4월을 반환합니다.  
  
```  
SELECT ParallelPeriod ([Date].[Calendar].[Calendar Semester]  
   , 3  
   , [Date].[Calendar].[Month].[October 2003])  
   ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
