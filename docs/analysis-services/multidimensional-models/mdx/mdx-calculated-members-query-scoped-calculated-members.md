---
title: "Members (MDX) 계산 된 쿼리 범위 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WITH keyword
- query-scoped calculated members [MDX]
ms.assetid: c4507149-e67b-4e5d-9192-cc911acd9adc
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a3e4bb973a314a6f5ba9103960c4d54cb1a119fa
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-calculated-members---query-scoped-calculated-members"></a>MDX 계산 멤버-쿼리 범위 계산된 멤버
  단일 MDX 쿼리에만 계산 멤버가 필요한 경우 WITH 키워드를 사용하여 해당 계산 멤버를 정의할 수 있습니다. WITH 키워드를 사용하여 만든 계산 멤버는 쿼리 실행이 종료된 다음에는 더 이상 존재하지 않습니다.  
  
 이 항목의 설명에서와 같이 WITH 키워드의 구문은 매우 유연하기 때문에 다른 계산 멤버를 기반으로 계산 멤버를 만들 수도 있습니다.  
  
> [!NOTE]  
>  계산 멤버에 대한 자세한 내용은 [계산 멤버를 MDX로 작성&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md)을 참조하세요.  
  
## <a name="with-keyword-syntax"></a>WITH 키워드 구문  
 WITH 키워드를 MDX SELECT 문에 추가하려면 기본 구문을 사용합니다.  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ] SELECT [ * | ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]FROM <SELECT subcube clause> [ <SELECT slicer axis clause> ][ <SELECT cell property list clause> ]  
<SELECT WITH clause> ::=  
   ( [ CALCULATED ] MEMBER <CREATE MEMBER body clause>) | <CREATE MEMBER body clause> ::= Member_Identifier AS 'MDX_Expression'  
   [ <CREATE MEMBER property clause> [ , <CREATE MEMBER property clause> ... ] ]  
<CREATE MEMBER property clause> ::=  
   ( MemberProperty_Identifier = Scalar_Expression )  
  
```  
  
 WITH 키워드 구문에서 `Member_Identifier` 값은 계산 멤버의 정규화된 이름입니다. 이 정규화된 이름에는 계산 멤버가 연결된 차원 또는 수준이 포함됩니다. `MDX_Expression` 값은 식 값이 계산된 후의 계산 멤버의 값을 반환합니다. `MemberProperty_Identifier` 값의 셀 속성 이름과 `Scalar_Expression` 값의 셀 속성 값을 제공하여 계산 멤버에 대한 기본 셀 속성 값을 지정할 수도 있습니다.  
  
## <a name="with-keyword-examples"></a>WITH 키워드 예  
 다음 MDX 쿼리는 `[Measures].[Special Discount]`계산 멤버를 정의하여 원래 할인 가격을 기준으로 특별 할인 가격을 계산합니다.  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Amount] * 1.5  
SELECT   
   [Measures].[Special Discount] on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
 계산 멤버는 계층 구조 안의 어느 지점에나 만들 수 있습니다. 예를 들어 아래 MDX 쿼리에서는 가상의 Sales 큐브에 대해 `[BigSeller]` 계산 멤버를 정의합니다. 이 계산 멤버는 지정된 상점의 맥주 및 포도주에 대한 단위 판매가 적어도 100.00 이상인지 여부를 확인합니다. 하지만 쿼리는 `[BigSeller]` 계산 멤버를 `[Product]` 차원의 자식 멤버로 만들지 않으며, 그 대신 `[Beer and Wine]` 멤버의 자식 멤버로 만듭니다.  
  
```  
WITH   
   MEMBER [Product].[Beer and Wine].[BigSeller] AS  
  IIf([Product].[Beer and Wine] > 100, "Yes","No")  
SELECT  
   {[Product].[BigSeller]} ON COLUMNS,  
   Store.[Store Name].Members ON ROWS  
FROM Sales  
  
```  
  
 계산 멤버는 큐브의 기존 멤버에 종속될 필요가 없습니다. 계산 멤버는 또한 동일 MDX 식에서 정의된 다른 계산 멤버에 기반할 수 있습니다. 예를 들어 다음 MDX 쿼리는 첫 번째 계산 멤버인 `[Measures].[Special Discount]`에서 만든 값을 사용하여 두 번째 계산 멤버인 `[Measures].[Special Discounted Amount]`의 값을 생성합니다.  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Percentage] * 1.5,   
   FORMAT_STRING = 'Percent'  
  
   MEMBER [Measures].[Special Discounted Amount] AS  
   [Measures].[Reseller Average Unit Price] * [Measures].[Special Discount],   
   FORMAT_STRING = 'Currency'  
  
SELECT   
   {[Measures].[Special Discount], [Measures].[Special Discounted Amount]} on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조&#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)   
 [SELECT 문&#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)   
 [멤버 &#40; 계산 된 세션 범위를 만들기 Mdx&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md)  
  
  

