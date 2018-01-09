---
title: TopCount (MDX) | Microsoft Docs
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
f1_keywords: TOPCOUNT
dev_langs: kbMDX
helpviewer_keywords: TopCount function
ms.assetid: 15026a8f-35c5-4307-8856-348f5c44bfd5
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: e68a27c85dde732a54b87e914b643565d8549933
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="topcount-mdx"></a>TopCount(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  집합을 내림차순으로 정렬하고 가장 높은 값을 갖는 요소를 지정된 수만큼 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
TopCount(Set_Expression,Count [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *개수*  
 반환할 튜플 수를 지정하는 유효한 숫자 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 숫자 식이 지정 되는 **TopCount** 내림차순으로 지정된 된 집합에 대해 계산 된 숫자 식으로 지정 된 값에 따라 지정 된 집합으로 지정 된 집합의 튜플을 정렬 작동 합니다. 집합을 정렬 한 후의 **TopCount** 함수는 가장 높은 값을 갖는 튜플에의 지정 된 수를 반환 합니다.  
  
> [!IMPORTANT]  
>  마찬가지로 [BottomCount](../mdx/bottomcount-mdx.md) 함수는 **TopCount** 함수 계층을 항상 무시 합니다.  
  
 숫자 식이 지정 하지 않으면 함수는 멤버 집합 일반적인 순서로 정렬 하지 않고 반환, 처럼 동작 하는 [Head (MDX)](../mdx/head-mdx.md) 함수입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Internet Sales Amount를 기준으로 상위 10개 날짜를 반환합니다.  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `TOPCOUNT([Date].[Date].[Date].MEMBERS, 10, [Measures].[Internet Sales Amount])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 다음 예에서는 Bike 범주에 대해 Geography 차원의 Geography 계층에 있는 City 수준의 멤버와 Date 차원의 Fiscal 계층에 있는 모든 회계 연도의 모든 조합을 포함하는 집합을 Reseller Sales Amount 측정값을 기준으로 판매량이 가장 많은 멤버부터 정렬한 다음 이 중 처음 5개의 멤버를 반환합니다.  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopCount  
   ({[Geography].[Geography].[City].Members   
      *[Date].[Fiscal].[Fiscal Year].Members}  
   , 5  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].Bikes)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
