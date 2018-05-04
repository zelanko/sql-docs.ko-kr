---
title: CREATE CELL CALCULATION 문 (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CELL CALCULATION
- CREATE
- CALCULATION
- CELL
- CREATE_CELL_CALCULATION
- CREATE CELL
- CREATE CELL CALCULATION
dev_langs:
- kbMDX
helpviewer_keywords:
- calculations [Analysis Services], creating
- CREATE CELL CALCULATION statement
- cubes [Analysis Services], calculations
ms.assetid: 01ced1b3-ada1-4b55-b350-e4255c3cc679
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: cb0f441fbb42602dad9bed7b06b4299680f5456c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---create-cell-calculation"></a>MDX 데이터 정의-셀 계산 만들기
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  큐브 내의 지정된 튜플 집합에서 MDX 식을 계산하는 계산 식을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
[WITH <CELL CALCULATION clause> Calculation_Name  
   [,WITH <CELL CALCULATION clause> Calculation_Name...n]  
CREATE CELL CALCULATION CURRENTCUBE | Cube_Name.Calculation_Name   
  
<CELL CALCULATION clause> ::=  
   FOR Set_Expression AS 'MDX_Expression'   
      [ [ CONDITION = 'Logical_Expression' ]   
    | [ DISABLED = { TRUE | FALSE } ]   
    | [ DESCRIPTION =String ]   
    | [ CALCULATION_PASS_NUMBER = Integer]   
    | [ CALCULATION_PASS_DEPTH = Integer]   
    | [ SOLVE_ORDER = Integer]   
    | [ Calculation_Name= Scalar_Expression ], ...n]  
```  
  
## <a name="arguments"></a>인수  
 *Cube_Name*  
 큐브 이름을 지정하는 유효한 문자열입니다.  
  
 *Calculation_Name*  
 셀 계산 이름을 지정하는 유효한 문자열입니다.  
  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *문자열*  
 유효한 문자열 값입니다.  
  
 *MDX_Expression*  
 유효한 MDX 식입니다.  
  
 *Logical_Expression*  
 유효한 MDX 논리 식입니다.  
  
 *정수*  
 유효한 정수 값입니다.  
  
 *Calculation_Name*  
 셀 계산 속성의 이름을 지정하는 유효한 문자열입니다.  
  
 *Scalar_Expression*  
 유효한 MDX 스칼라 식입니다.  
  
## <a name="remarks"></a>주의  
 클라이언트 응용 프로그램은 계산 셀을 사용하여 사용자 지정 롤업 수식 또는 계산 멤버의 경우에서와 같은 전체 셀 집합 대신 특정 셀 집합에 대한 롤업 값을 지정할 수 있습니다. 예를 들어 `{[Canada],[Time].[2000]}`에 의해 정의된 집합의 임의의 셀에 수식으로 정의된 값이 포함되도록 지정할 수 있습니다. 이 집합 내에 포함되지 않는 다른 셀은 일반적으로 계산됩니다.  
  
> [!NOTE]  
>  `{*(<comment> | <whitespace> | <newline>)}`의 BNF(Backus-Naur Form)는 이전 버전과의 호환성을 위해 `{*}`로 구문 분석됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [세션 범위 계산된 셀 만들기](../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-session-scoped-calculated-cells.md)   
 [쿼리 범위 셀 계산 만들기 & #40; 만들기 Mdx& #41;](../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations.md)   
 [MDX로 셀 계산 작성 &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)   
 [셀 속성 & #40;를 사용 하 여 Mdx& #41;](../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)   
 [FORMAT_STRING 내용 & #40; Mdx& #41;](../analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md)   
 [FORE_COLOR 및 BACK_COLOR 내용 &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md)   
 [MDX 데이터 정의 문 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
