---
title: StdevP (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 14117ed4a3e3e7afc0152c5e659d1c7f040957e9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150136"
---
# <a name="stdevp-mdx"></a>StdevP(MDX)


  편향된 모집단 수식을 사용 하 여 집합에 대해 계산 된 숫자 식의 모집단 표준 편차를 반환 합니다 (나누어 *n*).  
  
## <a name="syntax"></a>구문  
  
```  
  
StdevP(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression*  
 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 **StdevP** 함수는 편향된 모집단을 사용 하는 동안 수식 합니다 [Stdev](../mdx/stdev-mdx.md) 함수는 비편향된 모집단 수식을 사용 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 편향 모집단 수식을 사용하여 2003년의 처음 3개월 동안 집합된 Internet Order Quantity의 표준 편차를 반환합니다.  
  
```  
WITH MEMBER Measures.x AS   
   StdevP   
   ( { [Date].[Calendar].[Month].[January 2003],  
       [Date].[Calendar].[Month].[February 2003],  
       [Date].[Calendar].[Month].[March 2003]},  
    [Measures].[Internet Order Quantity])  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
