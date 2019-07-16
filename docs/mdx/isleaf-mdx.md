---
title: IsLeaf (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 400c55cdfcea35ae60859fb66489384870172744
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905940"
---
# <a name="isleaf-mdx"></a>IsLeaf(MDX)


  지정한 멤버가 리프 멤버인지 여부를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IsLeaf(Member_Expression)   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 합니다 **IsLeaf** 함수에서 반환 **true** 지정 된 멤버가 리프 멤버인 경우. 반환이 고, 그렇지 **false**합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 [Date].[Fiscal].CurrentMember가 리프 멤버인 경우 TRUE를 반환합니다.  
  
 `WITH MEMBER MEASURES.ISLEAFDEMO AS`  
  
 `IsLeaf([Date].[Fiscal].CURRENTMEMBER)`  
  
 `SELECT {MEASURES.ISLEAFDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
