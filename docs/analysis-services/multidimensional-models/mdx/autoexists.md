---
title: Autoexist | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3c156f9e0d6df2afbf7710b1ed5c19fb60034e92
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62800214"
---
# <a name="autoexists"></a>AUTOEXIST
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  *AUTOEXIST* 개념에서는 동일한 계층의 특성 계층 멤버로 만들 수 있는 모든 조합의 결과로 존재하는 셀이 아니라 큐브에서 실제로 존재하는 셀로 큐브 공간을 제한합니다. 이는 한 특성 계층의 멤버가 동일한 차원에 있는 다른 특성 계층의 멤버와 함께 존재할 수 없기 때문입니다. SELECT 문에서 동일한 차원의 특성 계층이 두 개 이상 사용되는 경우 Analysis Services에서는 이러한 특성의 멤버가 다른 모든 특성의 조건에 맞게 적절히 제한되도록 특성의 식을 계산합니다.  
  
 예를 들어 Geography 차원의 특성을 사용한다고 가정합니다. City 특성의 모든 멤버를 반환하는 식과 Country 특성의 멤버를 유럽의 모든 국가로 제한하는 다른 식이 있는 경우 City 멤버는 유럽 국가에 속한 도시로만 제한됩니다. 이것은 Analysis Services의 AUTOEXIST 특징 때문입니다. Autoexists는 한 특성 식에서 제외된 차원 레코드를 다른 특성 식에서 포함하지 않도록 하기 때문에 동일한 차원의 특성에만 적용됩니다. 결과적으로 차원 행에서 서로 다른 특성 식이 교차하는 것으로 AUTOEXIST를 이해할 수도 있습니다.  
  
## <a name="cell-existence"></a>셀 존재  
 다음 셀은 항상 존재합니다.  
  
-   동일한 차원에 있는 다른 계층의 멤버와 교차할 경우 모든 계층의 (All) 멤버  
  
-   비계산 형제 또는 비계산 형제의 부모나 하위 항목과 교차할 경우 계산 멤버  
  
## <a name="providing-non-existing-cells"></a>존재하지 않는 셀 제공  
 존재하지 않는 셀은 큐브에 존재하지 않은 셀을 요청하는 쿼리나 계산에 대한 응답으로 시스템에서 제공하는 셀입니다. 예를 들어 Geography 차원에 속하는 City 특성 계층 및 Country 특성 계층과 Internet Sales Amount 측정값이 있는 큐브에서 이 큐브의 공간에는 서로 함께 존재하는 멤버만 포함됩니다. 예를 들어 City 특성 계층에 New York, London, Paris, Tokyo 및 Melbourne이 포함되어 있고 Country 특성 계층에 United States, United Kingdom, France, Japan 및 Australia가 포함되어 있는 경우 Paris와 United States가 교차하는 지점의 공간(셀)은 해당 큐브 공간에 포함되지 않습니다.  
  
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
  
## <a name="deep-and-shallow-autoexists"></a>전체 및 단순 AUTOEXIST  
 AUTOEXIST는 식에 전체 또는 단순 적용될 수 있습니다. **Deep Autoexists** 는 slicer 식, 축의 하위 선택 식 등을 적용한 후 가능한 가장 범위가 큰 공간에 맞게 모든 식이 계산됨을 의미합니다. **Shallow Autoexists** 는 현재 식과 해당 결과가 현재 식에 전달되기 전에 외부 식이 계산됨을 의미합니다. 기본 설정은 전체 AUTOEXIST입니다.  
  
 다음 시나리오와 샘플에서는 여러 다른 유형의 AUTOEXIST를 보여 줍니다. 다음 예에서는 두 집합인 계산 식으로서의 집합과 상수 식으로서의 집합을 만듭니다.  
  
 `//Obtain the Top 10 best reseller selling products by Name`  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 다음과 같은 결과 집합을 얻을 수 있습니다.  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0.04%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0.53%**|  
|**Touring-1000**|**$6,723,794.29**|**$166,144.17**|**2.47%**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0.05%**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0.57%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
|**Road-150**|**$2,363,805.16**|**$0.00**|**0.00%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3.89%**|  
  
 이 결과 제품 집합은 Preferred10Products와 동일합니다. Preferred10Products 집합은 다음과 같습니다.  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 다음 결과에 따라 두 집합(Top10SellingProducts, Preferred10Products)은 동일합니다.  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0.04%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0.53%**|  
|**Touring-1000**|**$6,723,794.29**|**$166,144.17**|**2.47%**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0.05%**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0.57%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
|**Road-150**|**$2,363,805.16**|**$0.00**|**0.00%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3.89%**|  
  
 다음 예에서는 전체 Autoexists의 개념을 설명합니다. 예에서 [Mountain] 그룹의 Top10SellingProducts를 [Product].[Product Line] 특성별로 필터링합니다. 두 특성(slicer 및 축)이 동일한 차원인 [Product]에 속합니다.  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `// Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 결과 집합은 다음과 같습니다.  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
|**Mountain-300**|**$1,907,249.38**|**$876.95**|**0.05%**|  
|**Mountain-500**|**$1,067,327.31**|**$17,266.09**|**1.62%**|  
|**Mountain-400-W**|**$592,450.05**|**$303.49**|**0.05%**|  
|**LL Mountain Frame**|**$521,864.42**|**$252.41**|**0.05%**|  
|**ML Mountain Frame-W**|**$482,953.16**|**$206.95**|**0.04%**|  
|**ML Mountain Frame**|**$343,785.29**|**$161.82**|**0.05%**|  
|**Women's Mountain Shorts**|**$260,304.09**|**$6,675.56**|**2.56%**|  
  
 위 결과 집합에는 Top10SellingProducts 목록에 7개의 새 항목이 있으며 Mountain-200, Mountain-100 및 HL Mountain Frame이 목록 맨 위로 이동했습니다. 이전 결과 집합에서는 이러한 3개의 값이 섞였습니다.  
  
 Top10SellingProducts 집합이 쿼리의 조각화 조건을 충족하도록 계산되기 때문에 이를 전체 Autoexists라고 합니다. 전체 Autoexists는 slicer 식, 축의 하위 선택 식 등을 적용한 후 가능한 가장 범위가 큰 공간에 맞게 모든 식이 계산됨을 의미합니다.  
  
 그러나 다음 예와 같이 Top10SellingProducts를 Preferred10Products와 동등하게 분석하기를 원할 수 있습니다.  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 결과 집합은 다음과 같습니다.  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
  
 위의 결과에서 조각화를 수행하면 Preferred10Products가 상수 식이기 때문에 예상대로 [Product].[Product Line]에 있는 [Mountain] 그룹의 일부인 Preferred10Products의 제품만 포함하는 결과가 생성됩니다.  
  
 이러한 결과 집합을 단순 AUTOEXIST라고 합니다. 이는 식이 조각화 절 이전에 계산되기 때문입니다. 이전 예에서는 식이 개념 소개를 위한 설명을 제공하기 위해 상수 식이었습니다.  
  
 Autoexists 동작은 **Autoexists** 연결 문자열 속성을 사용하여 세션 수준에서 수정할 수 있습니다. 다음 예에서는 새 세션을 열고 *Autoexists=3* 속성을 연결 문자열에 추가하여 시작합니다. 예를 실행하기 위해 새 연결을 열어야 합니다. Autoexist 설정을 사용하여 연결을 설정하면 연결이 완료될 때까지 계속 연결이 유지됩니다.  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `//Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 다음 결과 집합은 이제 AUTOEXIST의 부분 동작을 보여 줍니다.  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Discount Amount**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
  
 Autoexists 동작은 사용 하 여 수정할 수 = [1 | 2 | 3]에서 연결 문자열을 매개 변수 참조 [지원 되는 XMLA 속성 &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 하 고 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 매개 변수 사용에 대 한 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX의 주요 개념&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [큐브 공간](../../../analysis-services/multidimensional-models/mdx/cube-space.md)   
 [튜플](../../../analysis-services/multidimensional-models/mdx/tuples.md)   
 [멤버, 튜플 및 집합 & #40; 사용 Mdx& #41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [보이는 값 합계 및 보이지 않는 값 합계](../../../analysis-services/multidimensional-models/mdx/visual-totals-and-non-visual-totals.md)   
 [MDX 언어 참조&#40;MDX&#41;](../../../mdx/mdx-language-reference-mdx.md)   
 [다차원 식 & #40; Mdx& #41; 참조](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
