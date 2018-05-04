---
title: 멤버 함수를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- member functions [MDX]
ms.assetid: 094c443f-0daa-4af7-801c-d2e1d686d755
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: f7aa6bf39c27a16cd70b222b6417d7059445dd44
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-member-functions"></a>멤버 함수 사용
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  멤버 함수는 멤버를 반환하는 MDX(Multidimensional Expressions) 함수입니다. 멤버 함수는 튜플 함수 및 집합 함수와 마찬가지로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 사용되는 다차원 구조를 처리하는 데 필수적입니다.  
  
 MDX의 많은 멤버 함수 중 가장 중요 한 것은 **CurrentMember** 현재 멤버는 계층 구조를 확인 하는 데 사용 되는 함수입니다. 다음 쿼리는와 함께 사용 하는 방법을 보여 줍니다는 **부모**, **상위**, 및 **Prevmember** 함수:  
  
 `WITH`  
  
 `//Returns the name of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[CurrentMemberDemo] AS [Date].[Calendar].CurrentMember.Name`  
  
 `//Returns the name of the parent of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[ParentDemo] AS [Date].[Calendar].CurrentMember.Parent.Name`  
  
 `//Returns the name of the ancestor of the currentmember on the Calendar hierarchy at the Year level`  
  
 `MEMBER MEASURES.[AncestorDemo] AS ANCESTOR([Date].[Calendar].CurrentMember, [Date].[Calendar].[Calendar Year]).Name`  
  
 `//Returns the name of the member before the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[PrevMemberDemo] AS [Date].[Calendar].CurrentMember.Prevmember.Name`  
  
 `SELECT{MEASURES.[CurrentMemberDemo],MEASURES.[ParentDemo],MEASURES.[AncestorDemo],MEASURES.[PrevMemberDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목:  
 [함수 &#40;MDX 구문&#41;](../mdx/functions-mdx-syntax.md)   
 [튜플 함수 사용](../mdx/using-tuple-functions.md)   
 [집합 함수 사용](../mdx/using-set-functions.md)  
  
  
