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
manager: kfile
ms.openlocfilehash: 3c5479aa3ce855b554f34f72c5c86aa86eb04b9f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63205830"
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
  
 *Index*  
 지정한 멤버와의 간격을 나타내는 멤버 위치 수를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>Remarks  
 수준 내의 멤버 위치는 특성 계층의 일반적인 순서에 따라 결정됩니다. 위치를 나타내는 번호는 0부터 시작합니다.  
  
 지정한 간격이 0 이면 합니다 **지연** 함수는 지정한 멤버를 반환 합니다.  
  
 지정한 간격이 음수 이면 합니다 **지연** 함수는 이후 멤버를 반환 합니다.  
  
 `Lag(1)` 해당 하는 [PrevMember](../mdx/prevmember-mdx.md) 함수입니다. `Lag(-1)` 해당 하는 [NextMember](../mdx/nextmember-mdx.md) 함수입니다.  
  
 **지연** 함수는를 [발생할](../mdx/lead-mdx.md) 함수와 합니다 **발생할** 함수와 검색 방향이 반대 합니다 **지연** 함수입니다. 즉, `Lag(n)`은 `Lead(-n)`과 동일합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
