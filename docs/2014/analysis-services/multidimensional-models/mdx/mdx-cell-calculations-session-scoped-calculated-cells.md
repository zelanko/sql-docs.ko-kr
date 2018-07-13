---
title: 세션 범위 계산 만들기 셀 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- session-scoped calculated members [MDX]
ms.assetid: f2d14a89-6286-4e74-9afb-091076f93f21
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1df213e83122d3d93a57c2bbdd131741043ffe7c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37232093"
---
# <a name="creating-session-scoped-calculated-cells"></a>세션 범위 계산 셀 만들기
    
> [!IMPORTANT]  
>  이 구문은 더 이상 사용되지 않습니다. 대신 MDX 대입을 사용하십시오. 할당에 대한 자세한 내용은 [기본 MDX 스크립트&#40;MDX&#41;](the-basic-mdx-script-mdx.md)를 참조하세요.  
  
 동일한 세션의 모든 쿼리에 사용할 수 있는 계산 셀을 만들려면 [CREATE CELL CALCULATION](/sql/mdx/mdx-data-definition-create-cell-calculation) 문 또는 [ALTER CUBE](/sql/mdx/mdx-data-definition-alter-cube) 문을 사용할 수 있습니다. 두 문의 결과는 동일합니다.  
  
## <a name="create-cell-calculation-syntax"></a>CREATE CELL CALCULATION 구문  
  
> [!IMPORTANT]  
>  이 구문은 더 이상 사용되지 않습니다. 대신 MDX 대입을 사용하십시오. 할당에 대한 자세한 내용은 [기본 MDX 스크립트&#40;MDX&#41;](the-basic-mdx-script-mdx.md)를 참조하세요.  
  
 세션 범위 계산 셀을 정의하려면 다음 구문을 이용해 CREATE CELL CALCULATION 문을 사용합니다.  
  
```  
CREATE CELL CALCULATION Cube_Expression.<CREATE CELL CALCULATION body clause>  
  
<CREATE CELL CALCULATION body clause> ::=CellCalc_Identifier FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
## <a name="alter-cube-syntax"></a>ALTER CUBE 구문  
  
> [!IMPORTANT]  
>  이 구문은 더 이상 사용되지 않습니다. 대신 MDX 대입을 사용하십시오. 할당에 대한 자세한 내용은 [기본 MDX 스크립트&#40;MDX&#41;](the-basic-mdx-script-mdx.md)를 참조하세요.  
  
 세션 범위 계산 셀을 정의하는 ALTER CUBE 문에는 다음 구문을 사용하십시오.  
  
```  
ALTER CUBE Cube_Identifier CREATE CELL CALCULATION  
FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
 `String_Expression` 값은 다음 표에 나열된 집합의 범주 중 하나로 확인되어야 하는 직각의 단일 차원 MDX 집합 식 목록을 포함합니다.  
  
|범주|Description|  
|--------------|-----------------|  
|빈 집합|빈 집합으로 확인되는 MDX 집합 식입니다. 이 경우 계산 셀의 범위는 전체 큐브입니다.|  
|단일 멤버 집합|단일 멤버로 확인되는 MDX 집합 식입니다.|  
|수준 멤버 집합|단일 수준의 멤버로 확인되는 MDX 집합 식입니다. 이러한 예로 *Level_Expression*합니다.`Members` MDX 함수. 계산된 멤버를 포함 하려면 사용 합니다 *Level_Expression*합니다.`AllMembers` MDX 함수.<br /><br /> 자세한 내용은 [AllMembers&#40;MDX&#41;](/sql/mdx/allmembers-mdx)를 참조하세요.|  
|하위 항목 집합|지정된 멤버의 하위 항목으로 확인되는 MDX 집합 식입니다. 이 예로 `Descendants`(*Member_Expression*를 *Level_Expression*를 *Desc_Flag*) MDX 함수입니다.<br /><br /> 자세한 내용은 [Descendants&#40;MDX&#41;](/sql/mdx/descendants-mdx)를 참조하세요.|  
  
## <a name="see-also"></a>관련 항목  
 [MDX로 셀 계산 작성 &#40;MDX&#41;](../../multidimensional-models-olap-logical-cube-objects/calculations.md)  
  
  
