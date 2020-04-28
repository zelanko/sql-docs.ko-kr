---
title: Children (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0af4d7b97777002dc5683c075f82531ccc8df86e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68016802"
---
# <a name="children-mdx"></a>Children(MDX)


  지정된 멤버의 자식 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.Children  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **Children** 함수는 지정 된 멤버의 자식을 포함 하는 자연스럽 게 정렬 된 집합을 반환 합니다. 지정된 멤버에 자식이 없는 경우 이 함수는 빈 집합을 반환합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Geography 차원에서 Geography 계층에 있는 United States 멤버의 자식을 반환합니다.  
  
```  
SELECT [Geography].[Geography].[Country].&[United States].Children ON 0  
FROM [Adventure Works]  
```  
  
 다음 예에서는 열 축에서 **측정값** 차원의 모든 멤버를 반환 합니다. 여기에는 모든 계산 멤버와 `[Product].[Model Name]` **어드벤처 Works** 큐브의 행 축에 있는 특성 계층의 모든 자식 집합이 포함 됩니다.  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
  
```  
  
|해제|기록|  
|-------------|-------------|  
|[!INCLUDE[ssBOL2005_R03](../includes/ssbol2005-r03-md.md)]|**변경된 내용**<br /> -명확성을 향상 시키기 위해 구문 및 인수가 업데이트 되었습니다.<br /><br /> -업데이트 된 예제를 추가 했습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
