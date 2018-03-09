---
title: LastPeriods (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: LASTPERIODS
dev_langs: kbMDX
helpviewer_keywords: LastPeriods function
ms.assetid: a15df7a1-b261-48ed-aacc-d2804db8dbf7
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a3a9f0940796ecbc8138447fa8dd4ba59febbe96
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="lastperiods-mdx"></a>LastPeriods(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>주의  
 지정 된 기간 개수가 양수인 경우이 **LastPeriods** 함수 만큼 이전에 있는 멤버부터 시작 하는 멤버의 집합을 반환 *인덱스* -지정 된 멤버 식 및 지정 된 멤버 끝에서 1입니다. 함수에서 반환 되는 멤버 수 같습니다 *인덱스*합니다.  
  
 지정 된 기간 개수가 음수인 경우이 **LastPeriods** 함수는 지정 된 멤버부터 시작 하는 멤버 집합을 반환 하 고 이후에 있는 멤버로 끝나는 (- *인덱스* -1)에서 지정된 된 멤버입니다. 함수에서 반환 된 멤버의 수는의 절대 값과 같은 *인덱스*합니다.  
  
 지정 된 기간 개수가 0 바이트인 경우는 **LastPeriods** 함수는 빈 집합을 반환 합니다. 반면는 **지연** 0을 지정 하는 경우 지정된 된 멤버를 반환 하는 함수입니다.  
  
 멤버가 지정 되지 않은 경우는 **LastPeriods** 함수는 **Time.CurrentMember**합니다. 차원이 시간 차원으로 표시되지 않은 경우 이 함수는 오류 없이 구문 분석되고 실행되지만 클라이언트 응용 프로그램에서는 셀 오류가 발생합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
