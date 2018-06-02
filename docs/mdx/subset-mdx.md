---
title: Subset (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e063d295480cff8e5db44f5ea30668a7a06ff74b
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581395"
---
# <a name="subset-mdx"></a>Subset(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 지정된 된 집합에서의 **하위 집합** 함수는 지정 된 수 만큼의 튜플이 지정 된 시작 위치에서 시작을 포함 하는 하위 집합을 반환 합니다. 시작 위치는 인덱스(0부터 시작)를 기반으로 합니다. 즉, 0은 지정된 집합의 첫 번째 튜플에 해당하고 1은 두 번째 튜플에 해당합니다.  
  
 경우 *Count* 를 지정 하지 않으면 함수까지 모든 튜플을 반환 *시작* 집합의 끝에 있습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Reseller Gross Profit를 기준으로 계층에 관계없이 판매량이 상위 5위 안에 속하는 제품 하위 범주에 대한 Reseller Sales 측정값을 반환합니다. **하위 집합** 함수는 사용 하 여 결과 정렬 한 후 결과에서 처음 다섯 개의 집합만 반환 하는 데 사용 되는 **순서** 함수입니다.  
  
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
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
