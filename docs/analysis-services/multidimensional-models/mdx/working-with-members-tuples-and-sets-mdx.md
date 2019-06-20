---
title: With Members, Tuples, and Sets (MDX) 작업 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 295a094505fdc2b532f337aaa87dc93ae0923dd2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62988611"
---
# <a name="working-with-members-tuples-and-sets-mdx"></a>멤버, 튜플 및 집합 작업(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  MDX는 하나 이상의 멤버, 튜플 또는 집합을 반환하거나 멤버, 튜플 또는 집합에 대해 실행되는 다양한 함수를 제공합니다.  
  
## <a name="member-functions"></a>멤버 함수  
 MDX는 차원, 수준, 집합 또는 튜플 등의 다른 MDX 엔터티에서 멤버를 검색할 수 있는 여러 함수를 제공합니다. 예를 들어 [FirstChild](../../../mdx/firstchild-mdx.md) 함수는 멤버에 대해 실행되고 멤버를 반환하는 함수입니다.  
  
 다음 예에서와 같이 Time 차원의 첫 번째 자식 멤버를 가져오기 위해 명시적으로 멤버를 지정할 수 있습니다.  
  
```  
SELECT [Date].[Calendar Year].[CY 2001] on 0  
FROM [Adventure Works]  
  
```  
  
 또한 다음 예에서와 같이 **FirstChild** 함수를 사용하여 앞의 예제와 동일한 멤버를 반환할 수 있습니다.  
  
```  
SELECT [Date].[Calendar Year].FirstChild on 0  
FROM [Adventure Works]  
  
```  
  
 MDX 멤버 함수에 대한 자세한 내용은 [MDX 함수 참조&#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)를 참조하세요.  
  
## <a name="tuple-functions"></a>튜플 함수  
 MDX는 튜플을 반환하는 몇 개의 함수를 제공하며 튜플이 허용되는 곳이면 어디든 이 함수를 사용할 수 있습니다. 예를 들어 [Item&#40;Tuple&#41;&#40;MDX&#41;](../../../mdx/item-tuple-mdx.md) 함수를 사용하여 집합에서 첫 번째 튜플을 추출할 수 있습니다. 이 함수는 집합이 단일 튜플로 구성되어 있을 때 튜플이 필요한 함수에 튜플을 제공하려는 경우에 매우 유용합니다.  
  
 다음 예에서는 튜플 집합 내의 첫 번째 튜플을 열 축에 반환합니다.  
  
```  
SELECT {  
   ([Measures].[Reseller Sales Amount]  
      ,[Date].[Calendar Year].[CY 2003]  
   )  
, ([Measures].[Reseller Sales Amount]  
      ,[Date].[Calendar Year].[CY 2004]  
   )  
}.Item(0)  
ON COLUMNS   
FROM [Adventure Works]  
```  
  
 튜플 함수에 대한 자세한 내용은 [MDX 함수 참조&#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)를 참조하세요.  
  
## <a name="set-functions"></a>집합 함수  
 MDX는 집합을 반환하는 여러 함수를 제공합니다. 명시적으로 튜플을 입력하고 중괄호로 묶는 것이 집합 검색을 위한 유일한 방법은 아닙니다. 집합을 반환하는 멤버 함수에 대한 자세한 내용은 [MDX의 주요 개념&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)를 참조하세요. 여러 가지 추가 집합 함수가 있습니다.  
  
 콜론 연산자를 사용하면 멤버의 자연 순서를 사용해 집합을 만들 수 있습니다. 예를 들어 다음 예의 집합은 2002년 1분기부터 4분기까지의 튜플을 포함합니다.  
  
```  
SELECT   
   {[Calendar Quarter].[Q1 CY 2002]:[Calendar Quarter].[Q4 CY 2002]}   
ON 0  
FROM [Adventure Works]  
```  
  
 콜론 연산자를 사용하여 집합을 만들지 않을 경우 다음 예에서처럼 튜플을 지정하여 동일한 멤버 집합을 만들 수 있습니다.  
  
```  
SELECT {  
   [Calendar Quarter].[Q1 CY 2002],   
   [Calendar Quarter].[Q2 CY 2002],   
   [Calendar Quarter].[Q3 CY 2002],   
   [Calendar Quarter].[Q4 CY 2002]  
   } ON 0  
FROM [Adventure Works]  
  
```  
  
 콜론 연산자는 시작과 끝을 포함하는 함수이므로 연산자 양쪽의 멤버도 결과 집합에 포함됩니다.  
  
 집합 함수에 대한 자세한 내용은 [MDX 함수 참조&#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)를 참조하세요.  
  
## <a name="array-functions"></a>배열 함수  
 배열 함수는 집합에 대해 실행되고 배열을 반환합니다. 배열 함수에 대한 자세한 내용은 [MDX 함수 참조&#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)를 참조하세요.  
  
## <a name="hierarchy-functions"></a>계층 함수  
 계층 함수는 멤버, 수준, 계층 또는 문자열에 대해 실행되며 계층을 반환합니다. 계층 함수에 대한 자세한 내용은 [MDX 함수 참조&#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)를 참조하세요.  
  
## <a name="level-functions"></a>수준 함수  
 수준 함수는 멤버, 수준 또는 문자열에 대해 실행되며 수준을 반환합니다. 수준 함수에 대한 자세한 내용은 [MDX 함수 참조&#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)를 참조하세요.  
  
## <a name="logical-functions"></a>논리 함수  
 논리 함수는 MDX 식에 대해 실행되며 식의 튜플, 멤버 또는 집합에 대한 정보를 반환합니다. 예를 들어 [IsEmpty&#40;MDX&#41;](../../../mdx/isempty-mdx.md) 함수는 식이 빈 셀 값을 반환했는지 여부를 확인합니다. 논리 함수에 대한 자세한 내용은 [MDX 함수 참조&#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)를 참조하세요.  
  
## <a name="numeric-functions"></a>숫자 함수  
 숫자 함수는 MDX 식에 대해 실행되며 스칼라 값을 반환합니다. 예를 들어 [Aggregate&#40;MDX&#41;](../../../mdx/aggregate-mdx.md) 함수는 지정된 집합의 튜플에 대해 측정값을 집계하여 계산된 스칼라 값을 반환합니다. 숫자 함수에 대한 자세한 내용은 [MDX 함수 참조&#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)를 참조하세요.  
  
## <a name="string-functions"></a>문자열 함수  
 문자열 함수는 MDX 식에 대해 실행되며 문자열을 반환합니다. 예를 들어 [UniqueName&#40;MDX&#41;](../../../mdx/uniquename-mdx.md) 함수는 차원, 계층, 수준 또는 멤버의 고유 이름이 들어 있는 문자열 값을 반환합니다. 문자열 함수에 대한 자세한 내용은 [MDX 함수 참조&#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [MDX의 주요 개념&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [MDX 쿼리 기본 사항 & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [MDX 함수 참조&#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  
