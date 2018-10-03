---
title: 사용자 정의 멤버 속성 (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- custom member properties [MDX]
ms.assetid: b64cc581-e784-42c4-bec8-932abd687423
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97f7a61772b93c78173f3eca8ad38fca1ade671a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48114313"
---
# <a name="user-defined-member-properties-mdx"></a>사용자 정의 멤버 속성(MDX)
  사용자 정의 멤버 속성을 차원 내의 특정한 이름의 수준에 특성 관계로 추가할 수 있습니다. 사용자 정의 멤버 속성을 추가할 수 없습니다는 `(All)` 자체 계층 구조 또는 계층의 수준입니다.  
  
## <a name="creating-user-defined-member-properties"></a>사용자 정의 멤버 속성 만들기  
 사용자 정의 멤버 속성을 서버 기반 차원 또는 큐브에 추가하는 데는 사용자 인터페이스 방식 또는 프로그래밍 방식을 사용할 수 있습니다.  
  
-   사용자 인터페이스를 통해 사용자 정의 멤버 속성을 추가하려면 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]의 차원 디자이너를 사용하세요. 자세한 내용은 [특성 관계 정의](../attribute-relationships-define.md)를 참조하세요.  
  
-   프로그래밍 방식으로 사용자 정의 멤버 속성을 추가하려면 응용 프로그램에서 AMO(Analysis Management Objects)를 사용하거나 XMLA(XML for Analysis) 및 ASSL(Analysis Services Scripting Language)을 조합하여 사용하십시오. 자세한 내용은 [특성 관계](../../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)를 참조하세요.  
  
## <a name="retrieving-user-defined-member-properties"></a>사용자 정의 멤버 속성 검색  
 사용자 정의 멤버 속성 중 하나를 사용 하 여 검색할 수 있습니다 합니다 `PROPERTIES` 키워드와 [속성](/sql/mdx/properties-mdx) 함수입니다.  
  
### <a name="using-the-properties-keyword-to-retrieve-user-defined-member-properties"></a>PROPERTIES 키워드를 사용한 사용자 정의 멤버 속성 검색  
 사용자 정의 멤버 속성을 검색하는 구문은 다음 구문과 같이 기본 수준 멤버 속성을 검색하는 구문과 비슷합니다.  
  
 `DIMENSION PROPERTIES [Dimension.]Level.<Custom_Member_Property>`  
  
 `PROPERTIES` 키워드는 축 사양의 집합 식 뒤에 표시 됩니다. 예를 들어 다음 MDX 쿼리를 `PROPERTIES` 키워드를 검색 합니다 `List Price` 및 `Dealer Price` 사용자 정의 멤버 속성 년 1 월에 판매 된 제품을 식별 하는 집합 식 뒤 및:  
  
```  
SELECT   
   CROSSJOIN([Ship Date].[Calendar].[Calendar Year].Members,   
             [Measures].[Sales Amount]) ON COLUMNS,  
   NON EMPTY Product.Product.MEMBERS  
   DIMENSION PROPERTIES   
              Product.Product.[List Price],  
              Product.Product.[Dealer Price]  ON ROWS  
FROM [Adventure Works]  
WHERE ([Date].[Month of Year].[January])   
```  
  
### <a name="using-the-properties-function-to-retrieve-user-defined-member-properties"></a>Properties 함수를 사용하여 사용자 정의 멤버 속성 검색  
 또는 `Properties` 함수를 사용해 사용자 정의 멤버 속성에 액세스할 수 있습니다. 예를 들어 다음 MDX 쿼리를 사용 하는 `WITH` 구성 된 계산된 멤버를 만들려면 키워드를 `List Price` 멤버 속성:  
  
```  
WITH   
   MEMBER [Measures].[Product List Price] AS  
   [Product].[Product].CurrentMember.Properties("List Price")  
SELECT   
   [Measures].[Product List Price] on COLUMNS,  
   [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
```  
  
 계산 멤버 작성에 대한 자세한 내용은 [계산 멤버를 MDX로 작성&#40;MDX&#41;](mdx-calculated-members-building-calculated-members.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [멤버 속성을 사용 하 여 &#40;MDX&#41;](mdx-member-properties.md)   
 [속성 &#40;MDX&#41;](/sql/mdx/properties-mdx)  
  
  
