---
description: Subset(MDX)
title: 하위 집합 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d0b7e79ebf0415011665ae63e7b9699200e374b1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386729"
---
# <a name="subset-mdx"></a>Subset(MDX)


  지정한 집합에서 튜플의 하위 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Subset(Set_Expression, Start [ ,Count ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *시작*  
 반환할 첫 번째 튜플의 위치를 지정하는 유효한 숫자 식입니다.  
  
 *Count*  
 반환할 튜플 수를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>설명  
 지정 된 집합에서 **하위 집합** 함수는 지정 된 시작 위치에서 시작 하 여 지정 된 수의 튜플을 포함 하는 하위 집합을 반환 합니다. 시작 위치는 인덱스(0부터 시작)를 기반으로 합니다. 즉, 0은 지정된 집합의 첫 번째 튜플에 해당하고 1은 두 번째 튜플에 해당합니다.  
  
 *Count* 를 지정 하지 않으면 함수는 *시작* 부터 집합 끝까지 모든 튜플을 반환 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Reseller Gross Profit를 기준으로 계층에 관계없이 판매량이 상위 5위 안에 속하는 제품 하위 범주에 대한 Reseller Sales 측정값을 반환합니다. **하위 집합** 함수는 **Order** 함수를 사용 하 여 결과를 정렬 한 후 결과에서 처음 다섯 개의 집합만 반환 하는 데 사용 됩니다.  
  
```  
SELECT Subset  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,0  
   ,5  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
