---
title: 빈 값 사용 | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ae8d6262f6502add09376b76a767a3076c830cb8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68125854"
---
# <a name="working-with-empty-values"></a>빈 값 작업


  빈 값은 특정 멤버, 튜플 또는 셀이 비어 있음을 나타냅니다. 빈 셀 값은 기본 팩트 테이블에서 지정한 셀에 대한 데이터를 찾을 수 없다는 것을 나타내거나 지정한 셀에 대한 튜플이 해당 큐브에 적합하지 않은 멤버 조합을 표시함을 나타냅니다.  
  
> [!NOTE]  
>  빈 값은 0의 값과는 다르지만 대부분의 경우에는 빈 값을 0으로 취급합니다.  
  
 다음 쿼리에서는 빈 값 및 0인 값의 동작을 보여 줍니다.  
  
```  
WITH  
//A calculated Product Category that always returns 0  
MEMBER [Product].[Category].[All Products].ReturnZero AS 0  
//Will return true for any null value  
MEMBER MEASURES.ISEMPTYDemo AS ISEMPTY([Measures].[Internet Tax Amount])  
//Will true for any null or zero value  
//To be clear: the expression 0=null always returns true in MDX  
MEMBER MEASURES.IsZero AS [Measures].[Internet Tax Amount]=0  
SELECT  
{[Measures].[Internet Tax Amount],MEASURES.ISEMPTYDemo,MEASURES.IsZero}  
ON COLUMNS,  
[Product].[Category].[Category].ALLMEMBERS  
ON ROWS  
FROM [Adventure Works]  
WHERE([Date].[Calendar].[Calendar Year].&[2001])  
```  
  
 빈 값에 다음 정보가 적용됩니다.  
  
-   [IsEmpty](../mdx/isempty-mdx.md) 함수는 함수에 지정 된 튜플이 식별 한 셀이 비어 있는 경우에만 **TRUE** 를 반환 합니다. 그렇지 않으면 함수는 **FALSE**를 반환 합니다.  
  
    > [!NOTE]  
    >  **IsEmpty** 함수는 멤버 식에서 null 값을 반환 하는지 여부를 확인할 수 없습니다. 식에서 null 멤버가 반환 되는지 여부를 확인 하려면 [is](../mdx/is-mdx.md)연산자를 사용 합니다.  
  
-   빈 셀 값이 숫자 연산자(+, -, *, /) 중 하나에 대한 피연산자인 경우 다른 피연산자가 비어 있지 않은 값이라면 빈 셀 값을 0으로 취급합니다. 두 피연산자 모두 빈 경우 숫자 연산자는 빈 셀 값을 반환합니다.  
  
-   빈 셀 값이 문자열 연결 연산자(+)에 대한 피연산자인 경우 다른 피연산자가 비어 있지 않은 값이라면 빈 셀 값을 빈 문자열로 취급합니다. 두 피연산자 모두 빈 경우 문자열 연결 연산자는 빈 셀 값을 반환합니다.  
  
-   빈 셀 값이 임의의 비교 연산자(=, <>, >=, \<=, >, <), 빈 셀 값은 다른 피연산자의 데이터 형식이 숫자나 문자열 인지 여부에 따라 0 또는 빈 문자열로 처리 됩니다. 두 피연산자 모두 빈 경우 두 피연산자 모두 0으로 취급합니다.  
  
-   숫자 값을 정렬할 때는 빈 셀 값이 0과 동일한 위치에서 정렬됩니다. 빈 셀 값과 0 사이에서는 빈 셀이 0보다 앞에 정렬됩니다.  
  
-   문자열 값을 정렬할 때는 빈 셀 값이 빈 문자열과 동일한 위치에서 정렬됩니다. 빈 셀 값과 빈 문자열 사이에서는 빈 셀 값이 빈 문자열보다 앞에 정렬됩니다.  
  
## <a name="dealing-with-empty-values-in-mdx-statements-and-cubes"></a>MDX 문과 큐브에서의 빈 값 처리  
 MDX 문에서 빈 값을 찾은 다음 유효한(즉, 비어 있지 않은) 데이터를 가진 셀에 대해 특정한 계산을 수행할 수 있습니다. 빈 셀 값이 포함되면 결과가 부정확해지는 계산(예: 평균)도 있으므로 계산을 수행할 때는 빈 값을 없애야 합니다.  
  
 빈 값이 기본 팩트 테이블 데이터에 저장되어 있는 경우 이러한 값은 기본적으로 큐브가 처리될 때 0으로 변환됩니다. 측정값에 **Null 처리** 옵션을 사용 하 여 null 팩트가 0으로 변환 되거나 빈 값으로 변환 되거나 처리 중에 오류를 발생 시키는 지 제어할 수 있습니다. 쿼리 결과에 빈 셀 값이 나타나지 않도록 하려면 빈 값을 없애거나 빈 값을 다른 값으로 바꾸는 쿼리, 계산 멤버 또는 MDX 스크립트 문을 만들어야 합니다.  
  
 쿼리에서 빈 행 또는 열을 제거하려면 축 집합 정의 앞에 NON EMPTY 문을 사용합니다. 예를 들어 다음 쿼리에서는 Calendar Year 2001에 판매된 유일한 Category가 Bikes이므로 Product Category인 Bikes만 반환합니다.  
  
 `SELECT`  
  
 `{[Measures].[Internet Tax Amount]}`  
  
 `ON COLUMNS,`  
  
 `//Comment out the following line to display all the empty rows for other Categories`  
  
 `NON EMPTY`  
  
 `[Product].[Category].[Category].MEMBERS`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Date].[Calendar].[Calendar Year].&[2001])`  
  
 더 일반적으로 집합에서 빈 튜플을 제거하려면 NonEmpty 함수를 사용합니다. 다음 쿼리에서는 두 계산 측정값을 보여 줍니다. 하나는 Product Categories 수를 계산하고, 다른 하나는 Calendar Year 2001의 [Internet Tax Amount] 측정값에 대한 값이 들어 있는 Product Categories 수를 보여 줍니다.  
  
 `WITH`  
  
 `MEMBER MEASURES.CategoryCount AS`  
  
 `COUNT([Product].[Category].[Category].MEMBERS)`  
  
 `MEMBER MEASURES.NonEmptyCategoryCountFor2001 AS`  
  
 `COUNT(`  
  
 `NONEMPTY(`  
  
 `[Product].[Category].[Category].MEMBERS`  
  
 `,([Date].[Calendar].[Calendar Year].&[2001], [Measures].[Internet Tax Amount])`  
  
 `))`  
  
 `SELECT`  
  
 `{MEASURES.CategoryCount,MEASURES.NonEmptyCategoryCountFor2001 }`  
  
 `ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
 자세한 내용은 [비어 있지 않은 &#40;MDX&#41;](../mdx/nonempty-mdx.md)를 참조 하세요.  
  
## <a name="empty-values-and-comparison-operators"></a>빈 값과 비교 연산자  
 데이터에 빈 값이 있는 경우 논리 및 비교 연산자는 단순히 TRUE 또는 FALSE가 아니라 EMPTY라는 제3의 결과가 반환할 가능성도 있습니다. 이와 같이 세 가지 결과를 가져오는 논리는 대부분 애플리케이션에서 오류의 원인이 됩니다. 다음은 빈 값 비교 결과를 정리한 테이블입니다.  
  
 이 테이블에서는 두 개의 부울 피연산자에 AND 연산자를 적용한 결과를 보여 줍니다.  
  
|AND|TRUE|EMPTY|FALSE|  
|---------|----------|-----------|-----------|  
|**TRUE**|TRUE|FALSE|FALSE|  
|**비우려면**|FALSE|EMPTY|FALSE|  
|**FALSE**|FALSE|FALSE|FALSE|  
  
 이 테이블에서는 두 개의 부울 피연산자에 OR 연산자를 적용한 결과를 보여 줍니다.  
  
|또는|TRUE|FALSE|  
|--------|----------|-----------|  
|**TRUE**|TRUE|TRUE|  
|**비우려면**|TRUE|TRUE|  
|**FALSE**|TRUE|FALSE|  
  
 이 테이블에서는 NOT 연산자가 부정하거나 반대로 바꾼 부울 연산자의 결과를 보여 줍니다.  
  
|NOT 연산자를 적용할 부울 식|결과|  
|-------------------------------------------------------------|------------------|  
|TRUE|FALSE|  
|EMPTY|EMPTY|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Mdx 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [MDX &#40;식&#41;](../mdx/expressions-mdx.md)  
  
  
