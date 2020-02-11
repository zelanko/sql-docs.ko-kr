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
ms.openlocfilehash: b852564510c6b5918c781e0c75e84e3b30aecd44
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088360"
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
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
