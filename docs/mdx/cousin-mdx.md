---
title: 사촌 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8a98d496467e2fd75924b0067257f192c79cdf6e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68047254"
---
# <a name="cousin-mdx"></a>Cousin(MDX)


  부모 멤버 아래에서 지정한 자식 멤버와 상대적으로 동일한 위치의 자식 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Cousin( Member_Expression , Ancestor_Member_Expression )  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
 *Ancestor_Member_Expression*  
 상위 멤버를 반환하는 유효한 MDX 멤버 식입니다.  
  
## <a name="remarks"></a>설명  
 이 함수는 수준 내에서 멤버의 순서와 위치에 대해 실행됩니다. 두 개의 계층에서 첫 번째 계층에는 네 개의 수준이 있고 두 번째 계층에는 다섯 개의 수준이 있는 경우, 첫 번째 계층에 속하는 세 번째 수준의 사촌은 두 번째 계층의 세 번째 수준입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 2003 회계 연도의 Year 수준 상위 항목을 기준으로 2002 회계 연도 4분기의 사촌을 검색합니다. 검색되는 사촌은 2003 회계 연도의 4분기입니다.  
  
```  
SELECT Cousin   
   ( [Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002],  
     [Date].[Fiscal].[FY 2003]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
 다음 예에서는 2004 회계 연도 2분기의 Quater 수준 상위 항목을 기준으로 2002 회계 연도 7월의 사촌을 검색합니다. 검색되는 사촌은 2003년의 10월입니다.  
  
```  
SELECT Cousin   
   ([Date].[Fiscal].[Month].[July 2002] ,  
    [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2004]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
