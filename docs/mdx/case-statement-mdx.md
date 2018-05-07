---
title: CASE 문 (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- statements [MDX], CASE
ms.assetid: 0aee3b4a-d5f7-4c9a-87b8-e5efc2da6b6d
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 9e43188839e18290232de0d1ce6849c328580ec4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="case-statement-mdx"></a>CASE 문(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  여러 비교에서 조건에 따라 특정 값을 반환할 수 있습니다. CASE 문에는 다음과 같은 두 가지 유형이 있습니다.  
  
-   식을 일련의 단순 식과 비교하여 특정 값을 반환하는 단순 CASE 문  
  
-   일련의 부울 식을 계산하여 특정 값을 반환하는 검색된 CASE 문  
  
## <a name="syntax"></a>구문  
  
```  
  
Simple Case Statement  
CASE [input_expression]  
WHEN when_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
  
Search Case Statement  
CASE   
WHEN Boolean_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
```  
  
## <a name="arguments"></a>인수  
 *input_expression*  
 스칼라 값으로 확인되는 MDX 식입니다.  
  
 *when_expression*  
 특정 스칼라 값입니다는 *input_expression* 계산 된 시기의 스칼라 값 true를 반환 하도록 평가 *else_result_expression*합니다.  
  
 *when_true_result_expression*  
 WHEN 절이 true일 때 반환되는 스칼라 값입니다.  
  
 *else_result_expression*  
 true인 WHEN 절이 없을 때 반환되는 스칼라 값입니다.  
  
 *Boolean_expression*  
 스칼라 값으로 계산되는 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 ELSE 절이 없고 WHEN 절이 모두 false를 반환한 경우 결과는 빈 셀이 됩니다.  
  
## <a name="simple-case-expression"></a>단순 CASE 식  
 MDX를 확인 하 여 단순 case 식을 계산는 *input_expression* 을 스칼라 값입니다. 이 스칼라 값은 다음의 스칼라 값과 비교는 *when_expression*합니다. 두 스칼라 값이 일치 하는 경우 해당 CASE 문은 값을 반환 된 *when_true_expression*합니다. 두 스칼라 값이 일치하지 않으면 다음 WHEN 절이 실행됩니다. 모든 WHEN 절 값을 false로 평가 하는 경우 *else_result_expression* ELSE 절의 있는 경우 반환 됩니다.  
  
 다음 예에서는 여러 WHEN 절에 대해 Reseller Order Count 측정값을 확인하고 각 연도의 Reseller Order Count 측정값에 따라 결과를 반환합니다. Reseller Order Count 값에 지정 된 스칼라 값과 일치 하지 않는 한 *when_expression* 의 스칼라 값 WHEN 절에는 *else_result_expression* 반환 됩니다.  
  
```  
WITH MEMBER [Measures].x AS   
CASE [Measures].[Reseller Order Count]  
   WHEN 0 THEN 'NONE'  
   WHEN 1 THEN 'SMALL'  
   WHEN 2 THEN 'SMALL'  
   WHEN 3 THEN 'MEDIUM'  
   WHEN 4 THEN 'MEDIUM'  
   WHEN 5 THEN 'LARGE'  
   WHEN 6 THEN 'LARGE'  
      ELSE 'VERY LARGE'  
END  
SELECT Calendar.[Calendar Year] on 0  
, NON EMPTY [Geography].[Postal Code].Members ON 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="searched-case-expression"></a>검색된 CASE 식  
 CASE 식을 사용하여 보다 복잡한 평가를 수행하려면 검색된 CASE 식을 사용합니다. 이 검색 식의 변형을 사용하면 입력 식이 값 범위 내에 있는지 여부를 확인할 수 있습니다. MDX는 WHEN 절이 CASE 문에 나타나는 순서대로 WHEN 절을 반환합니다.  
  
 다음 예에서는 Reseller Order Count 측정값을 확인에 대해 지정 된 *Boolean_expression* 여러 개의 각 WHEN 절에 대 한 합니다. 각 연도의 Reseller Order Count 측정값에 따라 결과를 반환합니다. WHEN 절은 나타나는 순서대로 확인되므로 6보다 큰 모든 값에 대해 각 값을 명시적으로 지정하지 않고 "VERY LARGE"라는 값을 쉽게 할당할 수 있습니다. 스칼라 값 WHEN 절에 지정 되지 않은 Reseller Order Count 값의 *else_result_expression* 반환 됩니다.  
  
```  
WITH MEMBER [Measures].x AS   
CASE   
   WHEN [Measures].[Reseller Order Count] > 6 THEN 'VERY LARGE'  
   WHEN [Measures].[Reseller Order Count] > 4 THEN 'LARGE'  
   WHEN [Measures].[Reseller Order Count] > 2 THEN 'MEDIUM'  
   WHEN [Measures].[Reseller Order Count] > 0 THEN 'SMALL'  
   ELSE "NONE"  
END  
SELECT Calendar.[Calendar Year] on 0,  
NON EMPTY [Geography].[Postal Code].Members on 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 스크립팅 문 & #40; Mdx& #41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
