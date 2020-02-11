---
title: BottomPercent (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cbcf9086cedc9221c39832bd0b7d55e5f0814c7f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68016915"
---
# <a name="bottompercent-mdx"></a>BottomPercent(MDX)


  집합을 오름차순으로 정렬하고 누적 합계가 지정한 백분율보다 크거나 같은 하위 값 튜플 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BottomPercent(Set_Expression, Percentage, Numeric_Expression)   
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *나타낸*  
 반환할 튜플의 백분율을 지정하는 유효한 숫자 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **BottomPercent** 함수는 지정 된 집합에 대해 계산 된 지정 된 숫자 식의 합계를 계산 하 여 집합을 오름차순으로 정렬 합니다. 그런 다음 총 합계 값에 대한 누적 백분율이 지정된 백분율 이상이 되는 하위 값 요소를 반환합니다. 이 함수는 누적 합계가 지정된 백분율 이상이 되는 집합의 가장 작은 하위 집합을 반환합니다. 반환되는 요소는 가장 큰 값에서 가장 작은 값 순서로 정렬됩니다.  
  
> [!IMPORTANT]  
>  [TopPercent](../mdx/toppercent-mdx.md) 함수와 마찬가지로 **BottomPercent** 함수는 항상 계층 구조를 중단 합니다. 자세한 내용은 Order 함수를 참조하십시오.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
