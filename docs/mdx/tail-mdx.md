---
title: Tail (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d48a374d7d84c1137f082eb12dec638557b14e5a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036666"
---
# <a name="tail-mdx"></a>Tail(MDX)


  집합의 끝에서 하위 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Tail(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *수*  
 반환할 튜플 수를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>설명  
 **Tail** 함수는 지정 된 집합의 끝에서 지정 된 개수의 튜플을 반환 합니다. 요소의 순서는 유지됩니다. *Count* 의 기본값은 1입니다. 지정된 튜플 수가 1보다 작은 경우 이 함수는 빈 집합을 반환합니다. 지정된 튜플 수가 집합의 튜플 수를 초과할 경우에는 원래 집합을 반환합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Reseller Gross Profit를 기준으로 계층에 관계없이 판매량이 상위 5위 안에 속하는 제품 하위 범주에 대한 Reseller Sales 측정값을 반환합니다. **Tail** 함수는 **Order** 함수를 사용 하 여 결과가 역순으로 정렬 된 후 결과에서 마지막 다섯 개의 집합만 반환 하는 데 사용 됩니다.  
  
```  
SELECT Tail  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BASC  
      )  
   ,5  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
