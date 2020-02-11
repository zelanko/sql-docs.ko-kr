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
ms.openlocfilehash: b419cbb05aa616f163f5878bda83c9d68203575d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905666"
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
 다음 예에서는 **Level** 함수를 사용 하 여 놀이 Works 큐브의 모든 월을 반환 합니다.  
  
```  
SELECT[Date].[Fiscal].[Month].[February 2002].Level.Members ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 다음 예에서는 **Level** 함수를 사용 하 여 놀이 Works 큐브의 Model name 특성 계층에 있는 모든 용도의 자전거에 대 한 수준의 이름을 반환 합니다.  
  
```  
WITH MEMBER Measures.x AS   
   [Product].[Model Name].[All-Purpose Bike Stand].Level.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
