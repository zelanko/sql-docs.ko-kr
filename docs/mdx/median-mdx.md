---
title: Median (MDX) | Microsoft Docs
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
- MEDIAN
dev_langs:
- kbMDX
helpviewer_keywords:
- Median function
ms.assetid: 7a326a3f-0123-45c4-9b18-31f83b90d986
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6d3a71c0fce496eba004ddca4419944a0cd5256a
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="median-mdx"></a>Median(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  집합에 대해 계산된 숫자 식의 중앙값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Median(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 숫자 식이 지정된 경우 지정된 숫자 식이 집합에 대해 계산된 다음 해당 계산에서 얻은 중앙값이 반환됩니다. 숫자 식이 지정되지 않은 경우 지정된 집합은 해당 집합에 포함된 멤버의 현재 컨텍스트에서 계산된 다음 해당 계산에서 얻은 중앙값이 반환됩니다.  
  
 중앙값은 정렬된 번호 집합의 가운데 값입니다. 중앙 값은 집합의 번호 개수로 나눈 번호 집합의 합계인 Mean 값과는 다릅니다. 중앙값은 집합에서 적어도 절반 이상의 값이 선택된 값보다 크지 않은 최소 값을 선택하여 결정됩니다. 집합 내 값의 개수가 홀수인 경우 중앙값은 단일 값을 따릅니다. 집합 내 값의 개수가 짝수인 경우 중앙값은 두 개의 중간 값의 합계를 2로 나눈 값을 따릅니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]는 정렬된 숫자 집합의 중앙값을 계산할 때 null을 무시합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Adventure Works 큐브의 각 분기, 각 하위 범주 및 각 국가에 대한 월별 판매량의 중앙값을 반환합니다.  
  
```  
WITH MEMBER Measures.x AS Median   
   ([Date].[Calendar].CurrentMember.Children  
      , [Measures].[Reseller Order Quantity]  
   )  
SELECT Measures.x ON 0  
,NON EMPTY [Date].[Calendar].[Calendar Quarter]*   
   [Product].[Product Categories].[Subcategory].members *  
   [Geography].[Geography].[Country].Members  
ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

