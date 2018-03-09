---
title: Tail (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: TAIL
dev_langs: kbMDX
helpviewer_keywords: Tail function
ms.assetid: d62a1bb2-55c0-4939-8526-cdc3d444ffe2
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2d8781dc0364699146d1d3706a8e2e976acc1f7c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="tail-mdx"></a>Tail(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  집합의 끝에서 하위 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Tail(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *개수*  
 반환할 튜플 수를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>주의  
 **꼬리** 함수는 지정된 된 집합의 끝에서 지정 된 튜플 수가 반환 합니다. 요소의 순서는 유지됩니다. 기본값 *Count* 는 1입니다. 지정된 튜플 수가 1보다 작은 경우 이 함수는 빈 집합을 반환합니다. 지정된 튜플 수가 집합의 튜플 수를 초과할 경우에는 원래 집합을 반환합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Reseller Gross Profit를 기준으로 계층에 관계없이 판매량이 상위 5위 안에 속하는 제품 하위 범주에 대한 Reseller Sales 측정값을 반환합니다. **꼬리** 함수는 결과 정렬 한 후 반대-를 사용 하 여 결과에서 마지막 다섯 개의 집합만 반환 하는 데 사용 되는 **순서** 함수입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
