---
title: 식 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 77ef7250c7af3918509e38c9aa1f5350f3ac5610
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62690838"
---
# <a name="expressions-mdx"></a>식(MDX)


  식에는 식별자, 값 및 평가 결과가 표시 될 수 있는 연산자의 조합입니다. 식은 데이터를 액세스하거나 변경하는 여러 위치에서 사용됩니다. 예를 들어 쿼리를 사용해 검색할 데이터 또는 특정 조건을 만족하는 데이터를 찾는 검색 조건으로 식을 사용할 수 있습니다.  
  
## <a name="simple-and-complex-expressions"></a>단순 식 및 복합 식  
 MDX 식에는 단순 식과 복합 식이 있습니다.  
  
 단순 식에는 다음과 같은 식이 있습니다.  
  
 상수  
 상수는 MDX의 특정 단일 값을 나타내는 기호입니다. 문자열, 숫자 및 날짜 값을 상수로 나타낼 수 있습니다. 숫자 상수와 달리 문자열 및 날짜 상수는 작은따옴표(')로 구분해야 합니다.  
  
 스칼라 함수  
 스칼라 함수는 MDX 내의 계산에서 단일 값을 반환합니다. 대부분의 MDX 식, 문, 및 스크립트는 단일 데이터 요소로 계산되지 않고 셀 또는 멤버와 같은 데이터 요소 그룹을 대상으로 반복적으로 계산되므로 이러한 차이는 MDX의 스칼라 함수 계산 방식을 이해하는 데 중요합니다. 스칼라 함수를 계산할 때 함수는 보통 단일 데이터 요소를 검토합니다.  
  
 개체 식별자  
 다차원 데이터의 특성에 의해 MDX는 개체 지향적입니다. 개체 식별자는 MDX에서 단순 식으로 간주됩니다. 식별자에 대 한 자세한 내용은 참조 하세요. [식별자 &#40;MDX&#41;](../mdx/identifiers-mdx.md)합니다.  
  
 이러한 엔터티를 연산자로 연결하여 복합 식을 만들 수도 있습니다.  
  
## <a name="expression-results"></a>식 결과  
 단일 상수, 변수, 스칼라 함수, 열 이름, 데이터 정렬, 전체 자릿수, 소수 자릿수 및 식의 값으로 이루어진 단순 식은 데이터 형식, 데이터 정렬, 전체 자릿수, 소수 자릿수 및 참조된 요소의 값입니다. MDX는 OLE VARIANT 데이터 형식만 직접 지원하므로 단순 식을 사용할 때는 강제 변환이 일어나지 않아야 합니다.  
  
 복합 식의 경우 데이터 형식이 서로 다른 두 개 이상의 단순 식을 사용할 때 강제 변환이 일어날 수 있습니다.  
  
## <a name="expression-examples"></a>식 예  
 다음 쿼리에서는 정의가 단순 식인 계산 멤버의 예를 보여 줍니다.  
  
 `WITH`  
  
 `MEMBER MEASURES.CONSTANTVALUE AS 1`  
  
 `MEMBER MEASURES.SCALARFUNCTION AS [Date].[Calendar Year].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.OBJECTIDENTIFIER AS [Measures].[Internet Sales Amount]`  
  
 `SELECT {MEASURES.CONSTANTVALUE,MEASURES.SCALARFUNCTION,MEASURES.OBJECTIDENTIFIER } ON 0,`  
  
 `[Date].[Calendar Year].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 `[Measures].[Discount Amount] * 1.5`와 같은 계산도 식으로 취급됩니다. 다음 예에서는 MDX SELECT 문에서 멤버를 정의하는 데 계산을 사용하는 방법을 설명합니다.  
  
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
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[큐브 및 하위 큐브 식 사용](../mdx/using-cube-and-subcube-expressions.md)|큐브 및 하위 큐브 식을 정의합니다.|  
|[차원 식 사용](../mdx/using-dimension-expressions.md)|차원 식을 정의합니다.|  
|[멤버 식 사용](../mdx/using-member-expressions.md)|멤버 식을 정의합니다.|  
|[튜플 식 사용](../mdx/using-tuple-expressions.md)|튜플 식을 정의합니다.|  
|[집합 식 사용](../mdx/using-set-expressions.md)|집합 식을 정의합니다.|  
|[스칼라 식 사용](../mdx/using-scalar-expressions.md)|스칼라 식을 정의합니다.|  
|[빈 값 작업](../mdx/working-with-empty-values.md)|비어 있는 값의 의미와 처리 방법을 설명합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [MDX 언어 참조 & #40; Mdx& #41;](../mdx/mdx-language-reference-mdx.md)   
 [MDX 쿼리 기본 사항&#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
