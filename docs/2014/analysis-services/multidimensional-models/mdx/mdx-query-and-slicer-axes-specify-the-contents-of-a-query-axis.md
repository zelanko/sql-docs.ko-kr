---
title: MDX 쿼리 축의 내용 지정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cellsets [MDX]
- query axis [MDX]
ms.assetid: c745ade0-738e-4a98-a3f0-3eabfd3eeba2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 892198c217918fd2b2a374261c6eac5e31d0a428
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074080"
---
# <a name="specifying-the-contents-of-a-query-axis-mdx"></a>쿼리 축의 내용 지정(MDX)
  쿼리 축은 MDX SELECT 문에 의해 반환되는 열 집합의 가장자리를 지정합니다. 열 집합의 가장자리를 지정하면 클라이언트에 표시되는 반환 데이터를 제한할 수 있습니다.  
  
 쿼리 축을 지정하려면 `<SELECT query axis clause>` 를 사용하여 집합을 특정 쿼리 축에 할당합니다. 각 `<SELECT query axis clause>` 값은 하나의 쿼리 축을 정의합니다. 데이터 세트의 축 수는 SELECT 문의 `<SELECT query axis clause>` 값의 개수와 동일합니다.  
  
## <a name="query-axis-syntax"></a>쿼리 축 구문  
 다음 구문은 `<SELECT query axis clause>`의 구문을 보여 줍니다.  
  
```  
  
<SELECT query axis clause> ::=  
   [ NON EMPTY ] Set_Expression [ <SELECT dimension property list clause> ] [<HAVING clause>]  
   ON {  
      Integer_Expression |   
      AXIS( Integer_Expression ) |   
      {COLUMNS | ROWS | PAGES | SECTIONS | CHAPTERS}     
      }  
  
```  
  
 각 쿼리 축에는 번호가 있습니다. 즉, x-축에는 0, y-축에는 1, z-축에는 2 등과 같은 번호가 지정됩니다. `<SELECT query axis clause>`구문에서 `Integer_Expression` 값은 축 번호를 지정합니다. MDX 쿼리는 지정된 축을 128개까지 지원할 수 있지만, 6개 이상의 축을 사용하는 MDX 쿼리는 극소수입니다. 처음 5개의 축에 대해서는 COLUMNS, ROWS, PAGES, SECTIONS 및 CHAPTERS와 같은 별칭을 대신 사용할 수 있습니다.  
  
 MDX 쿼리는 쿼리 축을 건너뛸 수 없습니다. 즉, 한 개 이상의 쿼리 축이 포함된 쿼리는 하위 번호 또는 중간 축을 제외해서는 안 됩니다. 예를 들어 COLUMNS 축 없이는 쿼리에 ROWS 축을 사용할 수 없습니다. 또는 ROWS 축 없이는 COLUMNS와 PAGES 축을 사용할 수 없습니다.  
  
 그러나 축 없이 SELECT 절(즉, 빈 SELECT 절)을 지정할 수 있습니다. 이 경우 모든 차원이 slicer 차원이며, MDX 쿼리에서 한 셀을 선택합니다.  
  
 앞에서 표시한 쿼리 축 구문에서 각 `Set_Expression` 값은 쿼리 축의 내용을 정의하는 집합을 지정합니다. 집합에 대한 자세한 내용은 [멤버, 튜플 및 집합 작업&#40;MDX&#41;](working-with-members-tuples-and-sets-mdx.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 아래의 간단한 SELECT 문은 Columns 축에 대한 측정값 Internet Sales Amount를 반환하고 MDX MEMBERS 함수를 사용하여 Rows 축의 Date 차원에 있는 Calendar 계층 구조의 모든 멤버를 반환합니다.  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
{[Date].[Calendar].MEMBERS} ON ROWS  
FROM [Adventure Works]  
  
```  
  
 다음 두 쿼리는 정확히 동일한 결과를 반환하지만 별칭 대신 축 번호의 사용을 보여 줍니다.  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON 0,  
{[Date].[Calendar].MEMBERS} ON 1  
FROM [Adventure Works]  
  
SELECT {[Measures].[Internet Sales Amount]} ON AXIS(0),  
{[Date].[Calendar].MEMBERS} ON AXIS(1)  
FROM [Adventure Works]  
  
```  
  
 집합 정의 전에 사용되는 NON EMPTY 키워드는 축에서 모든 빈 튜플을 제거하는 쉬운 방법입니다. 예를 들어, 지금까지 살펴본 예제에서 데이터가 없는 큐브의 2004 년 8 월 이상입니다. 열에 데이터가 없는 셀 집합에서 모든 행을 제거하려면 다음과 같이 Rows 축 정의의 집합 앞에 NON EMPTY를 추가합니다.  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
NON EMPTY  
{[Date].[Calendar].MEMBERS} ON ROWS  
FROM [Adventure Works]  
  
```  
  
 NON EMPTY는 쿼리의 모든 축에서 사용할 수 있습니다. 다음 두 쿼리의 결과를 비교해 보십시오. 첫 번째 쿼리는 NON EMPTY를 사용하지 않고 두 번째 쿼리는 두 축에서 모두 NON EMPTY를 사용합니다.  
  
```  
SELECT {[Measures].[Internet Sales Amount]}   
* [Promotion].[Promotion].[Promotion].MEMBERS  
ON COLUMNS,  
{[Date].[Calendar].[Calendar Year].MEMBERS} ON ROWS  
FROM [Adventure Works]  
WHERE([Product].[Subcategory].&[19])  
  
SELECT NON EMPTY {[Measures].[Internet Sales Amount]}   
* [Promotion].[Promotion].[Promotion].MEMBERS  
ON COLUMNS,  
NON EMPTY  
{[Date].[Calendar].[Calendar Year].MEMBERS} ON ROWS  
FROM [Adventure Works]  
WHERE([Product].[Subcategory].&[19])  
  
```  
  
 HAVING 절을 사용하여 특정 조건에 따라 축의 내용을 필터링할 수 있습니다. 이 방법은 동일한 결과를 얻을 수 있는 FILTER 함수 등의 다른 방법보다 융통성이 적지만 더 간단하게 사용할 수 있습니다. 다음 예제에서는 Internet Sales Amount가 $15,000보다 큰 날짜만 반환합니다.  
  
```  
SELECT {[Measures].[Internet Sales Amount]}   
ON COLUMNS,  
NON EMPTY  
{[Date].[Calendar].[Date].MEMBERS}   
HAVING [Measures].[Internet Sales Amount]>15000  
ON ROWS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [Slicer 축 & #40;의 내용을 지정 Mdx& #41;](mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)  
  
  
