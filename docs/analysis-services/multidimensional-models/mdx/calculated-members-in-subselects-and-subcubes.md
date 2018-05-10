---
title: 계산 멤버를 하위 Select 및 하위 큐브 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 87571f35126108d164293b2791ec13f90921de6f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="calculated-members-in-subselects-and-subcubes"></a>하위 SELECT 및 하위 큐브의 계산 멤버
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  계산 멤버는 값을 런타임 시 식에서 계산하는 차원 멤버이며 하위 SELECT 및 하위 큐브에서 사용하여 보다 정확하게 쿼리의 cubespace를 정의할 수 있습니다.  
  
## <a name="enabling-calculated-members-in-the-subspace"></a>하위 공간에서 계산 멤버 사용  
 **하위 쿼리** 의 연결 문자열 속성이 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> 또는 **DBPROPMSMDSUBQUERIES** 속성 [XMLA 속성 지원 &#40;XMLA&#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)하위 큐브 또는 하위 select에 동작이 나 허용 되는 계산된 멤버 또는 계산된 집합을 정의 합니다. 특별한 언급이 없으면 이 문서의 컨텍스트에서 하위 SELECT는 하위 SELECT 및 하위 큐브를 말합니다.  
  
 SubQueries 속성은 다음 값을 허용합니다.  
  
|||  
|-|-|  
|값|설명|  
|0|계산 멤버는 하위 SELECT 또는 하위 큐브에서 허용되지 않습니다.<br /><br /> 계산 멤버가 참조된 경우 하위 SELECT 또는 하위 큐브를 평가할 때 오류가 발생합니다.|  
|1|계산 멤버는 하위 SELECT 또는 하위 큐브에서 허용되지만 상위 항목 멤버는 반환 하위 공간에 포함되지 않습니다.|  
|2|계산 멤버는 하위 SELECT 또는 하위 큐브에서 허용되고 상위 항목 멤버는 반환 하위 공간에 포함됩니다. 또한 혼합 세분성이 계산 멤버 선택에서 허용됩니다.|  
  
 SubQueries 속성에서 값 1 또는 2를 사용하면 계산 멤버를 사용하여 하위 SELECT의 반환 하위 공간을 필터링할 수 있습니다.  
  
 예제는 개념을 명확히 하는 데 도움이 됩니다. 먼저 위에 언급한 동작을 보여 주기 위해 계산 멤버를 만든 다음 하위 SELECT 쿼리를 실행해야 합니다.  
  
 다음 샘플에서는 Washington 주 아래의 [Geography].[Geography] 계층에 [Seattle Metro]를 도시로 추가하는 계산 멤버를 만듭니다.  
  
 예제를 실행하려면 연결 문자열은 값이 1인 SubQueries 속성을 포함해야 하고 모든 MDX 문은 동일한 세션에서 실행되어야 합니다.  
  
> [!IMPORTANT]  
>  Management Studio를 사용하여 쿼리를 테스트하는 경우 연결 관리자에 있는 옵션 단추를 클릭하여 추가 연결 문자열 속성 창에 액세스합니다. 여기서 하위 쿼리=1 또는 2를 입력하여 하위 공간에 계산 멤버를 허용할 수 있습니다.  
  
 먼저 다음 MDX 식을 실행합니다.  
  
```  
  
CREATE MEMBER [Adventure Works].[Geography].[Geography].[State-Province].&[WA]&[US].[Seattle Metro Agg]   
   AS  AGGREGATE(   
                 {   
                   [Geography].[Geography].[City].&[Bellevue]&[WA]  
                 , [Geography].[Geography].[City].&[Issaquah]&[WA]  
                 , [Geography].[Geography].[City].&[Redmond]&[WA]  
                 , [Geography].[Geography].[City].&[Seattle]&[WA]  
                 }  
                )    
```  
  
 그런 후 다음 MDX 쿼리를 실행하여 하위 SELECT에서 허용되는 계산 멤버를 봅니다.  
  
```  
Select [Date].[Calendar Year].members on 0,  
       [Geography].[Geography].allmembers on 1  
from (Select {[Geography].[Geography].[State-Province].&[WA]&[US].[Seattle Metro Agg]} on 0 from [Adventure Works])  
Where [Measures].[Reseller Sales Amount]  
```  
  
 다음과 같은 결과를 얻을 수 있습니다.  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2011|CY 2012|CY 2013|CY 2014|  
|Seattle Metro Agg|$2,383,545.69|1$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 이전에 언급한 것처럼 SubQueries=1이면 [Seattle Metro]의 상위 항목이 반환된 하위 공간에 없으므로 [Geography].[Geography].allmembers는 계산 멤버만 포함합니다.  
  
 SubQueries=2를 사용하여 예제를 실행할 경우 연결 문자열에서는 다음과 같은 결과를 얻을 수 있습니다.  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2001|CY 2002|CY 2003|CY 2004|  
|All Geographies|(null)|(null)|(null)|(null)|(null)|  
|United States|(null)|(null)|(null)|(null)|(null)|  
|Washington|(null)|(null)|(null)|(null)|(null)|  
|Seattle Metro Agg|$2,383,545.69|$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 이전에 언급한 것처럼 SubQueries=2를 사용하면 [Seattle Metro]의 상위 항목이 반환된 하위 공간에 있지만 집계에 제공할 일반 멤버가 없으므로 이러한 멤버에 대한 값이 존재하지 않습니다. 따라서 이 예에서는 계산 멤버의 모든 상위 항목 멤버에 대해 NULL 값이 제공됩니다.  
  
 위 동작을 이해하려면 일반 멤버와 같이 계산 멤버가 해당 부모의 집계에 영향을 주지 않는다는 사실을 이해하는 것이 도움이 됩니다. 전자의 경우 결과 하위 공간의 집계 값에 영향을 주는 일반 멤버가 없으므로 계산 멤버로 필터링하면 빈 상위 항목이 얻어집니다. 일반 멤버를 필터링 식에 추가할 경우 집계 값은 이러한 일반 멤버에서 제공됩니다. 위 예제의 경우 다음 MDX 식과 같이 Oregon의 Portland와 Washington의 Spokane을 계산 멤버가 나타나는 동일한 축에 추가할 수 있습니다.  
  
```  
Select [Date].[Calendar Year].members on 0,  
       [Geography].[Geography].allmembers on 1  
from (Select {  
               [Seattle Metro Agg]  
             , [Geography].[Geography].[City].&[Portland]&[OR]  
             , [Geography].[Geography].[City].&[Spokane]&[WA]  
             } on 0 from [Adventure Works]  
     )  
Where [Measures].[Reseller Sales Amount]  
```  
  
 다음과 같은 결과를 얻을 수 있습니다.  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2001|CY 2002|CY 2003|CY 2004|  
|All Geographies|$235,171.62|$419.46|$4,996.25|$131,788.82|$97,967.09|  
|United States|$235,171.62|$419.46|$4,996.25|$131,788.82|$97,967.09|  
|Oregon|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|Portland|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|97205|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|Washington|$204,203.37|(null)|(null)|$114,345.85|$89,857.52|  
|Spokane|$204,203.37|(null)|(null)|$114,345.85|$89,857.52|  
|99202|$204,203.37|(null)|(null)|$114,345.85|$89,857.52|  
|Seattle Metro Agg|$2,383,545.69|$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 위 결과에서 [All Geographies], [United States], [Oregon] 및 [Washington]에 대한 집계 값은 &[Portland]&[OR] 및 &[Spokane]&[WA]의 하위 항목에 대한 집계에서 제공됩니다. 계산 멤버에서는 아무 것도 제공되지 않습니다.  
  
### <a name="remarks"></a>주의  
 전역 또는 세션 계산 멤버만 하위 SELECT 또는 하위 큐브 식에서 허용됩니다. MDX 식에 쿼리 계산 멤버가 있으면 하위 SELECT 또는 하위 큐브 식이 평가될 때 오류가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [쿼리의 하위 select](../../../analysis-services/multidimensional-models/mdx/subselects-in-queries.md)   
 [지원 되는 XMLA 속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)  
  
  
