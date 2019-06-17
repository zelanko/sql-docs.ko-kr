---
title: 기본 MDX 쿼리 (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 61975b6b24cda25454d10eb1eeb5b452cad0f1ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63025566"
---
# <a name="mdx-query---the-basic-query"></a>MDX 쿼리 - 기본 쿼리
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  기본 MDX (Multidimensional Expressions) 쿼리는 MDX에서 SELECT 문에 가장 자주 사용 되는 쿼리. MDX SELECT 문에서 결과 집합을 지정하는 방식, SELECT 문의 구문 정의 및 SELECT 문을 사용하여 간단한 쿼리를 만드는 방법을 이해하면 MDX를 사용하여 다차원 데이터를 쿼리하는 방법을 확실히 알 수 있습니다.  
  
## <a name="specifying-a-result-set"></a>결과 집합 지정  
 MDX에서 SELECT 문은 큐브로부터 반환된 다차원 데이터의 하위 집합이 포함되는 결과 집합을 지정합니다. 결과 집합을 지정하려면 MDX 쿼리에 다음과 같은 정보가 포함되어야 합니다.  
  
-   결과 집합에 포함할 축 수. MDX 쿼리에서는 축을 128개까지 지정할 수 있습니다.  
  
-   MDX 쿼리의 각 축에 포함할 멤버나 튜플의 집합  
  
-   MDX 쿼리의 컨텍스트를 설정하는 큐브 이름  
  
-   slicer 축에 포함할 멤버나 튜플의 집합. slicer 및 쿼리 축에 대한 자세한 내용은 [쿼리 및 Slicer 축으로 쿼리 제한&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)을 참조하세요.  
  
 쿼리 축, 쿼리될 큐브 및 slicer 축을 식별하기 위해 MDX SELECT 문은 다음 절을 사용합니다.  
  
-   MDX SELECT 문의 쿼리 축을 결정하는 SELECT 절. SELECT 절의 쿼리 축 구성에 대한 자세한 내용은 [쿼리 축의 내용 지정&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)을 참조하세요.  
  
-   쿼리될 큐브를 결정하는 FROM 절. FROM 절에 대한 자세한 내용은 [SELECT 문&#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)을 참조하세요.  
  
-   반환되는 데이터를 제한하기 위해 slicer 축에서 사용할 멤버나 튜플을 결정하는 선택적인 WHERE 절. WHERE 절의 slicer 축 구성에 대한 자세한 내용은 [Slicer 축의 내용 지정&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)을 참조하세요.  
  
> [!NOTE]  
>  SELECT 문의 여러 절에 대한 자세한 내용은 [SELECT 문&#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)을 참조하세요.  
  
## <a name="select-statement-syntax"></a>SELECT 문 구문  
 다음 구문은 SELECT, FROM 및 WHERE 절이 포함된 기본 SELECT 문을 보여 줍니다.  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ]   
SELECT [ * | ( <SELECT query axis clause>   
    [ , <SELECT query axis clause> ... ] ) ]  
FROM <SELECT subcube clause>   
[ <SELECT slicer axis clause> ]  
[ <SELECT cell property list clause> ]  
```  
  
 MDX SELECT 문은 WITH 키워드, 축 또는 slicer 축에 포함할 계산된 멤버를 만들기 위한 MDX 함수의 사용, 쿼리의 일부로 특정 셀 속성의 값을 반환하는 기능 등의 선택적 구문을 지원합니다. MDX SELECT 문에 대한 자세한 내용은 [SELECT 문&#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)을 참조하세요.  
  
### <a name="comparing-the-syntax-of-the-mdx-select-statement-to-sql"></a>MDX SELECT 문의 구문과 SQL 구문 비교  
 MDX SELECT 문의 구문 형식은 SQL 구문과 비슷합니다. 하지만 다음과 같은 점에서 근본적인 차이가 있습니다.  
  
-   MDX 구문은 튜플이나 멤버를 중괄호({})로 묶어 집합을 구분합니다. 멤버, 튜플 및 집합 구문에 대한 자세한 내용은 [멤버, 튜플 및 집합 작업&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)을 참조하세요.  
  
-   MDX 쿼리는 SELECT 문에서 쿼리 축을 0개, 1개, 2개 또는 128개까지 사용할 수 있습니다. 쿼리의 행과 열이 동작하는 방식이 크게 차이가 나는 SQL과 달리, 각 축은 똑같은 방식으로 동작합니다.  
  
-   SQL 쿼리의 경우와 마찬가지로, FROM 절은 MDX 쿼리에 대한 데이터 원본 이름을 지정합니다. 하지만 MDX FROM 절은 단일 큐브로 제한됩니다. LookupCube 함수를 사용하여 값 단위로 다른 큐브 정보를 검색할 수 있습니다.  
  
-   WHERE 절은 MDX 쿼리에서 slicer 축을 기술합니다. 쿼리의 행 축에 나타나는 항목에 직접적으로 영향을 미치지 않는 SQL WHERE 절과 달리, 이 WHERE 절은 표시되지 않는 쿼리의 추가 축처럼 동작하여 결과 집합의 셀에 나타나는 값을 조각화합니다. SQL WHERE 절의 기능은 FILTER 함수 등의 다른 MDX 함수를 통해 사용할 수 있습니다.  
  
## <a name="select-statement-example"></a>SELECT 문 예  
 다음 예는 SELECT 문을 사용하는 기본 MDX 쿼리를 보여 줍니다. 이 쿼리는 Southwest 판매 지역의 2002년 및 2003년 판매액과 세금액이 포함된 결과 집합을 반환합니다.  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON COLUMNS,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON ROWS  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 이 예에서 쿼리는 다음과 같은 결과 집합 정보를 정의합니다.  
  
-   SELECT 절은 Measuers 차원의 Sales Amount 및 Tax Amount 멤버 및 Date 차원의 2002 및 2003 멤버로 쿼리 축을 설정합니다.  
  
-   FROM 절은 데이터 원본이 Adventure Works 큐브임을 나타냅니다.  
  
-   WHERE 절은 Sales Territory 차원의 Southwest 멤버로 slicer 축을 정의합니다.  
  
 또한 쿼리 예에서는 COLUMNS 및 ROWS 축 별칭이 사용되었습니다. 이러한 축의 순서 위치가 사용될 수도 있습니다. 다음 예에서는 각 축의 순서 위치를 사용하도록 작성된 MDX 쿼리를 보여 줍니다.  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON 0,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON 1  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 자세한 예는 [쿼리 축의 내용 지정&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md) 및 [Slicer 축의 내용 지정&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [MDX의 주요 개념&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [SELECT 문 & #40; Mdx& #41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  
