---
title: Members (MDX) 계산 된 세션 범위 만들기 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1f587c6a34d69da4ad3a218678eaa5b3f026f01b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-calculated-members---session-scoped-calculated-members"></a>MDX 계산 멤버-세션 범위 계산된 멤버
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  MDX 세션 전체에서 사용할 수 있는 계산 멤버를 만들려면 [CREATE MEMBER](../../../mdx/mdx-data-definition-create-member.md) 문을 사용합니다. CREATE MEMBER 문을 사용하여 만든 계산 멤버는 MDX 세션이 닫힌 후까지 제거되지 않습니다.  
  
 이 항목에서 설명한 바와 같이 CREATE MEMBER 문의 구문은 간단하고 사용하기 쉽습니다.  
  
> [!NOTE]  
>  계산 멤버에 대한 자세한 내용은 [계산 멤버를 MDX로 작성&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md)을 참조하세요.  
  
## <a name="create-member-syntax"></a>CREATE MEMBER 구문  
 다음 구문을 사용하여 CREATE MEMBER 문을 MDX 문에 추가합니다.  
  
```  
CREATE [SESSION] MEMBER [<cube-name>.]<fully-qualified-member-name> AS <expression> [,<property-definition-list>]  
<cube name> ::= CURRENTCUBE | <Cube Name>  
<property-definition-list> ::= <property-definition>  
  | <property-definition>, <property-definition-list>  
<property-definition> ::= <property-identifier> = <property-value>  
<property-identifier> ::= VISIBLE | SOLVEORDER | SOLVE_ORDER | FORMAT_STRING | NON_EMPTY_BEHAVIOR <ole db member properties>  
```  
  
 CREATE MEMBER 문에 대한 구문에서 `fully-qualified-member-name` 값은 계산 멤버의 정규화된 이름입니다. 이 정규화된 이름에는 계산 멤버가 연결된 차원 또는 수준이 포함됩니다. `expression` 값은 식 값이 계산된 후의 계산 멤버의 값을 반환합니다.  
  
## <a name="create-member-example"></a>CREATE MEMBER 예  
 다음 예에서는 CREATE MEMBER 문을 사용하여 `LastFourStores` 계산 멤버를 만드는 방법을 보여 줍니다. 이 계산 멤버는 마지막 4개 매장에서 팔린 합계를 반환하고 큐브의 전체 세션에서 사용될 것입니다.  
  
```  
Create Session Member [Store].[Measures].LastFourStores as   
sum(([Stores].[ByLocation].Lag(3) :  
[Stores].[ByLocation].NextMember), [Measures].[Units Sold])  
```  
  
## <a name="see-also"></a>관련 항목:  
 [멤버 & #40; 계산 된 쿼리 범위를 만들기 Mdx& #41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md)  
  
  
