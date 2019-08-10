---
title: SELECT 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 83a381e36a31542d6ad39ed9d26864350004af5c
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891146"
---
# <a name="mdx-data-manipulation---select"></a>MDX 데이터 조작 - SELECT


  지정한 큐브에서 데이터를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
[ WITH <SELECT WITH clause>   
   [ , <SELECT WITH clause>...n ]   
]   
SELECT   
     [ *   
    | ( <SELECT query axis clause>   
                  [ , <SELECT query axis clause>,...n ]   
            )   
            ]  
FROM   
   <SELECT subcube clause>   
      [ <SELECT slicer axis clause> ]  
      [ <SELECT cell property list clause> ]  
  
<SELECT WITH clause> ::=  
     ( CELL CALCULATION <CREATE CELL CALCULATION body clause> )   
   | ( [ CALCULATED ] MEMBER <CREATE MEMBER body clause>)   
   | ( SET <CREATE SET body clause>)  
   | ( MEASURE = <measure body clause> )  
  
<SELECT query axis clause> ::=  
   [ NON EMPTY ] Set_Expression  
   [ <SELECT dimension property list clause> ]   
      ON   
            Integer_Expression   
       | AXIS(Integer)   
       | COLUMNS   
       | ROWS   
       | PAGES   
       | SECTIONS   
       | CHAPTERS   
  
<SELECT subcube clause> ::=  
      Cube_Name   
   | [NON VISUAL] (SELECT   
                  [ *   
       | ( <SELECT query axis clause> [ ,   
           <SELECT query axis clause>,...n ] )   
         ]   
            FROM   
         <SELECT subcube clause>   
         <SELECT slicer axis clause> )  
  
<SELECT slicer axis clause> ::=   
      WHERE Tuple_Expression  
  
<SELECT cell property list clause> ::=   
   [ CELL ] PROPERTIES CellProperty_Name   
      [ , CellProperty_Name,...n ]  
  
<SELECT dimension property list clause> ::=  
   [DIMENSION] PROPERTIES   
      (DimensionProperty_Name   
         [,DimensionProperty_Name,...n ] )   
    | (LevelProperty_Name   
         [, LevelProperty_Name,...n ] )   
    | (MemberProperty_Name   
         [, MemberProperty_Name,...n ] )  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Integer*  
 0에서 127 사이의 정수입니다.  
  
 *Cube_Name*  
 큐브 이름을 지정하는 유효한 문자열입니다.  
  
 *Tuple_Expression*  
 튜플을 반환하는 유효한 MDX 식입니다.  
  
 *CellProperty_Name*  
 셀 속성을 나타내는 유효한 문자열입니다.  
  
 *DimensionProperty_Name*  
 차원 속성을 나타내는 유효한 문자열입니다.  
  
 *LevelProperty_Name*  
 수준 속성을 나타내는 유효한 문자열입니다.  
  
 *MemberProperty_Name*  
 멤버 속성을 나타내는 유효한 문자열입니다.  
  
## <a name="remarks"></a>설명  
 `<SELECT slicer axis clause>` 식에는 지정된 `<SELECT query axis clause>` 식에서 참조되는 것 이외의 멤버가 차원 및 계층에 포함되어 있어야 합니다.  
  
 지정된 `<SELECT query axis clause>` 식과 `<SELECT slicer axis clause>` 값에 큐브의 특성이 생략되어 있으면 특성의 기본 멤버가 slicer 축에 암시적으로 추가됩니다.  
  
 하위 SELECT 문에 NON VISUAL 옵션을 사용하면 필터링된 합계 대신 순 합계를 유지하면서 멤버를 필터링할 수 있습니다. 즉, 상위 10개 매출 정보(사람/제품/지역)를 쿼리한 후 상위 10개의 매출 합계 값 대신 쿼리한 모든 멤버의 매출 순 합계를 반환 결과로 얻을 수 있습니다. 자세한 내용은 아래 예를 참조하십시오.  
  
 연결 문자열 매개 변수 하위 쿼리 \<를 사용 하 여 열을 열 때마다 계산 멤버를 SELECT 쿼리 축 > 절에 포함할 수 있습니다. *하위 쿼리 = 1*, [지원 되는 &#40;xmla 속성 xmla&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 및 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>매개 변수 사용. 하위 SELECT의 계산 멤버에 대한 예는 다음을 참조하십시오.  
  
## <a name="autoexists"></a>AUTOEXIST  
 SELECT 문에 두 개 이상의 차원 특성이 사용되는 경우 Analysis Services에서는 이러한 특성의 멤버가 다른 모든 특성의 기준에 맞도록 적절히 제한되도록 특성의 식을 계산합니다. 예를 들어 Geography 차원의 특성을 사용한다고 가정합니다. City 특성의 모든 멤버를 반환하는 식과 Country 특성의 멤버를 유럽의 모든 국가로 제한하는 다른 식이 있는 경우 City 멤버는 유럽 국가에 속한 도시로만 제한됩니다. 이러한 Analysis Services 특징을 Autoexists라고 하며 이는 동일한 차원의 특성에만 적용됩니다. Autoexists는 한 특성 식에서 제외된 차원 레코드를 다른 특성 식에서 포함하지 않도록 하기 때문에 동일한 차원의 특성에만 적용됩니다. 결과적으로 차원 레코드에서 서로 다른 특성 식이 교차하는 것으로 Autoexists를 이해할 수도 있습니다. 아래의 예를 참조하십시오.  
  
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
  
 이전 예에서는 두 집합인 계산 식으로서의 집합과 상수 식으로서의 집합을 만들었습니다. 이 예에서는 Autoexists의 다른 특성을 보여 줍니다.  
  
 Autoexists는 식에 전체 또는 단순 적용될 수 있습니다. 기본 설정은 전체입니다. 다음 예에서는 전체 Autoexists의 개념을 설명합니다. 예에서 [Mountain] 그룹의 Top10SellingProducts를 [Product].[Product Line] 특성별로 필터링합니다. 두 특성(slicer 및 축)이 동일한 차원인 [Product]에 속합니다.  
  
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
  
 이전 결과 집합에서는 Top10SellingProducts 및 Mountain-200, Mountain-100 및 HL Mountain Frame 목록에 대한 7개의 새 항목이 목록 맨 위로 이동했습니다. 이전 결과 집합에서는 이러한 3개의 값이 섞였습니다.  
  
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
  
 이러한 결과 집합을 부분 Autoexists라고 합니다. 이는 식이 조각화 절 이전에 계산되기 때문입니다. 이전 예에서는 식이 개념 소개를 위한 설명을 제공하기 위해 상수 식이었습니다.  
  
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
  
 Autoexists 동작은 연결 문자열의 AUTOEXISTS = [1 | 2 | 3] 매개 변수를 사용 하 여 수정할 수 있습니다. [지원 되는 xmla &#40;속성&#41; xmla](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 및 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 매개 변수 사용법을 참조 하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Measures.[Order Quantity]` **놀이 Works** 큐브에서 `Date` 차원에 포함 된 2003 년의 첫 8 개월 동안 집계 된 멤버의 합계를 반환 합니다.  
  
```  
WITH MEMBER [Date].[Calendar].[First8Months2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Year],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First8Months2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 **비 시각적 개체를** 이해 하기 위해 다음 예는 제품 범주가 열이 고 재판매인 비즈니스 유형이 행 인 테이블에서 [재판매인 Sales Amount] 수치를 가져오는 [놀이 Works]의 쿼리입니다. 합계는 제품과 대리점을 모두 포함합니다.  
  
 SELECT 문은 다음과 같습니다.  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 결과는 다음과 같습니다.  
  
|||||||  
|-|-|-|-|-|-|  
||**All Products**|**Accessories**|**Bikes**|**Clothing**|**Components**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$66,302,381.56**|**$1,777,840.84**|**$11,799,076.66**|  
|**Specialty Bike Shop**|**$6,756,166.18**|**$65,125.48**|**$6,080,117.73**|**$252,933.91**|**$357,989.07**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$30,892,354.33**|**$592,385.71**|**$3,307,774.48**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$29,329,909.50**|**$932,521.23**|**$8,133,313.11**|  
  
 Accessories 및 Clothing 제품과 Value Added Reseller 및 Warehouse 대리점에 대한 데이터만 포함된 테이블을 만들고 전체 합계를 유지하려면 NON VISUAL을 사용하여 다음과 같이 문을 작성할 수 있습니다.  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 결과는 다음과 같습니다.  
  
|||||  
|-|-|-|-|  
||**All Products**|**Accessories**|**Clothing**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$1,777,840.84**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$592,385.71**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$932,521.23**|  
  
 열에는 보이는 값 합계만 포함하고 행 합계에는 모든 [Category]의 순 합계를 표시하는 테이블을 만들려면 다음과 같은 쿼리를 실행해야 합니다.  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0`  
  
 `from ( Select {[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 0`  
  
 `from [Adventure Works])`  
  
 `)`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 NON VISUAL이 어떻게 [Category]에만 적용되는지 확인하십시오.  
  
 위 쿼리는 다음과 같은 결과를 생성합니다.  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$73,694,430.80|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 이전 결과와 비교하면 [All Resellers] 행에는 [Value Added Reseller] 및 [Warehouse]에 표시된 값에 대한 합계가 표시되고 [All Products] 열에는 표시되지 않은 제품을 포함한 모든 제품의 합계 값이 표시되는 것을 알 수 있습니다.  
  
 다음 예에서는 하위 SELECT에서 계산 멤버를 사용하여 멤버를 필터링하는 방법을 보여 줍니다. 이 샘플을 재현할 수 있으려면 연결 문자열 매개 변수 *하위 쿼리 = 1*을 사용 하 여 연결을 설정 해야 합니다.  
  
 `select Measures.allmembers on 0`  
  
 `from (`  
  
 `Select { [Measures].[Reseller Sales Amount]`  
  
 `, [Measures].[Reseller Total Product Cost]`  
  
 `, [Measures].[Reseller Gross Profit]`  
  
 `, [Measures].[Reseller Gross Profit Margin]`  
  
 `} on 0`  
  
 `from [Adventure Works]`  
  
 `)`  
  
 위 쿼리는 다음과 같은 결과를 생성합니다.  
  
|||||  
|-|-|-|-|  
|Reseller Sales Amount|Reseller Total Product Cost|Reseller Gross Profit|Reseller Gross Profit Margin|  
|$80,450,596.98|$79,980,114.38|$470,482.60|0.58%|  
  
## <a name="see-also"></a>관련 항목  
 [MDX의 주요 개념&#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)   
 [Mdx 데이터 조작 문 &#40;mdx&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [쿼리 및 Slicer 축 &#40;MDX를 사용 하 여 쿼리 제한&#41;](~/analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)  
  
  

