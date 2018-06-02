---
title: DrilldownLevel (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 99e8c47164d920ec531bf6ab51e35979b060c35d
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578005"
---
# <a name="drilldownlevel-mdx"></a>DrilldownLevel(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  집합의 구성원을 집합에 나타나는 최저 수준보다 한 수준 낮은 수준으로 드릴다운합니다.  
  
 수준을 지정 하 드릴 다운 선택 사항 이지만 수준의 설정한 경우 사용할 수 있습니다는 **식 수준** 또는 **인덱스 수준**합니다. 이러한 인수는 상호 배타적입니다. 마지막으로, 계산 멤버가 쿼리에 있는 경우 행 집합에 이러한 계산 멤버가 포함되도록 인수를 지정할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
DrilldownLevel(Set_Expression [,[Level_Expression] ,[Index]] [,INCLUDE_CALC_MEMBERS])  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Level_Expression*  
 선택 사항입니다. 드릴다운할 수준을 명시적으로 식별하는 MDX 식입니다. 수준 식을 지정하는 경우 아래의 인덱스 인수를 건너뛰세요.  
  
 *Index*  
 선택 사항입니다. 집합 내에서 드릴다운할 대상 계층 번호를 지정하는 유효한 숫자 식입니다. Level_Expression 대신 인덱스 수준을 사용하여 드릴다운할 수준을 명시적으로 식별할 수 있습니다.  
  
 *Include_Calc_Members*  
 선택 사항입니다. 드릴다운 수준에서 계산된 구성원 포함 여부(존재하는 경우)를 나타내는 플래그입니다.  
  
## <a name="remarks"></a>Remarks  
 **DrilldownLevel** 함수 반환 일련의 자식 멤버는 지정 된 집합에 포함 된 멤버에 기반을 계층적 순서로 합니다. 이때 함수의 결과 집합에 포함되는 모든 자식 구성원이 해당 부모 구성원 바로 아래에 포함된다는 점만 제외하고 지정된 집합의 원래 구성원 순서가 유지됩니다.  
  
 여러 수준 계층적 데이터 구조의 경우, 드릴다운할 수준을 명시적으로 선택할 수 있습니다. 수준을 지정하는 두 가지 상호 배타적인 방법이 있습니다. 첫 번째 방법은 설정 하는 **level_expression** 지정 하는 다른 방법은 수준을 반환 하는 MDX 식을 사용 하 여 인수는 **인덱스** 번호로 수준을 지정 하는 숫자 식을 사용 하 여 인수입니다.  
  
 수준 식이 지정된 경우 이 함수는 지정된 수준에 있는 해당 구성원의 자식만 검색하여 계층적 순서로 집합을 구성합니다. 수준 식이 지정되고 해당 수준에 구성원이 없는 경우, 수준 식은 무시됩니다.  
  
 인덱스 값이 지정된 경우 이 함수는 인덱스(0부터 시작)에 따라 지정된 집합에서 참조되는 계층의 다음 최하위 수준에 있는 구성원의 하위만 검색하여 집합을 계층적 순서로 구성합니다.  
  
 수준 식과 인덱스 값이 모두 지정되지 않은 경우 이 함수는 지정된 집합에서 참조되는 첫 번째 차원의 최하위 수준에 있는 구성원의 자식만 검색하여 집합을 계층적 순서로 구성합니다.  
  
 XMLA 속성 MdpropMdxDrillFunctions 쿼리는 서버에서 드릴 함수;에 제공 하는 지원 수준을 확인할 수 있습니다. 참조 [XMLA 속성 지원 &#40;XMLA&#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) 세부 정보에 대 한 합니다.  
  
## <a name="examples"></a>예  
 Adventure Works 큐브를 사용하여 SSMS의 MX 쿼리 창에서 다음 예를 시도할 수 있습니다.  
  
 **예 1 – 최소 구문 설명**  
  
 첫 번째 예제에 대 한 최소한의 구문을 보여 줍니다. **DrilldownLevel**합니다. 필요한 인수는 집합 식뿐입니다. 이 쿼리를 실행 해 서 상위 [All Categories]와 다음 수준의 멤버: [Accessories], [Bikes] 등입니다. 이 예제는 단순, 코드를 보여 줍니다의 기본적인 목표는 **DrilldownLevel** 아래의 다음 수준으로 드릴 하는 함수를 합니다.  
  
```  
SELECT DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]}}) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 예 2 – 명시적 인덱스 수준을 사용하는 대체 구문  
  
 이 예에서는 숫자 식을 통해 인덱스 수준이 지정되는 대체 구문을 설명합니다. 이 경우 인덱스 수준은 0입니다. 0부터 시작하는 인덱스의 경우, 이 수준이 최저 수준입니다.  
  
```  
SELECT  
DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]},,0) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 결과 집합은 이전 쿼리와 동일합니다. 일반적으로 특정 수준에서 드릴다운을 시작하려고 하지 않는 한, 인덱스 수준 설정은 필요하지 않습니다. 이전 쿼리를 다시 실행하여 인덱스 값을 1로 설정한 다음 2로 설정합니다. 인덱스 값을 1로 설정한 경우, 드릴다운은 계층의 두 번째 수준에서 시작합니다. 인덱스 값을 2로 설정한 경우, 드릴다운은 이 예에서 최고 수준인 세 번째 수준에서 시작합니다. 숫자 식이 클수록 인덱스 수준도 높아집니다.  
  
 **예제 3 – 수준 식 설명**  
  
 다음 예에서는 수준 식을 사용하는 방법을 보여줍니다. 계층 구조를 나타내는 집합의 경우, 수준 식을 사용하면 드릴다운을 시작할 계층 수준을 선택할 수 있습니다.  
  
 이 예에서 드릴 다운 수준에서 시작 [City]의 두 번째 인수로 **DrilldownLevel** 함수입니다. 이 쿼리를 실행할 때 Washington 및 Oregon 주에 대해 [City] 수준에서 드릴다운이 시작합니다. 당는 **DrilldownLevel** 함수를 결과 집합도 [Postal codes] 아래쪽 다음 수준의 멤버를 포함 합니다.  
  
```  
SELECT [Measures].[Internet Sales Amount] ON COLUMNS,  
   NON EMPTY (  
   DRILLDOWNLEVEL(  
       {[Customer].[Customer Geography].[Country].[United States],  
           DESCENDANTS(  
             { [Customer].[Customer Geography].[State-Province].[Washington],    
               [Customer].[Customer Geography].[State-Province].[Oregon]},   
               [Customer].[Customer Geography].[City]) } ,  
[Customer].[Customer Geography].[City] ) )  ON ROWS  
FROM [Adventure Works]  
```  
  
 **예 4 – 계산된 멤버를 포함 하 여**  
  
 결과의 맨 아래에 표시 되는 계산된 멤버를 추가할 때 설정 하는 마지막 예제는 **include_calculated_members** 플래그입니다. 플래그는 네 번째 매개 변수로 지정됩니다.  
  
 이 예는 계산된 구성원이 계산되지 않은 구성원과 같은 수준에 있으므로 작동합니다. 계산된 구성원 [West Coast]는 [United States]보다 한 수준 아래에 있는 모든 구성원을 포함한 [United States]의 구성원으로 이루어집니다.  
  
```  
WITH MEMBER   
[Customer].[Customer Geography].[Country].&[United States].[West Coast] AS  
[Customer].[Customer Geography].[State-Province].&[OR]&[US] +  
[Customer].[Customer Geography].[State-Province].&[WA]&[US] +  
[Customer].[Customer Geography].[State-Province].&[CA]&[US]  
SELECT [Measures].[Internet Order Count] ON 0,  
DRILLDOWNLEVEL([Customer].[Customer Geography].[Country].&[United States],,,INCLUDE_CALC_MEMBERS) on 1  
FROM [Adventure Works]  
```  
  
 플래그를 제거하고 쿼리를 다시 실행하는 경우, 계산된 구성원 [West Coast]를 제외하고 같은 결과를 얻습니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
