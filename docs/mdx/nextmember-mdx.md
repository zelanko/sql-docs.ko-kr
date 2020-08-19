---
description: NextMember(MDX)
title: NextMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 33824ba605fc3acd0a994d0e0a6b411afdda2306
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483745"
---
# <a name="nextmember-mdx"></a>NextMember(MDX)


  지정한 멤버를 포함하고 있는 수준에서 다음 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.NextMember   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **Nextmember** 함수는 동일한 수준에서 지정 된 멤버를 포함 하는 다음 멤버를 반환 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 July 2001 멤버의 다음 멤버로 August 2001 멤버를 반환합니다.  
  
```  
SELECT [Date].[Calendar].[Month].[July 2001].NextMember ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
