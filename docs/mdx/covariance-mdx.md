---
title: Covariance (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COVARIANCE
dev_langs:
- kbMDX
helpviewer_keywords:
- Covariance function
ms.assetid: 5faf6742-62db-4c5c-8797-096bf1cab273
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ede1c98c6087dc31c91cc95041461908bd6bb229
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="covariance-mdx"></a>Covariance(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  x-y 값 쌍의 개수로 나누는 편향 모집단 수식을 사용하여 집합에 대해 계산된 x-y 값 쌍의 모집단 공변성(covariance)을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Covariance(Set_Expression,Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Numeric_Expression_y*  
 Y축 값을 나타내는 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
 *Numeric_Expression_x*  
 X축 값을 나타내는 숫자를 반환하는 셀 좌표의 유효한 숫자 식으로서, 일반적으로 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 **공** 함수는 y 축에 대 한 값을 가져오려는 첫 번째 숫자 식에 대해 지정 된 집합을 계산 합니다. 그런 다음 두 번째 숫자 식(지정된 경우)에 대해 지정된 집합을 계산하여 X축 값 집합을 구합니다. 두 번째 숫자 expressionis 지정 하지 않으면 함수는 x 축에 대 한 지정된 된 집합에 있는 셀의 현재 컨텍스트 값으로 사용 합니다.  
  
 **공** 함수는 편향된 모집단 수식을 사용 합니다. 이 달리는 [CovarianceN](../mdx/covariancen-mdx.md) 함수는 (x, y 쌍의 개수로 나눈 다음 1을 빼는) 비편향된 모집단 수식을 사용 합니다.  
  
> [!NOTE]  
>  **공** 함수는 빈 셀 이나 텍스트를 포함 하는 셀 또는 논리 값은 무시 됩니다. 그러나 값이 0인 셀은 포함시킵니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Covariance 함수를 사용하는 방법을 보여 줍니다.  
  
```  
WITH   
MEMBER [Measures].[CovarianceDemo] AS  
COVARIANCE([Date].[Date].[Date].Members, [Measures].[Internet Sales Amount], [Measures].[Internet Order Count])   
SELECT {[Measures].[CovarianceDemo]} ON 0   
FROM  
[Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

