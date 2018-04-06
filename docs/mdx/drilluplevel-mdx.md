---
title: DrillupLevel (MDX) | Microsoft Docs
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
- DRILLUPLEVEL
dev_langs:
- kbMDX
helpviewer_keywords:
- DrillupLevel function
ms.assetid: 63431f79-f3a1-40c4-bf57-2b6bd8991cc3
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ec561536a098e927731a3359edae3f2e35f3d481
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="drilluplevel-mdx"></a>DrillupLevel(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 수준 아래에 있는 집합의 멤버를 드릴업합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DrillupLevel(Set_Expression [ , Level_Expression ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Level_Expression*  
 수준을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 **DrillupLevel** 지정된 된 집합에 포함 된 멤버에 따라 멤버 집합을 계층적으로 구성 하는 함수 반환 합니다. 지정된 집합의 멤버 간 순서는 유지됩니다.  
  
 수준 식이 지정 되는 **DrillupLevel** 함수는 지정 된 수준의 위쪽에 있는 멤버만 검색 하 여 집합을 구성 합니다. 수준 식이 지정되어 있고 지정된 집합에 지정된 수준의 멤버가 표시되지 않는 경우에는 지정된 집합이 반환됩니다.  
  
 수준 식이 지정되지 않은 경우 이 함수는 지정된 집합에서 참조되는 첫 번째 차원의 가장 낮은 수준보다 한 수준 높은 멤버만 검색하여 집합을 구성합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 첫 번째 집합에서 Subcategory 수준의 위쪽에 있는 멤버의 집합을 반환합니다.  
  
```  
SELECT DrillUpLevel   
  ({[Product].[Product Categories].[All Products]  
    ,[Product].[Product Categories].[Subcategory].&[32],  
    [Product].[Product Categories].[Product].&[215]},  
  [Product].[Product Categories].[Subcategory]  
    )  
  ON 0  
  FROM [Adventure Works]  
  WHERE [Measures].[Internet Order Quantity]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
