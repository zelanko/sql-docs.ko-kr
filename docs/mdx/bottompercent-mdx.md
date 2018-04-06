---
title: BottomPercent (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BOTTOMPERCENT
dev_langs:
- kbMDX
helpviewer_keywords:
- BottomPercent function
ms.assetid: c04866e6-e6dd-4ed1-ae79-c718c194930c
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 078221baa088e0375af381e1e4ef5579280a2cb3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="bottompercent-mdx"></a>BottomPercent(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  집합을 오름차순으로 정렬하고 누적 합계가 지정한 백분율보다 크거나 같은 하위 값 튜플 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BottomPercent(Set_Expression, Percentage, Numeric_Expression)   
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *백분율*  
 반환할 튜플의 백분율을 지정하는 유효한 숫자 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 **BottomPercent** 함수 집합을 오름차순 정렬, 지정 된 집합에 대해 계산 된 특정된 숫자 식의 합계를 계산 합니다. 그런 다음 총 합계 값에 대한 누적 백분율이 지정된 백분율 이상이 되는 하위 값 요소를 반환합니다. 이 함수는 누적 합계가 지정된 백분율 이상이 되는 집합의 가장 작은 하위 집합을 반환합니다. 반환되는 요소는 가장 큰 값에서 가장 작은 값 순서로 정렬됩니다.  
  
> [!IMPORTANT]  
>  **BottomPercent** 같은 함수는 [TopPercent](../mdx/toppercent-mdx.md) 함수, 계층을 항상 무시 합니다. 자세한 내용은 Order 함수를 참조하십시오.  
  
## <a name="example"></a>예제  
 다음 예에서는 2003 회계 연도 동안 Bike 범주에서 Geography 차원의 Geography 계층에 속하는 City 수준의 멤버 집합 중 Reseller Sales Amount 측정값을 사용한 누적 합계가 총 누적 합계의 15% 이상이 되는 가능한 한 작은 집합을 반환합니다. 이 집합은 판매량이 가장 적은 멤버부터 정렬됩니다.  
  
```  
SELECT  
[Product].[Product Categories].Bikes ON 0,  
BottomPercent  
   ({[Geography].[Geography].[City].Members}  
   , 15  
   , ([Measures].[Reseller Sales Amount],[Product].[Product Categories].Bikes)  
   ) ON 1  
FROM [Adventure Works]  
WHERE ([Measures].[Reseller Sales Amount],[Date].[Fiscal].[Fiscal Year].[FY 2003])  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
