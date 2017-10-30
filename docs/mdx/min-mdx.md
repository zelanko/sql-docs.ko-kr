---
title: Min (MDX) | Microsoft Docs
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
- MIN
dev_langs:
- kbMDX
helpviewer_keywords:
- Min function [MDX]
ms.assetid: 9f3799c0-2502-4056-a259-053898f69b7c
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1d6fa17a65a5930e600c2aea2591b33e1d0d3890
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="min-mdx"></a>Min(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  집합에 대해 계산된 숫자 식의 최소값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Min( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 숫자 식이 지정된 경우 지정된 숫자 식이 집합에 대해 계산된 다음 해당 계산에서 얻은 최소값이 반환됩니다. 숫자 식이 지정되지 않은 경우 지정된 집합은 해당 집합에 포함된 멤버의 현재 컨텍스트에서 계산된 다음 해당 계산에서 얻은 최소값이 반환됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]는 숫자 집합의 최소값을 계산할 때 Null을 무시합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Adventure Works 큐브의 각 하위 범주와 각 국가에 대한 최소 분기별 판매량을 반환합니다.  
  
```  
WITH MEMBER Measures.x AS Min   
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
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

