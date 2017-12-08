---
title: "사용자 정의 멤버 속성 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: custom member properties [MDX]
ms.assetid: b64cc581-e784-42c4-bec8-932abd687423
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: eaeb79931b4c9c57088ada093148047a26b614d2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="mdx-member-properties---user-defined-member-properties"></a>MDX 멤버 속성-사용자 정의 멤버 속성
  사용자 정의 멤버 속성을 차원 내의 특정한 이름의 수준에 특성 관계로 추가할 수 있습니다. 계층의 **(All)** 수준 또는 수준 자체에는 사용자 정의 멤버 속성을 추가할 수 없습니다.  
  
## <a name="creating-user-defined-member-properties"></a>사용자 정의 멤버 속성 만들기  
 사용자 정의 멤버 속성을 서버 기반 차원 또는 큐브에 추가하는 데는 사용자 인터페이스 방식 또는 프로그래밍 방식을 사용할 수 있습니다.  
  
-   사용자 인터페이스를 통해 사용자 정의 멤버 속성을 추가하려면 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]의 차원 디자이너를 사용하세요. 자세한 내용은 [특성 관계 정의](../../../analysis-services/multidimensional-models/attribute-relationships-define.md)를 참조하세요.  
  
-   프로그래밍 방식으로 사용자 정의 멤버 속성을 추가하려면 응용 프로그램에서 AMO(Analysis Management Objects)를 사용하거나 XMLA(XML for Analysis) 및 ASSL(Analysis Services Scripting Language)을 조합하여 사용하십시오. 자세한 내용은 [특성 관계](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)를 참조하세요.  
  
## <a name="retrieving-user-defined-member-properties"></a>사용자 정의 멤버 속성 검색  
 사용자 정의 멤버 속성을 검색하는 데는 **PROPERTIES** 키워드 또는 [Properties](../../../mdx/properties-mdx.md) 함수를 사용할 수 있습니다.  
  
### <a name="using-the-properties-keyword-to-retrieve-user-defined-member-properties"></a>PROPERTIES 키워드를 사용한 사용자 정의 멤버 속성 검색  
 사용자 정의 멤버 속성을 검색하는 구문은 다음 구문과 같이 기본 수준 멤버 속성을 검색하는 구문과 비슷합니다.  
  
 `DIMENSION PROPERTIES [Dimension.]Level.<Custom_Member_Property>`  
  
 **PROPERTIES** 키워드는 축 사양의 집합 식 뒤에 표시됩니다. 예를 들어 다음 MDX 쿼리에는 1월에 판매된 제품을 식별하는 집합 식 뒤에 **및** 사용자 정의 멤버 속성을 검색하는 `List Price` PROPERTIES `Dealer Price` 키워드가 있습니다.  
  
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
 또는 **Properties** 함수를 사용해 사용자 정의 멤버 속성에 액세스할 수 있습니다. 예를 들어 다음 MDX 쿼리는 **WITH** 키워드를 사용해 `List Price` 멤버 속성으로 구성된 계산 멤버를 만듭니다.  
  
```  
WITH   
   MEMBER [Measures].[Product List Price] AS  
   [Product].[Product].CurrentMember.Properties("List Price")  
SELECT   
   [Measures].[Product List Price] on COLUMNS,  
   [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
```  
  
 계산 멤버 작성에 대한 자세한 내용은 [계산 멤버를 MDX로 작성&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [멤버 속성 사용&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties.md)   
 [속성 &#40; Mdx&#41;](../../../mdx/properties-mdx.md)  
  
  
