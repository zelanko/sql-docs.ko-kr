---
title: "큐브 공간 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c3a012b4-9ca0-4fb8-9c26-5ecc0e2e2b2b
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 316809a9fa0b00a04dd6cee85eceb3d9a0349801
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/13/2018
---
# <a name="cube-space"></a>큐브 공간
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
큐브 공간은 큐브 특성 계층의 멤버와 큐브의 측정값을 곱하여 생성된 공간입니다. 따라서 큐브 공간은 큐브의 모든 특성 계층 멤버와 큐브의 측정값을 곱한 결과의 조합으로 결정되며 큐브의 최대 크기를 정의합니다. 실제로는 조합이 불가능한 것으로 간주될 수도 있지만(예: 도시는 파리이고 국가는 잉글랜드, 스페인, 일본 또는 인도인 조합의 경우) 이 공간은 특성 계층 멤버의 가능한 모든 조합을 포함합니다.  
  
## <a name="autoexists-and-cube-space"></a>AUTOEXIST 및 큐브 공간  
 *AUTOEXIST* 의 개념은 이 큐브 공간을 실제로 존재하는 셀로 제한합니다. 한 차원에 있는 특성 계층의 멤버가 동일한 차원에 있는 다른 특성 계층의 멤버와 함께 존재하지 않을 수 있습니다.  
  
 예를 들어 City 특성 계층, Country 특성 계층 및 Internet Sales Amount 측정값이 있는 큐브에서 이 큐브의 공간에는 서로 함께 존재하는 멤버만 포함됩니다. 예를 들어 City 특성 계층에 New York, London, Paris, Tokyo 및 Melbourne이 포함되어 있고 Country 특성 계층에 United States, United Kingdom, France, Japan 및 Australia가 포함되어 있는 경우 Paris와 United States가 교차하는 지점의 공간(셀)은 해당 큐브 공간에 포함되지 않습니다.  
  
 존재하지 않는 셀을 쿼리하면 존재하지 않는 셀에서는 Null이 반환됩니다. 즉, 이 셀에는 계산이 들어 있지 않으며 이 공간에 쓰는 계산은 정의할 수 없습니다. 예를 들어 다음 문은 존재하지 않는 셀을 포함합니다.  
  
```  
SELECT [Customer].[Gender].[Gender].Members ON COLUMNS,  
{[Customer].[Customer].[Aaron A. Allen]  
   ,[Customer].[Customer].[Abigail Clark]} ON ROWS   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  이 쿼리에서는 [Members(집합)(MDX)](../../../mdx/members-set-mdx.md) 함수를 사용하여 Gender 특성 계층의 멤버 집합을 열 축에 반환하고 Customer 특성 계층의 지정한 멤버 집합과 이 집합을 행 축에서 교차시킵니다.  
  
 앞의 쿼리를 실행하면 Aaron A. Allen과 Female이 교차하는 셀에는 Null이 표시됩니다. 마찬가지로 Abigail Clark와 Male이 교차하는 셀에도 Null이 표시됩니다. 이러한 셀은 존재하지 않으며 값을 포함할 수 없지만 쿼리에서 반환되는 결과에는 존재하지 않는 셀도 나타날 수 있습니다.  
  
 [Crossjoin(MDX)](../../../mdx/crossjoin-mdx.md) 함수를 사용하여 동일한 차원에 있는 특성 계층의 특성 계층 멤버 간 교차곱을 반환할 때 AUTOEXIST는 전체 카티전 곱이 반환되는 것이 아니라 실제 존재하는 튜플 집합만 반환되도록 튜플을 제한합니다. 예를 들어 다음 쿼리를 실행한 다음 실행 결과를 확인하십시오.  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[State-Province].Members  
  ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  0은 열 축을 지정하는 데 사용되었으며 열 축을 나타내는 axis(0)을 줄여 쓴 것입니다.  
  
 앞의 쿼리는 쿼리의 각 특성 계층에서 서로 함께 존재하는 멤버의 셀만 반환합니다. 이전 쿼리는 [*(Crossjoin)(MDX)](../../../mdx/crossjoin-mdx-operator-reference.md) 함수의 새로운 * 변형을 사용하여 작성할 수도 있습니다.  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 이 쿼리는 다음과 같이 작성할 수도 있습니다.  
  
```  
SELECT [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
 결과 집합의 메타데이터는 다르지만 반환되는 셀 값은 동일합니다. 예를 들어 앞의 쿼리를 사용할 경우 Country 계층은 WHERE 절을 통해 slicer 축으로 이동되므로 결과 집합에 명시적으로 나타나지 않습니다.  
  
 앞의 세 쿼리는 각각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 AUTOEXIST 동작이 미치는 영향을 보여 줍니다.  
  
## <a name="user-defined-hierarchies-and-cube-space"></a>사용자 정의 계층 및 큐브 공간  
 이 항목의 앞에 나온 예제에서는 특성 계층을 사용하여 큐브 공간 내의 위치를 정의합니다. 그러나 차원의 특성 계층에 따라 정의한 사용자 정의 계층을 사용하여 큐브 공간 내의 위치를 정의할 수도 있습니다. 사용자 정의 계층은 사용자가 큐브 데이터를 쉽게 찾을 수 있도록 디자인된 특성 계층의 한 계층입니다.  
  
 예를 들어 이전 섹션의 **CROSSJOIN** 쿼리를 다음과 같이 작성할 수도 있습니다.  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[Customer Geography].[State-Province].Members  
   )   
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 이 쿼리에서 Customer 차원 내의 사용자 정의 계층인 Customer Geography는 이전에 특성 계층을 사용하여 정의한 큐브 공간 내의 위치를 정의하는 데 사용됩니다. 즉, 큐브 공간 내의 동일한 위치를 특성 계층이나 사용자 정의 계층 중 하나를 사용하여 정의할 수 있습니다.  
  
##  <a name="AttribRelationships"></a> 특성 관계 및 큐브 공간  
 관련된 특성 간의 특성 관계를 정의하면 적절한 집계를 쉽게 만들 수 있으므로 쿼리 성능이 향상되며 특성 계층 멤버와 함께 나타나는 관련 특성 계층의 멤버에 영향을 줄 수 있습니다. 예를 들어 City 특성 계층의 멤버를 포함하는 튜플을 정의할 때 해당 튜플에 Country 특성 계층 멤버가 명시적으로 정의되어 있지 않으면 기본 Country 특성 계층 멤버가 Country 특성 계층의 관련 멤버가 됩니다. 그러나 이는 City 특성 계층과 Country 특성 계층 간에 특성 관계가 정의되어 있는 경우에만 해당됩니다.  
  
 다음 예에서는 쿼리에 명시적으로 포함되지 않은 관련 특성 계층의 멤버를 반환합니다.  
  
```  
WITH MEMBER Measures.x AS   
   Customer.Country.CurrentMember.Name  
SELECT Measures.x ON 0,  
Customer.City.Members ON 1  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  **WITH** 키워드는 [CurrentMember(MDX)](../../../mdx/currentmember-mdx.md) 및 [Name(MDX)](../../../mdx/name-mdx.md) 함수와 함께 쿼리에 사용할 계산 멤버를 만드는 데 사용됩니다. 자세한 내용은 [기본 MDX 쿼리&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)를 참조하세요.  
  
 앞의 쿼리에서는 State 특성 계층의 각 멤버와 관련된 Country 특성 계층의 멤버 이름이 반환됩니다. 이 경우 City 특성과 Country 특성 간의 특성 관계가 정의되어 있으므로 예상한 Country 멤버가 나타납니다. 그러나 동일한 차원의 특성 계층 간에 특성 관계가 정의되어 있지 않으면 (All) 멤버가 반환됩니다. 다음 쿼리에서는 이를 보여 줍니다.  
  
```  
WITH MEMBER Measures.x AS   
   Customer.Education.Currentmember.Name  
SELECT Measures.x  ON 0,   
Customer.City.Members ON 1  
FROM [Adventure Works]  
```  
  
 이 쿼리에서는 Education과 City 간의 관계가 없으므로 (All) 멤버("All Customers")가 반환됩니다. 따라서 Education 특성 계층의 (All) 멤버는 Education 멤버가 명시적으로 지정되지 않은 경우 City 특성 계층이 관련된 모든 튜플에서 사용되는 Education 특성 계층의 기본 멤버입니다.  
  
## <a name="calculation-context"></a>계산 컨텍스트  
  
## <a name="see-also"></a>관련 항목:  
 [MDX &#40;의 주요 개념 Analysis Services &#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [튜플](../../../analysis-services/multidimensional-models/mdx/tuples.md)   
 [Autoexist](../../../analysis-services/multidimensional-models/mdx/autoexists.md)   
 [멤버, 튜플 및 집합 &#40; 사용 Mdx&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [보이는 값 합계 및 보이지 않는 값 합계](../../../analysis-services/multidimensional-models/mdx/visual-totals-and-non-visual-totals.md)   
 [MDX 언어 참조 &#40; Mdx&#41;](../../../mdx/mdx-language-reference-mdx.md)   
 [다차원 식 &#40; Mdx&#41; 참조](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
