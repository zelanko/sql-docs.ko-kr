---
title: "&lt;= (작거나 같음) (MDX) | Microsoft Docs"
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
- <=
dev_langs:
- kbMDX
helpviewer_keywords:
- <= (less than or equal to operator)
- less than or equal to operator (<=)
ms.assetid: 6c805c68-cf9d-48ca-a00b-2ef9ade89b0a
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d7c4f714a78223afb9bdd1309eea9835b3e2bfc3
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="lt-less-than-or-equal-to-mdx"></a>&lt;= (작거나 같음) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  하나의 MDX 식의 값이 다른 MDX 식의 값보다 작거나 같은지 확인하는 비교 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
MDX_Expression <= MDX_Expression  
```  
  
#### <a name="parameters"></a>매개 변수  
 *MDX_Expression*  
 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 다음 조건을 기반으로 하는 부울 값입니다.  
  
-   t**rue** 매개 변수가 모두 null이 아닌 아니고 첫 번째 매개 변수는 값으로 포함 하는 경우 두 번째 매개 변수 값 보다 작습니다.  
  
-   f**alse** 매개 변수가 모두 null이 아니고 첫 번째 매개 변수 값이 경우는 두 번째 매개 변수 값 보다 큽니다.  
  
-   매개 변수 중 하나가 Null이거나 둘 다 Null인 경우 Null입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이 연산자의 사용 방법을 보여 줍니다.  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for Australia where the GPM is less than or equal to 30%.  
With Member [Measures].[LowGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] <= .5,  
      [Measures].[Gross Profit Margin],  
      null)  
SELECT   
NON EMPTY [Sales Territory].[Sales Territory Country].[Australia] ON 0,  
    NON EMPTY [Product].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[LowGPM])  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 연산자 참조 &#40; Mdx&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

