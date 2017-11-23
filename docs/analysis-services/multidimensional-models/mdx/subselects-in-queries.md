---
title: "쿼리의 하위 select | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
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
ms.assetid: 9e361798-688e-4b11-9eef-31fc793e8ba4
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 513ec56cc2f73b1c9e0b1746ec2d22bc5ee31145
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="subselects-in-queries"></a>쿼리의 하위 SELECT
  하위 SELECT 식은 바깥쪽 외부 SELECT가 실행되는 큐브 공간을 제한하는 데 사용되는 중첩 SELECT 식입니다. 하위 SELECT를 사용하면 모든 계산이 실행되는 새로운 공간을 정의할 수 있습니다.  
  
## <a name="subselects-by-example"></a>하위 SELECT 예  
 첫 번째 예에서는 표시할 결과를 생성하는 데 하위 SELECT가 어떻게 사용되는지를 보여 줍니다. 상위 10개 제품에 대한 여러 해 동안의 판매액을 표시하는 테이블을 생성하라는 요청을 받았다고 가정합니다.  
  
 결과는 다음 테이블과 같아야 합니다.  
  
|||||  
|-|-|-|-|  
||Sum of Years|Year 1|...|  
|Sum of Top 10 Products||||  
|Product A||||  
|...||||  
  
 다음 MDX 식을 작성하여 위와 같은 작업을 수행할 수 있습니다.  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , TOPCOUNT( [Product].[Product].MEMBERS  
               , 10  
               , [Measures].[Sales Amount]  
               ) ON 1  
  FROM [Adventure Works]  
```  
  
 이 식은 다음 결과를 반환합니다.  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 20062|CY 2007|CY 2008|  
|All Products|$80,450,596.98|$8,065,435.31|$24,144,429.65|$32,202,669.43|$16,038,062.60|  
|Mountain-200 Black, 38|$1,634,647.94|(null)|(null)|$894,207.97|$740,439.97|  
|Mountain-200 Black, 42|$1,285,524.65|(null)|(null)|$722,137.65|$563,387.00|  
|Mountain-200 Silver, 38|$1,181,945.82|(null)|(null)|$634,600.78|$547,345.03|  
|Mountain-200 Black, 46|$995,927.43|(null)|(null)|$514,995.76|$480,931.68|  
|Mountain-200 Silver, 42|$1,005,111.77|(null)|(null)|$529,543.29|$475,568.49|  
|Mountain-200 Silver, 46|$975,932.56|(null)|(null)|$526,759.30|$449,173.26|  
|Road-150 Red, 56|$792,228.98|$382,159.24|$410,069.74|(null)|(null)|  
|Mountain-200 Black, 38|$1,471,078.72|(null)|$789,958.49|$681,120.23|(null)|  
|Road-350-W Yellow, 48|$1,380,253.88|(null)|(null)|$744,988.37|$635,265.50|  
  
 쿼리가 10개 제품을 반환하지 않고 9개 제품을 반환했으며 All Products 총계가 이 경우 반환된 상위 9개의 합계가 아닌 모든 제품의 합계를 반영한다는 점을 제외하고, 이 테이블은 우리가 찾고 있는 테이블과 매우 비슷합니다. 문제 해결을 위해 MDX 쿼리를 다음과 같이 수정해 볼 수 있습니다.  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , TOPCOUNT( [Product].[Product].CHILDREN, 10, [Measures].[Sales Amount]) ON 1  
  FROM [Adventure Works]  
```  
  
 이 식은 다음 결과를 반환합니다.  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|Mountain-200 Black, 38|$1,634,647.94|(null)|(null)|$894,207.97|$740,439.97|  
|Mountain-200 Black, 42|$1,285,524.65|(null)|(null)|$722,137.65|$563,387.00|  
|Mountain-200 Silver, 38|$1,181,945.82|(null)|(null)|$634,600.78|$547,345.03|  
|Mountain-200 Black, 46|$995,927.43|(null)|(null)|$514,995.76|$480,931.68|  
|Mountain-200 Silver, 42|$1,005,111.77|(null)|(null)|$529,543.29|$475,568.49|  
|Mountain-200 Silver, 46|$975,932.56|(null)|(null)|$526,759.30|$449,173.26|  
|Road-150 Red, 56|$792,228.98|$382,159.24|$410,069.74|(null)|(null)|  
|Mountain-200 Black, 38|$1,471,078.72|(null)|$789,958.49|$681,120.23|(null)|  
|Road-350-W Yellow, 48|$1,380,253.88|(null)|(null)|$744,988.37|$635,265.50|  
|Road-150 Red, 62|$566,797.97|$234,018.86|$332,779.11|(null)|(null)|  
  
 제품 합계만 누락되었기 때문에 이 테이블은 원하는 결과와 매우 비슷합니다. 이 시점에서 위의 MDX 식을 약간 수정하여 누락된 줄을 추가할 수 있지만 이보다 더 간단한 방법이 있습니다.  
  
 바로 MDX 식이 확인되는 큐브 공간을 재정의하는 것입니다. '새' 큐브에 상위 10개 제품의 데이터만 포함되게 하면 새 큐브에 상위 10개 제품으로만 조정된 All 멤버가 포함되므로 간단한 쿼리를 사용하여 원하는 결과를 얻을 수 있습니다.  
  
 다음 MDX 식은 하위 SELECT 문을 사용하여 큐브 공간을 상위 10개 제품으로 재정의하고 원하는 결과를 생성합니다.  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN  
                       , 10  
                       , [Measures].[Sales Amount]  
                       ) ON 0  
          FROM [Adventure Works]  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 위의 식은 다음 결과를 반환합니다.  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|All Products|$19,997,183.30|$1,696,815.63|$2,816,611.28|$7,930,797.72|$7,552,958.66|  
|Mountain-200 Silver, 38|$2,160,981.60|(null)|(null)|$1,024,359.10|$1,136,622.49|  
|Mountain-200 Silver, 42|$1,914,547.85|(null)|(null)|$903,061.68|$1,011,486.18|  
|Mountain-200 Silver, 46|$1,906,248.55|(null)|(null)|$877,077.79|$1,029,170.76|  
|Mountain-200 Black, 38|$1,811,229.02|(null)|$896,511.60|$914,717.43|(null)|  
|Mountain-200 Black, 38|$2,589,363.78|(null)|(null)|$1,261,406.37|$1,327,957.41|  
|Mountain-200 Black, 42|$2,265,485.38|(null)|(null)|$1,126,055.89|$1,139,429.49|  
|Mountain-200 Black, 46|$1,957,528.24|(null)|(null)|$946,453.88|$1,011,074.37|  
|Road-150 Red, 62|$1,769,096.69|$828,011.68|$941,085.01|(null)|(null)|  
|Road-150 Red, 56|$1,847,818.63|$868,803.96|$979,014.67|(null)|(null)|  
|Road-350-W Yellow, 48|$1,774,883.56|(null)|(null)|$877,665.59|$897,217.96|  
  
 위의 결과는 우리가 원하는 테이블과 정확히 일치합니다.  
  
 하위 SELECT가 어떤 역할을 했는지 검토해보겠습니다. 하위 SELECT는 제품의 다른 모든 차원을 포함한 새로운 큐브를 반환했지만, 제품 차원에서는 우리가 원하는 상위 10개 제품에 맞게 모든 멤버를 필터링했습니다. 이는 상위 10개 조건에 맞지 않는 모든 데이터를 제거하고 큐브를 다시 작성한 것과 같습니다. 이 예에서 이해해야 할 다른 중요한 개념은 큐브에서 다른 모든 차원의 All 멤버에 대해 상위 10개 제품이 계산되었다는 사실입니다. 앞에서 설명한 하위 SELECT의 역할은 다른 필터링 제한이 하위 SELECT에 적용되지 않았기 때문에 가능합니다.  
  
 필요에 따라 하위 SELECT를 복잡하게 사용할 수 있습니다. 다음 예에서는 위에서 언급한 것과 유사한 테이블을 생성하는 방법을 설명하지만 Sales Territory 차원에서 France에 대해 필터링하고 Sales Channel 차원에서 Internet에 대해 필터링했습니다.  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN  
                       , 10  
                       , [Measures].[Sales Amount]  
                       ) ON 0  
             , [Sales Territory].[Sales Territory].[Region].[France] on 1  
             ,  [Sales Channel].[Sales Channel].[Internet] on 2  
          FROM [Adventure Works]  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 결과는 다음과 같습니다.  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|All Products|$748,682.49|$32,204.43|$73,125.18|$269,506.56|$373,846.32|  
|Mountain-200 Silver, 38|$90,479.61|(null)|(null)|$41,759.82|$48,719.79|  
|Mountain-200 Silver, 42|$97,439.58|(null)|(null)|$39,439.83|$57,999.75|  
|Mountain-200 Silver, 46|$102,079.56|(null)|(null)|$27,839.88|$74,239.68|  
|Mountain-200 Black, 38|$26,638.28|(null)|$12,294.59|$14,343.69|(null)|  
|Mountain-200 Black, 38|$96,389.58|(null)|(null)|$41,309.82|$55,079.76|  
|Mountain-200 Black, 42|$80,324.65|(null)|(null)|$43,604.81|$36,719.84|  
|Mountain-200 Black, 46|$107,864.53|(null)|(null)|$45,899.80|$61,964.73|  
|Road-150 Red, 62|$46,517.51|$14,313.08|$32,204.43|(null)|(null)|  
|Road-150 Red, 56|$46,517.51|$17,891.35|$28,626.16|(null)|(null)|  
|Road-350-W Yellow, 48|$54,431.68|(null)|(null)|$15,308.91|$39,122.77|  
  
 위의 결과는 Internet 채널을 통해 France에서 판매된 상위 10개 제품입니다.  
  
## <a name="subselect-statement"></a>하위 SELECT 문  
 하위 SELECT의 BNF는 다음과 같습니다.  
  
```  
[WITH [<calc-clause> ...]]  
SELECT [<axis-spec> [, <axis-spec> ...]]  
FROM [<identifier> | (< sub-select-statement >)]  
[WHERE <slicer>]  
[[CELL] PROPERTIES <cellprop> [, <cellprop> ...]]  
  
< sub-select-statement > :=  
   SELECT [<axis-spec> [, <axis-spec> ...]]  
   FROM [<identifier> | (< sub-select-statement >)]  
   [WHERE <slicer>]  
  
```  
  
 하위 SELECT는 외부 SELECT가 실행되는 큐브 공간이 축 사양과 슬라이서 사양을 기준으로 필터링되는 또 다른 SELECT 문입니다.  
  
 축 또는 슬라이서 절 중 하나에서 멤버를 지정하면 해당 상위 및 하위 항목과 함께 멤버가 하위 SELECT에 대한 하위 큐브 공간에 포함됩니다. 축 또는 슬라이서 절에서 언급되지 않은 모든 형제 멤버와 해당 하위 항목은 하위 공간에서 필터링됩니다. 이러한 방식으로 외부 SELECT 공간이 앞에서 언급한 대로 상위 및 하위 항목과 함께 축 절 또는 슬라이서 절의 기존 멤버로 제한되었습니다.  
  
 축 또는 슬라이서 절에서 언급되지 않은 모든 차원의 All 멤버가 SELECT 공간에 속하기 때문에 해당 차원에서 All 멤버의 모든 하위 항목도 하위 SELECT 공간의 일부입니다.  
  
 새 공간 제약 조건의 영향을 반영하여 하위 큐브 공간의 모든 차원에서 All 멤버가 다시 확인됩니다.  
  
 다음 예에는 위에서 설명한 내용이 나와 있습니다. 첫 번째 MDX 식은 큐브에서 필터링되지 않은 값을 표시하는 데 도움이 되고, 두 번째 MDX는 하위 SELECT 절의 필터링 효과를 설명합니다.  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,  {[Measures].[Internet Sales Amount], [Measures].[Reseller Sales Amount]} ON 0  
  FROM [Adventure Works]  
```  
  
 다음 값을 반환합니다.  
  
||||  
|-|-|-|  
||Internet Sales Amount|Reseller Sales Amount|  
|All Customers|$29,358,677.22|$80,450,596.98|  
|United States|$9,389,789.51|$80,450,596.98|  
|Oregon|$1,170,991.54|$80,450,596.98|  
|Portland|$110,649.54|$80,450,596.98|  
|Washington|$2,467,248.34|$80,450,596.98|  
|Seattle|$75,164.86|$80,450,596.98|  
  
 위의 예에서 Seattle은 Washington의 자식이고 Portland는 Oregon의 자식이며 Oregon과 Washington은 United States의 자식이고 United States는 [Customer Geography].[All Customers]의 자식입니다. 이 예의 표시된 모든 멤버에는 부모 집계 값에 적용되는 다른 형제가 있습니다. 예를 들어, Spokane, Tacoma 및 Everett은 Seattle의 형제 도시이고 모두 Washington Internet Sales Amount에 적용됩니다. Reseller Sales Amount 값은 Customer Geography 특성에 독립적이므로 All 값이 결과에 표시됩니다. 다음 MDX 식은 하위 SELECT 절의 필터링 효과를 설명합니다.  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,  {[Measures].[Internet Sales Amount], [Measures].[Reseller Sales Amount]} ON 0  
  FROM ( SELECT [Customer].[State-Province].&[WA]&[US] ON 0  
           FROM [Adventure Works]  
        )  
```  
  
 다음 값을 반환합니다.  
  
||||  
|-|-|-|  
||Internet Sales Amount|Reseller Sales Amount|  
|All Customers|$2,467,248.34|$80,450,596.98|  
|United States|$2,467,248.34|$80,450,596.98|  
|Washington|$2,467,248.34|$80,450,596.98|  
|Seattle|$75,164.86|$80,450,596.98|  
  
 위의 결과는 Washington State의 상위 항목과 하위 항목만 외부 SELECT 문이 실행된 하위 공간의 일부임을 보여 줍니다. Washington을 언급할 때 하위 SELECT에서 Oregon과 다른 모든 형제 주를 언급하지 않았기 때문에 Oregon과 Portland는 하위 큐브에서 제거되었습니다.  
  
 All 멤버는 Washington에 대한 필터링을 반영하도록 조정되었으며 [Customer Geography] 차원뿐 아니라 [Customer Geography]과 교차하는 다른 모든 차원에서도 조정되었습니다. [Customer Geography]와 교차하지 않는 모든 차원은 하위 큐브에 그대로 유지됩니다.  
  
 다음 두 MDX 문은 하위 SELECT의 필터링 효과에 맞게 다른 차원의 All 멤버를 조정하는 방법을 설명합니다. 첫 번째 쿼리는 변경되지 않은 결과를 표시하고 두 번째는 필터링의 영향을 보여 줍니다.  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,   [Product].[Product Line].MEMBERS ON 0  
  FROM [Adventure Works]  
 WHERE [Measures].[Internet Sales Amount]  
```  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Products|Accessory|Components|Mountain|Road|Touring|  
|All Customers|$29,358,677.22|$604,053.30|(null)|$10,251,183.52|$14,624,108.58|$3,879,331.82|  
|United States|$9,389,789.51|$217,168.79|(null)|$3,547,956.78|$4,322,438.41|$1,302,225.54|  
|Oregon|$1,170,991.54|$30,513.17|(null)|$443,607.98|$565,372.10|$131,498.29|  
|Portland|$110,649.54|$2,834.17|(null)|$47,099.91|$53,917.17|$6,798.29|  
|Washington|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Seattle|$75,164.86|$2,695.74|(null)|$19,914.53|$44,820.06|$7,734.54|  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,   [Product].[Product Line].MEMBERS ON 0  
  FROM ( SELECT [Customer].[State-Province].&[WA]&[US] ON 0  
           FROM [Adventure Works]  
        )  
 WHERE [Measures].[Internet Sales Amount]  
```  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Products|Accessory|Components|Mountain|Road|Touring|  
|All Customers|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|United States|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Washington|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Seattle|$75,164.86|$2,695.74|(null)|$19,914.53|$44,820.06|$7,734.54|  
  
 위의 결과는 예상대로 Washington State의 값으로만 All Products 값이 조정되었음을 보여 줍니다.  
  
 사용 가능한 메모리 내에서 하위 SELECT를 원하는 만큼 중첩할 수 있습니다. 가장 내부의 하위 SELECT는 필터링이 적용되고 다음 외부 SELECT로 전달되는 시작 하위 공간을 정의합니다. 여기서 주목해야 할 중요한 점은 중첩이 누적 연산이 아니므로 중첩을 설정하는 순서에 따라 결과가 다를 수 있다는 사실입니다. 다음 예에서는 중첩 순서를 선택할 때의 차이점을 보여 줍니다.  
  
```  
SELECT [Sales Territory].[Sales Territory Region].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN, 5, [Measures].[Sales Amount]) ON 0  
          FROM (SELECT TOPCOUNT( [Sales Territory].[Sales Territory Region].CHILDREN, 5, [Measures].[Sales Amount]) on 0  
                  FROM [Adventure Works]  
               )  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 다음 결과를 반환했습니다.  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Sales Territories|Australia|Canada|Central|Northwest|Southwest|  
|All Products|$7,591,495.49|$1,281,059.99|$1,547,298.12|$600,205.79|$1,924,763.50|$2,238,168.08|  
|Mountain-200 Silver, 38|$1,449,576.15|$248,702.93|$275,052.45|$141,103.65|$349,487.01|$435,230.12|  
|Mountain-200 Black, 38|$1,722,896.50|$218,024.05|$418,726.43|$123,929.46|$486,694.63|$475,521.93|  
|Mountain-200 Black, 42|$1,573,655.14|$239,137.96|$319,921.61|$130,102.75|$420,445.84|$464,046.98|  
|Mountain-200 Black, 46|$1,420,500.58|$192,320.16|$230,875.99|$117,044.49|$424,813.66|$455,446.27|  
|Road-150 Red, 56|$1,424,867.11|$382,874.89|$302,721.64|$88,025.44|$243,322.36|$407,922.78|  
  
```  
SELECT [Sales Territory].[Sales Territory Region].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Sales Territory].[Sales Territory Region].CHILDREN, 5, [Measures].[Sales Amount]) ON 0  
          FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN, 5, [Measures].[Sales Amount]) on 0  
                  FROM [Adventure Works]  
               )  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 다음 결과를 반환했습니다.  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Sales Territories|Australia|Canada|Northwest|Southwest|United Kingdom|  
|All Products|$7,938,218.56|$1,096,312.24|$1,474,255.49|$2,042,674.72|$2,238,099.55|$1,086,876.56|  
|Mountain-200 Silver, 38|$1,520,958.53|$248,702.93|$275,052.45|$349,487.01|$435,230.12|$212,486.03|  
|Mountain-200 Silver, 42|$1,392,237.14|$198,127.15|$229,679.01|$361,233.58|$407,854.24|$195,343.16|  
|Mountain-200 Black, 38|$1,861,703.23|$218,024.05|$418,726.43|$486,694.63|$475,521.93|$262,736.19|  
|Mountain-200 Black, 42|$1,702,427.25|$239,137.96|$319,921.61|$420,445.84|$464,046.98|$258,874.87|  
|Mountain-200 Black, 46|$1,460,892.41|$192,320.16|$230,875.99|$424,813.66|$455,446.27|$157,436.31|  
  
 두 집합의 결과가 다름을 확인할 수 있습니다. 첫 번째 쿼리는 상위 5개 판매 지역에서 잘 팔리는 제품이 무엇인가라는 질문에 답했고, 두 번째 쿼리는 상위 5개 판매 제품이 가장 많이 팔리는 지역이 어디인가라는 질문에 답변했습니다.  
  
### <a name="remarks"></a>주의  
 하위 SELECT에는 다음과 같은 제한이 있습니다.  
  
-   WHERE 절은 하위 공간을 필터링하지 않습니다.  
  
-   WHERE 절은 하위 큐브에서만 기본 멤버를 변경합니다.  
  
-   축 절에서는 NON EMPTY 절을 사용할 수 없습니다. 대신 [NonEmpty&#40;MDX&#41;](../../../mdx/nonempty-mdx.md) 함수 식을 사용하세요.  
  
-   축 절에서는 HAVING 절을 사용할 수 없습니다. 대신 [필터&#40;MDX&#41;](../../../mdx/filter-mdx.md) 함수 식을 사용하세요.  
  
-   기본적으로 계산된 멤버; 하위 select에서 허용 되지 않습니다. 그러나이 제한을 변경할 수 있습니다, 세션 별로에서 값을 할당 하 여는 **하위 쿼리** 의 연결 문자열 속성이 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 또는 **DBPROP_MSMD_SUBQUERIES** 속성[ 지원 되는 XMLA 속성 &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md). [SubQueries](../../../analysis-services/multidimensional-models/mdx/calculated-members-in-subselects-and-subcubes.md) 또는 **DBPROP_MSMD_SUBQUERIES** 의 값에 따른 계산 멤버의 동작에 대한 자세한 내용은 **하위 SELECT 및 하위 큐브의 계산 멤버**를 참조하세요.  
  
  
