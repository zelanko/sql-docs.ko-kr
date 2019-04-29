---
title: Level (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8406d02e167258901c3a6ce9ed3a1d7de935df54
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63048517"
---
# <a name="level-mdx"></a>Level(MDX)


  멤버의 수준을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.Level  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
### <a name="examples"></a>예  
 다음 예제에서는 합니다 **수준** Adventure Works 큐브의 모든 월을에서 반환 하는 함수입니다.  
  
```  
SELECT[Date].[Fiscal].[Month].[February 2002].Level.Members ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 다음 예제에서는 합니다 **수준** Adventure Works 큐브에 있는 Model Name 특성 계층의 All-Purpose Bike Stand에 대 한 수준 이름을 반환 하는 함수입니다.  
  
```  
WITH MEMBER Measures.x AS   
   [Product].[Model Name].[All-Purpose Bike Stand].Level.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
