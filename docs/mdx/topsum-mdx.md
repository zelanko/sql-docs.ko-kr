---
title: TopSum (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TOPSUM
dev_langs:
- kbMDX
helpviewer_keywords:
- TopSum function
ms.assetid: e32496fd-4897-43c9-a388-4028609f4ffb
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 58a7bffc672af75c52eacca28f2e83d36a56af0c
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="topsum-mdx"></a>TopSum(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  집합을 정렬하고 누적 합계가 지정한 값 이상이 되는 상위 요소를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
TopSum(Set_Expression, Value, Numeric_Expression)   
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Value*  
 각 튜플과 비교할 기준 값을 지정하는 유효한 숫자 식입니다.  
  
 *Numeric_Expression*  
 측정값을 반환하는 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 **TopSum** 함수 집합을 내림차순 정렬, 지정 된 집합에 대해 특정된 측정값의 합계를 계산 합니다. 그런 다음 지정된 숫자 식의 합계가 지정된 값(합계) 이상이 되는 상위 값 요소를 반환합니다. 이 함수는 누적 합계가 지정된 값 이상이 되는 집합의 가장 작은 하위 집합을 반환합니다. 반환되는 요소는 가장 큰 값에서 가장 작은 값 순서로 정렬됩니다.  
  
> [!IMPORTANT]  
>  마찬가지로 [BottomSum](../mdx/bottomsum-mdx.md) 함수는 **TopSum** 함수 계층을 항상 무시 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Bike 범주에 대해 Geography 차원의 Geography 계층에 있는 City 수준의 멤버 중에서 Reseller Sales Amount 측정값을 사용한 누적 합계가 6,000,000 이상인 멤버의 최소 집합을 판매량이 가장 많은 멤버부터 반환합니다.  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopSum  
   ({[Geography].[Geography].[City].Members}  
   , 6000000  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].Bikes)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

