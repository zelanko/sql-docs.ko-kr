---
title: Subset (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b1f9a79c0e0ba6d578b82d7b1d072f3543888a1c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036705"
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
  
 *개수*  
 반환할 튜플 수를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>설명  
 지정된 된 집합에서의 **하위 집합** 함수는 튜플, 지정 된 시작 위치부터 지정한 수를 포함 하는 하위 집합을 반환 합니다. 시작 위치는 인덱스(0부터 시작)를 기반으로 합니다. 즉, 0은 지정된 집합의 첫 번째 튜플에 해당하고 1은 두 번째 튜플에 해당합니다.  
  
 하는 경우 *개수* 지정 하지 않으면 함수에서 모든 튜플은 반환 *시작* 집합의 끝에 있습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Reseller Gross Profit를 기준으로 계층에 관계없이 판매량이 상위 5위 안에 속하는 제품 하위 범주에 대한 Reseller Sales 측정값을 반환합니다. 합니다 **하위 집합** 함수를 사용 하 여 결과 정렬 한 후 결과에서 처음 다섯 개의 집합만 반환 되는 **순서** 함수입니다.  
  
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
  
  
