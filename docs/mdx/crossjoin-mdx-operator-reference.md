---
title: '* (Crossjoin) (MDX) | Microsoft Docs'
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 03a229dd7ab766a858967eb8c4891edadaaa6b92
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577635"
---
# <a name="crossjoin----mdx-operator-reference"></a>Crossjoin-MDX 연산자 참조
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  두 집합의 교차곱을 반환하는 집합 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set_Expression * Set_Expression  
```  
  
## <a name="parameter"></a>매개 변수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 지정된 두 매개 변수의 교차곱을 포함하는 집합입니다.  
  
## <a name="remarks"></a>Remarks  
 **\* (Crossjoin)** 연산자는 기능적으로 동일는 [Crossjoin](../mdx/crossjoin-mdx.md) 함수입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이 연산자의 사용 방법을 보여 줍니다.  
  
```  
-- This query returns the gross profit margin for product types  
-- and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
    [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Gross Profit Margin])  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
