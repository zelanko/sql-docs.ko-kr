---
description: DefaultMember(MDX)
title: DefaultMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7363d650073b301eba6b29d509590e22dee5661a
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196027"
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
  
## <a name="remarks"></a>설명  
 특성의 기본 멤버는 쿼리에 특성이 포함되어 있지 않을 때 식을 평가하는 데 사용됩니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 **DefaultMember** 함수를 **Name** 함수와 함께 사용 하 여 놀이 Works 큐브의 Destination Currency 차원에 대 한 기본 멤버를 반환 합니다. 이 예에서는 **미국 달러**를 반환 합니다. **Name** 함수는 측정값의 default 속성 ( **value**)이 아닌 측정값의 이름을 반환 하는 데 사용 됩니다.  
  
```  
WITH MEMBER Measures.x AS   
   [Destination Currency].[Destination Currency].DefaultMember.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [기본 멤버 정의](/analysis-services/multidimensional-models/attribute-properties-define-a-default-member)  
  
