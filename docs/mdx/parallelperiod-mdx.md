---
title: ParallelPeriod (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b4122c13a5371cc0ffe1c5c6235ad750e7fdadad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020703"
---
# <a name="parallelperiod-mdx"></a>ParallelPeriod (MDX)


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
  
## <a name="remarks"></a>설명  
 유사 하지만 [사촌](../mdx/cousin-mdx.md) 함수는 **ParallelPeriod** 함수 시계열에 보다 밀접 한 관련이 있습니다. 합니다 **ParallelPeriod** 함수 지정된 된 수준에서 지정된 된 멤버의 상위 항목을 사용 하는 지정한 간격이 상위의 형제로 찾아서 마지막 간에 지정된 된 멤버의 병렬 기간을 반환 합니다.는 형제의 하위 항목입니다.  
  
 합니다 **ParallelPeriod** 함수에는 기본값을 지정 합니다.  
  
-   기본 멤버 값의 형식 사용 하 여 첫 번째 차원에 첫 번째 계층의 현재 멤버는 수준 식과 멤버 식이 모두를 지정 하는 경우 *시간* 측정값 그룹에 있습니다.  
  
-   수준 식이 지정 된 경우 하지만 멤버 식이 지정 되지 않은 경우 기본 멤버 값은 *Level_Expression*. **Hierarchy.CurrentMember**합니다.  
  
-   기본 인덱스 값은 1입니다.  
  
-   기본 수준은 지정된 멤버의 부모 수준입니다.  
  
 합니다 **ParallelPeriod** 함수는 다음 MDX 문과 동일 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
