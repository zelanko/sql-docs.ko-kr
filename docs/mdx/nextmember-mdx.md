---
title: NextMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4535b837d81db10f41f1445a7051678ce4fdd688
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63277862"
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
  
## <a name="remarks"></a>Remarks  
 합니다 **NextMember** 함수는 지정 된 멤버를 포함 하는 동일한 수준에서 다음 멤버를 반환 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 July 2001 멤버의 다음 멤버로 August 2001 멤버를 반환합니다.  
  
```  
SELECT [Date].[Calendar].[Month].[July 2001].NextMember ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
