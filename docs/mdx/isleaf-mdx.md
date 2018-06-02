---
title: IsLeaf (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a04964b0fe2512c008d376d8758c2d4106394133
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578725"
---
# <a name="isleaf-mdx"></a>IsLeaf(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 멤버가 리프 멤버인지 여부를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IsLeaf(Member_Expression)   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>Remarks  
 **IsLeaf** 함수에서 반환 **true** 지정 된 멤버가 리프 멤버인 경우. 그렇지 않으면 함수가 반환 **false**합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 [Date].[Fiscal].CurrentMember가 리프 멤버인 경우 TRUE를 반환합니다.  
  
 `WITH MEMBER MEASURES.ISLEAFDEMO AS`  
  
 `IsLeaf([Date].[Fiscal].CURRENTMEMBER)`  
  
 `SELECT {MEASURES.ISLEAFDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
