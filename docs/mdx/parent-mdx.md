---
title: Parent (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 16de50e05bf139d590f90630e338fdb7cbb428e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63278432"
---
# <a name="parent-mdx"></a>Parent(MDX)


  멤버의 부모 항목을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.Parent   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **부모** 함수는 지정 된 멤버의 부모 멤버를 반환 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 July 1, 2001 멤버의 부모 멤버를 반환합니다. 첫 번째 예에서는 Date 특성 계층의 컨텍스트에서 이 멤버를 지정하고 All Periods 멤버를 반환합니다.  
  
```  
SELECT [Date].[Date].[July 1, 2001].Parent ON 0  
FROM [Adventure Works]  
```  
  
 다음 예에서는 Calendar 계층의 컨텍스트에서 July 1, 2001 멤버를 지정합니다.  
  
```  
SELECT [Date].[Calendar].[July 1, 2001].Parent ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
