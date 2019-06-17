---
title: DefaultMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3a0c11acadcbdcadfd9398baff09db9292c87eb2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63248126"
---
# <a name="defaultmember-mdx"></a>DefaultMember(MDX)


  계층의 기본 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Hierarchy_Expression.DefaultMember  
```  
  
## <a name="arguments"></a>인수  
 *Hierarchy_Expression*  
 계층을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 특성의 기본 멤버는 쿼리에 특성이 포함되어 있지 않을 때 식을 평가하는 데 사용됩니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 합니다 **DefaultMember** 함수를 함께 합니다 **이름** Adventure Works 큐브에 있는 Destination Currency 차원의 기본 멤버를 반환 합니다. 이 예에서는 반환 **미국 달러**합니다. 합니다 **이름을** 함수는 사용 되는 측정값의 기본 속성 대신 측정값의 이름을 반환 **값**합니다.  
  
```  
WITH MEMBER Measures.x AS   
   [Destination Currency].[Destination Currency].DefaultMember.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 & #40; Mdx& #41;](../mdx/mdx-function-reference-mdx.md)   
 [기본 멤버 정의](../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  
