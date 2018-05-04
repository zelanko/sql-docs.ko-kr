---
title: ': (범위) (MDX) | Microsoft Docs'
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
- ':'
dev_langs:
- kbMDX
helpviewer_keywords:
- ': (range operator)'
- range operator (:)
ms.assetid: f9b36aca-4efd-49b4-9e4f-12914c1b24a6
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: cba26f6b69ca22a1ab39fa753749d6a8b1a150df
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="-range-mdx"></a>: (범위) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 두 멤버를 끝점으로 사용하고 지정한 두 멤버 사이의 모든 멤버를 집합의 멤버로 포함시켜 일반적인 순서로 정렬된 집합을 반환하는 집합 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression : Member_Expression      
```  
  
#### <a name="parameters"></a>매개 변수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 지정된 멤버를 포함하는 집합과 지정된 멤버 사이의 모든 멤버입니다.  
  
## <a name="remarks"></a>주의  
 두 매개 변수는 모두 특정 차원과 동일한 수준 및 계층 내에서 멤버를 지정해야 합니다. 매개 변수가 모두 동일한 멤버를 지정 하는 경우는 **: (범위)** 연산자는 지정 된 멤버만 포함 하는 집합을 반환 합니다. 첫 번째 매개 변수가 Null인 경우 집합에는 두 번째 매개 변수에 지정된 멤버 수준의 처음부터 해당 멤버까지 포함하여 모든 멤버가 들어 있습니다. 두 번째 매개 변수가 Null인 경우 집합에는 첫 번째 매개 변수에 지정된 멤버에서 동일한 수준의 마지막 멤버까지 포함하여 모든 멤버가 들어 있습니다.  
  
 MDX에는 이 집합 연산자에 해당하는 기능이 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이 연산자의 사용 방법을 보여 줍니다.  
  
```  
-- This query returns the freight cost per user  
-- for products, averaged by month, for the first quarter.  
With Member [Measures].[Freight Per Customer] as  
 (  
     [Measures].[Internet Freight Cost]  
     /   
     [Measures].[Customer Count]  
)  
  
SELECT   
    {[Ship Date].[Calendar].[Month].&[2004]&[1] : [Ship Date].[Calendar].[Month].&[2004]&[3]} ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Freight Per Customer])  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
