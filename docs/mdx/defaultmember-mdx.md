---
title: DefaultMember (MDX) | Microsoft Docs
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
- DefaultMember
dev_langs:
- kbMDX
helpviewer_keywords:
- DefaultMember function
ms.assetid: c1b53b3a-6e73-4c41-a4fe-9f5c96da5463
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 738d66b3c6486c51978d3a68f5fbca73598c0382
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="defaultmember-mdx"></a>DefaultMember(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  계층의 기본 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Hierarchy_Expression.DefaultMember  
```  
  
## <a name="arguments"></a>인수  
 *Hierarchy_Expression*  
 계층을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 특성의 기본 멤버는 쿼리에 특성이 포함되어 있지 않을 때 식을 평가하는 데 사용됩니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 **DefaultMember** 와 함께에서 함수는 **이름** 함수 Adventure Works 큐브에 있는 Destination Currency 차원에 대 한 기본 멤버를 반환 하 합니다. 이 예에서는 반환 **미국 달러**합니다. **이름** 함수는 사용 하는 측정값의 기본 속성 대신 측정값의 이름을 반환 **값**합니다.  
  
```  
WITH MEMBER Measures.x AS   
   [Destination Currency].[Destination Currency].DefaultMember.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)   
 [기본 멤버 정의](../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  

