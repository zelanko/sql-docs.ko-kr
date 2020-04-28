---
title: 상위 항목 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 16c6f812d1d7cae5a81a8e64fb425f4d33f4cb5c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68017063"
---
# <a name="ascendants-mdx"></a>Ascendants(MDX)


  멤버 자체를 포함하여 지정한 멤버의 상위 항목 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Ascendants(Member_Expression)  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **상위 항목** 함수는 멤버의 모든 상위 항목을 멤버 자체에서 멤버 계층의 최상위까지 반환 합니다. 구체적으로 말하면, 지정 된 멤버에 대해 계층 구조의 사후 순서 순회를 수행한 다음 해당 멤버와 관련 된 모든 상위 항목 멤버를 집합에 반환 합니다. 이는 특정 수준에서 특정 상위 항목 멤버 또는 상위 항목을 반환 하는 [상위](../mdx/ancestor-mdx.md) 함수와는 대조적입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 **상위 항목 큐브의 재판매인** 주문 `[Sales Territory].[Northwest]` 수와 해당 멤버의 모든 멤버를 반환 합니다. **상위 항목** 함수는 ROWS 축에 대 한 `[Sales Territory].[Northwest]` 멤버 및 해당 상위 항목를 포함 하는 집합을 생성 합니다.  
  
```  
SELECT  
   Measures.[Reseller Order Count] ON COLUMNS,  
   Order(  
      Ascendants(  
         [Sales Territory].[Northwest]  
      ),  
      DESC  
   ) ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
