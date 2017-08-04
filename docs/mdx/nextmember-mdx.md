---
title: NextMember (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NEXTMEMBER
dev_langs:
- kbMDX
helpviewer_keywords:
- NextMember function
ms.assetid: f67be3d0-082e-4bec-92e4-ba6ff33af303
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 665fe7316413bbe163ee4e51062c41f92023e7e2
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="nextmember-mdx"></a>NextMember(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 멤버를 포함하고 있는 수준에서 다음 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.NextMember   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 **NextMember** 함수는 지정 된 멤버를 포함 하는 동일한 수준에서 다음 멤버를 반환 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 July 2001 멤버의 다음 멤버로 August 2001 멤버를 반환합니다.  
  
```  
SELECT [Date].[Calendar].[Month].[July 2001].NextMember ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

