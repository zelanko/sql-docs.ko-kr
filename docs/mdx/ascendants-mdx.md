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
ms.openlocfilehash: 1ef9cccb488cebb08c1b9721c40cb8037ea8687a
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34739622"
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
 **Ascendants** 함수 멤버의 계층의 최상위까지 멤버 자체에서 모든 멤버의 상위 항목을 반환; 보다 구체적으로, 지정된 된 멤버에 대 한 계층의 후 위 순회를 수행 하 고 다음 반환 모든 상위 항목 멤버와 관련 된 멤버를 집합에서 자신을 포함 하 합니다. 이 달리는 [상위](../mdx/ancestor-mdx.md) 특정 구성원, 또는 특정 수준에서 상위 항목을 반환 하는 함수입니다.  
  
## <a name="examples"></a>예  
 한에 대 한 대리점 주문 건수를 반환 하는 다음 예제는 `[Sales Territory].[Northwest]` 멤버와 해당 멤버의 모든 상위 항목은 **Adventure Works** 큐브. **상위** 포함 된 집합을 구성 하는 함수는 `[Sales Territory].[Northwest]` 멤버 및 ROWS 축에 대 한 상위 항목입니다.  
  
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
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
