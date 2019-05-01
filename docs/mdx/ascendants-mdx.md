---
title: Ascendants (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3122b3aa2f53da69f88e6ffad508f12c8e10da1c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63249817"
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
  
## <a name="remarks"></a>Remarks  
 합니다 **상위 항목** 함수 멤버의 계층의 최상위까지 멤버 자체부터 멤버의 상위 항목 모두 반환 합니다; 지정된 된 멤버에 대 한 계층의 후 위 순회 수행 보다 구체적으로, 한 다음 자체를 포함 하 여 집합의 멤버에 관련 된 모든 상위 항목 멤버를 반환 합니다. 이 달리는 합니다 [상위](../mdx/ancestor-mdx.md) 특정 상위 항목 멤버 또는 특정 수준에서 상위 항목을 반환 하는 함수입니다.  
  
## <a name="examples"></a>예  
 다음 예제에 대 한 대리점 주문 수를 반환 합니다.는 `[Sales Territory].[Northwest]` 멤버와 해당 멤버의 모든 상위 항목을 **Adventure Works** 큐브. **상위** 함수를 포함 하는 집합을 구성 합니다 `[Sales Territory].[Northwest]` 멤버 및 ROWS 축에 대 한 해당 상위 항목입니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
