---
description: LastPeriods(MDX)
title: LastPeriods (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 60e8adf1dba453fb536f95a4fa113e16f6950f62
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494886"
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
 지정 된 기간 수가 양수인 경우 **Lastperiods** 함수는 지정 된 멤버 식의 *인덱스* -1을 지연 하 고 지정 된 멤버로 끝나는 멤버의 집합을 반환 합니다. 함수에서 반환 되는 멤버 수는 *인덱스*와 같습니다.  
  
 지정 된 기간 수가 음수 이면 **Lastperiods** 함수는 지정 된 멤버에서 시작 하 여 지정 된 멤버에서 (- *Index* -1)로 이어지는 멤버로 끝나는 멤버 집합을 반환 합니다. 함수에서 반환 되는 멤버 수는 *인덱스*의 절대값과 같습니다.  
  
 지정 된 기간 수가 0 이면 **Lastperiods** 함수는 빈 집합을 반환 합니다. 이 함수는 0이 지정 된 경우 지정 된 멤버를 반환 하는 **Lag** 함수와는 다릅니다.  
  
 멤버가 지정 되지 않은 경우 **Lastperiods** 함수는 **Time. currentmember**를 사용 합니다. 차원이 시간 차원으로 표시되지 않은 경우 이 함수는 오류 없이 구문 분석되고 실행되지만 클라이언트 애플리케이션에서는 셀 오류가 발생합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 2002 회계 연도의 2분기, 3분기 및 4분기의 기본 측정값을 반환합니다.  
  
```  
SELECT LastPeriods(3,[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]) ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  이 예제는: (콜론) 연산자를 사용 하 여 작성할 수도 있습니다.  
>   
>  `[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]: [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2002]`  
  
 다음 예에서는 2002 회계 연도의 1분기에 대한 기본 측정값을 반환합니다. 지정된 기간 수는 3이지만 해당 회계 연도에 보다 이전의 기간이 없으므로 한 분기만 반환될 수 있습니다.  
  
```  
SELECT LastPeriods  
   (3,[Date].[Fiscal].[Fiscal Quarter].[Q1 FY 2002]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
