---
title: Parent (MDX) | Microsoft Docs
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
- PARENT
dev_langs:
- kbMDX
helpviewer_keywords:
- Parent function
ms.assetid: 7be9b172-4241-4618-bdba-53cde8badd9b
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 50a7c9b5df87a716db1ca5f64b1351e882d7a05d
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="parent-mdx"></a>Parent(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  멤버의 부모 항목을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member_Expression.Parent   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 **부모** 함수는 지정된 된 멤버의 부모 멤버를 반환 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

