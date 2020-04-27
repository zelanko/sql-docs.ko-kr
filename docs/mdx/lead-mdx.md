---
title: 리드 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cc4d362fbc7656e9427548a352b32d5d8297071e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905739"
---
# <a name="lead-mdx"></a>Lead(MDX)


  멤버 수준을 따라 지정한 위치 번호만큼 지정한 멤버의 뒤에 있는 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.Lead( Index )  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
 *인덱스*  
 멤버 위치 번호를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>설명  
 수준 내의 멤버 위치는 특성 계층의 일반적인 순서에 따라 결정됩니다. 위치를 나타내는 번호는 0부터 시작합니다.  
  
 지정 된 리드가 영 (0) 이면 **리드** 함수는 지정 된 멤버를 반환 합니다.  
  
 지정 된 리드가 음수 이면 **리드** 함수는 이전 멤버를 반환 합니다.  
  
 `Lead(1)`는 [Nextmember](../mdx/nextmember-mdx.md) 함수와 동일 합니다. `Lead(-1)`은 [PrevMember](../mdx/prevmember-mdx.md) 함수와 동일 합니다.  
  
 **지연** 함수는 **리드** 함수와 반대 방향으로 표시 된다는 점을 제외 하 고 **리드** 함수는 [lag](../mdx/lag-mdx.md) 함수와 비슷합니다. 즉, `Lead(n)`은 `Lag(-n)`과 동일합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 2001년 12월의 값을 반환합니다.  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(-2) ON 0  
FROM [Adventure Works]  
  
```  
  
 다음 예에서는 2002년 3월의 값을 반환합니다.  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
