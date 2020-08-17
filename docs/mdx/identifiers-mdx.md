---
description: 식별자(MDX)
title: 식별자 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fe8494558f7026355cb25e1415f9269fbeb1bed3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387499"
---
# <a name="identifiers-mdx"></a>식별자(MDX)


  식별자는 Analysis Services 개체의 이름입니다. 모든 개체에는 식별자가 있어야 하 고 식별자가 있어야 합니다. 식별자로는 큐브, 차원, 계층, 수준, 멤버 등이 있습니다. MDX 문에서는 개체를 참조하는 개체의 식별자를 사용합니다.  
  
 개체의 이름을 어떻게 지정하느냐에 따라 개체 식별자는 일반 식별자 또는 구분 식별자가 됩니다.  
  
> [!NOTE]  
>  일반 식별자 및 구분 식별자 모두는 1-100자의 문자로 이루어져야 합니다.  
  
## <a name="using-regular-identifiers"></a>일반 식별자 사용  
 일반 식별자는 일반 식별자에 대한 다음 서식 설정 규칙에 맞는 개체 이름입니다. 구분 기호와 함께 또는 구분 기호 없이 일반 식별자를 사용할 수 있습니다.  
  
### <a name="formatting-rules-for-regular-identifiers"></a>일반 식별자 서식 설정 규칙  
  
1.  첫 문자는 다음 중 하나여야 합니다.  
  
    -   유니코드 표준 2.0에 정의 된 문자입니다. 다른 언어의 문자 외에도 문자의 유니코드 정의에는 a에서 z까지 그리고 A에서 Z까지의 라틴 문자가 포함됩니다.  
  
    -   밑줄(_)  
  
2.  그 다음 문자에는 다음과 같은 문자를 사용할 수 있습니다.  
  
    -   유니코드 표준 2.0에 정의 된 문자입니다.  
  
    -   기본 라틴 또는 기타 국가 스크립트의 10진수  
  
    -   밑줄(_)  
  
3.  MDX 예약어는 식별자로 사용할 수 없습니다. MDX에서 예약어는 대/소문자를 구분하지 않습니다. 자세한 내용은 [&#40;MDX 구문&#41;예약 키워드 ](../mdx/reserved-keywords-mdx-syntax.md)를 참조 하세요.  
  
4.  포함된 공백이나 특수 문자는 사용할 수 없습니다.  
  
### <a name="examples-of-regular-identifiers"></a>일반 식별자의 예  
 다음 MDX 문에서 식별자, `Measures`, `Product` 및 `Style`은 일반 식별자에 대한 서식 지정 규칙을 따릅니다. 이런 일반 식별자에는 구분 기호가 필요하지 않습니다.  
  
 `SELECT Measures.MEMBERS ON COLUMNS,`  
  
 `Product.Style.CHILDREN ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 ``  
  
 필요하지는 않지만 일반 식별자와 함께 구분 기호를 사용해도 됩니다. 다음 MDX 문에서는 `Measures`, `Product` 및 `Style` 일반 식별자를 대괄호를 사용하여 제대로 구분했습니다.  
  
 `SELECT [Measures].MEMBERS ON COLUMNS,`  
  
 `[Product].[Style].CHILDREN ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 ``  
  
## <a name="using-delimited-identifiers"></a>구분 식별자 사용  
 일반 식별자에 대한 서식 설정 규칙에 맞지 않는 식별자는 항상 대괄호([])를 사용하여 분리해야 합니다.  
  
> [!NOTE]  
>  구분 기호는 식별자에만 사용됩니다. 구분 기호는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 키워드가 예약된 것으로 표시되어 있는지 여부에 상관없이 키워드에는 사용할 수 없습니다.  
  
 다음 상황에서는 구분 식별자를 사용합니다.  
  
-   개체 이름 또는 이름 중 일부에 예약어를 사용하는 경우  
  
     예약어는 개체 이름으로 사용하지 않는 것이 좋습니다. 이전 버전의에서 업그레이드 된 데이터베이스에는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 이전 버전에서 예약 되지 않은 단어를 포함 하는 식별자가 포함 되어 있지만 현재 예약 되어 있습니다. 해당 개체에 대한 식별자를 변경할 수 있을 때까지는 구분 식별자를 사용하여 개체를 참조할 수 있습니다.  
  
-   개체 이름에 정규화된 식별자로 나열되지 않은 문자를 사용하는 경우  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 구분 식별자가 현재 코드 페이지에 있는 어떤 문자라도 사용할 수 있습니다. 그러나 개체 이름에 특수 문자를 무분별하게 사용하면 MDX 문 및 스크립트를 읽고 유지 관리하기가 어려워질 수 있습니다.  
  
### <a name="formatting-rules-for-delimited-identifiers"></a>구분 식별자에 대한 서식 설정 규칙  
 구분 식별자의 본문에는 구분 문자 자체를 포함하여 현재 코드 페이지에 있는 문자의 어떤 조합이라도 포함될 수 있습니다. 구분 식별자 본문에 구분 문자가 포함되는 경우에는 특수하게 처리해야 합니다.  
  
-   식별자 본문에 왼쪽 대괄호([)만 포함된 경우에는 추가로 처리하지 않아도 됩니다.  
  
-   식별자 본문에 오른쪽 대괄호(])가 포함된 경우에는 오른쪽 대괄호 두 개(]])를 지정해야 합니다.  
  
### <a name="examples-of-delimited-identifiers"></a>구분 식별자의 예  
 다음 가상 MDX 문에서는 `Sales Volume`, `Sales Cube` 및 `select`가 구분 식별자입니다.  
  
 `-- The [Sales Volume] and [Sales Cube] identifiers contain a space.`  
  
 `SELECT Measures.[Sales Volume]`  
  
 `FROM [Sales Cube]`  
  
 `WHERE Product.[select]`  
  
 `-- The [select] identifier is a reserved keyword.`  
  
 다음 예에서 개체 이름은 `Total Profit [Domestic]`입니다. 이 개체를 참조하려면 다음 구분 식별자를 사용해야 합니다.  
  
 `[Total Profit [Domestic]]]`  
  
 구분 식별자를 만들려고 `Domestic` 앞에 있는 왼쪽 대괄호를 변경할 필요는 없었습니다. 하지만 `Domestic` 뒤에 나오는 오른쪽 대괄호는 두 개의 오른쪽 대괄호로 바꾸어야 했습니다.  
  
### <a name="delimiting-identifiers-with-multiple-parts"></a>여러 부분으로 식별자 구분  
 정규화된 개체 이름을 사용할 때는 개체 이름을 구성하는 식별자 중 둘 이상을 구분해야 합니다. 예를 들어 다음 코드에 있는 Front Brakes 식별자는 구분해야 합니다.  
  
 SELECT [Measures].MEMBERS ON COLUMNS,  
  
 [Product].[Product].[Front Brakes] ON ROWS  
  
 FROM [Adventure Works]  
  
 또한 둘 이상의 식별자를 구분하는 것을 보여 주기 위해 이전 예에서는 Measures 식별자를 구분했습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 언어 참조 &#40;MDX&#41;](../mdx/mdx-language-reference-mdx.md)   
 [MDX 쿼리 기본 사항 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services)   
 [MDX 구문 요소&#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
