---
title: Lag (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c7e95af96249b64f86bb1466283e8a1a38a32d90
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905773"
---
# <a name="lag-mdx"></a>Lag(MDX)


  멤버 수준에서 지정한 위치 번호만큼 지정한 멤버의 앞에 있는 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.Lag(Index)   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
 *인덱스*  
 지정한 멤버와의 간격을 나타내는 멤버 위치 수를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>설명  
 수준 내의 멤버 위치는 특성 계층의 일반적인 순서에 따라 결정됩니다. 위치를 나타내는 번호는 0부터 시작합니다.  
  
 지정 된 간격이 0 이면 **lag** 함수는 지정 된 멤버를 반환 합니다.  
  
 지정 된 간격이 음수 이면 **lag** 함수는 이후 멤버를 반환 합니다.  
  
 `Lag(1)`은 [PrevMember](../mdx/prevmember-mdx.md) 함수와 동일 합니다. `Lag(-1)`는 [Nextmember](../mdx/nextmember-mdx.md) 함수와 동일 합니다.  
  
 **Lag** 함수는 리드 함수 [는 리드 함수와](../mdx/lead-mdx.md) 유사 합니다. 단, **리드** 함수는 **지연** 함수에서 반대 방향으로 보입니다. 즉, `Lag(n)`은 `Lead(-n)`과 동일합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 2001년 12월의 값을 반환합니다.  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(2) ON 0  
FROM [Adventure Works]  
  
```  
  
 다음 예에서는 2002년 3월의 값을 반환합니다.  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(-1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
