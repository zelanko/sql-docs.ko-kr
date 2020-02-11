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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
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
  
 *인덱싱할*  
 지정한 멤버와의 간격을 나타내는 병렬 기간 수를 지정하는 유효한 숫자 식입니다.  
  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 [사촌](../mdx/cousin-mdx.md) 함수와 유사 하지만 **ParallelPeriod** 함수는 시계열과 더 밀접 하 게 관련 되어 있습니다. **ParallelPeriod** 함수는 지정 된 수준에서 지정 된 멤버의 상위 항목을 가져오고, 지정 된 지연 시간 동안 상위 항목의 형제를 찾고, 마지막으로 형제의 하위 항목 사이에 지정 된 멤버의 병렬 기간을 반환 합니다.  
  
 **ParallelPeriod** 함수에는 다음과 같은 기본값이 있습니다.  
  
-   수준 식과 멤버 식이 모두 지정 되지 않은 경우 기본 멤버 값은 측정값 그룹의 *시간* 유형과 첫 번째 차원에 있는 첫 번째 계층의 현재 멤버입니다.  
  
-   수준 식이 지정 되었지만 멤버 식이 지정 되지 않은 경우 기본 멤버 값은 *Level_Expression*입니다. **계층. CurrentMember**.  
  
-   기본 인덱스 값은 1입니다.  
  
-   기본 수준은 지정된 멤버의 부모 수준입니다.  
  
 **ParallelPeriod** 함수는 다음 MDX 문과 동일 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
