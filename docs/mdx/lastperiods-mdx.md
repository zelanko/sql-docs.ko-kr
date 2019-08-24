---
title: LastPeriods (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6a9337e925da40f148bbe0d2c77fb1cf4f5f1a99
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905775"
---
# <a name="lastperiods-mdx"></a>LastPeriods(MDX)


  지정한 멤버까지 포함하는 멤버 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
LastPeriods(Index [ ,Member_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Index*  
 여러 기간을 지정하는 유효한 숫자 식입니다.  
  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 지정 된 기간 개수가 양수인 경우 합니다 **LastPeriods** 큼 이전에 있는 멤버를 사용 하 여 시작 하는 멤버 집합을 반환 *인덱스* -지정 된 멤버 식에서 끝나는 1는 지정 된 멤버입니다. 함수에서 반환 하는 멤버 개수 값과 같음 *인덱스*합니다.  
  
 지정 된 기간 개수가 음수인 경우 합니다 **LastPeriods** 함수는 지정된 된 멤버를 사용 하 여 시작 하는 멤버 집합을 반환 하 고 이후에 있는 멤버로 끝나는 (- *인덱스* -1)에서 지정 된 멤버입니다. 절대 값 함수에서 반환 하는 멤버 수가 같은지 *인덱스*합니다.  
  
 지정 된 기간 개수가 0 이면 합니다 **LastPeriods** 함수는 빈 집합을 반환 합니다. 이 점이 합니다 **지연** 0을 지정 하는 경우 지정된 된 멤버를 반환 하는 함수입니다.  
  
 멤버를 지정 하지 않으면 경우는 **LastPeriods** 함수는 **Time.CurrentMember**합니다. 차원이 시간 차원으로 표시되지 않은 경우 이 함수는 오류 없이 구문 분석되고 실행되지만 클라이언트 애플리케이션에서는 셀 오류가 발생합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 2002 회계 연도의 2분기, 3분기 및 4분기의 기본 측정값을 반환합니다.  
  
```  
SELECT LastPeriods(3,[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]) ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  사용 하 여이 예제에서는 작성할 수도 있습니다는: (콜론) 연산자:  
>   
>  `[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]: [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2002]`  
  
 다음 예에서는 2002 회계 연도의 1분기에 대한 기본 측정값을 반환합니다. 지정된 기간 수는 3이지만 해당 회계 연도에 보다 이전의 기간이 없으므로 한 분기만 반환될 수 있습니다.  
  
```  
SELECT LastPeriods  
   (3,[Date].[Fiscal].[Fiscal Quarter].[Q1 FY 2002]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
