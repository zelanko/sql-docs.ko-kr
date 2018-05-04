---
title: Head (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- HEAD
dev_langs:
- kbMDX
helpviewer_keywords:
- Head function
ms.assetid: 2a909bda-1366-4537-93b0-c089554fc11f
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 5529333ef2e81b8fee7d78765e0fb528ecb02577
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="head-mdx"></a>Head(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  집합에서 중복된 항목을 포함하여 처음 나오는 지정한 수만큼의 요소를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Head(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *개수*  
 반환할 튜플 수를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>주의  
 **h e a d** 함수는 지정 된 튜플 수가 지정된 된 집합의 시작 부분에서 반환 합니다. 요소의 순서는 유지됩니다. Count의 기본값은 1입니다. 지정 된 튜플 수가 1 보다 작은 경우는 **h e a d** 함수는 빈 집합을 반환 합니다. 지정된 튜플 수가 집합의 튜플 수를 초과할 경우에는 원래 집합을 반환합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Reseller Gross Profit를 기준으로 계층에 관계없이 판매량이 상위 5위 안에 속하는 제품 하위 범주를 반환합니다. **h e a d** 함수를 사용 하 여 사용 하 여 결과 정렬 한 후 결과에서 처음 5 개 집합에만 반환 하는 **순서** 함수입니다.  
  
```  
SELECT   
[Measures].[Reseller Gross Profit] ON 0,  
Head  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,5  
   ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [비상 &#40;MDX&#41;](../mdx/tail-mdx.md)   
 [항목 &#40;튜플&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)   
 [항목 &#40;멤버&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)   
 [순위 &#40;MDX&#41;](../mdx/rank-mdx.md)   
 [MDX 함수 참조 & #40; Mdx& #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
